# Micro-Frontends

## 
Here’s a good video on Single-SPA + SystemJS: https://www.youtube.com/watch?v=wU06eTMQ6yI


Summary of both SystemJS and single-spa:

**SystemJS**

-   [**What**: SystemJS is a hookable, standards-based module loader](https://github.com/systemjs/systemjs)[^1^](https://github.com/systemjs/systemjs).  SystemJS is basically a ES6 module importmap polyfill with a few more features.
SystemJS.
-   [**Features**: It supports loading of multiple module formats, including CommonJS, AMD, ES modules, and more](https://hix.dev/tools/javascript/system-js)[^2^](https://hix.dev/tools/javascript/system-js). [It can load modules dynamically, which means that modules can be loaded on demand](https://github.com/systemjs/systemjs)[^2^](https://hix.dev/tools/javascript/system-js). [It also supports plugin-based loading of non-JavaScript assets such as CSS, HTML, and JSON](https://github.com/systemjs/systemjs)[^2^](https://hix.dev/tools/javascript/system-js).
-   [**Why**: SystemJS provides a workflow where code written for production workflows of native ES modules in browsers can be transpiled to the System.register module format to work in older browsers](https://github.com/systemjs/systemjs)[^1^](https://github.com/systemjs/systemjs).
-   [**How**: SystemJS works by loading System modules from disk or the network, with included caching that respects the Content-Type header](https://github.com/systemjs/systemjs)[^1^](https://github.com/systemjs/systemjs). [It supports loading bare specifier names with import maps](https://github.com/systemjs/systemjs)[^1^](https://github.com/systemjs/systemjs).
-   [**Example**: An example of SystemJS usage can be found in its official GitHub repository](https://github.com/systemjs/systemjs)[^1^](https://github.com/systemjs/systemjs).

**single-spa**

-   [**What**: single-spa is a JavaScript router for front-end microservices](https://github.com/systemjs/systemjs)[^3^](https://single-spa.js.org/).
-   [**Features**: It allows you to use multiple frameworks on the same page without page refreshing (React, AngularJS, Angular, Ember, etc.)](https://github.com/systemjs/systemjs)[^4^](https://single-spa.js.org/docs/getting-started-overview/). [It enables independent deployment of your microfrontends](https://github.com/systemjs/systemjs)[^4^](https://single-spa.js.org/docs/getting-started-overview/) [and allows you to write code using a new framework, without rewriting your existing app](https://github.com/systemjs/systemjs)[^4^](https://single-spa.js.org/docs/getting-started-overview/).
-   [**Why**: single-spa enables many benefits such as independent deployments, migration and experimentation, and resilient applications](https://github.com/systemjs/systemjs)[^4^](https://single-spa.js.org/docs/getting-started-overview/).
-   [**How**: single-spa works by registering applications with a name, a function to load the application's code, and a function that determines when the application is active/inactive](https://github.com/systemjs/systemjs)[^4^](https://single-spa.js.org/docs/getting-started-overview/).
-   [**Example**: An example of single-spa usage can be found in its official documentation](https://single-spa.js.org/)[^3^](https://single-spa.js.org/).

[Please note that while both SystemJS and single-spa can be used together, they each have their own distinct functionalities and use-cases](https://single-spa.js.org/docs/faq/)[^5^](https://single-spa.js.org/docs/faq/)[^6^](https://single-spa.js.org/docs/ecosystem-vite/). [SystemJS is a module loader, while single-spa is a top-level router for microfrontends](https://single-spa.js.org/docs/faq/)[^5^](https://single-spa.js.org/docs/faq/).
