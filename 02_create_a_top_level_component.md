# Create a Top-Level Component

The entry point to an Angular 2 application is a top level component that we use as a container for all of our other components. In the code below, we are bootstrapping our Angular 2 application using the **bootstrap** method and passing in **AppComponent** as our top level component. 

```javascript
import { bootstrap } from '@angular/platform-browser-dynamic';
import { ROUTER_PROVIDERS } from '@angular/router';
import { AppComponent, environment } from './app/';

bootstrap(AppComponent, [ROUTER_PROVIDERS]);
```

For our **AppComponent** to be instantiated in our application, we need to add it to our **index.html** page via its selector which in this case is **app**.  

```html
<body>
  <app>Loading...</app>

  <script>
    System.import('system-config.js').then(function () {
      System.import('main');
    }).catch(console.error.bind(console));
  </script>
</body>
```

We can approximate this same pattern by first creating an **app** module that we bootstrap with **ng-app**. More importantly, we keep all of our Angular code wrapped in a single, top-level **app** component which we have created using **.component('app', appComponent)**. 

```javascript
import angular from 'angular';
import appComponent from './app.component';
import CommonModule from './common/common';
import ComponentsModule from './components/components';

angular.module('app', [
    CommonModule.name,
    ComponentsModule.name
  ])
  .component('app', appComponent)
;
```

And then we can add our component to our **index.html** page and then try to figure out when we write `<app>Loading...</app>` or `<app>Loading...</app>`, which one is Angular 1 and which one is Angular 2.

```html
<body ng-app="app" ng-strict-di ng-cloak>
  <app>Loading...</app>

  <script src="bundle.js"></script>
</body>
```