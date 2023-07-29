# Service Workers
Spec: https://www.w3.org/TR/service-workers/

* A JS file registered with the browser
* Stays registered while offline
* Can load content when there is no internet connection

* Sits between browser and remote server:
Browser -> Service Worker -> Remote Server

* Cannot access DOM directly
* Programmable network proxy
* Terminated when not used
* Use promises
* Require HTTPS unless localhost

### Uses
* Offline browsing
* Caching assets & API calls
* Push notifications / API
* Background data sync/preload - not fully supported yet - defer calls until later

### Lifecycle
Register -> Install -> Activate

### Support
All Major browsers

### Simple Example
* WARNING: add the service worker js file to the ROOT directory of your site or it will not work as expected.  For details, see \[1]

See this example for responding to cross origin fetch requests:
https://stackoverflow.com/questions/54619653/can-a-service-worker-fetch-and-cache-cross-origin-assets


\[1] https://stackoverflow.com/questions/55494335/does-serviceworker-js-need-to-load-from-the-root
> If you load a service worker in /modules/pwa/js, it can only manage resources under this path. So, you have to place your SW at the root of your public path. A solution is to use url rewrite with an htaccess file for example.
