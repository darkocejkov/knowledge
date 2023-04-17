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

## Custom Validation
