# Angular-basic-notes
My Angular 8+ Notes.......
This repository is notes of my angular 8 journey.I will write everthing that I learn, Maybe this repository guide you too.

## SECTION 1: INTRODUCTION

* Angular creates single page web apps. As the users browses the app, content is dynamically loaded into the html using Javascript. (Without changing url)
* src folder is where the work happens. Assets folder can be used to store static files like images etc, app folder is for the app code. and the environments folder can be used to store needed variables
* In Angular we use components to build up the page
* with [(ngModel)]="" you can bind something to a property of the component.ts, which is connected to the html file. the .html is what you see, while the .ts is the logic behind it
* Directives are helpers/instructions you can place in your html template which will do something at runtime depending on what commands you gave it
* Typescript is a Javascript superset. It offers more features than Javascript like classes, interfaces, types. Uses strong typing(you define if something is a string, number etc). Builds into vanilla JS
* Angular-cli.json allows you to define imports of global stylesheets

## SECTION 2: The Basics

* The server serves the index.html file to the browser
* In the component.ts the decorator has a selector which gives it a name, for example 'app-root'. This can than be used in the index.html like <app-root></app-root> to connect it with that component. Component.html has the actual content
* When using ng serve to save your project, it bundles the needed Javascript files and adds them to the html (files Angular needs to work)
* main.ts is the code that gets exectured first on page load
* platformBrowserDynamic().bootstrapModule(AppModule); starts/bootstrapts the Angular app by passing a 'AppModule' to this method. And 'AppModule' refers to the app.module.ts file
* main.ts starts things off by bootstrapping an angular app, passes AppModule as an argument -> in this module you say that there is a app.component which should be known when you start yourself(bootstrap array) -> Angular checks the component.ts and now knows the selector (eg: <app-root>) and now is able to handle this selector in the index.html file

### COMPONENTS

* Your app is build by composing multiple components (You start off with the app/root component, which holds the entire app by nesting components within it)
* Angular components allow you to split up a big app in multiple reusable parts. Each component with it's own 'busines logic'/styling
* New components you create aren't added to the bootstrap array, thus directly to the index.html. But instead are added to the app.component.html. As this is the root component (because it's called on by main.ts and added in the bootstrap array in the app.module.ts)
* Generally all your app related subfolders and files go into the 'app' folder. This includes new components
* It's good practice that each component has it's own folder
* It's good practice to name a component like this: name.component.ts
* A component is a typescript class. Angular uses this as a blueprint to create objects with it
* Using export class makes it so that a component can be used outside of it's own file, like in other components
* Typescript decorators can be used to 'enhance' your classes and other elements of code
* Using import { Component } from '@angular/core'; you can important the decorator @Component so angular knows to use it. Within @Component you can store metadata about the class
* 'Selector' within a class decorator is basically the HTML tag which you can use to call this component in templates (has to be unique)
* 'templateUrl' let's you define the html template file that the specific component uses
* Modules are used to bundle up multiple components into 'packages', describing which functionalities and features these components use
* Modules start off as a component but are transformed into something else by using a decorator. the @NgModule decorator
* New components need to be registered in the module so Angular knows it's there. Angular won't scan all your files automatically
* @NgModuyle has declarations. This is where you can declare new components to be used
* Added components need to be imported into the module
* 'imports' in @NgModule let's you import other modules into this one. To make this one a bit leaner and outsource some stuff
* You can create components using the cli with 'ng generate component name'. This creates the folder structure within the app folder with the component files
* You can nest components by calling their selector in a html template, and then calling the component to which that html belongs again in another component
* Each component has to have a template or a templateUrl defined. Depending if you want a seperate template or inline templateUrl. Styles and selectors are optional, but template/templateUI isn't
* Styles can be defined inline or externally by using styleUrls. StyleUrls is an array so you can use multiple external stylesheets
* using styles inline within the component.ts is done by creating an array of objects, with properties as style lines
* You can use the component selectors in multiple ways. You can use a html tag, class or attribute as the selector name to call it within the html template
* The constructor in the export class is a method that's executed at the moment that the component is created by Angular(method typescript has which is called once component is created)

### DATABINDING

* Databinding is a communication between your component Typescript code and the html template (output data or react to user events)
* String interpolation {{ data }}
* Property binding [property]="data"
* Event binding (event)="express", this allows to react to user input, like clicking a link
* Two-way-databinding (reacting to user events and outputting data at the same time)

#### String interpolation (outputting data in a template)

* Using {{VARIABLE}} you can have a piece of data that's exported by the component in the html, instead of a static string
* You put methods or strings between the {{}}, whatever is between it; it must return a string in the end (no multiline expressions like IF)

#### Property binding

* `[disabled]="!allowNewServer"` allows you to bind a property to a html element. This can be a method which returns true/false
* Binding the elements (native) property to our typescript property, if our property in the typescript file changes, this is updated automatically in the DOM
* This is a power of Angular, it enables you to easily interact with your DOM and change things in runtime
* You can bind to html elements, directives and your own components.

#### Property binding VS string interpolation

* Instead of string interpolation {{STRING}} you can databind a string to the element like `[innerText="STRING"]`
* If you want to put some text into your html use string interpolation, if you want to dynamically change a property use property binding
* Don't mix property binding and string interpolation

#### Event binding

* Events use () instead of [] to signal event binding `(click)="METHOD()">`
* As a general rule you don't want to put too much logic into your template, but instead in your typescript and use methods to call it
* You can bind to all properties and events, use console.log() on the elements to see which properties and events it offers
* For events you don't bind to onclick but only to click (=> (click))
* Google YOUR_ELEMENTS properties or YOUR_ELEMENT events to see lists
* `$event` is a variable used to send the data to the method. An event has data, like click location or input value. With `$event` we can capture this data and use it
* (<HTMLInputElement>event.target).value; This tells Typescript that we're getting the value from an HTML element


#### Two-way binding

* Instead of (input) you can use `[(ngModel)]="serverName"`. This is called using a directive. It will trigger on input event and update the variable automatically
* Using two-way binding, the ngModel updates the value of the input aswell as the variable it refers too in the method.
* Two-way binding is an easy way to react to an event in both directions
* In order for two-way binding to work you need to enable the ngModel directive. This is done by adding FormsModule to the imports[] array in the AppModule
* You also need to important the `@angular/forms` in the app.module.ts file `import { FormsModule } from '@angular/forms';`

### Directives

* Directives are instructions in the DOM. For example using a component selector in the HTML to tell angular to use it. Components are directives with templates
* `<p appTurnGreen>Receives a green background!</p>` is a directive without a template. It's a custom directive which instructs Angular to do something in the DOM
* Directes are used with the attribute selector (css classes are also possible just like with component selectors)
* Using the `@Directive({})` decorator you can define the selector, you can write the logic for it in the TS file

#### build in Angular directives

##### ngIf (structural directive)

* ngIf directive allows you to conditionally output data
* Use a `*` symbol (#ngIf) before a directive when it changes something in the structure of the DOM. Either adding or removing elements
* #ngIf requires a true/false. `#nfIg="true/false"` or an expression that returns true or false
* nfIf adds or removes elements from the DOM, it doesn't just hide them
* if looping through an array with ngIf, the ngIf needs to be in the ngFor, meaning in a child element etc
* Using a marker you can set an else for the ngIf:

```
<p *ngIf="serverCreated; else noServer">Server was created, server name is {{serverName}}</p>
<ng-template #noServer>
    <p>
        No server was created
    </p>
</ng-template>
```

##### ngStyle (attribute directive)

* attribute directives don't add or remove elements in the DOM. They only change the element they were placed on
* Using [ngStyle], the square brackets aren't part of the directive name. We only indicate that we want to bind the directive to a property
* `[ngStyle]="{backgroundColor: getColor()}">` we're binding a method which returns a color to the element:
```
getColor() {
    return this.serverStatus === 'online' ? 'green' : 'red';
}
````
* ngStyle allows us to dynamically update styles

##### ngClass

* ngClass allows you to enter classes conditionally (true/false)
* [ngClass]="{online: serverStatus === 'online'}", the online class is added to the element if the server is online

##### ngFor (structural directive)

* loop through an array and create elements based on it ( for of loop)
* `<app-server *ngFor="let server of servers"></app-server>`, this loops through server and assign a <app-server> component for each in the array
* `*ngFor="let logItem of log; let i = index"` this gives you access to the index of the current iteration, when looping an array

