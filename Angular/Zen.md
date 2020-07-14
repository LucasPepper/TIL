# The Zen of AngularJS

AngularJS is built around the belief that declarative code is better than imperative when it comes to building UIs and wiring software components together, while imperative code is excellent for expressing business logic.

* It is a very good idea to decouple DOM manipulation from app logic. This dramatically improves the testability of the code.
* It is a really, really good idea to regard app testing as equal in importance to app writing. Testing difficulty is dramatically affected by the way the code is structured.
* It is an excellent idea to decouple the client side of an app from the server side. This allows development work to progress in parallel, and allows for reuse of both sides.
* It is very helpful indeed if the framework guides developers through the entire journey of building an app: From designing the UI, through writing the business logic, to testing.
* It is always good to make common tasks trivial and difficult tasks possible.
AngularJS frees you from the following pains:

* Registering callbacks: Registering callbacks clutters your code, making it hard to see the forest for the trees. Removing common boilerplate code such as callbacks is a good thing. It vastly reduces the amount of JavaScript coding you have to do, and it makes it easier to see what your application does.
* Manipulating HTML DOM programmatically: Manipulating HTML DOM is a cornerstone of AJAX applications, but it's cumbersome and error-prone. By declaratively describing how the UI should change as your application state changes, you are freed from low-level DOM manipulation tasks. Most applications written with AngularJS never have to programmatically manipulate the DOM, although you can if you want to.
* Marshaling data to and from the UI: CRUD operations make up the majority of AJAX applications' tasks. The flow of marshaling data from the server to an internal object to an HTML form, allowing users to modify the form, validating the form, displaying validation errors, returning to an internal model, and then back to the server, creates a lot of boilerplate code. AngularJS eliminates almost all of this boilerplate, leaving code that describes the overall flow of the application rather than all of the implementation details.
* Writing tons of initialization code just to get started: Typically you need to write a lot of plumbing just to get a basic "Hello World" AJAX app working. With AngularJS you can bootstrap your app easily using services, which are auto-injected into your application in a Guice-like dependency-injection style. This allows you to get started developing features quickly. As a bonus, you get full control over the initialization process in automated tests.

[Angular Docs](https://docs.angularjs.org/guide/introduction)