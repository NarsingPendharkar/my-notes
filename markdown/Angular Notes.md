**Basic Concepts**

**What is Angular, and how is it different from AngularJS?**

* Angular is open-source typescript based front end framework for building dynamic single page application.
* AngularJS (v1.x) is based on JavaScript and uses a two-way binding architecture
* It is developed by google and mainly used for development of single page application.
* Angular offers improved performance with A head-of-Time (AOT) compilation, component-based architecture, and dependency injection.
* Angular is a TypeScript based full-stack web framework for building web and mobile applications.

**Difference between Angular and AngularJS**

|  |  |
| --- | --- |
| Angular | AngularJS |
| Angular is based on TypeScript language. | AngularJS is based on JavaScript language. |
| All the popular mobile browsers support Angular. | Mobile browsers do not support AngularJS. |
| It has the feature of dependency injection. | It does not support dependency injection. |
| Angular has CLI tool. | CLI tool is not available in AngularJS. |
| It has component-based structure. | It has MVC (Model View Controller) based architecture. |

**How to install Angular?**

* **Installation of Node.js and npm (node –version) (npm-v)**
* **Installation of typescript (npm install -g typescript)**
* **Installation of angular Command line interface (npm install -g @angular/cli)**
* **Check Angular Version :**  **ng --version**

**Steps to create Angular Application**

1. **Install angular CLI**
2. **Create first app using ng new my-app-name**
3. **Locate to project directory**
4. **Run project by using ng serve**

### Angular CLI Workspace for practice to save disk

#### Step-by-step:

ng new angular-learning-workspace --create-application false

cd angular-learning-workspace

ng generate application project-one

ng generate application project-two

📁 Your structure will look like:

angular-learning-workspace/

├── node\_modules/ <-- Shared

├── projects/

│ ├── project-one/

│ └── project-two/

├── angular.json

🟢 Only one node\_modules, one package.json.

**Project Structure of Angular Application**

**![](data:image/png;base64...)**

* **src:** This directory contains all the source code for your Angular application, including components, services, modules, templates, styles, and assets.
* **app:** It is a sub-folder of src directory. It contains component files.
* **angular.json:** This is the workspace configuration file which means it defines the configuration options for the entire Angular workspace.
* **node\_modules:** This directory contains all the npm packages installed as dependencies for the project.
* **package.json:** This file contains metadata about the project and lists the npm dependencies required for the project.
* **tsconfig.json:** It is the TypeScript configuration file that specifies the compiler options for TypeScript files.
* **public**: This file is used to store asset files like images.
* **styles.css :** To apply CSS globally.

**What is the purpose of Angular CLI? Can you name some CLI commands?**

* **Command Line Interface (CLI) is a powerful command line tool provided by the angular to develop, build, Run and Create the components.**
* CLI automates app creation, testing, and deployment.

**Common commands:**

|  |  |
| --- | --- |
| Command | Description |
| ng new my-app | Create a new Angular project |
| ng serve | Run dev server (usually on http://localhost:4200) |
| ng build | Compile and build the project |
| ng generate component my-comp  OR ng g c my-comp | Generate a new component |
| ng generate service my-service OR ng g s my-service | Generate a new service |
| ng generate module my-module | Create a new module |
| ng generate directive my-directive | Create a new directive |
| ng generate pipe my-pipe | Create a new pipe |
| ng test | Run unit tests with Karma |
| ng lint | Lint the code for style and errors |
| ng build --prod | Build app for production (minified + optimized) |

**What is TypeScript, and why is it used in Angular?**

* **TypeScript** is a **superset of JavaScript** developed by Microsoft that adds **static typing**, **interfaces**, **classes**, and **modern ES features** to JavaScript.
* Angular is a **complex and large-scale framework**, so TypeScript brings **structure, scalability, and safety**.
* TypeScript is a superset of JavaScript that adds static typing. Angular uses TypeScript for better tooling, maintainability, and early error detection.
* In simple terms: **TypeScript = JavaScript + Types + OOP Features + Better Tooling**

### **Key Features:**

* Static type checking (string, number, boolean, etc.)
* ES6+ features (arrow functions, classes, async/await, etc.)
* Interfaces and type aliases
* Strong IDE support (auto-complete, refactoring)
* Compile-time error detection
* Modular architecture (via import/export)

**What are the building blocks of Angular?**

The primary building blocks of Angular are:

1. **Modules** (e.g., NgModules)
2. **Components**
3. **Templates**
4. **Directives**
5. **Services**
6. **Dependency Injection**
7. **Pipes**
8. **Routing**

**Components**

**What is a Component in Angular?**

* A **Component** is a **TypeScript class** which has html template and CSS which is responsible for handling template (**View**).
* Components are the building block of angular application.
* Command to create component : **ng generate component <component-name>**

**To create a component manually, follow steps below:**

1. Create folder in app for component ex: navbar
2. Create **nav.component.html**
3. Create **nav.component.css**
4. Create **nav.component.ts**

import { Component } from "@angular/core";

@Component({

    selector: "app-nav",

    templateUrl: "./nav.component.html",

    styleUrls: ["./nav.component.css"],

    imports: []

})

export class NavComponent {

    title = "Nav Component !";

}

**Every Angular Component consists of 3 things:**

|  |  |  |
| --- | --- | --- |
| Part | File Extension | Purpose |
| Class (logic) | .component.ts | Business logic, variables, methods |
| Template (view) | .component.html | UI structure (HTML) |
| Styles (optional) | .component.css / scss | Component-specific styles |

**Important Concepts :**

@Component({

    selector: "app-nav",

    template: `<h1>Hello!</h1>`,

    styles:['h1{color:blue}'],

    imports: []

})

**@Component** Decorator is used to provide metadata about the component about how to process and render the component.

**Selector :** The HTML tag used to include this component elsewhere. Ex : <app-nav></app-nav>

We can use selector by.

1. Name : **selector: "[app-nav]", // name selector**
2. Attribute : **selector: "[app-nav]", // attribute selector**
3. class **selector: ".app-nav", // class selector**
4. id : **selector: "[#app-nav]", // ID selector**

**templateUrl vs template**

* **templateUrl:** External HTML file
* **template:** Inline HTML in the .ts file

Ex : template: `<h1>Hello!</h1>`

**styleUrls vs styles**

* **styleUrls**: External CSS file
* **styles**: Inline styles

Ex : styles: [`h1 { color: red; }`]

**Standalone** :

Angular 17 and above use **standalone:true** feature by **defaut**. Although they were first introduced in Angular 14. Along with Standalone, there is imports new in decorator.

With **standalone:true** , **NgModule** is not required. This will simplify angular code and reduce extra boilerplate code.

**Export Class** : export class is used to export properties to template.

**Components Communications**

* Angular components can communicate with each other and they can share data like arrays , objects, strings , number and html etc.
* Two more components can communicate with each other by using services
* Child and parent components can communicate with each other by using @input and @Output decorators
* A child component is a component used inside parent component. Any component used inside app-component is its child component.

**Types of Component Communication:**

|  |  |  |
| --- | --- | --- |
| Communication Type | Technique | Direction |
| **Parent ➡️ Child** | @Input() | From parent to child |
| **Child ➡️ Parent** | @Output() + Event Emitter | From child to parent |
| **Sibling ↔️ Sibling** | Shared service + Subject | Cross-component |
| **Any ↔️ Any** | Using Router params, Local Storage, or Services |  |

**@Input :**

This decorator is used to pass the data from parent component to child component and we can fetch that data in child class using @input decorator

Example :

Consider we have two components i.e parent and child

1. Set the property to send from parent to child in parent class

export class ParentComponent {

  parentMsg = 'Hello from Parent!';

}

1. Send the data to child component form html

<app-child *[childMessage]*="parentMsg"/>

1. Fetch data in child component

export class ChildComponent {

  @Input()childMessage='';

}

1. Use data in Template

<h1>{{childMessage}}</h1>

**@Output:**

**@Output** decorator is used to emit event from child component to parent component. We also need to use **EventEmitter** for **@Output**.

Consider we have two components i.e parent and child and want to send data from child to parent

1. Emit the data from child component by using @output decorator and EventEmitter

@Output() messageToParent = new EventEmitter<number>();

  counter=0;

  sendMessage() {

    let count = **this**.counter++; *// Example number*

**this**.messageToParent.emit(count); *// Emit a number*

  }

1. Call this function from child component to send data

<button *(click)*="sendMessage()">Send Message</button>

1. Create a function to get data from child

count :number=0;

  showCount(*count*:number):void{

**this**.count=*count*;

  }

1. Fetch data from child

<app-child *[childMessage]*="parentMsg" *(messageToParent)*="showCount($event)"></app-child>

**Data Binding**

**What is data binding, and what are its types?**

* **Data binding is a mechanism by using that component class and templates communicate with each other.**
* **Data binding is used to establish communication between component class to view template and view template to the component class.**
* **Angular uses the MVC framework to handle data binding**
* **Types of Data Binding :**

1. **One Way Data Binding**
2. **Two Way Data Binding**

![types of data binding in angular](data:image/png;base64...)

**One Way Data Binding**

* In one way data binding data flows only in one direction i.e. component to view or view to component

![one way data binding in angular](data:image/png;base64...)

1. **Interpolation**: {{data}} (one-way from component to view).
2. **Property Binding**: [property]="valuefromcomponentclass" (one-way).
3. **Event Binding**: (event)="handler()" (one-way from view to component).
4. **Attribute Binding** : [attr.placeholder]=”Valuefromcomponetclass”

**Text Interpolation: (Read-only)**

* Text Interpolation is used to display data from a component to a view.
* we use the curly braces **{{ }}.**

**Example** : Let us consider a variable, name available in the component.

title = 'bank-app';

Then, the title can be used in the template using interpolation as shown below −

<p> Title : {{title}}</p>

Title : bank-app

**Event Binding:** **(Write-only)**

* Event binding is the process of setting an action to the event of an HTML element or another component.
* It is used to achieve one-way data binding where data flows from the view template to the component class. Here, we use the **parentheses ( ).**
* Events are actions like a mouse click, double click, hover or any other keyboard and mouse actions.
* If a user interacts with an application and performs some actions, then an event will be raised.
* Suppose there is **myAction()** function inside the component.

 myAction() {

    alert(“Button clicked !”);

 }

For this, event binding can be written as shown below −

<button *type*="submit" *(click)*="myAction">Click here</button>

Once the click event is fired, **myAction()** method will be called and executed.

**Property Binding: (Read-only)**

* Property binding lets us bind a property of a DOM.
* It is used to show or hide a DOM element, or simply manipulate the DOM. Here, we use square brackets [ ]

Let us consider a property, name available in the component.

name: string = "John"

Property binding can be written as shown below −

  <input *type*="text" *name*="username" *[value]*="name" />

**Attribute binding: (Read-only)**

* Attribute binding is used to bind the data from component to HTML attributes.
* The syntax is as follows −

**<HTMLTag [attr.ATTRNAME]="Component data">**

For example, let's consider a property, placeholder available in the component.

Placeholder : string = "Enter your name :"

Attribute binding can be written as shown below −

  <input *type*="text" *name*="username" *[attr.placeholder]*="Placeholder" />

**Two-way Data Binding**

**Two-Way Binding:**[(ngModel)]="property" (two-way).

* Two-way data binding is a two-way interaction where data flows in both ways, from component to views and views to component at the same time.
* If you do any changes in your property (or model) then, it reflects in your view and vice-versa. It is the combination of property and event binding.
* To use two way binding you need to import **FormsModule**

Example :

  <input *[(ngModel)]*="username" *placeholder*="Enter name" />

  <p>Hello {{ username }}!</p>

Username in component class

username:string='narsing';

**Directives**

* **Directives are the elements that are used to change the appearance or behaviour of DOM elements**
* **Directives are responsible for converting static DOM into Dynamic DOM.**
* **Directives are categorized based on the type of feature they provide**

**Structural Directives**

**Attribute Directive**

**Component**

## **Structural Directives**

* Change the structure of DOM by adding or removing elements.
* It is denoted by an asterisk **(\*)** symbol with three pre-defined directives **ngIf, ngFor** and **ngSwitch**.

1. **\*ngIf() :** Hide and show elements based on condition .
2. **\*ngFor():** Used to repeat elements of list of items
3. **\*ngSwitch() :** When we have multiple condition

Example :

<div *\*ngFor*="let question of questions; let i = index">

  <h1>Q{{ i + 1 }}:{{ question.question }}</h1>

  <div>

    <div *class*="answers">

      <div *\*ngFor*="let options of question.options; let i = index">

        <p>{{ i + 1 }}={{ options }}</p>

      </div>

    </div>

    <input

*type*="text"

*name*="selected"

*[(ngModel)]*="selected"

*[attr.placeholder]*="placeholder"

    />

  </div>

</div>

<div *\*ngIf*="isTrue">

  <p>Condition is true !</p>

</div>

<div *\*ngSwitch*="value">

  <h1 *\*ngSwitchCase*="1">One</h1>

  <h1 *\*ngSwitchCase*="2">Two</h1>

  <h1 *\*ngSwitchCase*="3">Three</h1>

</div>

## **Attribute Directives :**

* Attribute directives change the appearance or behavior of DOM elements or components.
* It is used just like a normal HTML attribute.
* However, the directive should be enclosed within square brackets [ ] to bind it to the element.
* The most commonly used attribute directives are as follows:
* **ngStyle** − It is used to add dynamic styles.
* **ngClass** − It adds or removes CSS classes in HTML elements.
* **ngModel** − This directive is used for two-way binding.

Example : <div>

  <h1 *[ngClass]*="clasname">NgClass Directive change the css class </h1>

</div>

<div>

  <h1 *[ngStyle]*="{'color': 'blue', 'font-size': '14px'}">ng Style Directive which chagne css style </h1>

</div>

## **Component Directives:**

* Each component of an Angular application is a directive itself.
* It is a special directive with Views.
* Also, it has @Input and @Output decorator to send and receive information between parent and child components.

**Explain the difference between components and directives.**

* **Components** control views, have a template and styles, and are the main building blocks of UI.
* **Directives** modify the behavior or appearance of DOM elements.
* **Structural Directives**: Change DOM structure (e.g., \*ngIf, \*ngFor).
* **Attribute Directives**: Change the appearance or behavior of an element (e.g., ngClass, ngStyle).

**Custom Directive in Angular**

* A **custom directive** is a user-defined directive that allows developers to extend the functionality of HTML elements.
* Command to create custom directive : ng generate directive <directive-name>
* Add custom behaviour to DOM elements (like highlight, show/hide, change color, etc.)

Steps to create custom directive :

1. Generate directive using cmd.
2. Import ElementRef, Renderer2 to select element and apply style

import { Directive,ElementRef,Renderer2 } from '@angular/core';

@Directive({

  selector: '[appCustomstyle]'

})

export class CustomstyleDirective {

  constructor(*el*: ElementRef,*renderer*: Renderer2) {

*renderer*.setStyle(*el*.nativeElement, 'background-color', 'yellow');

*renderer*.setStyle(*el*.nativeElement, 'color', 'blue');

*renderer*.setStyle(*el*.nativeElement, 'font-weight', 'bold');

*renderer*.setStyle(*el*.nativeElement, 'padding', '10px');

*renderer*.setStyle(*el*.nativeElement, 'border', '2px solid green');

  }

}

1. Import it in the component where we want to use.
2. Use it in HTML element where you want to apply

<p *appCustomstyle* >This is a custom Directive</p>

@Component({

  selector: 'app-root',

  imports: [FormsModule,CommonModule,CustomstyleDirective],

  templateUrl: './app.component.html',

  styleUrl: './app.component.css'

})

**Pipes**

* **Pipes** are simple functions that **transform data** in the **template**.
* When we get raw data from server , we can’t show as it to end-user. To make good user experience we need to modify the data into specific format and in such cases, we use pipes.
* Angular pipes take the raw data from server and transform that data into specific format and then it shown to end user.
* we can say that the angular pipes transform the data into a specific format before displaying them to the end-users.
* For pipes we use **PIPE( | )** operator.
* There are so many built in pipes in angular like uppercase, lowercase, titlecase, date, percent, currency etc.
* You can **chain multiple pipes** together.

**Example : {{ user.name | lowercase | slice:0:5 }}**

* Syntax : **(“DATA” | “FORMAT”=”FORMATEDDATA”)**

**Example:**

**{{ todayDate | date }}**

**{{ 1500 | currency }}**

**![](data:image/png;base64...)**

## **Types of Pipes in Angular:**

1. **Built In Pipes**

|  |  |
| --- | --- |
| Pipe | Usage |
| date | Formats a date |
| uppercase / lowercase | Changes text case |
| currency | Formats a number as currency |
| percent | Formats a number as a percentage |
| json | Converts object to JSON string |
| slice | Returns part of a string/array |
| async | Works with Observables/Promises |

**Example :**

  <tbody>

      <tr *\*ngFor*="let std of Student">

        <td>{{ std.name | titlecase | prefix:std.gender }}</td>

        <td>{{ std.gender }}</td>

        <td>{{ std.dob | date:'fullDate' }}</td>

        <td>{{ std.bio | slice:0:10 }}</td>

        <td>{{ std.address }}</td>

        <td>{{ std.marks | percent }}</td>

        <td>{{ std.fees | currency:'INR' }}</td>

      </tr>

    </tbody>

1. **Custom Pipes**

We can create custom pipes in angular application.

Step 1: Create pipe using cmd : **ng generate pipe pipename**

Step 2: Decorate the created TypeScript class with **@Pipe** Decorator. Inside this decorator, specify a name for the pipe.

Step 3: In the end, inherit the **PipeTransform** interface and implement its transform() method.

Example :

import { Pipe, PipeTransform } from '@angular/core';

@Pipe({

  name: 'prefix'

})

export class PrefixPipe implements PipeTransform {

  transform(*name*: String,*gender*:string ): string {

    if(*gender*=='Male'){

      return "Mr "+*name*;

    }else{

      return "Mrs "+*name*;

    }

  }

}

Import it in component class where we want to use it

import { PrefixPipe } from './prefix.pipe';

Then use it

 <tr *\*ngFor*="let std of Student">

        <td >{{std.name |prefix:std.gender}}</td>

        <td >{{std.gender}}</td>

        <td >{{std.dob|date:'fullDate'}}</td>

        <td >{{std.bio | slice:0:10}}</td>

        <td >{{std.address}}</td>

        <td>{{std.marks|percent}} <td>

        <td>{{std.fees|currency:'INR'}} <td>

      </tr>

**Parameterized Pipes:**

In Angular, we can pass any number of parameters to the pipe using a colon (:) and when we do so, it is called Angular Parameterized Pipes. The syntax to use Parameterized Pipes in Angular Application is given below.

![](data:image/png;base64...)

Angular - Forms

## **What are forms ?**

* **Forms are used to collect input data from users and enable users to interact with the application.**
* **A general form consists of various input fields such as text boxes, radio buttons, checkboxes, and dropdowns, along with a submit button that triggers the action of sending data to a server or performing some other operation within the application**

## **What are Angular Forms?**

* **Developing forms requires design skill as well as framework support for two-way data binding, change tracking, validation, error handling, etc.**
* **The Angular Framework, provides two different ways to collect and validate the data from a user. They are as follows:**

**1) Template-Driven Forms**

**2) Model-Driven Forms (Reactive Forms)**

**✅ Both provide:**

* Validation
* Form Control
* Error handling
* Form Submission

### **Template Driven Forms in Angular:**

* **Template Driven Forms are simple forms which can be used to develop forms.**
* **These are called Template Driven as everything that we are going to use in an application is defined into the template that we are defining along with the component.**
* **In order to use template driven forms we need to import FormsModule in main component.**

|  |  |
| --- | --- |
| Concept | Description |
| FormsModule | Must be imported to use Template-Driven Forms. |
| ngForm | Angular automatically creates a Form object. |
| ngModel | Used to bind input fields to variables. |
| required, minlength, etc. | Built-in validations in HTML. |
| (ngSubmit) | Handles form submission event. |

**Steps to create Template Driven From:**

1. **Import FormsModule in app component**
2. **Create a form using ngForm, ngModel, and simple validation attributes.**

<form *#userdatafromform*="ngForm" *(ngSubmit)*="onSubmit(userdatafromform)">

  <div *class*="form-group">

    <label *for*="username">Username:</label>

    <input *type*="text" *id*="username" *name*="username" *class*="form-control" *ngModel* />

  </div>

  <div *class*="form-group">

    <label *for*="email">Email:</label>

    <input *type*="email" *id*="email" *name*="email" *class*="form-control" *ngModel* />

  </div>

  <div *class*="form-group">

    <label *for*="password">Password:</label>

    <input *type*="password" *id*="password" *name*="password" *class*="form-control" *ngModel* />

  </div>

  <button *type*="submit" *class*="btn btn-primary">Submit</button>

</form>

1. **Handle Form Submission (Component TS)**

import { Component } from '@angular/core';

import { FormsModule, NgForm } from '@angular/forms';

@Component({

  selector: 'app-templateform',

  imports: [FormsModule],

  templateUrl: './templateform.component.html',

  styleUrl: './templateform.component.css'

})

export class TemplateformComponent {

  public onSubmit(*userdatafromform* :NgForm){

  console.log(*userdatafromform*.value);

  }

}

### **Model-Driven Forms (Reactive Forms) in Angular:**

* In a model driven approach, the model which is created in the .ts file is responsible for handling all the user interactions and validations
* **For this, first, we need to create the model using Angular’s inbuilt classes like FormGroup and FormControl and then we need to bind that model to the HTML form.**

**Creating Angular Reactive Forms:**

* **Step 1 : Import ReactiveFormsModule, FromGroup, FormControl from angular/form package.**
* **Step 2: Instantiate FormGroup and FormControl inside your component's TypeScript file (e.g., app.component.ts).**

import { Component } from '@angular/core';

import { EmailValidator, FormControl, FormGroup, ReactiveFormsModule, Validators } from '@angular/forms';

@Component({

  selector: 'app-reactive-form',

  imports: [ReactiveFormsModule],

  templateUrl: './reactive-form.component.html',

  styleUrl: './reactive-form.component.css'

})

export class ReactiveFormComponent {

  userdata=new FormGroup({

      username:new FormControl('',[Validators.required,Validators.maxLength(5)]),

      password:new FormControl('',[Validators.required])

    });

  afterSubmit(){

    console.log(**this**.userdata.value)

  }

  }

* **Step 3 : Now, open component's HTML template (e.g., app.component.html) and bind the form using formGroup.**

<h2>Reactive Form</h2>

<div *class*="w-50 justify-content-center " >

    <form *[formGroup]*="userdata" *(ngSubmit)*="afterSubmit()">

        <div *class*="mb-3">

          <label *for*="username" *class*="form-label">Username</label>

          <input *type*="text" *class*="form-control" *formControlName*="username" *name*="username"   />

        </div>

        <div *class*="mb-3">

          <label *for*="password" *class*="form-label">Password</label>

          <input *type*="password" *class*="form-control"  *name*="password"  *formControlName*="password" />

        </div>

        <div *class*="text-end">

          <button *type*="submit" *class*="btn btn-primary" *[disabled]*="userdata.invalid" >Submit</button>

        </div>

      </form>

</div>

* **Step 4 : At the end, use formControlName to bind each individual input field to the corresponding form control**

 userdata=new FormGroup({

      username:new FormControl('',Validators.required),

      password:new FormControl('',Validators.required)

    });

### **Which one is better – Template Driven or Reactive Forms?**

* Neither reactive nor template driven are better over each other. For example, Template Driven forms are generally used to **create simple forms**.
* On the other hand, Reactive forms are used to create **complex forms**. For example, if you want to add form controls dynamically or perform cross-field validation, then you need to use the Reactive forms approach.

## Difference between Template Driven Forms and Reactive Froms

|  |  |  |
| --- | --- | --- |
| Concept | Template-Driven Forms | Reactive Forms |
| Form building | HTML + ngModel | TS code (FormGroup, FormControl) |
| Validation | HTML attributes + Angular directives | Full programmatic control |
| Data Flow | Two-way binding | Observable streams |
| When to use? | Simple forms (login, feedback) | Complex forms (multi-step forms, dynamic forms) |

### **Angular Form Classes**

|  |  |  |
| --- | --- | --- |
| Concept | Meaning | Example |
| FormControl | Represents a single form field | Name, Email |
| FormGroup | Group of multiple FormControls | Registration form (name + email + password) |
| FormArray | Dynamic array of controls | Add multiple addresses/phone numbers |
| Validators | Functions to check validity | Required, MinLength, Pattern |
| Custom Validator | Your own logic for validation | Passwords should match |
| FormBuilder | Shortcut service to create forms faster | fb.group({...}) |

Routing

## **What is routing in angular ?**

**Answer:**

* It is the mechanism which is used to navigate between one view to another view.
* A Route is like a map that shows the way to a specific view or template.

## **Key concepts of Routes:**

1. **Routes : it is mapping between URL path and component.**

**routes = [**

**{path: 'home', component: HomeComponent},**

**{path: 'about', component: AboutComponent}**

**]**

**routes: An array contains all the routes for different components.**

**path: A path, which you can access on the URL to load the target component.**

**component: A target component will be loaded when the path is active on the URL.**

1. **Routing Module : a routing module is a module that configures the routing for an application.**
2. **Router Outlet : It is the directive that mark’s location where the router should display the routed component.**
3. **Router Link: it creates a link for routing.**
4. **Activated Route: it is the route that is currently being displayed.**

![Routing](data:image/jpeg;base64...)

## Types of routes in Angular****:****

1. **Static Routes :** Static routes are the simple routes that map specific URL path to a component.

**{path: 'path-name', component: component-name}**

1. **Dynamic Routes :** Dynamic routes allow you to display different component based on the parameter provided in URL. These routes are use parameters in the URL to dynamically load different entities of a components based on current parameter passed in URL.

**{path: 'path-name/:parameter', component: component-name}**

1. **Wildcard Routes:** These routes matches the invalid URL and then redirect to specific URL.

**{path: '\*\*', component: component-name}**

1. **Nested routes:** Nested routes are the nested inside other routes. Sometimes we want to load child component when parent component is loaded then we use nested routes to load child components.

**{ path: 'parent-path', loadChildren: [**

**{path: 'child-path1', component: component-name},**

**{path: 'child-path2', component: component-name} ] }**

Example :

export const routes: Routes = [

    {path:'',component:HomeComponent,children:[

        {path:'one/:id',component:StudentOneComponent},

        {path:'two/:id',component:StudentTwoComponent}

    ]},

    {path:'slist',component:StudentlistComponent},

    {path:'sdata',component:StudentdataComponent},

    {path:'\*\*',component:PagenotfoundComponent},

];

## Configure Routing in Angular

* To configure basic routing in application we can provide a command to create routing while creating the application.
* Cmd : ng new routing-app –routing
* If even –routing flag is not provided angular application generate routing config file by default i.e **app.routes.ts**

## Using RouterLink for Navigation

* RouterLink Directive used to set path for navigating between views and components.

<a *class*="row display-6  " *routerLink*="slist">Student List</a>

<a *class*="row display-6 " *routerLink*="sdata">Student Data</a>

<button *class*="btn btn-info ms-2 px-4" *(click)*="return()">Return to home</button>

return(){

**this**.router.navigate(['']);

  }

****Angular Services****

## What are Angular Services?

* Angular services is the peace of code that is used to perform specific task.
* Service can contain function or values or both
* A service is a reuseable class that contains business logic , data operations and helper methods to perform specific task
* Services are used to share data between components and encapsulates logic from the component.
* Whenever you need to reuse the same data and logic across multiple components of your application, then you need to go for angular service. That means whenever you see the same logic or data-access code duplicated across multiple components, then you need to think about refactoring the same logic or data access code into a service.

## What is Dependency Injection (DI)?

* DI is a design pattern which is used to inject the services and other dependency into components and other classes.
* DI provide loose coupling
* Code reusability and easy testing.

## ****Creating Angular Service****

1. Create service by using cmd : **ng generate service <service-name>**
2. To create Manually we need to create one export class and we need to decorate that class with @Injectable decorator which in angular core library ![What are Angular Services?](data:image/png;base64...)
3. The **@Injectable()** decorator in angular is used to inject other dependencies into the service.
4. When we create service it will generate tow files **service-name.service.ts** and **service-name.service.spec.ts**
5. Write Business Logic in the Service **service-name.service.ts**
6. Use the Service in a Component ![How to use register and use angular services?](data:image/png;base64...)

**Key concept :**

* **@Injectable** : This decorator indicates that the class is a service and can be injected into components.
* **providedIn:’root’ :** This speicify that the service should be provided at the root level of application.

Example :

import { Injectable } from '@angular/core';

@Injectable({

  providedIn: 'root'

})

export class DataService {

  constructor() { }

  private data = [

    {

      ID: 'std101', FirstName: 'Preety', LastName: 'Tiwary',

      Branch: 'CSE', DOB: '29/02/1988', Gender: 'Female'

    },

    {

      ID: 'std102', FirstName: 'Anurag', LastName: 'Mohanty',

      Branch: 'ETC', DOB: '23/05/1989', Gender: 'Male'

    },

    {

      ID: 'std103', FirstName: 'Priyanka', LastName: 'Dewangan',

      Branch: 'CSE', DOB: '24/07/1992', Gender: 'Female'

    },

    {

      ID: 'std104', FirstName: 'Hina', LastName: 'Sharma',

      Branch: 'ETC', DOB: '19/08/1990', Gender: 'Female'

    },

    {

      ID: 'std105', FirstName: 'Sambit', LastName: 'Satapathy',

      Branch: 'CSE', DOB: '12/94/1991', Gender: 'Male'

    }

  ]

  getData() {

    return **this**.data;

  }

}

import { Component } from '@angular/core';

import { DataService } from '../services/data.service';

import { CommonModule } from '@angular/common';

import { FormsModule } from '@angular/forms';

import{Pipe} from '@angular/core'

import { GenderpipePipe } from '../genderpipe.pipe';

@Component({

  selector: 'app-dataviewer',

  imports: [CommonModule,FormsModule,GenderpipePipe],

  templateUrl: './dataviewer.component.html',

  styleUrl: './dataviewer.component.css'

})

export class DataviewerComponent {

person:any=[];

constructor(private *dataservice*:DataService){};

ngOnInit(){

**this**.person= **this**.dataservice.getData();

}

}

<h1 *class*="text-bg-danger text-center text-white p-3 m-3  shadow-lg">Person Data</h1>

<div *class*="table-responsive">

    <table *class*="table table-hover">

        <thead>

            <tr>

                <th *scope*="col">ID</th>

                <th *scope*="col">First Name</th>

                <th *scope*="col">Last Name</th>

                <th *scope*="col">Branch</th>

                <th *scope*="col">DOB</th>

                <th *scope*="col">Gender</th>

            </tr>

        </thead>

        <tbody>

            <tr *\*ngFor*="let dataviewer of person">

                <td *scope*="row">{{dataviewer.ID|uppercase}}</td>

                <td *scope*="row">{{dataviewer.FirstName }}</td>

                <td *scope*="row">{{dataviewer.LastName}}</td>

                <td *scope*="row">{{dataviewer.Branch}}</td>

                <td *scope*="row">{{dataviewer.DOB}}</td>

                <td *scope*="row">{{dataviewer.Gender|genderpipe}}</td>

            </tr>

        </tbody>

    </table>

</div>

****Angular - HTTP Client****

## Angular - HTTP Client :

* Angular’s **HttpClient** service (from the @angular/common/http package) is used to communicate with backend services via HTTP protocols (GET, POST, PUT, DELETE, etc.).
* Angular provides a module called **HttpClientModule** and a service called **HttpClient** to handle HTTP programming.

## Configure Http client:

1. **HttpClient** Service is available inside **HttpClientModule** which is available inside the @angular/common/http package.
2. To register HttpClientModule module. You need to import the HttpClientModule in AppComponent:
3. Create a Standalone Component with HttpClient
4. Import HttpClientModule and Use HttpClient
5. Bootstrap in main.ts

Example : .

**Step 1: Implement the service**

In data.service.ts, add the following code:

TypeScript

import { Injectable } from '@angular/core';

import { HttpClient } from '@angular/common/http';

@Injectable({

providedIn: 'root'

})

export class DataService {

private apiUrl = 'https://jsonplaceholder.typicode.com/posts';

constructor(private http: HttpClient) { }

getPosts() {

return this.http.get(this.apiUrl);

}

getPost(id: number) {

return this.http.get(`${this.apiUrl}/${id}`);

}

createPost(post: any) {

return this.http.post(this.apiUrl, post);

}

updatePost(id: number, post: any) {

return this.http.put(`${this.apiUrl}/${id}`, post);

}

deletePost(id: number) {

return this.http.delete(`${this.apiUrl}/${id}`);

}

}

This service uses the HttpClient to make requests to a JSONPlaceholder API.

**Step 2: Implement the component**

import { Component, OnInit } from '@angular/core';

import { DataService } from '../services/data.service';

@Component({

selector: 'app-http-demo',

templateUrl: './http-demo.component.html',

styleUrls: ['./http-demo.component.css']

})

export class HttpDemoComponent implements OnInit {

posts: any[] = [];

constructor(private dataService: DataService) { }

ngOnInit(): void {

this.getPosts();

}

getPosts() {

this.dataService.getPosts().subscribe(response => {

this.posts = response;

});

}

getPost(id: number) {

this.dataService.getPost(id).subscribe(response => {

console.log(response);

});

}

createPost() {

const post = { title: 'New Post', body: 'This is a new post' };

this.dataService.createPost(post).subscribe(response => {

console.log(response);

});

}

updatePost(id: number) {

const post = { title: 'Updated Post', body: 'This is an updated post' };

this.dataService.updatePost(id, post).subscribe(response => {

console.log(response);

});

}

deletePost(id: number) {

this.dataService.deletePost(id).subscribe(response => {

console.log(response);

});

}

}

<div>

<h1>HTTP Demo</h1>

<ul>

<li \*ngFor="let post of posts">{{ post.title }}</li>

</ul>

<button (click)="createPost()">Create Post</button>

<button (click)="getPost(1)">Get Post 1</button>

<button (click)="updatePost(1)">Update Post 1</button>

<button (click)="deletePost(1)">Delete Post 1</button>

</div>

**Step 3: Add HttpClientModule in app.config.ts**

import { ApplicationConfig, provideZoneChangeDetection } from '@angular/core';

import { provideRouter } from '@angular/router';

import { routes } from './app.routes';

import { provideClientHydration, withEventReplay } from '@angular/platform-browser';

import { provideHttpClient, withFetch } from '@angular/common/http';

export const appConfig: ApplicationConfig = {

  providers: [

    provideZoneChangeDetection({ eventCoalescing: true }),

    provideRouter(routes),

    provideClientHydration(withEventReplay()),

    provideHttpClient(withFetch())

  ]

};

# **Lifecycle Hooks**

* **Angular application** goes through entire set of process or has a life cycle right from it initialization to end of application.

**![](data:image/png;base64...)**

|  |  |  |
| --- | --- | --- |
| Hook | Trigger | Purpose |
| ngOnChanges() | On input-bound property change | React to changes in @Input() properties |
| ngOnInit() | After component initialized | Fetch data, set up defaults |
| ngDoCheck() | During every change detection run | Custom change detection |
| ngAfterContentInit() | After content (ng-content) projected | Work with projected content |
| ngAfterContentChecked() | After projected content checked | Respond after checks |
| ngAfterViewInit() | After component's views initialized | DOM/query child elements |
| ngAfterViewChecked() | After view checked | Post-processing on views |
| ngOnDestroy() | Just before component is destroyed | Clean up (unsubscribe, etc.) |

**Angular - Authentication and Authorization**

* **Authentications means who you are or process of identification of user.**
* **Authorization means giving the permissions to the resource based on conditions**
* **Normally in web applications resource is access by using URL and based on roles access is provided to the specific URLs .**
* **In angular URL are handled by routes**
* **Angular provides the concept of router guards which is used to provide security to the application which uses authentication and authorisation**
* **Angular Route Guards help us prevent the user from accessing certain parts of the applications under specific conditions**
* **Angular provides multiple guards as follows:**

1. **CanActivate : Used to stop the access to the routes.**
2. **CanActivateChild : Used to stop access to the child**
3. **CanDeactivate: Used to stop ongoing process getting feedback from user. For example delete process can be stopped if user the user replies negative.**
4. **Resolve : Used to prefetch data before navigating to routes.**
5. **CanLoad :** Used to load assets.

**🔐 Authentication :**

**Definition:** Authentication is the process of verifying the identity of a user.

**Purpose:** It ensures that the user is who they claim to be.

**Example:** Login with username and password.

**🔒 Authorization :**

**Definition:** Authorization determines which resources the authenticated user can access.

**Purpose:** It restricts users from accessing parts of the system they’re not allowed to.

**Example:** A regular user can view profile; an admin can view user list.

|  |  |  |
| --- | --- | --- |
| Guard | Purpose | Use |
| CanActivate | Prevents navigation to a route | Used to check if user is logged in or user has permissions |
| CanActivateChild | Prevents navigation to child routes |  |
| CanDeactivate | Prevents navigation from a route (e.g., unsaved form changes) | Confirm from user before leaving unsaved changes |
| Resolve | Pre-fetches data before navigating to a route | PreFetch data from API |
| CanLoad | Prevents the lazy loading of modules |  |

**Components and Templates**

1. **What is the difference between template-driven forms and reactive forms?**
   * **Template-Driven Forms**: Define forms in the HTML template; simpler for small forms.
   * **Reactive Forms**: Define forms in the component class using FormGroup and FormControl; better for dynamic and complex forms.
2. **How do you handle events in Angular templates?**
   * Use event binding syntax: (event)="handlerFunction()". Example: <button (click)="onClick()">Click Me</button>
3. **What are lifecycle hooks? Can you name and explain their purposes?**
   * Lifecycle hooks allow developers to tap into component events. Examples:
     + ngOnInit(): Executes after the component is initialized.
     + ngOnChanges(): Executes when input properties change.
     + ngOnDestroy(): Executes just before the component is destroyed.

### **Services and Dependency Injection**

1. **What is a service in Angular, and how do you create one?**
   * A service contains reusable business logic. Create it using CLI:
2. ng generate service serviceName
3. **What is dependency injection, and how does Angular implement it?**
   * DI is a design pattern where dependencies are provided to a class rather than created by it. Angular implements DI using the injector hierarchy.
4. **What is the purpose of a singleton service?**
   * A singleton service ensures that a single instance of the service is shared across the app.
5. **Explain the difference between providedIn: 'root' and providing a service in a specific module.**
   * providedIn: 'root': Makes the service available app-wide.
   * Providing in a module: Restricts availability to that module.

### **Routing in Angular**

1. **How does routing work in Angular?**
   * Angular routing allows navigation between views (components) within a single-page application (SPA).
   * The **Router** listens to URL changes and maps them to a specific component using route configuration.
   * Example:
2. const routes: Routes = [
3. { path: 'home', component: HomeComponent },
4. { path: 'about', component: AboutComponent },
5. { path: '', redirectTo: 'home', pathMatch: 'full' }
6. ];
7. @NgModule({
8. imports: [RouterModule.forRoot(routes)],
9. exports: [RouterModule]
10. })
11. export class AppRoutingModule {}
12. **What is the purpose of RouterModule and Routes?**
    * **RouterModule**: Provides the necessary services and directives for routing (e.g., <router-outlet>, routerLink).
    * **Routes**: Defines the mapping of URL paths to components. It is an array of objects, where each object represents a route.

Example:

const routes: Routes = [

{ path: 'dashboard', component: DashboardComponent },

{ path: 'profile', component: ProfileComponent }

];

1. **How do you implement lazy loading in Angular?**
   * Lazy loading loads feature modules only when their associated route is accessed, reducing the initial bundle size.
   * Steps:
     1. Create a feature module (e.g., AdminModule).
     2. Define routes within the feature module.
     3. Use the loadChildren property in the app's routes to point to the feature module.

Example:

const routes: Routes = [

{ path: 'admin', loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule) }

];

In AdminModule:

const adminRoutes: Routes = [

{ path: '', component: AdminDashboardComponent }

];

@NgModule({

imports: [RouterModule.forChild(adminRoutes)],

exports: [RouterModule]

})

export class AdminRoutingModule {}

1. **What are route guards, and what types of guards are available?**
   * **Route Guards** control navigation to and from routes based on conditions.
   * Types of Guards:
     + **CanActivate**: Determines if a route can be activated.
     + **CanActivateChild**: Determines if child routes can be activated.
     + **CanDeactivate**: Determines if a user can leave a route.
     + **Resolve**: Pre-fetches data before the route is activated.
     + **CanLoad**: Determines if a module can be lazy-loaded.

Example of CanActivate:

@Injectable({

providedIn: 'root'

})

export class AuthGuard implements CanActivate {

canActivate(): boolean {

return isAuthenticated(); // Custom logic

}

}

Apply guard in routes:

const routes: Routes = [

{ path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }

];

1. **How do you pass parameters in Angular routes?**
   * **Route Parameters**:
     + Define a route with a parameter:
2. const routes: Routes = [
3. { path: 'profile/:id', component: ProfileComponent }
4. ];

- Access the parameter in the component:

```typescript

constructor(private route: ActivatedRoute) {}

ngOnInit() {

this.route.params.subscribe(params => {

console.log(params['id']);

});

}

```

* **Query Parameters**:
  + Pass query parameters:
* <a [routerLink]="['/profile']" [queryParams]="{ id: 123 }">Profile</a>
  + Access query parameters in the component:
* constructor(private route: ActivatedRoute) {}
* ngOnInit() {
* this.route.queryParams.subscribe(params => {
* console.log(params['id']);
* });
* }

### **Forms**

1. **What is the difference between reactive forms and template-driven forms?**
   * **Reactive Forms**:
     + Defined programmatically in the component using FormGroup and FormControl.
     + More scalable and testable.
     + Ideal for dynamic forms.
   * **Template-Driven Forms**:
     + Defined in the template using directives like ngModel.
     + Simpler, ideal for small forms.
2. **How do you perform form validation in Angular?**
   * Reactive Forms: Add validators programmatically:
3. this.myForm = new FormGroup({
4. name: new FormControl('', [Validators.required, Validators.minLength(3)])
5. });

* Template-Driven Forms: Use validation directives in the template:
* <input name="name" ngModel required minlength="3" />

1. **How do you bind form data to the component?**
   * **Reactive Forms**: Use FormGroup and FormControl bindings.
   * **Template-Driven Forms**: Use [(ngModel)]="property" for two-way binding.

### **HTTP and Observables**

1. **How do you make HTTP requests in Angular?**
   * Use the HttpClient module:
2. this.http.get('api/url').subscribe(data => console.log(data));
3. **What is the purpose of the HttpClient module?**
   * Simplifies HTTP requests and handles tasks like request headers, responses, and error handling. It also supports observables.
4. **What is an observable, and how is it used in Angular?**
   * Observables are streams of data that can emit multiple values over time. Angular uses observables for asynchronous operations like HTTP calls and event handling.
5. **What is the difference between Promise and Observable?**
   * **Promise**: Emits a single value and is not cancellable.
   * **Observable**: Emits multiple values, can be cancellable, and supports operators like map and filter.

# **Angular Modules**

**What is a Module in Angular or purpose of NgModule?**

An Angular Module is a container that groups related components, directives, pipes, and services together. It helps organize an application into cohesive blocks of functionality.

**What are the different types of modules in Angular?**

|  |  |
| --- | --- |
| Module Type | Purpose |
| **AppModule** | Root module that bootstraps the application. |
| **FeatureModule** | Organizes related features (e.g., UserModule, ProductModule). |
| **SharedModule** | Contains reusable components, directives, and pipes used across modules. |
| **CoreModule** | Contains singleton services like auth, logger; imported once in AppModule. |

**What is standalone: true in Angular?**

**standalone: true** is a property in Angular 14+ that allows you to create components, directives, and pipes **without declaring them in a module**. These are **self-contained and reusable** entities.

### **When to use standalone: true?**

Use it when:

* You want reusable components without tight coupling to a module.
* You are building micro frontends or lazy-loaded components.
* You want to simplify the structure in Angular 14+ apps.

### **Does standalone: true improve performance?**

Yes. It improves tree-shaking during build time and allows for faster lazy loading since Angular doesn't need to analyze full modules to render components.

**Explain the difference between feature modules and shared modules.**

**Feature Modules**: Contain components, services, and directives specific to a feature.

**Shared Modules:** Contain reusable components, pipes, and directives to be imported into other modules.

**How do you organize an Angular application into modules?**

Create feature modules for individual functionalities, a shared module for reusable code, and core modules for singleton services.

# **Performance and Optimization**

1. **What is AOT (Ahead-of-Time) compilation, and why is it important?**
   * AOT compiles Angular HTML and TypeScript into JavaScript at build time, reducing runtime overhead and improving performance.
2. **How does Angular handle tree shaking?**
   * Tree shaking removes unused modules and code during the build process, reducing bundle size.
3. **What are some ways to optimize an Angular application?**
   * Use lazy loading for routes.
   * Minimize change detection with OnPush.
   * Optimize template bindings.
   * Enable AOT compilation.
   * Use lightweight libraries.

### **Miscellaneous**

1. **What are Angular Pipes? How do you create a custom pipe?**
   * Pipes transform data in templates. Create a custom pipe:
2. @Pipe({ name: 'customPipe' })
3. export class CustomPipe implements PipeTransform {
4. transform(value: string): string {
5. return value.toUpperCase();
6. }
7. }
8. **What is the difference between Angular’s ngOnInit and the constructor?**
   * **Constructor**: Used for dependency injection.
   * **ngOnInit**: Executes after component initialization, ideal for initialization logic.
9. **What is the purpose of Angular’s zone.js?**
   * zone.js intercepts and keeps track of asynchronous tasks, enabling Angular's change detection.
10. **What are interceptors, and how are they used in Angular?**
    * Interceptors intercept HTTP requests and responses for tasks like adding headers or handling errors.
11. @Injectable()
12. export class AuthInterceptor implements HttpInterceptor {
13. intercept(req: HttpRequest<any>, next: HttpHandler) {
14. const authReq = req.clone({ setHeaders: { Authorization: 'Bearer token' } });
15. return next.handle(authReq);
16. }
17. }
18. **Explain the role of Change Detection in Angular.**
    * Change detection updates the DOM whenever data changes in the component. Strategies:
      + **Default**: Checks the entire component tree.
      + **OnPush**: Only checks when input properties change.
19. **What is the role of the trackBy function in ngFor?**
    * Optimizes rendering by tracking items using a unique identifier. Prevents unnecessary DOM updates.

### **Practical Scenarios**

1. **How would you debug an Angular application?**
   * Use browser dev tools, Angular DevTools, and console.log().
   * Debug HTTP calls with network tools.
   * Check errors in the console and investigate stack traces.
2. **How would you handle a slow-loading Angular application?**
   * Implement lazy loading and AOT compilation.
   * Optimize bindings and use the OnPush change detection strategy.
   * Minimize heavy computations in templates.
3. **Describe a project you worked on and your role in the team.**
   * Prepare a concise description of a project, highlighting your role in implementing features, solving problems, or optimizing performance.
4. **How do you manage version control in Angular projects?**
   * Use Git for version control. Follow practices like branching, committing changes with meaningful messages, and using pull requests for code review.

Let's focus on advanced concepts and real-world scenarios:

### **Architecture and Best Practices**

1. **How do you design a scalable Angular application architecture?**
   * **Answer**:
     + Use a modular architecture with feature modules for specific functionality.
     + Implement a shared module for reusable components and pipes.
     + Use a core module for singleton services.
     + Apply lazy loading for optimizing large-scale applications.
     + Follow SOLID principles for component and service design.
2. **How do you handle state management in Angular applications?**
   * **Answer**:
     + Use libraries like NgRx, Akita, or services with BehaviorSubjects.
     + Implement NgRx for complex applications with features like selectors, effects, and reducers.
     + Use the OnPush change detection strategy for performance.
     + Ensure immutability by using libraries like immer or plain JavaScript techniques.
3. **How do you ensure consistent coding standards in a team project?**
   * **Answer**:
     + Use **Angular Style Guide** for consistent structure.
     + Enforce linting rules with **ESLint** or **TSLint**.
     + Implement **prettier** for code formatting.
     + Set up pre-commit hooks with **Husky** to run linters and unit tests.
     + Conduct regular code reviews and encourage pair programming.

### **Performance Optimization**

1. **How do you optimize the performance of an Angular application?**
   * **Answer**:
     + Enable **Ahead-of-Time (AOT)** compilation for faster rendering.
     + Use **lazy loading** and **preloading strategies** for modules.
     + Optimize template bindings and minimize watchers with ChangeDetectionStrategy.OnPush.
     + Avoid large DOM manipulations and use Angular's **trackBy** in ngFor directives.
     + Cache HTTP requests with RxJS operators like shareReplay.
2. **What tools and techniques do you use for debugging Angular applications?**
   * **Answer**:
     + Use **Augury** or **Angular DevTools** for component tree debugging.
     + Debug HTTP calls with browser DevTools' network tab.
     + Add console.log or Angular’s **DebugElement** for runtime checks.
     + Use RxJS debugging techniques with tap or libraries like **RxJS Spy**.
     + Monitor performance using tools like **Lighthouse** or **Webpack Bundle Analyzer**.

### **Advanced Topics**

1. **How does Angular handle dependency injection at a deeper level?**
   * **Answer**:
     + Angular uses a hierarchical dependency injection system.
     + Providers declared in **AppModule** are shared across the application.
     + Providers in **lazy-loaded modules** create their own instances.
     + Multi-provider tokens allow multiple values for the same injection token.
     + Use @Inject to resolve tokens and @Optional() for optional dependencies.
2. **Explain the Angular Compiler's role in optimizing performance.**
   * **Answer**:
     + The Angular compiler pre-compiles templates and components during the build process using AOT.
     + It reduces runtime errors and improves security by detecting issues early.
     + Generates optimized JavaScript code, enabling tree shaking to remove unused code.
3. **What is the difference between Zone.js and Angular's Change Detection?**
   * **Answer**:
     + **Zone.js**: Tracks asynchronous operations (e.g., HTTP calls, events) to trigger change detection.
     + **Change Detection**: Updates the DOM based on changes in the application state.
     + Use ChangeDetectorRef to fine-tune or manually trigger change detection.

### **Testing**

1. **How do you ensure robust testing for large Angular applications?**
   * **Answer**:
     + Write **unit tests** using Jasmine and Karma for components, services, and pipes.
     + Write **integration tests** using Angular Testing Utilities like TestBed.
     + Use **end-to-end (E2E)** testing with Protractor or Cypress.
     + Mock dependencies using libraries like **Jest** or Angular’s testing utilities.
     + Maintain high code coverage and integrate testing in CI/CD pipelines.
2. **What strategies do you use for mocking HTTP requests in Angular tests?**
   * **Answer**:
     + Use Angular’s HttpTestingController to mock HTTP requests in unit tests.
     + Example:
   * it('should fetch data', () => {
   * service.getData().subscribe(data => {
   * expect(data).toEqual(mockData);
   * });
   * const req = httpTestingController.expectOne('api/data');
   * req.flush(mockData);
   * });

### **Real-World Challenges**

1. **How do you handle application security in Angular?**
   * **Answer**:
     + Sanitize user inputs with Angular’s **DomSanitizer**.
     + Avoid cross-site scripting (XSS) by using Angular's template bindings ({{}}) and avoiding direct DOM manipulations.
     + Use Angular's built-in **CSRF protection**.
     + Secure HTTP calls with HTTPS and add authentication tokens to headers.
2. **How do you handle version upgrades in large Angular projects?**
   * **Answer**:
     + Use **Angular Update Guide** for a step-by-step upgrade plan.
     + Upgrade Angular CLI and dependencies incrementally.
     + Run unit tests and e2e tests after each upgrade.
     + Refactor deprecated APIs gradually.
3. **How do you manage feature toggles in Angular applications?**
   * **Answer**:
     + Use configuration files or services to toggle features dynamically.
     + Leverage **NgRx Store** or custom state management for feature toggles.
     + Hide or show UI elements based on feature toggle flags.

### **Enterprise-Level Practices**

1. **What is micro-frontend architecture, and how can Angular implement it?**
   * **Answer**:
     + Micro-frontends split large applications into smaller, independently deployable modules.
     + Use frameworks like **Module Federation** in Webpack to load Angular modules dynamically.
     + Ensure communication between micro-frontends using shared services or libraries.
2. **How do you manage large-scale forms with dynamic validation in Angular?**
   * **Answer**:
     + Use **Reactive Forms** for dynamic validation.
     + Build dynamic form controls using a configuration object.
     + Validate inputs using custom validators.
     + Leverage FormArray for handling dynamic collections of form controls.

Angular

## Phase 1: TypeScript Fundamentals

1. ✅Introduction to TypeScript
2. Variables and Data Types
3. Functions
4. Interfaces and Classes
5. Modules and Namespaces
6. Generics
7. Decorators (used in Angular)

### 📘 Phase 2: Angular Basics

1. What is Angular? Why use it?
2. Angular Architecture Overview
3. Angular CLI – Setup & Commands
4. Creating First Angular App
5. Project Structure Explained
6. Modules, Components, and Templates
7. Data Binding (Interpolation, Property, Event, Two-way)
8. Directives (ngIf, ngFor, ngClass, ngStyle)

### 📘 Phase 3: Services and Dependency Injection

1. Creating Services
2. Injectable Decorator
3. Dependency Injection
4. Using HTTPClient to Make API Calls

### 📘 Phase 4: Routing and Navigation

1. RouterModule and Route Configuration
2. Route Parameters
3. Navigating with RouterLink
4. Route Guards

### 📘 Phase 5: Forms in Angular

1. Template-Driven Forms
2. Reactive Forms
3. Form Validation
4. FormGroup and FormControl

### 📘 Phase 6: Advanced Angular

1. Pipes (Built-in & Custom)
2. Lifecycle Hooks
3. Component Communication (Input, Output, EventEmitter)
4. Observables & RxJS
5. Angular Modules (Shared Module, Core Module)
6. Environment Configuration

### 📘 Phase 7: Angular with REST API

1. Consuming APIs using HttpClient
2. Error Handling
3. JWT Authentication (Basic)
4. Interceptors

### 📘 Phase 8: Angular Best Practices

1. Folder Structure
2. Lazy Loading Modules
3. State Management Basics (Intro to NgRx)
4. Unit Testing with Jasmine & Karma
5. Deployment (Angular Build, Host on Netlify/Vercel)

# TypeScript Essentials

📌 What is TypeScript?

TypeScript is a superset of JavaScript that adds static typing.

✅ Installation

npm install -g typescript

tsc --version

🧪 Basic Types

let username: string = 'nirav';

let age: number = 25;

let isAdmin: boolean = true;

let roles: string[] = ['ADMIN', 'USER'];

📦 Interfaces & Classes

interface User {

name: string;

age: number;

}

class Person implemen User {

constructor(public name: string, public age: number) {}

greet() {

console.log(`Hello, I’m ${this.name}`);

}

}

const p = new Person('Nirav', 30);

p.greet();

🚀 Functions with Types

function add(a: number, b: number): number {

return a + b;

}

⚙️ Modules & Imports

// user.ts

export class User {

constructor(public username: string) {}

}

// main.ts

import { User } from './user';

const u = new User('nirav');

### **Basic Concepts**

1. **What is Angular, and how is it different from AngularJS?**
2. **What are the building blocks of Angular?**
3. **Explain the difference between components and directives.**
4. **What is data binding, and what are its types?**
5. **What is the purpose of Angular CLI? Can you name some CLI commands?**
6. **What is a TypeScript, and why is it used in Angular?**

### **Components and Templates**

1. **What is a component? How do you create and use it?**
2. **Explain the role of @Input() and @Output() decorators.**
3. **What is the difference between template-driven forms and reactive forms?**
4. **How do you handle events in Angular templates?**
5. **What are lifecycle hooks? Can you name and explain their purposes?**
6. **How would you implement conditional rendering in an Angular template?**

### **Directives**

1. **What are Angular directives, and how are they classified?**
2. **What is the difference between structural and attribute directives?**
3. **How do you create a custom directive?**
4. **Explain the purpose of ngIf, ngFor, and ngClass.**

### **Services and Dependency Injection**

1. **What is a service in Angular, and how do you create one?**
2. **What is dependency injection, and how does Angular implement it?**
3. **What is the purpose of a singleton service?**
4. **Explain the difference between providedIn: 'root' and providing a service in a specific module.**

### **Routing**

1. **How does routing work in Angular?**
2. **What is the purpose of RouterModule and Routes?**
3. **How do you implement lazy loading in Angular?**
4. **What are route guards, and what types of guards are available?**
5. **How do you pass parameters in Angular routes?**

### **Forms**

1. **What is the difference between reactive forms and template-driven forms?**
2. **How do you perform form validation in Angular?**
3. **How do you bind form data to the component?**

### **HTTP and Observables**

1. **How do you make HTTP requests in Angular?**
2. **What is the purpose of the HttpClient module?**
3. **What is an observable, and how is it used in Angular?**
4. **What is the difference between Promise and Observable?**

### **Angular Modules**

1. **What is the purpose of NgModules?**
2. **Explain the difference between feature modules and shared modules.**
3. **How do you organize an Angular application into modules?**

### **Performance and Optimization**

1. **What is AOT (Ahead-of-Time) compilation, and why is it important?**
2. **How does Angular handle tree shaking?**
3. **What are some ways to optimize an Angular application?**

### **Miscellaneous**

1. **What are Angular Pipes? How do you create a custom pipe?**
2. **What is the difference between Angular’s ngOnInit and constructor?**
3. **What is the purpose of Angular’s zone.js?**
4. **What are interceptors, and how are they used in Angular?**
5. **Explain the role of Change Detection in Angular.**
6. **What is the role of the trackBy function in ngFor?**

### **Practical Scenarios**

1. **How would you debug an Angular application?**
2. **How would you handle a slow-loading Angular application?**
3. **Describe a project you worked on and your role in the team.**
4. **How do you manage version control in Angular projects?**

Would you like me to create short notes or examples for any of these topics?

#### Here are comprehensive answers to all the Angular interview questions you listed, organized by topic: