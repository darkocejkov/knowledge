___

# What / Why?
- HTML and CSS is the standard for *static* site content, but as soon as you need to have dynamic content that "reacts" to user input - you need JavaScript.
- **Angular** is a JS framework for easily building dynamic components 
- It's based on component architectures, and anytime components *share* functionality, we can create common "services" that components *use*, which is a form of **dependency injection**.
	- seperates the UI from the Business Logic

# TypeScript : [[repo/personalLearning/languages/JavaScript/TypeScript]]
- Angular is built on TypeScript

# Components and Decorators
- Most "Angular" built decorators, directives, etc. use the shorthand `ng`, which stands for Angular
- Angular depends on Decorators - they tell Angular *what* to parse something as. 

## `NgModule`
- A decorator that is meant to create a "module" for Angular
- It can be thought of as a way to define a file as a *module* that contains imports, declarations, and the "entry point" of an application (root module)

```ts
import {NgModule} from '@angular/core'
import {BrowserModule} from '@angular/platform-browser'

import {AppComponent} from './app.component'
import {MediaItemComponent} from '.media-item.component'

@NgModule({
	imports: [
		BrowserModule
	], 
	declarations: [
		AppComponent,
		MediaItemComponent
	],
	bootstrap: [
		AppComponent
	]
})
export class AppModule { }

//
```
> A 'decorator' lives *on top* of a class, it needs to decorate *something*.

- `@NgModule()` is the syntax to use a decorator, and we pass this decorator an object literal - which is the *metadata* of the object
	- the `imports` list declare a list of *imported* modules
	- the `declarations` list declares a collection of modules you are *creating*
		- inside this declarations, we must declare all *components*, *directives*, and *pipes* that are used throughout our hierarchy, regardless of if we include them where they are used
			- so, we import them in both the *root* module, *and* the module we use them in.
	- the `bootstrap` option declares the entry point of the application - Angular will run this root module, and see you are *bootstrapping* the application using a declared component.

## `Component`
- the `Component` decorator allows us to specify how components are used, and what they "output"

```tsx
import {Component} from '@angular/core'
@Component({
	selector: 'app-custom-component',
	templateUrl: './app.custom.component.html',
	//template: `<h2>hey there</h2>`
	stylesUrl: ['./app.custom.component.css']
})
export class AppComponent {}

//app.custom.component.html
<section>
  <header>
    <h1>Media Watch List</h1>
    <p class="description">Keeping track of the media I want to watch.</p>
  </header>
  <mw-media-item-list></mw-media-item-list> %%%%
</section>

//media-item-list.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'mw-media-item-list',
  templateUrl: './media-item-list.component.html',
  styleUrls: ['./media-item-list.component.css']
})
export class MediaItemListComponent {
	mediaItems = [
		{},
		{},
		{},
	]

	onMediaItemDelete(mediaItme) {}
}

//media-item-list.component.html
<section>
  <mw-media-item 
    [ngClass]="{'medium-movies': mediaItem.medium==='Movies', 'medium-series':mediaItem.medium==='Series'}"
    *ngFor="let mediaItem of mediaItems"
    [mediaItem]="mediaItem"
    (delete)="onMediaItemDelete($event)"></mw-media-item>
</section>
```
- `selector` specifes how we "target" this component using HTML
	- `<app-custom-component></app-custom-component>`
		- components are never self closing
- `templateUrl` is a URL that specifies the "template" code (written in HTML)
	- we can *either* supply a seperate file via URL, or provide an in-line template
- `stylesUrl` is similar to the template, we can pass it an *array* of stylesheets to style the component
	- component styles applied thru a decorator are *shimmed* when the source code is compiled and parsed

- we must export this class / component to import as a module in other modules
- similarly, if we want to use a component, like `MediaItemListComponent` as `<mw-media-item-list>` in our "root" module, we *import* it.

- Within the *class* `MediaItemListComponent`, we can define properties (variables + methods), which are like runtimes

## Templating

### Interpolation
```tsx
//media-item.component.html
<h2>{{ mediaItem.name }}</h2>
<ng-template [ngIf]="mediaItem.watchedOn">
  <div>Watched on {{ mediaItem.watchedOn }}</div>
</ng-template>
//<div *ng-if="mediaItem.watchedOn">Watched on {{ mediaItem.watchedOn }}</div>
<div>{{ mediaItem.category }}</div>
<div>{{ mediaItem.year }}</div>

<div class="tools">
  <svg class="favorite" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
    <path d="M12 9.229c.234-1.12 1.547-6.229 5.382-6.229 2.22 0 4.618 1.551 4.618 5.003 0 3.907-3.627 8.47-10 12.629-6.373-4.159-10-8.722-10-12.629 0-3.484 2.369-5.005 4.577-5.005 3.923 0 5.145 5.126 5.423 6.231zm-12-1.226c0 4.068 3.06 9.481 12 14.997 8.94-5.516 12-10.929 12-14.997 0-7.962-9.648-9.028-12-3.737-2.338-5.262-12-4.27-12 3.737z"
    />
  </svg>
  <a class="delete" (click)="onDelete()">
    remove
  </a>
  <a class="details">
    watch
  </a>
</div>
```

- Within the HTML, we can see that we have special *template* language inserted in there that allows us to have dynamic content inserted.
- the `{{mediaItem.name}}` template takes the `.name` property on some passed variable to display it
	- this "interpolation" is specifically meant to "read" variables - we cannot include code that assigns, creates new variables, or mutates the original value 
		- if we want to "transform" data before it is displayed, we can use [[#Pipes]]
	- the "binding" of `mediaItem` is dependent on some item with the *same name* within the property of the class

### Property Binding
- The `{{mediaItem.name}}` "interpolation" can be *binded* a different way, 
```tsx
<h2 [textContent]="mediaItem.name"></h2>
<h2 textContent="mediaItem.name"></h2> //DOESN'T WORK (because it does not evaluate "textContent" as a binding)
<h2 textContent="{{mediaItem.name}}"></h2> //WORKS

```

### Event Binding
- Wire events to elements, either *native* (DOM) or *custom*
```tsx
//.ts
export class MediaItem(){

	onDelete(){}
}

//.html
<a class="delete" (click)="onDelete()">
```
- we wire the `click` native DOM element event to the `onDelete()` method specified within the properties of the class
	- native DOM elements usually are prefixed with `on`, but all the native APIs in Angular do not have this prefix

### Data Binding
- Passing data to components requires the use of the `Input` decorator
	- instead of decorating the class, you decorate properties
- We can have data defined within the class, like an array of items - however, they are static. Angular is very forward about *dependency* injection, so we want to move this dependency *outside* of the component itself, whether its from an API or from a random file, it doesn't matter, the point is that the data lives outside the component, and we "bind" any data by "inputting" it into this component:
```tsx
//app.component.ts
export class AppComponent {
	item = {
		id: 1,
		name: 'A Media Event'
	}
}
//app.component.html
<section>
	<mw-media-item [mediaItem]="item"></mw-media-item>
</section>
//media-item.component.ts
export class MediaItemComponent{
	@Input() mediaItem
}
//media-item.component.html
<h2>{{mediaItem.name}}</h2>
```
> If we want to *alias* the binding point, we can pass a string literal to the `Input` decorator

### Output / Event Emitting
- We can create "custom" events by using the `Output` decorator, which allows us to *emit* custom, named events. 
	- This allows us to "propagate" these events upwards, to parent components
```tsx
//media-item.component.ts
import {Output, EventEmitter} from '@angular/core'
export class MediaItemComponent{
	@Input() mediaItem;
	@Output() delete = new EventEmitter();

	onDelete(){
		this.delete.emit(this.mediaItem)
	}
}
//media-item.component.html
<button (click)="onDelete()">delete!</button>
//app.component.ts
export class AppComponent {
	item = {
		id: 1,
		name: 'A Media Event'
	}
	onMediaItemDelete(mediaItem) {}
}
//app.component.html
<section>
	<mw-media-item [mediaItem]="item" (delete)="onMediaItemDelete($event)"></mw-media-item>
</section>
```
- In the component, we use the `Output` decorator to create an emitter property, called `delete`, which has a `.emit` method - which we pass an argument.
	- the argument can be anything, but it's useful to pass back the dynamic binded data 
- when the `delete` event is emitted (the name of the event is the same of the defined event property), the event propagates upwards to the parent, because we assigned the `delete` event to be binded, which results in the function `onMediaItemDelete` being called - with a single parameter `$event`.
	- this function is then invoked only when the button is pressed, which invokes `onDelete`, which emits the `delete` event, which triggers the `onMediaItemDelete` with an argument.

## Structural Directives
- These are *directives* which change the DOM tree, meaning they can add or remove elements

### `ngIf`
- Say that we wanted to *conditionally* render something, meaning that we only render it when for certain evaluations of a condition. If there is no `watchedOn` property for instance, we don't need to render the template for `<div>Watched On {{ mediaItem.watchedOn }}</div>`, since we know this is empty.

- the `ngIf` "directive" allows us to create HTML-like attributes on elements which contain some expression, whose evaluation determines whether or not this element gets inserted into the DOM tree:
```tsx
<div *ngIf="mediaItem.watchedOn">Watched on {{ mediaItem.watchedOn }}</div>
```

#### Syntactic Sugar
- The syntax involving an asterisk: `*ngIf` is a syntax sugar that allows you to skip writing the long version, but knowing this long way can be very useful:
```tsx
<ng-template [ngIf]="mediaItem.watchedOn">
	<div>Watched on {{ mediaItem.watchedOn }}</div>
</ng-template>
```
> This would be useful, if say that we wanted to *group* sibling elements to be dependent on the same conditional logic.

### `ngFor`
- This directive allows us to set up an inline "for-loop" in our template
```tsx
//media-item-list.component.ts
export class MediaItemListComponent{
	mediaItems = [
		{},
		{},
		{},
	]
}

//media-item-list.component.html
<section>
	<mw-media-item 
		*ngFor="let item of mediaItems" 
		[mediaItem]="item"
		(delete)="onMediaItemDelete($event)"
	></mw-media-item>
</section>
```

- it is identical to the `for _ of _` JavaScript for-loop

## Attribute Directives
- Changes the *behaviour* or *appearance* of elements without changing the overall structure of the tree

### `ngClass`
- a directive that allows for changing the *class* of an element based on conditional logic
	- you pass it an *object literal* within the string literal, that describes the various classes applied by their names as the *key* properties, while their conditional logic in the *value* 
```tsx
<mw-media-item 
	*ngFor="let item of mediaItems" 
	[mediaItem]="item"
	(delete)="onMediaItemDelete($event)"
	[ngClass]="{ 'medium-movies': mediaItem.medium === 'Movie', 'medium-series': mediaItem.medium === 'Series'}"
></mw-media-item>
```
- the class-name `medium-movies` is used if the `.medium` property of the `mediaItem` class data binding has the value `Movie`

### Custom Attribute Directives
```tsx
//favorite.directive.ts
import {Directive, HostBinding, Input} from '@angular/core'
@Directive({
	selector: '[mwFavorite]'
})
export class FavoriteDirective{
	@HostBinding('class.is-favorite') isFavorite = true;
	@Input() set mwFavorite(value){
		this.isFavorite = value
	}
}

//media-item-list.component.html
<mw-media-item 
	[mwFavorite]="mediaItem.isFavorite"
	*ngFor="let item of mediaItems" 
	[mediaItem]="item"
	(delete)="onMediaItemDelete($event)"
	[ngClass]="{ 'medium-movies': mediaItem.medium === 'Movie', 'medium-series': mediaItem.medium === 'Series'}"
></mw-media-item>
```
- similar to components, the *selector* of the directive is the attribute-like "name" that we use to apply this directive
- the logic of the directive lies in the class definition
- the `class.is-favorite` is a way to target a DOM element's class properties, which is done thru the `HostBinding` property directive that allows us to target DOM element properties in general
	- the `isFavorite` property is defaulted to *true*
- Basically, we are creating a custom directive to control the logic of the whether or not a component has a class called `is-favorite`, based on the value of the `isFavorite` data binding.

> [!tip] a "component" in Angular, is essentially a *directive* that includes a *template*

> [!tip] the square brackets around a property indicate that we are *binding* a property. Angular will parse these and allow us to bind some expression or value to the resulting directive

- If we recall back to [[#Data Binding]], we use the `Input` decorator to *decorate* a property in the class, which receives a data binding from `[mediaItem]='item'`, so it ingests the value
- the `Input` directive can also decorate *functions* like a class *setter* method, like in our example above.
	- we use a weird syntax `set mwFavorite(value) {}` 
		- a *setter method* is a method called when a property of the *same name*, is set to a value from an *instance* of that class
			- TL;DR: any time value that it is binded to changes, the setter method is invoked with that value, allowing us to "react" to changes
- to recap, we created a custom directive that uses the select `[mwFavorite]`, which can be used with/out the *binding* square brackets. However, if we want to bind a value, like the `isFavorite` property from the `item` mapped from the `ngFor` directive, we use the square brackets to bind the directive to that value. Using the `HostBinding` directive, we can target the class properties of the DOM element, and add the `is-favorite` class, because it's linked to the truthiness/falsyness of the local property `isFavorite`. We binded the directive to this locally scoped property using the `Input` directive, and decorated a *setter method*, which is basically a sister method that listens to changes in the value that `mwFavorite` is binded to - which allows us to change the `isFavorite` local prop, resulting in the `is-favorite` class to exist on this element, if the binded value of the `mediaItem` has it's `isFavorite` property set to true, and otherwise not if false.

### Directives and Events
- It's great that we can *bind* properties, directives to values - but we want to use directives with events (custom *or* native):
```tsx
import {Directive, HostBinding, HostListener, Input} from '@angular/core'
@Directive({
	selector: '[mwFavorite]'
})
export class FavoriteDirective{
	@HostBinding('class.is-favorite') isFavorite = true;
	
	@HostBinding('class.is-favorite-hovering') hovering = true
	@HostListener('mouseenter') onMouseEnter(){
		this.hovering = true
	}
	@HostListener('mouseleave') onMouseEnter(){
		this.hovering = false
	}

	@Input() set mwFavorite(value){
		this.isFavorite = value
	}
}
```
- using the `HostListener` decorator, we can decorate functions like `onMouseEnter` and `onMouseLeave` to listen to host events like `mouseenter` (remember, its the native event `onmouseenter`, without the `on` prefix...)

## Pipes
- These are template expressions *operators* that allows us to receive an input, and returns a value (a transform function).
	- They are usually *chainable*

### `date`
- built-in pipe to parse some values of a date into other formats
```tsx
<div>Watched on {{ mediaItem.watchedOn | date }}</div>
// Watched on 1927151819231 -> Watched on Jan 11, 2021 (example lol)
```
	- pipes can take "arguments", using colon arguments:
```jsx
mediaItem.watchedOn | date: 'shortDate'
mediaItem.name | slice: 0: 10 | uppercase
```

### Custom Pipes
```tsx
import {Pipe, PipeTransform} from '@angular/core'

@Pipe({
	name: 'categoryList'
	//pure: true 
	//optional
	//determines whether it is "stateful" or "stateless"
	// if a function is pure, then the pipe takes in data, and returns it without side effects
})
export class CategoryListPipe implements PipeTransform{
	transform(mediaItems){
		//basically, take in a list and return all list of all categories as a comma-sep string
		return mediaItems.forEach(item => return item.category).join(', ')
	}
	
}
```
> a "side-effect" is a change that happens in a scope larger than the function itself. Functions are not pure if they contain side-effects, meaning that they change or mutate values outside the ones given to it
- pipes are *pure* (stateless) by default
- anytime we call a pipe, Angular runs a function called `transform`
- the `PipeTransform` import is a typescript *interface*, that allows us to better structure our pipe
- the parameters to our *transform* function are supplied based on what is input
	- there is always 1 implicit argument, the input: `mediaItems | categoryList`
	- if we want to supply other arguments through colons, the arguments arrive as a list

# Forms
- Forms are extremely important, because there are 2 big jobs for web applications:
	- Displaying Data
	- Collecting Data
- Forms are the "collecting data" aspect, and allow us to obviously provide some interface to collect various *types* of data, but not only that, they allow the *tracking* of changes, and the *validation* of data. So, based on the tracked changes, the form should automatically validate all changes in the data, and if data is not suitable, then we should display some form of *invalidity*
- they are kind of like a super-set of the data and event binding we were previously looking at, allowing easily binding form inputs and their events, tracking changes on a higher abstract level, and performing validation

- Forms are either:
	1. [[#Template Forms]]
	2. [[#Model Forms]]

## Template Forms
```tsx
import {FormsModule} from '@angular/forms'
//...
@NgModule({
	imports: [FormsModule]
})
```

```tsx
//media-item-form.component.html
<form #mediaItemForm="ngForm" (ngSubmit)="onSubmit(mediaItemForm.value)">
  <ul>
    <li>
      <label for="medium">Medium</label>
      <select name="medium" id="medium" ngModel>
        <option value="Movies">Movies</option>
        <option value="Series">Series</option>
      </select>
    </li>
    <li>
      <label for="name">Name</label>
      <input type="text" name="name" id="name">
    </li>
    <li>
      <label for="category">Category</label>
      <select name="category" id="category">
        <option value="Action">Action</option>
        <option value="Science Fiction">Science Fiction</option>
        <option value="Comedy">Comedy</option>
        <option value="Drama">Drama</option>
        <option value="Horror">Horror</option>
        <option value="Romance">Romance</option>
      </select>
    </li>
    <li>
      <label for="year">Year</label>
      <input type="text" name="year" id="year" maxlength="4">
    </li>
  </ul>
  <button type="submit">Save</button>
</form>
```
- based on the template markup, so we build the interactions within the template itself
- uses the `ngForm` directive to tell Angular what *form* elements (`<form>`) to care about, while each input needs to use the `ngModel` directive
	- the `ngForm` directive is automatically applied to `<form>` elements because it is one of the selectors that it can use
	- however, we need to manually "opt-in" to specific form *controls* using the `ngModel` directive

### `ngModel`
- this directive must be manually applied to template-based form controls
- it basically tells Angular to "watch" those inputs
- rather then having to specify some Angular-based name, this directive uses the `name` attribute to identify controls

### `ngSubmit`
- built-in directive to intercept the default HTML form submit
	- the `type="submit"` button submits

### `#<handle>`
- in our example, we use this hash syntax to create a "handle" or "template reference variables" to the form itself, because we need some way to reference the form to pass the value of the (watched) fields to our handler `onSubmit()` function
	- this handle name can be custom
- when we assign this handle to the `ngForm` variable, it assigns a FormGroup into the handle variable for us 

```tsx
//media-item-form.component.ts
export class MediaItemFormComponent {
	onSubmit(mediaItem) {
		//handle the submission
		//the only fields "captured" in the submission are ones 
			//that included the `ngModel` directive
	}
}
```

## Model Forms
- based on the component's class
```tsx
import {ReactiveFormsModule} from '@angular/forms'
//...
@NgModule({
	imports: [ReactiveFormsModule]
})
```

```tsx
import {Component, OnInit} from '@angular/core'
import {FormGroup, FormControl} from '@angular/forms'

@Component({})
export class MediaItemFormComponent implements OnInit {
	form: FormGroup;

	ngOnInit(){
		this.form = new FormGroup({
			medium: new FormControl('movies'),
			name: new FormControl(''),
			year: new FormControl(''),
		});
	}

	onSubmit(mediaItem) {
		//handle the submission
	}
}
```

### Lifecycle
- Right now is a great time to touch on "lifecycle" methods, which are handled by Angular itself to invoke when specific lifecycle events happen to a component, like it's initialization. 
	- [there are many others](https://angular.io/guide/lifecycle-hooks)
- Lifecycles work through TypeScript interfaces, using the `implements` syntax to "give" our component that lifecycle hook
- in this form example, we use the `ngOnInit()` initialization lifecycle hook to intialize something about our form

### FormGroup & FormControl
- we create a `form` property using a TypeScript type to enforce that this property is a FormGroup.
- within the init. hook, we intialize the form property to a new `FormGroup` instance, for which we pass an object literal containing our form "model", a group of controls.
- the `FormControl` initializes that property, whether it's medium, name, or year with some default value

```tsx
<form [formGroup]="form" (ngSubmit)="onSubmit(form.value)">
	<select name="medium" id="medium" formControlName="medium">
        <option value="Movies">Movies</option>
        <option value="Series">Series</option>
	</select>
</form>
```
- instead of passing a *handle*, we bind the `formGroup` directive to the value of "form", and the submission function can use the `form` value instead of `mediaItemForm`
- instead of using `ngModel` directives to "hook" those inputs into the model, we've created the models directly in the FormGroup in the class - so we only need to indicate to Angular which inputs are which models using the `formControlName` directive.

# Form Validation

## Built-In
- using the `Validators` built-in form validator
```tsx
import {FormGroup, FormControl, Validators} from '@angular/forms' 

ngOnInit(){
	this.form = new FormGroup({
		medium: new FormControl('movies'),
		name: new FormControl('', Validators.compose([
			Validators.required,
			Validators.pattern('[\\w\\-\\s\\/]+')
		])),
		year: new FormControl(''),
	});
}

//form.html
<form [formGroup]="form" (ngSubmit)="onSubmit(form.value)">
	<select name="medium" id="medium" formControlName="medium">
        <option value="Movies">Movies</option>
        <option value="Series">Series</option>
	</select>
	<button type="submit" [disabled]="!form.valid">Submit</button>
</form>
```
- the `Validators` class has methods to describe validation *rules*, like if a field is *required*, or it must pass a *regex pattern*. 
- Within the *html* of the form, we can *bind* the disabled attribute to the validity of the form, using the `FormGroup`'s handle of `form`, and access whether or not the form is in a valid state using `.valid`
- In the `FormControl` constructor, we can pass a validator function. The `Validators` class comes with a handy `.compose` function that takes an array of validator functions, to compose multiple rules into a single function.

## Custom Validation
- To create a custom validation rule, we need to create a function take takes an object - which is either a FormControl, FormGroup, or FormArray.
	- returns `null` when *valid*, and an object when *invalid*
- This function can be any function, but it makes sense to create that custom validation as a method to the form component's class

```tsx
ngOnInit(){
	this.form = new FormGroup({
		medium: new FormControl('movies'),
		name: new FormControl('', Validators.compose([
			Validators.required,
			Validators.pattern('[\\w\\-\\s\\/]+')
		])),
		year: new FormControl('', this.yearValidator),
	});
}

yearValidator(control: FormControl){
	if(control.value.length === 0) return null
	const year = parseInt(control.value, 10)
	const minYear = 1900
	const maxYear = 2100
	if (year >= minYear && year <= maxYear) return null
	else{
		return{
			year: {
				minYear,
				maxYear,
			}
		}
	}
}
```
- The object we return can contain any values, but it's really useful to return objects with validation information to help the user decipher the problem
- the object should contain a property that matches the *name* of the `FormControl`.

## Error Handling & Display
```tsx
//form.html
<form [formGroup]="form" (ngSubmit)="onSubmit(form.value)">
	<select name="medium" id="medium" formControlName="medium">
        <option value="Movies">Movies</option>
        <option value="Series">Series</option>
	</select>
	
	<li>
      <label for="name">Name</label>
      <input type="text" name="name" id="name" formControlName="name">
      <div *ngIf="form.get('name').hasError('pattern')" class='error'>
	      Name has invalid character
      </div>
    </li>

	<li>
      <label for="year">Year</label>
      <input type="text" name="year" id="year" maxlength="4">
      <div *ngIf="form.get('year').errors as yearErrors" class='error'>
	      Year must be between {{ yearErrors.minYear }} and {{ yearErrors.maxYear }}
      </div>
    </li>

	<button type="submit" [disabled]="!form.valid">Submit</button>
</form>
```
- For the *name* error, we are conditionally displaying the error by binding the structural directive `ngIf` to the expression of checking whether our form's control called `name` has an error of the type "pattern" - we could also similarly check for the "required" error
- For the *year* error, we are doing something similar as for the name error, but instead of invoking the `hasError(type)` (which we can still do), we create a *handle* for the `.errors` property as `yearErrors`. If the form control of name `"year"` has errors, then it displays this element.
	- We can then also use the *handle* of `yearErrors` to access the values of the object in element templates

# Depedency Injection & Services
- Dependency Injection is something that is innate in Angular
- It is a way to implement the *inversion of control* design pattern, where we shift the control of functions to be in seperate areas. Dependency injection does this by seperating how services, directives, and components are implemented - they don't need to know *how* they are implemented.
	- We pass these things to each other to create "blackbox" environments. Components receive services, and we know how to invoke them - what to input, and and where to store the output. 
	- The implementation of these functions are then seperate, so they no longer "depend" on one-another, so if our API logic changes - we don't have to then change all components.

- Angular implements dependency injection through TWO steps:
	1. Service Registration, telling Angular about all the *injectable* services
	2. Service retreival, by *injecting* these *injectable* services into components
		1. `@Inject` decorator
		2. constructor injection `constructor() { }`

- When we inject services into classes by either the decorator, or by enforcing a service *type* (via typescript) in the constructor, Angular will used *cached services* to accomplish using this injectable service.
	- This means that Angular will check if a service *instance* exists - if it does, it uses that existing instance, otherwise, it creates a *new* service instance, and caches it
- Something really important about services and injectables is that it matters at which point in the element tree they are injected - because injected services are available only to the direct injected interface *component*, and all its *children*
	- this means that *bootstrapped* services, are available from the root component, and all children of the root.
- If we want to create *custom* services - we can declare classes with re-usable logic as injectables through the `@Injectable` decorator

## Services
- not an Angular construct, but rather a "pattern"
	- they are regular classes that encapsulate *logic* that may/not be used in various components
	- they don't need some specific naming or logic to be considered as services
- a "service" is very much like a middle-man, a very common "service" is a data service, that deals with getting and setting data.
	- The "dependency injection" part becomes obvious in this pseudo-code:
```tsx
export class DataService {
	get(id?) {}
	set() {}
}

export class Component {
	DataService.get()
	DataService.set()
}
```
- If we create some "blackbox" DataService class that handles getting and setting data, the components that use it only use the *exposed API* that it provides (`get()` and `set()`) - meaning that components are not dependent on the implementation of these functions - but rather the *usage* of the API itself - what you input and what is output.
	- For a more concrete example, our DataService class can either implement a *real* connection to a database, and issue *real* commands to get and set records - or it can just use a simple, volatile memory list of items. As long as both implementations create the *same* API interfaces for components to use, then it does not matter.
- Furthermore, if we create a service that can be used in >= 1 component, then it properly encapsulates the logic that would be used in multiple places
- Angular has built-in "services" that help you accomplish specific things:
	- Http
	- FormBuilder
	- Router

## Constructor Injection (`FormBuilder`)
```tsx
import {FormGroup, FormControl, Validators, FormBuilder} from '@angular/forms'

export class MediaItemForm implements OnInit {
	constructor(private formBuilder: FormBuilder)

	ngOnInit(){
		this.form = new this.formBuilder.group({
			medium: new this.formBuilder.control('movies'),
			name: new this.formBuilder.control('', Validators.compose([
				Validators.required,
				Validators.pattern('[\\w\\-\\s\\/]+')
			])),
			year: new this.formBuilder.control('', this.yearValidator),
		});
	}
}
```
- constructor injection relies on using TypeScript to "inject" a service as a *type*. `FormBuilder` is a service, and we create a `formBuilder` parameter to the constructor as the type of the service - which tells Angular to inject the `FormBuilder` into this component
- something else that's kind of weird, is the use of the `private` modifier on the `formBuilder` property. `private` is another use of TypeScript, and allows us to create a *property* called `formBuilder` that lives on the class, and not just in the constructor.
	- now, since the constructor will inject the `FormBuilder` service into the `formBuilder` property, we can use this property within the `ngOnInit` lifecycle hook to de-couple the FormGroup and FormControl code from our component
		- if we then wanted to modify the underlying form paradigm - we can do so globally by changing how the `FormBuilder` is implemented

## Custom Service
```tsx
//media-item.service.ts
export class MediaItemService{

	mediaItems = [
		{},
		{},
		{},
		{},
	]

	get(){
		return this.mediaItems
	}

	add(mediaItem){
		this.mediaItems.push(mediaItem)
	}

	delete(mediaItem){
		this.mediaItems = this.mediaItems.filter(i => i.id !== mediaItem.id)
	}

	/* This is why dependency injection is so useful, we can implement these 
		however we like, we can use different methods.
	delete(mediaItem){
		const index = this.mediaItems.indexOf(mediaItem)
		if(index >= 0) this.mediaItems.splice(index, 1)
	}
	*/
}
```
- Here we can easily see that a "media service" is just a class that controls logic. In this case, we hold the value of a list of items, can get, add, and delete items from this list. Dependency injection allows us to hold this implementation seperate from the components that use it.
	- This bonus makes it easier to logically organize things based on their function, but also provides a really incredible benefit to unit testing. 
	- Instead of having components depend on this logic directly in their implementation, we can *unit test* our components using "Mock" services made for testing - instead of using a real implementation of a database for example.

### Providing a Service

#### Directly in the root module
```tsx
//app.module.ts
import {MediaItemService} from './media-item.service'

@NgModule({
	imports: [...],
	declarations: [...],
	bootstrap: [AppComponent],
	providers: [
		MediaItemService
	]
})
```
- We can declare our service within the `providers` property of a module
	- when we do this, we tell Angular to *instantiate* this service for *this* module, and *all* other modules down the tree.

#### By using the `Injectable` decorator
```tsx
//media-item.service.ts
import {Injectable} from '@angular/core'

@Injectable({
	providedIn: 'root'
})
export class MediaItemService { }
```
- Instead of needing to import and declare this service as a `provider` within the root module, we can use  `Injectable` to decorate this class to be 'provided in' the root module.
	- This keeps the provider logic next to the service, and also helps Angular optimize
		- adds support to lazy load this module
- If we use this `Injectable` decorator, we don't need to import nor declare it as a provider in the root module file.

### Using the service in a component

#### By using constructor injection
```tsx
import {MediaItemService} ...

@Component()
export class MediaItemList implements OnInit {

	mediaItems;

	constructor(private mediaService: MediaItemService)

	ngOnInit(){
		this.mediaItems = this.mediaService.get()
	}

	onMediaItemDelete(mediaItem){
		this.mediaService.delete(mediaItem)
	}
}

//media-form.component.ts
export class MediaItemForm implements OnInit {
	constructor(private formBuilder: FormBuilder, private mediaService: MediaItemService)

	onSubmit(mediaItem){
		this.mediaService.add(mediaItem)
	}
}
```

### Providing *value* types
- If we wanted to provide the types/constraints of *values* for fields, we need to use a different syntax:
```tsx
const lookupLists = {
	mediums: ['Movies', 'Series']
}

@NgModule({
	imports: [],
	declarations: [],
	providers: [
		{ provide: 'lookupListToken', useValue: lookupLists }
	]
})
```
- This is a little bit confusing, but think of a "global" variable - we want to be able to dynamically render a list of "mediums" for media. Imagine that we have control logic and render logic that depends on hardcoded types, we need to do extra work to add a new medium - add it to the HTML and the javascript handlers and such.
- In the root module, we can "provide" this value type list as a provider
	- we must give it a name, like `lookupListToken` that allows us to reference this specific list, and we tell Angular to attach the value in the `lookupLists` constant to this provided value
```tsx
//media-item-form.component.ts
import {..., Inject} from '@angular/core'

export class MediaItemForm {
	constructor(
		private formBuilder: FormBuilder, 
		private mediaService: MediaItemService,
		@Inject('lookupListToken') public lookupLists,
	) {}
}
```
- using the `@Inject` decorator, we can *decorate* a parameter to the constructor to use a specific provided service.
	- In this case, we pass the name of the lookup lists that contain our value types.
	- Similar to how we use the `private` modifier for `formBuilder` and `mediaService`, we use the **`public`** modifier for this injected, provided value 
		- this is because *public* scoped properties *can* be used in the "template" files.

```tsx
//media-item-form.component.html
<select name="medium" formControlName="medium">
	<option 
		*ngFor="let token of lookupLists.mediums"
		[value]="token"
	> {{ token }} </option>
</select>
```
- heading over to the template file, we can then change the rendering of the `<select>` to use the value types stored in the lookup lists - making this rendering dynamic to the options set "globally".
	- The way it does this is that `lookupLists` is a public-scoped property, and the list that we want to render is actually the `.mediums` property.
	- So, we use the `*ngFor` directive to iterate over items in this list, using the block-scope variable of `token` (or whatever we want - the example uses `medium`) to use the actual *value*.
	- we bind the value attribute of the `<option>` element so our form can know the value of selected options correctly, and the displayed label is a template evaluation of the token as well.

### Avoiding String Literals
- Using string literals as "names" for these providable things is a risk because it's a hardcoded way to abstract something - and is harder for Angular or intellisense to help enforce these types
- We can use **Injection Tokens** to work around this:

```tsx
// NEW: providers.ts
import {InjectionToken} from '@angular/core'

export const lookupListToken = new InjectionToken('lookupListToken')

export const lookupLists = {
	mediums: ['Movies', 'Series']
}

//app.module.ts
import {lookupListToken, lookupLists} from './providers.ts'
@NgModule({
	imports: [],
	declarations: [],
	providers: [
		{
			provide: lookupListToken, useValue: lookupLists
		}
	]
})
export class AppComponent {}

//media-item-form.component.ts
constructor(
		private formBuilder: FormBuilder, 
		private mediaService: MediaItemService,
		@Inject(lookupListToken) public lookupLists,
	) {}
```
- We can hoist up the string literal value into a *providers* file (or wherever, honestly), and supply it as an argument to the `InjectionToken` class, which is put into the `lookupListToken` constant.
- Now, in our *module* and *components*, we can use the `InjectionToken` constant that we import from the providers file, and don't need to use a string literal.

# HTTP Module and providing a Service

## `HttpClientModule`
- is an *optional* module that allows us to create HTTP calls

```tsx
import { HttpClientModule } from '@angular/common/http'

@NgModule({
	 imports: [
		 HttpClientModule
	 ]
})
export class AppComponent {}
```

## `HttpXhrBackend` 
- is the *backend* code that handles *requests* to an endpoint - like a server.
- because DI (dependency injection) is such an important part of Angular, we can create a "mock" backend service that receives calls to its endpoint. The point being is that we can "intercept" calls to `HttpXhrBackend` and use a mock backend for development purposes

```tsx
import { HttpClientModule, HttpXhrBackend } from '@angular/common/http'
import {MockXHRBackend} from './mock-xhr-backend'

@NgModule({
	 imports: [
		 HttpClientModule
	 ],
	 providers: [
		 {provide: HttpXhrBackend, useClass: MockXHRBackend}
	 ]
})
export class AppComponent {}
```
- since we set up this provider code, anytime a component asks for an instance of `HttpXhrBackend`, it receives an instance of `MockXHRBackend` instead.

## `HttpClient`
- A *service* for making HTTP requests, and handles HTTP responses
```tsx
//media-item.service.ts
import {HttpClient} from '@angular/common/http'

export class MediaItemService {
	constructor(private http: HttpClient) {}

	get(){
		//return this.mediaItems
		return this.http.get('mediaitems')
	}
}
```
- We use constructor injection to use a `HttpClient` service instance in the property `http`
- our `get()` function now uses the `.get` method of the HttpClient service to make a request to a backend endpoint  `mediaitems`.
	- HttpClient then uses the HttpXhrBackend (which is really hooked up to `MockXHRBackend`) to make a request to this backend endpoint
- the `.get` method, returns an "`Observable`" object of HTTP responses, so we need to "parse" out the list of media items to return, and NOT the HTTP response
	- we can use `rxjs`'s `map` operator:

```tsx
//media-item.service.ts
import { map } from 'rxjs/operators'

export class MediaItemService {
	 get(){
		return this.http.get<MediaItemResponse>('mediaitems')
			.pipe(map(response => { 
				return response.mediaItems
			}))
	}
}

//create a typescript type to describe the shape of a media item
interface MediaItem {
	id: number,
	name: string,
	medium: string,
	//...
}

interface MediaItemResponse {
	mediaItems: MediaItem[]
}
```
- In the API service that we created, we need to deal with the `Observable` using the `map` method - but we can only do so by "piping" the result of `.get` into a chain of operators.
	- In this `.pipe`, we pass operators to perform transformations of the received HTTP response. The `.map` method from `rxjs` allows us to parse the response, then return the `.mediaItems` property of the response 
- Because the backend API is decoupled from the frontend - TypeScript doesn't know the types of the incoming objects. We create interfaces for the items and responses to help TypeScript creating typing information to propagate throughout our components

```tsx
//media-item-list.component.ts
export class MediaItemList implements OnInit {
	ngOnInit() {
		this.mediaItemService.get()
			.subscribe(mediaItems => {
				this.mediaItems = mediaItems
			})
	}
}
```
- This step is extremely important, because the `.get` method creates a **cold** observable - it "prepares" this endpoint to be called, and is not actually called until `.subscribe` is called on the resulting `get` service API

### Next, Error, Complete
- An observable has THREE events associated with the data stream:
	- Next
		- new item in the data stream
	- Error
		- error occurred, stream stops, arrives with an error messages
	- Complete
		- stream complete, no more data to emit (will *not* emit)
- the `.subscribe` method takes up to THREE callbacks, one for *each* event for its handling
	- we *don't need to* provide all 3 
	- once we program the `.subscribe` API with a "next" callback, this callback sets the public property on the class called `mediaItems` to the resulting data from the observable.

## URL Search Parameters in HTTP
```tsx
//media-item.service.ts
export class MediaItemService {
	const getOptions = {
		params: { medium }
	}

	 get(medium){
		return this.http.get<MediaItemResponse>('mediaitems', getOptions)
			.pipe(map(response => { 
				return response.mediaItems
			}))
	}
}
```
- If we want to support sending a request with URL parameters to our backend, mock or real, we pass an options object to the `http.get` method with the `params` property, which is its own object with property "medium"

```tsx
//media-item-list.component.ts
export class MediaItemList implements OnInit {

	medium = '';
	mediaItems: mediaItem[];

	constructor(private mediaItemService: MediaItemService) {}

	ngOnInit() {
		this.getMediaItems(this.medium)
	}

	getMediaItems(medium: string) {
		this.medium = medium
		this.mediaItemService.get(medium)
			.subscribe(mediaItems => {
				this.mediaItems = mediaItems
			})
	}
}
```
- as for the components that actually use the service, since we added the a parameter to the `get` service API we created, we pass a string indicating the current "medium", which is the empty string by default
	- meaning that if no medium is supplied, it's identical to not providing any URL params, getting *all* items of *any* medium

# HTTP POST, PUT, DELETE
```tsx
//media-item.service.ts

export class MediaItemService {
	const getOptions = {
		params: { medium }
	}

	 get(medium){
		return this.http.get<MediaItemResponse>('mediaitems', getOptions)
			.pipe(map(response => { 
				return response.mediaItems
			}))
	}

	add(mediaItem){
		return this.http.post('mediaitems', mediaItem)
	}

	delete(mediaItem){
		return this.http.delete(`mediaItems/${mediaItem.id}`)
	}
}
```
- using POST, PUT, and DELETE is similar to using GET, but instead of receiving data back, we are strictly sending data, and requesting an action be done *other* than strictly reading
```tsx
//media-item-form.component.ts
onSubmit(mediaItem) {
	this.mediaItemService.add(mediaItem)
		.subscribe()
}

//media-item-list.component.ts
onMediaItemDelete(mediaItem){
	this.mediaItemService.delete(mediaItem)
		.subscribe(() => {
			this.getMediaItems(this.medium)
		})
}
```
- we must still *subscribe* to the Observable APIs to invoke them
- when an item is *deleted*, we invoke the `.delete` service API we created, which invokes the `http.delete` method with an endpoint - which is specified as an ID'ed endpoint.
	- on the asynchronous completion of this deletion, the subscribe interface allows us to invoke a callback, which we can use to re-fetch items because we modified them
- however, for an item submission - when we `.add`, which invokes `http.post`, it *does* create a new item in the backend, but this submission functionality is *seperate* from the "list" functionality, which handles all of the getting, so we cannot just call `getMediaItems`
	- this will be covered in the [[#Routing]] section

## HTTP Errors
- use the RxJS operator `catchError` within a pipe
```tsx
import {HttpClient, HttpErrorResponse} from '@angular/common/http'
import { map, catchError } from 'rxjs/operators'
import { throwError } from 'rxjs'

export class MediaItemService {
	get(medium){
		return this.http.get<MediaItemResponse>('mediaitems', getOptions)
			.pipe(
				map(response => { 
					return response.mediaItems
				}),
				catchError(this.handleError)
			)
	}


	private handleError(error: HttpErrorResponse) {
		// DO SOMETHING (error.message)
		return throwError('A data error occurred, please try again.')
	}
}


```

# Routing
- Routing in Angular requires that we have a base element with the "root" of our application. This element should be a child of the `<head>` section:

```html
<head>
	<base href='/'>
</head>
```

## Creating Routes
```tsx
//app.routing.ts
import { Routes } from '@angular/router'
import { MediaItemFormComponent } from './media-item-form.component'
import { MediaItemListComponent } from '...'

const appRoutes: Routes = [
	{ path: 'add', component: MediaItemFormComponent },
	{ path: ':medium', component: MediaItemListComponent },
	{ path: '', redirectTo: 'all', pathMatch: 'full'}
];
```
- Creating routes does not require anything special, we only import the Routes type so that our application has a better understanding of what we are trying to create
- in this list of routes, we pass object literals to describe a *URL Path*, and which component to associate to that path
	- these paths build on the *base* route
	- these paths are *relative* to the base
		- thus, 'add' means `/add`, which should render the MediaItemFormComponent
		- the `:medium` path matcher means that we are creating a dynamic route parameter, with the name of medium.
		- the `''` is the default route `/`
			- when we try and use the default (root/base) route, our rule setups a `redirectTo` property, which will redirect to `/all`. The `pathMatch` property set to "full" means that the *full* URL path must be the default route for this rule to apply.
	- *order matters*, meaning that the order within the list creates priority for certain paths. For example, if the `:medium` pattern was *above* `add`, then we'd never reach the `/add` route, because it would think that "add" is a binding to the `:medium` parameter.

```tsx
//app.routing.ts
import { Routes, RouterModule } from '@angular/router'
const appRoutes = [
	//...
]

export const routing = RouterModule.forRoot(appRoutes)
```
- unlike `FormsModule` or `BrowserModule`, we did not import the `RouterModule` in our root app module directly. Instead, we import it into our routing *file*, and call the `forRoot` static method from `RouterModule`, providing the array of routing objects we created, and exporting the result of this function.
```tsx
//app.module.ts
import { routing } from './app.routing'

@NgModule({
	imports: [
		//...,
		routing
	],
})
```
- Now, we import that `routing` export and set it as a module import. 
- Under the hood, the `RouterModule` has all the module-related things, like components, directives, and services - and we import and build on top of the module using our custom routes.

## Integrating Routes
- In order to use routes, we need to use the components and directives that comes from the `RouterModule` that we are using.
- What a router does, is it listens to the *route* of the browser URL for changes, and we use a router outlet to conditionally render:
```tsx
//app.component.html
<section>
	<header>
	</header>
	<router-outlet></router-outlet>
</section>
```
- `router-outlet` is a *structural directive*, not a component. It tells Angular to hook into the routing rules at this specific place in the HTML template.

## Router Links
- use the `routerLink` directive to create a *link* for to a specific route:
```tsx
<nav>
	<a routerLink="/"></a>
	<a routerLink="/Movies"></a>
	<a routerLink="/Series"></a>
</nav>
```
- using `routerLink` allows us to do 2 simultaneous things: attach an `href` to an anchor, and tell Angular that these links start path changes, and to do router changes with these links.

## Route Parameters
- use the `ActivatedRoute` service to get information about the *currently* activated route.
```tsx
import { ActivatedRoute } from '@angular/router'

export class MediaItemList implements OnInit {
	constructor(
		private mediaItemService: MediaItemServce,
		private activatedRoute: ActivatedRoute
	) {}

	ngOnInit(){
		this.activatedRoute.paramMap
			.subscribe(paramMap => {
				let medium = paramMap.get('medium');
				if(medium.toLowerCase() === 'all') medium = ''
				
				this.getMediaItems();
			})
	}
}
```
- as per typical services, we can use constructor injection to create a private property for us
- the activated route passes a `paramMap` property to us, which is an `Observable` (just like in HTTP! - this is because an Observable is a continuous data stream)
	- so, in order to actually "activate" it, we invoke `.subscribe`, and pass a callback for `next` events.
	- because we set up the routing for this project to have the `/all` route, it *will* get picked up as a route parameter
	- so, we want to parse the `medium` parameter and check if it is a valid value for our purpose

## Programmatic Routing
- Instead of routing routes and links to be within *HTML templates*, we can use the Router class to route and navigate:

```tsx
import { Router } from '@angular/router'

export class MediaItemForm implements OnInit {
	constructor(
		private formBuilder: FormBuilder,
		//...,
		private router: Router
	) {}

	onSubmit(mediaItem) {
		this.mediaItemService.add(mediaItem)
			.subscribe(() => {
				this.router.navigate(['/', mediaItem.medium])
			})
	}
}
```
- using the instantiated service property `router`, we invoke `.navigate`
	- in order to use `.navigate`, we pass it a link parameters array
	- thus, it navigates to `/:medium`, when we submit the form based on the submitted item's medium

## Routing and "feature" modules
- When we start implementing more features, we're going to want to create sub-modules that organize our feature sets.
- however, in order to use structural directives like `ngIf`, we need `BrowserModule` - but that should only be imported in the *root* module.
	- the solution is to import the *common* module, which is auto-imported by `BrowserModule`, so we can just import those specific things instead
```tsx
//new-item.module.ts
import { CommmonModule } from '@angular/common'
import { ReactiveFormsModule } from '@angular/forms'
import MediaItemFormComponent from '...'
import { newItemRouting} from './new-item.routing'

@NgModule({
	imports: [
		CommonModule, ReactiveFormsModule, newItemRouting
	],
	declarations: [
		MediaItemFormComponent
	]
})
export class NewItemModule {}

//new-item.routing.ts
import { Routes, RouterModule } from '@angular/router'
import { MediaItemFormComponent } from './...'
const newItemRoutes: Routes = [
	{ path: 'add', component: MediaItemFormComponent }
]
export const newItemRouting = RouterModule.forChild(newItemRoutes)

//app.module.ts
import { NewItemModule } from './new-item/new-item.module'
@NgModule({
	imports: [
		//...
		NewItemModule
	]
})
```
- The point here is that we *abstract* all our feature's imports and functionality into this module specifically.
- we can also create feature-specific routing, by doing a very similar approach to routing with our feature's components
	- the difference here is that we want to use `.forChild` from the router module because we are creating routes for child modules.
- lastly, we need to import the new module into the root and set it as an import in the `NgModule`

## Lazy Loading Modules
- Feature modules are great because they physically organize feature-specific code into its own folders, files, modules, and imports.
	- They are also great, because not all features and code are flat-implemented within the root module, which allows us to modulate how we import and load features
	- lazy loading is the ability to only deliver the necessary modules/functionality when they are *needed*. If the base "state" does not invoke certain features, we don't need to load them until they are strictly needed.
		- the payoff depends on the complexity of the application and features, and can have big impact on initial loading times
- Whenever we include a module in the `imports: []` array within the *root* `NgModule` metadata, Angular sees that and includes it in the total bundle build.
	- However, that makes it *not* lazy loaded - in order to lazy load, we need to import modules differently, so that Angular can *bundle* these modules and features seperately, to be delivered only when their routes are invoked

```tsx
//app.module.ts
// REMOVE ALL IMPORTS AND REFERENCES TO THE MODULES TO LAZY LOAD -->

//app.routing.ts
const appRoutes: Routes = [
	{ 
		path: 'add', 
		loadChildren: () => {
			import('./new-item/new-item.module')
				.then(m => return m.NewItemModule)
		} 
	},
	{ path: ':medium', component: MediaItemListComponent },
	{ path: '', redirectTo: 'all', pathMatch: 'full'}
];

//new-item.routing.ts
const newItemRoutes: Routes = [
	{ 
		path: '', //WAS 'add'
		component: MediaItemFormComponent
	}
]
```
- Lazy loading happens all in the routing, because we move the child's main routing to the root module's routing
	- instead of supplying a component, we use the `loadChildren` property, passing a callback to an import of the module we would like to lazy load
	- the import returns a *promise*, so we need to handle the promise by using `.then`, and returning the `NewItemModule` module *object* that we extracted
- Because we put the `'add'` routing path into the root module as a lazy loading path, we need to remove it from the feature routing - and replace that main route with the default route
	- otherwise, the route would look like `/add/add`

# Styling
- We can control *how* Angular handles per-component styles by using the `ViewEncapsulation` modes
```tsx
import { Component, ViewEncapsulation } from '@angular/core'

@Component({
	selector: '...',
	templateUrl: '...',
	styleUrls: ['...'],
	encapsulation: ViewEncapsulation.None
	//encapsulation: ViewEncapsulation.Emulated
	//encapsulation: ViewEncapsulation.ShadowDom
	//encapsulation: ViewEncapsulation.Native (deprecated by ShadowDom)
})
```
- the `ViewEncapsulation` is a typescript ENUM that has THREE types (technically 4)
	- None
		- don't do anything special modular enhancement
		- the styles in either URLs and in-line are put in the global styles *exactly* the same way you write it
	- Emulated (DEFAULT)
		- *emulate* the ShadowDom on CSS build
	- ShadowDom
		- render the way the ShadowDom does, but this is not supported in all browsers
	- Native (deprecated, use ShadowDom)

## Shadow DOM & Emulated
- The point of using the Shadow DOM is to scope CSS to a *block* of HTML, so that it only applies to a specific set of HTML, and not the whole project
- Angular's default mode of style encapsulation is that it will *emulate* the Shadow DOM to scope CSS rules to the component, and all children of the component
	- if we remember back, Angular "shims" the CSS with unique component-based IDs 

### Why?
- Because we then only need to write CSS in a way that's unique to the *component*, and not the entire project. We can write general CSS rather than worrying about replacing those rules - components can be written in simple CSS that selects elements rather than classes, etc.

## Custom Elements
- Since we are creating "custom" elements using selectors, the browser does not help apply "block-level" styles
- for example, we can add a "host" pseudo-selector in our styles to add block-level styles to selectors of certain types
```tsx
@Component({
	selector: 'mw-category-list',
	template: ``,
	styles: [
		`
			:host{
				display: block;
				margin-bottom: 20px;
			}

			:host-context(.medium-movies) span {
				background-color: #...
			}

			:host-context(.medium-series) span {
				background-color: #...
			}
		`
	]
})
```
- the `:host` psuedo-selector allows us to select the *host* element, being that of elements `<mw-category-list>` in this case.
- likewise, the `:host-context` pseudo-selector allows us to apply styles based on the *context* of the host element
	- it will match the *selectors* that we pass into the *function* call of any ANCESTORS of this host component, meaning any *parents* of it.
	- any parent that has a `<mw-category-list>` component nested in it, will be selected by this context