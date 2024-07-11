# Angular

###Q.Hooks pending

---

### Q.share data between components

Method 1: Parent to Child via @Input decorator.

Method 2: Child to Parent via @Output decorator and EventEmitter.

Method 3: Child to Parent via @ViewChild decorator.

Method 4: Unrelated Components via a Service.

---

### constructor vs ngOnInit()
The constructor() should only be used to initialize class members but shouldn't do actual “work”. So, we should use constructor() to setup Dependency Injection, Initialization of class fields etc. ngOnInit() is a better place to write “actual work code” that we need to execute as soon as the class is instantiated.

---

### Q.AOT vs JIT

	Angular provides two compilation techniques, AOT and JIT, to optimize and improve performance.
 	default : AOT

  	![aot](https://github.com/shridharssg/Angular/assets/139750756/c1cdf022-81ba-4bb0-bab3-031741da9787)


---

### Q. why angular is called single page application--- 
	Single-Page Applications (SPAs) are Web apps that load a single HTML page and
	dynamically update that page as the user interacts with the app.

---

### Q. What is Typescript & why we use it?
TypeScript is an object-oriented programming language developed and maintained by Microsoft Corporation.
It is a superset of JavaScript and contains all of its elements and we can say that TypeScript is modern JavaScript with classes, optional types, interfaces, and more.
TypeScript totally follows the OOPS concept and with the help of TSC (TypeScript Compiler), we can convert Typescript code (.ts file) to JavaScript (.js file)
code.ts------>typescript compiler------->code.js

USES:
TypeScript simplifies JavaScript code which is easier to read and debug
TypeScript is Open source
TypeScript provides highly productive development tools for JavaScript IDE 
TypeScript makes code easier to read and understand
TypeScript is nothing but JavaScript with some additional features

---

### Q. Difference between typescript and javascript:

typescript 
	1.In contrast of type we can say that Typescript is a heavy weight and strongly typed object oriented compile language which is developed by Microsoft.
	2.Internal implementation of Typescriipt does not allow it to be used at server side.It can only be used at client side.
	3.For binding the data at code level Typescript uses concepts like types and interfaces to describe data being used.
	4.Code written in Typescript first need to get compiled and then converted to Javascript this process of conversion is known as Trans-piled

javascript
	1.Javascript on other hand is a light weight interpreted language and is introduced by Netscape.
	2.On other hand Javascript can be used both at client side and server side.
	3.No such concepts has been introduced in Javascript.
	4.On other hand no compilation is needed in case of Javascript.

---

### Q. Angular structure

Angular is a single page framework and platform to develop scalable applications.
An angular application is built on top of Node.js and written in TypeScript.
An Angular application is a tree of components, in which the Top level component is the application itself.
It is compiled by node and rendered by the browser itself, when bootstrapping the application.
NgModules, Components, Views, and Services are the basic building blocks of an angular application.

1.Module:A collection of NgModules forms an angular application having at least one NgModule, which is the root Module conventionally called AppModule.
@NgModule(…) decorator is used to decorate a TypeScript class into a Module.

2.Component:A Component is a functional code block as a typescript class decorated with @Component(…) decorator having some metadata which defines a template.

3.Template:Templates are the UI elements of the application, which are defined by the Components

4.Service (injectable):If the data or functionality is not view specific, then it can be moved into a service.
 A Service provides extra functionality that can be injected into Components through dependency injection

---

### Q. Data Binding

Data binding in AngularJS is the synchronization between the model and the view.

1.One-way data binding provides a unidirectional connection that binds the variables between the model and the view.
--Interpolation:
String interpolation allows you to embed variables dynamically in the corresponding component template by using the {{ <variable> }} syntax.
Eg:<div>
  <a href="{{ link }}">{{ pizza.name }}</a>
  <p>Ingredients: {{ pizza.ingredients.join(', ') }}</p>
</div>

2.Property Binding:This allows you to assign values to the properties of html elements in the template
Eg: <div>
<img [src]=link> //property binding syntax [<property name>] = value

3.Event binding allows you listen and respond to user interactions. This could be mouse clicks or movements, or keystrokes.
     Parenthesis (<event to listen for>) are used here to bind to a target event.

In Angular, it is also possible to define custom events. Custom events allow a child component to transfer data to a parent component when an event is triggered.
This can be useful when user input data is retrieved in one component but is required in a separate component.
To define a custom event, the @Output decorator is used which is assigned to an EventEmitter object

4.Two-way data binding is a combination of property binding and event binding
  it listens for events and updates values to the view simultaneously.
  Angular uses the syntax [(<property>)] for two-way data binding. We’re using the ngModel directive here to to bind review to the input value.

Eg:<div class="container">
    <input type="text" [(ngModel)]="review">
    <p>{{ review }}</p>
    <button>Submit Review</button>    
</div>

@Component({
  selector: "app-root",
  templateUrl: "./app.component.html",
  styleUrls: ["./app.component.css"],
})
export class AppComponent {
  review="Default review";
}

---

### Q. Pipes

. Angular Pipes are used to transform data on a template, without writing a boilerplate code in a component.
. A pipe takes in data as input and transforms it to the desired output.
. We can apply two formats to single data by chaining pipes. A chained pipe is when the output of the first pipe is input to the next pipe.
. It is decorated with @pipe and implements from PipeTransform

Eg:Date Pipe: {{ dateToday | date | uppercase}}<br>       o/p:JAN 24, 2022
Name: {{ name | uppercase}}       o/p:RAMYA

1.Pure pipe
	A pure pipe is only called when Angular detects a change in the value or the parameters passed to a pipe
	Eg: {{ myVariable | filterPipe }}
	@Pipe({
	  name: 'filterPipe', 
	  pure: true     
	})
	export class FilterPipe {}


2.Impure pipe:
	An impure pipe is called for every change detection cycle no matter whether the value or parameter(s) changes.
	 you can make *any* Pipe impure just by setting the pure flag to false in your declaration 
	
	@Pipe({
	  name: 'filterPipe', 
	  pure: false
	})
	export class FilterPipe{}


Pure pipes are the pipes which are executed only when a “PURE CHANGE” to the input value is detected.
So impure pipe executes everytime irrespective of source has changed or not. which leads to bad performance. thats why it is not recommneded to use pipes for filtering data.

3.Custom Pipes:
	convert the data in the format that you desire. Angular Pipes are TypeScript classes with the @Pipe decorator. 

(https://medium.com/@ghoul.ahmed5/pure-vs-impure-pipe-in-angular-2152cf073e4d) Link for Pipe

```
---
```

### Q. Angular Route Guards

We use the Angular Guards to control, whether the user can navigate to or away from the current route.

-->Why Route guards:One of the common scenario, where we use Route guards is authentication.
    We want our App to stop the unauthorized user from accessing the protected route.
    We achieve this by using the CanActivate guard, which angular invokes when the user tries to navigate into the protected route

-->Uses of  Angular Route Guards

To Confirm the navigational operation
Asking whether to save before moving away from a view
Allow access to certain parts of the application to specific users
Validating the route parameters before navigating to the route
Fetching some data before you display the component.

-->Types of Route Guards
The Angular Router supports Five different guards, which you can use to protect the route
1.CanActivate
2.CanDeactivate
3.Resolve
4.CanLoad
5.CanActivateChild

---

### Q. Forms

--Forms are used to handle user input data. Angular 8 supports two types of forms. They are Template driven forms and Reactive forms

1.Template driven forms : Template driven forms is created using directives in the template. It is mainly used for creating a simple form application
2.Reactive Forms

Reactive Forms is created inside component class so it is also referred as model driven forms. Every form control will have an object in the component and this provides greater control and flexibility in the form programming. Reactive Form is based on structured data model.

---

### Q. SetValue and patchValue difference

1. If setValue is passed with an object that have lesser or greater number of keys as compared to form controls, then setValue will through error.
If patchValue is passed with an object that have lesser or greater number of keys as compared to form controls, then patchValue will patch value for those controls which are matching with this FormGroup structure and will not throw any error.

2. Suppose we pass an object to setValue with an extra key, let’s say, ‘xyz’ which are not part of the structure of userForm.We will get error in browser console.
Object with extra key will work with patchValue method. It will not throw error and update the form control value for matching keys.

---

### Q. Directives

AngularJS directives are extended HTML attributes with the prefix ng-.
The ng-app directive initializes an AngularJS application.
The ng-init directive initializes application data.
The ng-model directive binds the value of HTML controls (input, select, textarea) to application data.

eg: <div ng-app="" ng-init="firstName='John'">
<p>Name: <input type="text" ng-model="firstName"></p>
<p>You wrote: {{ firstName }}</p>
</div>

---

### Q. Routing

If you want to navigate to different pages in your application, but you also want the application to be a SPA (Single Page Application), with no page reloading, you can use the ngRoute module.

EG:  var app = angular.module("myApp", ["ngRoute"]);
app.config(function($routeProvider) {
  $routeProvider
  .when("/", {
    templateUrl : "main.htm"
  })
Now your application has access to the route module, which provides the $routeProvider(to configure diff routes in app)

---

**lazy loading**

Lazy loading is a technology of angular that allows you to load JavaScript components when a specific route is activated. It improves application load time speed by splitting the application into many bundles.
Lazy loading helps to keep the bundle size small, which helps reduce load times. We must use the class decorator to create an Angular module @NgModule, and the decorator uses a metadata object that defines the module.

**Eager Loading**:
used to load core modules and feature modules that are required to start the application.
Pre-Loading: used to load specific feature modules that are very likely to be used soon after the application started.
Lazy Loading: all other modules could be lazily loaded on demand after the application started.

The main properties are:

import: Components of this module are used with Array with other modules.
Declarations: It receives an array of the components.
Export: Defines an array of components, directives, and pipes used by other modules.
Provider: Declares services that are available to the entire application if it is a root module.

---

### Q. sharing data
1.Share data b/w parent to child component:

---

### Q. Diff b/w promise and observable
Promise-A Promise handles a single event when an async operation completes or fails.            							
Observable-An Observable is like a Stream (in many languages) and allows to pass zero or more events where the callback is called for each event.

Observable also has the advantage over Promise to be cancellable. If the result of an HTTP request to a server or some other expensive async operation isn't needed anymore, the Subscription of an Observable allows to cancel the subscription, while a Promise will eventually call the success or failed callback even when you don't need the notification or the result it provides anymore.

Observable:
handles multiple values over a period of time
Is not called until we subscribe to the Observable
Can be canceled by using the unsubscribe() method
Provides the map, forEach, filter, reduce, retry, and retryWhen operators

Promise:
handles only a single value at a time
Calls the services without .then and .catch
Cannot be canceled
Does not provide any operators

While a Promise starts immediately, an Observable only starts if you subscribe to it. This is why Observables are called lazy.
			  Error
promise------------->then-------->fail
			|success
			---------->data
		  fail
Observable	---------->fail
		|
		|	cancel
------------------------------->retry
		|
		|	success
		---------------->subscribe(), map(),Filter()

---

### Q. async pipe

The async pipe in angular will subscribe to an Observable or Promise and return the latest value it has emitted. Whenever a new value is emitted from an Observable or Promise, the async pipe marks the component to be checked for changes. When the component gets destroyed, the async pipe unsubscribes automatically to avoid potential memory leaks.

The example below binds the time Observable to the view. The Observable continuously updates the view with the current time.
@Component({
  selector: 'async-observable-pipe',
  template: '<div><code>observable|async</code>: Time: {{ time | async }}</div>'
})
export class AsyncObservablePipeComponent {
  time = new Observable<string>((observer: Observer<string>) => {
    setInterval(() => observer.next(new Date().toString()), 1000);
  });
}

---

### Q. Http Modules(get,Post)

Post syntax:this.http.post<any>('apiURL')//<any> is used to handle any properties returned in the response
Get Syntax: this.http.get<any>('apiURL')

---

### Q.Interceptors

HttpInterceptor was introduced with Angular 4.3. It provides a way to intercept HTTP requests and responses to transform or handle them before passing them along.Although interceptors are capable of mutating requests and responses, the HttpRequest and HttpResponse instance properties are read-only, rendering them largely immutable

		req		  req
Angular app--------->Interceptors---------->Backend
	  <---------    	<----------	   	
	        res		   res

---

let emp=[{}]
emp.sort((a,b)=>{
return a.ge-b.age
})
emp.forEach((e)=>{
console.log(${e.name}${e.age})
})

fun removeDuplicateArrayValues(arr){
return [new Set(...arr]

---

### Q.Circular dependency:

Circular dependency occurs when service A injects service B, but service B in turn injects service A, usually indirectly. For example, B depends on service C which depends on
A – A -> B -> C -> A forms a circle

how to resolved it ?

In some scenarios,
 we can duplicate the required code and solve circular dependency.
Or we can create a new service and move that code to that new service to avoid circular dependency.

