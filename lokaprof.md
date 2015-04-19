# Wepo, Vefforritun

**Author: Arnar Kári Ágústsson**

---
## 1. JavaScript
---
### 1.1 Introduction
* What is JS
 - JavaSript is "an object-oriented computer programming language commonly used to create interactive effect within web browsers."

### 1.2 Functions
* Function parameters
 - If a function is called with too few or too many parameters, no one minds. -> The JS engine will simply pass **undefined** instead of the missing parameters.

* A function has access to its parameters in 2 ways: 
  - via the specified parameter names
  - via the "arguments" implicit variable (array)

* Return
 - Functions in JS always return something! (undefined) 1.1.4. Calling. 
 - Function can also be called in at least two separate ways:
	1. Function.call()
	2.  Function.apply()

* Calling function immediately.
```
    (function() {
        // Some code...
    })();
```

* Inner functions 
 - Inner functions are only visible (callable) within the outer function
 - ...unless the outer function returns the inner function as a return value

### 1.3 Arrays

* Arrays in JS are not typed, i.e items can be of any type (numbers, strings, objects, even other **arrays**).
```
    var arr = []; // create array
    arr.push(7);
    arr.unshift(17); // add to the front
    console.log(arr); //prints [17, 7]
```
* Proper way of forEach’ing, loops through all items, add applies a function to each:
```
    arr.forEach( function (item) { 
        console.log(item);
    });
```

* Removing
 - `arr.shift();` \- remove first item.
 - `arr.pop();` \- remove last item.
 - `arr.splice(index, numbItems);` \- remove numItems beginning at index.
 - `arr.slice()` \- same as splice but doesn't mess with the array.

* Methods
 - `sort()` \- accepts compare function, and sorts the items in the array according to the result of the function.
 - `join()` \- creates a single string out of all the items in the array
 - `map()` \- same as map() in scheme, **returns a new array**.
 - `filter()`
 - `reduce() / recuceRight()` \- collapse items in a array into a single value
 - `each()` \- returns true if all items in a array satisfy some condition.
 - `some()` \- returns true if at least one item in an array satisfies some.

### 1.4 Objects

* new Object()
```javascript
	var shape = new Object();
	shape.color = "Red";
```

* Constructor functions
```javascript
	function Shape () { 
		// Possibly some initialization code..
		this.color = "Red";
	}
	var shape = new Shape();
```

* Object literals
```javascript
	var shape = {
		color: "Red",
		size: 10
	};
	// OR :
	var shape = {};
	shape.color = "Red";
	shape.size = 10;
```

* Properties of class instances 
```javascript
	var shape = new Shape();
	shape.x = 10;
	shape["y"] = 20; // also allowed.
```

* Constructor context 
 - `this` refers to the instance created by new
 - if the constructor function is called without the *new* keyword, the context of the constructor (the object referred to by this) is the global object - the window object in web pages.

* Adding functions to objects
```javascript
	function Shape () {
		// ...
		this.GetArea = function () { 
			return this.x * this.y;
		};
	}
```
* or
```javascript
	function Shape () {
		// ...
	}
	Shape.prototype.GetArea = function () {
		return this.x * this.y;
	};
```

### 1.5 OOP patterns
* 3 pillars of OOP are:
 	- encapsulation
 	- inheritance
 	- polymorphism
* JS is not a pure OOP language, but rather a hybrid language. 
* Encapsulation
	- Private and public member variables in JS using constructor functions:
	```javascript
		function Shape (x, y) {
			this.x = x; // public
			var privateY = y; // private 
			this.getY = function () {
				return privateY;
			};
		}
	```
* Inheritance - read article
*  Polymorphism
	-  Since variables are not strongly typed, we can never have a reference of base class types which refer to a subclass.
	- We need to ensure classes use the same function names for methods that should appear polymorphic.
* Base.js by Dean Edwards

### 1.6 Scope
* There are basically only two types of scope in JS:
	- Global scope
	- Function scope
* Global scope
	- When JS code executes inside a browser, global variables are stored as properties of the window object.
* Local scope
	-  **make a habit of declaring all variables at the top of a function**
	-  Location of declaration within the function doesn't matter.
		+  Variables will be *hoisted* to the top
	-  `if/while/for` etc. will **not** create new scope.
	-  if a variable is declared in global scope, and then another variable with the same name is declared in the local scope, the local variable will *override/hide* the global variable within the function.
		+  Choose unique names for your variables.
*  Changing context
	-  Using functions `Function.apply()` and `Function.call()`, we can pass in some objects as the context.
		+  The difference lies in the way how parameters to are function are handled
*  Closure
	-  a closure is the local variables for a function - kept alive after the function has returned, or 
	-  a closure is a stack-frame which is not deallocated when the function returns.
*  Hoisting
	-  When a variable (or a function) is not declared at the top of a scope, but still accessible there, because the JS engine "moves" the declaration to the top.

### 1.7 The Good Parts

* Douglas Crockford
* The bad parts:
	- Avoid global variables
	- automatic semicolon insertion
	- automatic variable declaration
		+ If the JS engine runs into a variable name that hasn't been declared, it will declare it automatically, and in global scope!
	- The `eval()` function 
	- `typeof` operator
		+ reports array as an object
	- the `with` operator
	- The + operator can both add and concatenate
	- == and !=
		+ use === and !==
* The good parts:
	- Lambda, passing functions as parameters
	- Dynamic objects
		+ able to add properties to objects at will
	- Loose typing
	- Object literals
* Misc points
	- Avoid using /\* ... \*/ (regular expressions can legally contain \*/)
	- The for - in statement loops through all properties in a object - including functions! - as well as properties from the prototype chain
		+ Object.hasOwnProperty could come in handy to ensure we're only looking at properties of the object itself

### 1.8 Async

* A lot of operation in JS are asynchronous, often in the format "pass me a function and I will call it sometimes later" (i.e. a **callback**).
	- `setTimeOut()` - accepts a function as a parameter and calls it after a specified timeout
	- `setInterval()` - accepts a function as a parameter and calls it repeatedly, with a given interval between
	- jQuery's `$.ajax()` function - has both a success and error handler, which are called ones a reply is received
* Promise 
	- A promise is an object that will have a value at some point in the future
	- `then()` - accepts two functions as its parameters: *success* and *failure*. Either one will get called.
* Promise implementations
	- q
	- rsvp
	- when
	- AngularJS has its own implementation ($q)

### 1.9 Tools

* Grunt is a **task runner** tool, with lost of plugins.
	- Configuration-based
* Gulp is also a task runner
	- it relies more on regular JS code.
	- allows tasks to pipe data to other tasks

### 1.10 Libraries

* Categorizes

| Frameworks    | Data binding libraries  | Utility libraries  |
| ------------- | ----------------------- | ------------------ |
| jQuery        | Knockout				  | Underscore/Lodash  |
| Prototype     | Backbone      		  | Mustache		   |
| MooTools      | Ember         		  | Sugar			   |
| script.		| Batman				  | Moment			   |
| aculo.us 		| AngularJS 			  |					   |

* Pros and cons of single page apps
	- Pros:
		+ The HTML is only loaded once
		+ HTML is only repeated on the client, therefore reducing traffic from the server to client
		+ Each request only fetches data (Json/XML), but not any boilerplate HTML
	- Cons:
		+ The user must have JS enabled!
		+ If we don't update the URL after an action, the user will get a different page when (s)he reloads
		+ What about SEO? Will search engine be able to crawl pages written like this? (Do we want them to? SPA's are applications, not usual web pages!)
* The MV\* pattern family
	- MVC - Model-View-Controller
	- MVP - Model-View-Presenter
		+ presenter has smaller role then a Controller
	- MVVM - Model-View-ViewModel
	- JS MV\* frameworks: same examples as the data binding libraries
* Module libraries
	- When web applications become large, dependencies between modules may become hard to maintain.
		+ RequireJS 
		+ CommonJS
* Date manipulation
	- MomentJS most popular
		+ fullCalendar and jQuery-timepicker depend on it
* UI Controls
	- Bootstrap
	- Select2
	- Chosen
	- Ace editor

### 1.11 Unit testing

* All code we write should be unit tested
* Each module should be as small as possible -> *single responsibility principle*
* All dependencies should be injected into modules, makes things easier
* Test should focus more on the logic within a module, not the logic it depends on.
	- instead provide a **test double** of the depend module
* Test:
	- branch statement (if-else)
	- loops
	- assignments (expecially calculations!)
* Test tools
	- Karma/Jasmine combo
		+ Mocha/Chai/Sinon
	- Karma is a test runner
	- Jasmine is a test framework
	- If the test will be executed in a continuous integration environment, test in a windowless browser.
* Types of test objects
	- **mocks** objects only implement the functionality which is required by the test scenario, and provide us with info on if these functions were called
	- **stubs** functions usually return hard-coded data
	- **fakes** have a working implementation, not ready for production though (i.e. use an in-memory DB)
	- **dummies** not really used, except for filling a list of parameters

---
## 2. AngularJS
---
### 2.1 Introduction
* AngularJS is one of the client-side MVC frameworks
	- Misko Hevery (Google)
* Allows you to define your own DSL (Domain Specific Language)
* Enables developers to write testable code
* App
	- ng-app directive is used to specify the scope of the application
	- A corresponding **module** is then defined, including a dependency list of other modules.
	- `angular.module("TodoApp", [dependencies]);
* $scope
	- the `$scope` variable contains the model objects(s) and is *injected* into the controller.
	- Each controller has its own scope
* Dependencies
	- object which our code relies on:
		+ a global object
		+ a static object
		+ a member variable in our class
		+ an object created using new
	- if a function doesn't depend on anything, it is called a *pure function*

### 2.2 Multi-page apps

* By default, URLs used in AngularJS Single-Page Apps use hash-tag to ensure the page won't reload.
* However, HTML5 includes function which manipulate the browser history, which allows us to use regular URLs.

### 2.3 Data binding

* Model object should be stored in the `$scope`
* Angular will ensure that the UI and the model object(s) are in sync. 
	- Digest cycle
	- Edge cases -> inform Angular that something has happed
* Ng-repeat
	- `$index` - 0-based index of the current item
	- `$first` - true if this is the first item in the collection
	- `$last` 
	- `$middle` - true if neither first nor last
	- `$even/$odd`
	- **track by** - Angular changes only DOM elements of data elements that have actually changed

### 2.4 Services

* 5 types of services:
	- Constants
	- Values
	- Factories
	- Services
	- **Provides** (used to implement the other behind the scenes)
* Factories
	- can be a function which takes care of some functionality
	- can be a object which stores some data and has methods
	- useful when we've gt code which must be shared across modules/controllers
* Service
	- The **service** singleton object will be created using the *new* operator - meaning that the service function is a **constructor function**
	- The **factory** singleton object is created bu us, i.e using object literal syntax. We can run code before we create the object, such as some code which declares local/hidden variables/functions in a closure
* Providers
	- The object returned by a provider must implement on method called `$get`, which return the singleton object

### 2.5 Form validation

* Attributes
	- ng-minlength
	- ng-maxlength
	- ng-pattern
	- ng-required
	- ng-change
	- ng-trim
* We can query individual elements for the following properties:
	- `$pristine/$dirty` - true/false if the value has not been modified by the user
	- `$valid/$invalid` - true/false if the field passes validation or not
	- `error` - contains sub-properties, which indicate what caused the error (example: `$error.minlength`)
* Angular adds automatically the CSS classes to elements, depending on their state: (`ng-pristine ng-dirty ng-valid ng-invalid`)

### 2.6 Directives

* Directives can be used to create new markup - i.e. create your own tags
* Similar to Web Components (support Firefox, Chrome and Opera)
* Only place where JS code should be manipulating DOM elements!
* Include jQuery before including angular
* Directive names
	- camelCasing in JS code
	- dash-separted lowercasing in the HTML
* Directives can target 4 different types:
	- DOM Elements (such as `<tab>` etc.) Use:
		+ `restrict: "E"
	- Attributes (such as `<div tab>`). Use:
		+ `restrict: "A"
	- Class values (such as `<div class="tab">`). Use:
		+ `restrict: "C"
	- Comments (rerely needed). Use:
		+ `restrict: "M"
* Link function
	- The role of the link function is to bind together the model and the HTML, set up event handlers and more.
	- It accepts the following parameters:
		+ `scope`(no $ sign!)
		+ `element` - the element which our directive has been applied to
		+ `attrs` - a collection of attributes applied to the element
	- Angular will always pass these variables in as parameters and in this order, no matter what we call them
```javascript
	angular.modele("TodoApp").directive('myTag', function () {
		return {
			restrict: 'E',
			template: '<div> etc. </div>',
			link: function ( scope, element, attr ) {
				// Here we can call code which manipulates the 
				// element in question: add/remove attributes
				// add event handlers etc.
			}
		};
	});
```
* Directive scope
	- By default, the scope of the directive is the same as the scope of the enclosing controller
	- Directives can have their own scope, independent from the controller
		+ `scope: {}`
	- Sending elements from parent to directive scope
		+ "@" - pass as interpolated string
		+ "=" - two way data bind (allows the directive to update values in the controller scope)
		+ "&" - pass as function (allows the directive to call a function defined in the controller)

### 2.7 AngularJS and REST

* Web services have been very RPC-like (Remote Procedure Call)
	- http://www.mysite.com/service/DoStuff - results in a function getting called on the server
* Many types of web services (SAOP for instance) hardly use the services provided by the HTTP protocol, except as a means to transmit text (usually XML), i.e. services such as:
	- Status codes
	- Mime types/Accept header
	- Caching
* Main characteristics of **REST** (*Roy Fielding*)
	- *Client/server* - servers are not aware of what UI the clients user (and don't care)
	- *Stateless* - the server should not maintain client state. State is sent with each request
	- *Cacheable* - resources decide for themselves if they are chacheable or not.
	- *Hypertext driven* - clients should only know the root URL of the service, and can use that to discover the rest of the API, i.e. resources include URLs to sub-resources (**HATEOAS**)
* Resources
	- `/api/songs`, `/api/artist`, `/api/albums`
	- We then use HTTP methods (GET, POST, PUT, DELETE, etc.) to perform operation on these resources.
	- Sub resources
		+ `/api/artist/7/albums`
* HTTP status codes
	- 200 OK - everything went well
	- 30X - resource has been moved or can be found elsewhere (i.e. redirect)
	- 40X - client errors, such as 
	 	+ 400 - Bad request - when parameters are illegal
		+ 401 - Unauthorized 
	- 50X - server errors, an (unexpected) error occurred on the server
* REST data format
	-  REST services should not rely on a single type of data format (XML, JSON)
	-  A good REST service will serve data using the format asked for by the client.
*  Designing a REST Service
	-  use the HTTP verbs for standard CRUD operations
	-  use Cache-Control HTTP header value to control cacheability
	-  use Location HTTP header value to indicate location of newly created items
	-  use HTTP status codes generously
	-  use correct MIME type
*  REST Maturity Model
	-  Leonard Richardson
		0. The Swamp of POX
		1. Recourses
		2. HTTP Verbs
		3. Hypermedia Controls
		+ Glory of REST
* REST and AngularJS
	- the `$http service` can interact with any HTTP service
		+ it uses the Promise API, and adds `success() / error()`
	- AngularJS defines the `$resource service`, which is specifically created to interact with a single resource in a REST service
	- RESTangular project - very promising
```javascript
	angular.module('MusicApp').factory('SongResource', ['$http', function($http){
		return {
			getSongs: function () {
				return $http({ method: 'GET', url:'api/v1/songs' });
			},
			//	...
		};
	}]);
```
* Cross-origin issues 
	- client issues a request to a web service , and the two are not from the same origin. Usually results in an error, unless the service has been configured to allow request from other origin.
	- The client will begin by issuing an HTTP OPTIONS request, asking for permission to make a real request.

### 2.8 UI Controls

* AngularUI
	- ui-bootstrap
		+ `$modal` - flottur 'alert' gluggi
		+ `EntitDlg.show().then(function(newEntity) { });`
* AngularStrap
* KendoUI

### 2.9 Unit testing

* When testing Angular modules, we need to include the `ngMock module`
* If angular-mock is included after Jasmine, it will add:
	- `module()` - ensures app modules are available in our tests if we include the following in our test spec: `beforeEach(module('MyApp'));`
	- `inject()` - ensures we can use dependency injection in our code, i.e. we can wrap parameters in this function and it will take care of locating the dependencies

* Code coverage
	- Istanbul

---
## 3. HTML5
---

### 3.1 Introduction

* New elements
	- structural elements: `<header>`, `<footer>`, `<nav>`, `<article>`, `<section>`, `<aside>`
	- form elements and their attributes: `<input type='color|data|ragnge etc.'>`, `<input placeholder>`
	- multimedia elements: `<canvas>`, `<audio>`, `<video`, and `<source>`
	- other elements: `<command>`, `<datagrind>`, `<datalist>`, `<datatemplate>`, `<details>`, `<dialog>`, `<event-source>`, `<figure>`, `<mark>`, `<meter>`, `<menu>`, etc.
* Obsolete elements
	- `frameset`, `frame`, `noframe`
	- `acronym`
	- font, big, center and strike
	- presentational attributes such as bgcolor, cellspaceing.
* Reborn elements
	- `small` - indicates small print 
	- `b` - its purpose now is "to be stylistically offset from the normal prose without conveying any extra importance"
	- `i` - text "in an alternate voice or mood"
* The data- attribute
	- All elements may use attributes with custom names, as long as the name starts with "data-"
		+ `<span data-songlength='3m12s'>Special</span>`
* JS APIs
	- geolocation
	- local storage
	- battery status
	- gamepad API
	- device orientation
	- page visibility
	- vibration
	- web sockets (now have their own spec)
* **polyfills** - features/elements emulated in older browser using a combination of JS and CSS.
* Feature detection
	- Don't use browser checks
	- Modernizr lib - checks each feature individually

### 3.2 Canvas

* `<canvas>` provides a drawing surface
	- in theory, supports both 2D and 3D drawing
		+ in practice, only 2D drawing is supported currently
	- All drawing on the canvas is done using JS
	- **canvas is a raster image**
* Registering events
```
	canvas.addEventListener('click', function () {
		// Code ...
	}, false);
```

	- Mouse events:
		+ `mousedown` / `mouseup`
		+ `mousemove`
		+ `mouse over` / `mouseout`
		+ `click`
		+ `dblclick`
* Drawing a rectangle
	- `fillRect()`, `strokeRect()`, `clearRect()`
```javascript
	context.fillStyle = 'blue';
	context.fillRect(x, y, width, height);
	context.strokeRect(x, y, width, height); // Drawing the outline
```

* Drawing a line
```javascript
	context.beginPath();
	context.moveTo(x1, y1);
	context.lineTo(x2, y2);
	context.stroke();
```

* Drawing a circle
```javascript
	context.beginPath();
	context.arc(x, y, radius, 0, 2 * Math.PI, false );
	context.stroke();
```

* Drawing text
```javascript
	context.strokeText();
	context.fillText();
	context.measureText();
```

* Libraries and alternatives
	- KineticJS
	- RaphealJS
		+ encapsulates vector drawings using SVG (not canvas!)

### 3.3 Web Sockets

* Before HTML5
	- polling
		+ "are we there yet?"
	- long polling
		+ client initiates a request -> server replies when there is something to deliver
		+ when the sever sends a response back the client immediately issues anther request
* WebSockets
	- two-way connection with the server
	- Opens the possibility of pushing data from server to client, without the client explicitly requesting the data
* WebSockets interface
	- 3 public methods
		+ `constructor`
		+ `send()`
		+ `close()`
	- few events are exposed:
		+ `onopen` - called when the connection has been opened
		+ `onmessage` - called when a message from the server is received
		+ `onclose` - called wen the connection has been closed
		+ `onerror` - if an error occurs
* WebSockets encapsulated
	- Socket.io
	- SignalR is an APS.NET encapsulation
	- Often these libraries resort to long polling if web sockets are not supported by the client
* Server Side Events
	- data flows only from server to client
	- Uses HTTP as a transmission protocol (WebSockets use their own protocol)
	- has built-in support for multiple event types
* Socket.io events and AngularJS
	- Events received from the socket.io are not visible to Angular by default
	- We must *wrap* the changes to our scope objects in `$scope.$apply`

### 3.4 New Elements

* Structural elements
	- `<section>` 
	- `<article>`
	- `<header>`
	- `<hgroup>`
	- `<footer>`
	- `<nav>`
	- `<aside>`
	- `<main>`
* Images and captions
	- `<figure>` and `<figcaption>`
* Other elements
	- `<time>`
	- `<menu>`
	- `<menuitem>`
	- `<details>/<summary>`
	- `<dialog>`
	- `<ruby>`
	- `<bdi>`
	- `<mark>`
	- `<wbr>`

### 3.5 Form Elements

* <input> type:
	- `search`
	- `email`
	- `url`
	- `tel`
	- `range`
	- `number`
	- `date`, `datetime`, `time`, `month`, `week`
	- `color`
* Form element attributes
	- `placeholder`
	- `autofocus`
	- `required`
	- `autocomplete`
* Other form-related elements
	- `<meter>` - represents a scalar value within a know range, which value will usually not change
	- `<datalist>` - can be used to implement `autocomplete`, contains a list of `<options>s`
	- `<progress>` - represents the completion progress of a task
	- `<keygen>` - when requesting certificates
	- `<output>` - should be used to display the result of some calculation
* Form validation JS API
	- `willValidate` - returns true if a form validates
	- `validationMessage` - if we want to control the validation message displayed to the user

### 3.6 JS APIs

* Geolocation
	- navigator object
	- `getCurrentPosition()`
		+ return latitude/longitude coordinates (and more information)
	- is an opt-in service
	- async method, accepts a callback parameter
```javascript
	if ( navigator.geolocation ) {
		navigator.geolocation.getCurrentPosition(onGetPos);
	}
	function onGetPos(position) {
		console.log(position.coords.latitute);
		console.log(position.coords.longitute);
	}
```

* Web Workers
	- allow us to execute (long running) scripts in a different thread
	- should **never** touch the DOM
	- communication between the main code and the worker must happen using `postMessage()`
	- get a copy of the data being sent to them
```javascript
	var worker = new Worker('ProcessData.js');
	worker.onmessage = function(e) { 
		console.log(e.data);
	};
	worker.postMessage({ ... }); // Ask worker to stat
	onmessage = function(e) {
		// Where the actual work should happen
		postMessage("I am done");
	}
```

* Local Storage
	- Previously, the only method web pages had for storing data locally was to use cookies
	- Local storage is a simple key/value store, stored only on the client
	- 5MB approximately
	- Property of the `window` object
* Battery Status
	- Property of the `navigator` object
```javascript
	if (navigator.battery) {
		console.log('Is charing? ' + navigator.battery.charing);
		console.log('Level ' + navigator.battery.level);
	}
```

* Device Orientation
	- `window.DeviceOrientationEvent`
	- the event gives us alpha, beta and gamma values
* Fullscreen
	-
```javascript
	if (document.documentElement.requestFullScreen) {
		document.documentElement.requestFullScreen();
	}
```

* Page Visibility
```javascript
	document.addEventListener('visibilityChange', function (e) {
		if (document.hidden){
			// Stop fetching some updates...
		}
	}, false);
```

* Gamepad API
	- Allow us to hood a console gamepad to our computer and receive events from it in our web page

* User Media
	- `getUserMedia()`
	- Gives te code access to devices such as the webcam, microphone etc.	

### 3.7 Audio/Video

* `<audio>`
	- Attributes:
		+ `autoplay`
		+ `controls`
		+ `loop`
		+ `preload`
		+ `src`
	- inside the `<autio>` tag, multiple `<source>` elements can be present
		+ `src` - url to file
		+ `type` - MIME type of the file
* `<audio>` JS API
	- attributes:
		+ `loop`
		+ `currentTime`
		+ `volume`
	- Functions:
		+ `play()/pause()`
		+ `canPlayType(mimieType)` - returns "", "maybe", "probably"
* `<audio>` events
	- `onended` - when the song has been played
	- `progress` - indicate in our UI the progress of loading the file
	- `timeupdate` - shoe the current position
	- `oncanplay` - file has loaded enough to start playing
	- `onerror`

* `<video>` 
	- `<track>` - for subtitles

---
## 4. CSS
---

### 4.1 Fashions

* Icon fonts
	- Many icons in one file
	- Can be any size
	- Any color on any background
	- Support high DPI screens
	- Easy icon shadows
* Retina
	- Use icon font for icons
	- Use SVG's for simple images
	- Use background-size in CSS
	- Don't waste download

### 4.2 Modular CSS

* Zen Style
	-
```CSS
	#header {...}
	#header img {...}
	#header h1 {...}
	#header h1 span {...}

	.frontpage #header {...}
	.frontpage #header h1 {...}

	#header.collapsed {...}
```

	- Problem?
		+ Hard coupling of tags limits reusability

* Only use classes
	- Separate tags from styles	
```CSS
	.header {...}
	.header .loge{...}
	.header .title {...}
	.header .title .text {...}
	...
```

	- Problem?
		+ Nesting hurts performance
		+ Class name conflicts
		+ Composition conflicts

* Modular styles
	- Reusable
	- Self-contained
	- Testable
	- Composable 
	- Approachable
	- Performance
* Methodologies 
	- BEM
	- SUIT
	- Scalable and Modular Architecture for CSS
	- Object Oriented CSS
* Module design
	- Standalone
	- Low coupling 
	- Specific instead of generic
	- Small and simple
	- Don't care where used 
	- Use available space (separate layout and theme)
	- File per module (even folder)
```CSS
	.Header {...}
	.Header-logo {...}
	.Header-title {...}
	.Header-title-text {...}
	...
```

	- Pro's
		+ Minimal conflicts
		+ Great selector performance
		+ Scales to large project with multiple collaborators

### 4.3 LESS / SASS

* Precompiled CSS
	- DRY and maintainalbe
* Less/Sass - Features
	- Variables
	- Nesting
	- Parent Selector
	- Mixins
	- 
```LESS
	.size(@width; @height: auto) {
		width: @width;
		height: @height;
	}
	.box {
		.size(600px);
	}
```

	- Operators & Functions 
	-
```
	@fontsize: 13px;
	.box {
		font-size: (@fontsize * 1.2);
	}
```

	- `@import`
		+ `@import "styles.css"`
	- Extend (Inheritance)

```LESS
	.clearfix() {
		// ..
	}
	.grind:extend(.clearfix) {
		border: 1px solid #333;
	}
```

* Less
	- Needs JS runtime to compile (NodeJS)
	- compiler can run in browser during dev
* SASS
	- Needs ruby to compile
	- Often used with Compass
		+ Reusable mixins
		+ Asset helpers (data-uri, sprites)
	- Custom functions
* Other popular tools
	- Autoprefixer
	- Stylus
	- Rework

### 4.4 Responsive Web Design

* Grid layouts
	- Fixed grids
		+ Uses pixels to specify the width of each column
		+ Employs tricks for responsiveness 
	- Fluid grids
		+ Uses relative column size
		+ Fluidly fits any browser size
		+ Usually stops at some max-width
		+ When using relative size, the context becomes important
			* When the width of an element is specified in %, it is relative to the size of the parent element
			* When it is specified in `em's`, it is relative to the `font-size` of the element.
* Fluid typograpy
	- Make text smaller on smaller screens
	- Simple to implement
		+ Use `em's` for font sizes across the page
		+ Target small screens with a media query which make the base `font-size` smaller
	- Sadly, you lose a free text-zoom accessibility bonus
* Media types
	

### 4.5 Transform

* 2D Transform Functions
	- `translate(x,y) translateX(x) translateY(y)`
	- `scale(x,y) ...`
	- `rotate(z)`
	- `skewX(x) skewY(y)`
	- `martrix(a, b, c, d, tx, ty)`
* 3D Perspective
	- First need perspective
	- Default perspective none or 0 makes everything flat
	- Child element can then be transformed in 3D
		+ Positive Z appears closer to the camera
		+ Negative Z appears further away
		+ The effect is more intense with lower perspective
* 3D Transform Functions
	- `translate3d(x, y, z)`
	- `scale3d(x,y,z)`
	- `rotate3d(x, ,y z)`
	- `martrix3d(m00...)`

### 4.6 Animations

* Predefine animations using `@keyframes` blocks
* Keyframes have no knowledge of timing
* Only affect styles of one element


### 4.7 Graphics Performance

* For most DOM and CSS changes, the browser needs to do one or more of the following
	- **Layout/Reflow** - calculates the position of all affected DOM nodes
	- **Paint/Render** - Paints dirty regions of the page into a bitmap buffer
	- **Composite** - Overlays bitmap buffer/layers on top of each other, often of the GPU
* Layout
	- Things that cause layout
		+ All DOM changes
		+ All positional styles
	- Things that slow down layout
		+ Very large DOM trees
		+ Changes that affect the whole page
		+ Complicated layout
* Frames per second
	- Animations should try to match the refresh rate of the device
		+ Phones: 55-60hz
		+ Laptops: 58-60hz
		+ Most monitors: 50-60hz
	- Performance
		+ < 15 fps - individual frames can be made out
		+ 30 fps - can be smooth as long as it's constant 30 fps
		+ 6 fps - smoothest animations
	- The eye is sensitive to **jank**, a disruption in consistent frame rate
* `requestAnimationFrame(function () { ... }):`
* Frame budget
	- At 60 fps, each frame only has 16.6 ms to do everything it needs
* What is hardware accelerated
	- Animated transforms and opacity
	- 3D transforms
	- Composition
	- Canvas drawing 
	- WebGL
* Moving to the GPU
	- Remove all layout and paints events in your animation frames
	- For animated elements, move the to the GPU using a 3D transfrom
	- Then only change transform and opacity in rAF
* Parallax
	- *Bad implementation* 
		+ Add event listener for scroll In event handler
		+ In event handler, change background-position based on scroll
	- *Best parallax*
		+ Add event listener for scroll
		+ Scroll handler requests an animation frame (once)
		+ In animation frame, set translate3D of child element based on the scroll
