---
layout: post
title: Set up CORS header for Cloudflare proxied websites
date: 2021-10-21
summary: For some reasons, Cloudflare proxy would mess up the CORS headers, and here is a quick work around.
---

For some reasons, Cloudflare proxy would mess up the [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) headers, in particular those [pre-flight](https://developer.mozilla.org/en-US/docs/Glossary/Preflight_request) OPTIONS requests.

If you want legitimate CORS responses for some paths of your Cloudflare site, just follow the steps below to create a [Cloudflare worker](https://workers.cloudflare.com/):

1\. Click into domain page -> workers -> manage workers -> create worker

![](/images/cors-worker/manage_worker.png)

![](/images/cors-worker/create_worker.png)

2\. Set up name to the worker (top left), e.g. `add-cors-to-requests`

3\. Copy and paste the code below:
{% highlight javascript %}

// Reference: https://developers.cloudflare.com/workers/examples/cors-header-proxy
const corsHeaders = {
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "GET,HEAD,POST,OPTIONS",
        "Access-Control-Max-Age": "86400",
}
function handleOptions (request) {
        // Make sure the necessary headers are present
        // for this to be a valid pre-flight request
        let headers = request.headers
        if (
                headers.get("Origin") !== null &&
                headers.get("Access-Control-Request-Method") !== null &&
                headers.get("Access-Control-Request-Headers") !== null
        ) {
                // Handle CORS pre-flight request.
                // If you want to check or reject the requested method + headers
                // you can do that here.
                let respHeaders = {
                        ...corsHeaders,
                        // Allow all future content Request headers to go back to browser
                        // such as Authorization (Bearer) or X-Client-Name-Version
                        "Access-Control-Allow-Headers": request.headers.get("Access-Control-Request-Headers"),
                }
                return new Response(null, {
                        headers: respHeaders,
                })
        }
        else {
                // Handle standard OPTIONS request.
                // If you want to allow other HTTP Methods, you can do that here.
                return new Response(null, {
                        headers: {
                                Allow: "GET, HEAD, POST, OPTIONS",
                        },
                })
        }
}
async function handleRequest (request) {
        let response
        if (request.method === "OPTIONS") {
                response = handleOptions(request)
        }
        else {
                response = await fetch(request)
                response = new Response(response.body, response)
                response.headers.set("Access-Control-Allow-Origin", "*")
                response.headers.set("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS")
        }
        return response
}
addEventListener("fetch", (event) => {
        event.respondWith(
                handleRequest(event.request).catch(
                        (err) => new Response(err.stack, { status: 500 })
                )
        );
});

{% endhighlight %}
4\. Click `Save and Deploy`

![](/images/cors-worker/worker_code.png)

5\. Click into domain page -> workers -> add route

![](/images/cors-worker/add_route.png)

6\. Set up the routes that would need the CORS worker, and select the newly created worker. For security reasons, you should only select the paths that would really need the CORS access.

![](/images/cors-worker/save_route.png)


7\. Future requests to those paths will trigger the worker. (The DNS entry must have the cloudflare proxy enabled, of course)

## Side Note

1\. If you got any problem and need to debug, you may check the error in the worker playground:

<https://developers.cloudflare.com/workers/learning/playground>


2\. The workers are global and could be reused in any other sites of your Cloudflare account.

3\. With the approach, nothing need to be done on your Apache / Nginx configurations.
