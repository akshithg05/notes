### [[2026-02-25]]
## What are service workers ?

Service workers act as programmable proxies which sit between the web application, web browser and the network (when available). It is a piece of JavaScript code which runs on a thread other than the main thread.

Service workers run behind the scene on a separate thread. It is a different thread allocated by the browser. It acts as a proxy server.

They are intended to create effective offline experiences in our website.

If there is no network connection, generally most of the network/ API calls will fail and we cannot load anything. But there are a few websites which work offline. For building that we can make our website run offline.

We can also intercept network requests and take appropriate action based on whether network is available and update the assets sent by the server.

Service workers run only on HTTPS. This is because we can perform man in the middle attacks, hence it is available only on HTTPS. In firefox private window we cannot even use service worker.

Service worker is no present everywhere. Only on specific browsers and specific operating systems. But it works on most modern browsers.

Service workers also allow push notifications and background sync APIs.

## Concepts and usage

- They are event driven workers, registered against an origin and path. It will only work for a specific domain + port + protocol.
- It takes the form of a JS file that control the web-page.

**Service worker does not have access to DOM because it runs on a different thread**
Service workers cannot access web storage APIs as well as it runs in a different thread.

(For  more check MDN docs.)

## Go through the code and practical example.

- First check if service worker will be available in the web-browser while writing the script. We can do this by going to the browser console and checking -

```js
navigator.serviceWorker
```

if this is available it will show an object and we can see the results of the object in it.

![[Pasted image 20260225092302.png]]

### Registering a service worker
![[Pasted image 20260225093140.png]]
### How to see service worker in our application.

- Go to browser, dev tools -> Application tab -> service worker in the side menu


## Service worker lifecycle

First the service worker is -
1. Installed
2. Activated
3. Operations.

Service worker is event-driven. There are certain events like installed, activated, fetch, etc. It works on a event basis and these will be available in our sw js file.

Since service worker does not have access to the DOM APIs, we cannot use window.add eventListener, we need to use "self" or "this".


### WE can build a seamless offline experience using service worker

We can do this using caching, by caching resources using service worker, and serve these cache when we are offline.


## There are different ways to provide offline experience

Whenever a file is requested - 
1. Check the cache, and return it from the cache. If cache is not available then fetch from the network call. But this is not a very good way of doing things. If the cache is available we will never make a network call. We will always fetch from the cache itself. So if there are any updates which take place we will not be able to see any of these.

So a better way of doing this is to -
2.  First fetch from first netowrk. Update cache with new data. If there no network then use cache as a back up/ fall back. This is a good strategy to implement things

Use cache as back up , not as a primary source.

![[Pasted image 20260226085618.png]]


Good caching strategy

![[Pasted image 20260226092015.png]]

