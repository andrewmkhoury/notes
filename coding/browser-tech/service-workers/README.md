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

