# Angular Shell created to demonstrate creation of service worker using @angular/service-worker 
 
Currently there are various libararies available for creating service workers 
- sw-precache
- workbox
- @angular/service-worker.

I have created various shell repositories using sw-precache and workbox to try out their functionality.
This repository would work with service-worker library shipped with @angular.
This is currently in beta - 1.0.0-beta.14

This is currently deployed [here] (https://happyahluwalia.github.io/angular_service_worker
/). Its a simple PWA with a quick startup time, service worker, manifest and the whole nine yards.

The service worker is generated using the @angular/service-worker


# Setup
Run following commands

```
ng set apps.0.serviceWorker=true

npm install @angular/service-worker
```

ng set command will enable service worker in the project. You can see this in the .angular-cli.json file

npm install @angular/service-worker will install the required node module. Currently 1.0.0-beta.14.
With these two commands done every time a production build is created using the ng build -prod command the service worker will automatically be added to the project.

# Production Build
On production build it generates the following
- **_ngsw-manifest.json_** : This file contains all the files that are generated by the ng build -prod command. These files would be downloaded by the service worker in the browser and cached. The javascript and css files have a hash in the file name. Whenever the file is updated the hash would change, so the file name would change and the service worker would know that an updated file is to be downloaded from the server.
This file is the heart of the service worker logic as it contains what caching mechanism to be used for a certain set of urls, what kind of static assets should be ignored by the service worker, external files that we the application use for e.g fonts, css downloaded directly from cdn etc

- **_sw-register.xxxxhashcode....js_** : This file has the code to register the service worker in the browser

- **_worker-basic.min.js_** : This is the main service worker file generated as part of the production build.
