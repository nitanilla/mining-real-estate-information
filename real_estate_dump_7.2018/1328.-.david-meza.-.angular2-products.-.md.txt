===================================
How to write an Angular 2 Component 
===================================

The Angular team introduced quite a few changes in version 2 of the framework, and components are one of the important ones. If you are familiar with Angular 1 applications, components are actually a form of directives that have been extended with template-oriented features. In addition, components are optimized for better performance and simpler configuration than a directive since it doesn’t support all its features. And, while a component is technically a directive, it is so distinctive and central to Angular 2 applications that you’ll find it is often separated as a different ingredient for the architecture of an application.

So, what is a component? In simple words, a component is a building block of an application that controls a part of your screen real estate, or your “view.” It does one thing and it does it well. For example, you may have a component to display a list of active chats in a messaging app (which in turn may have child components to display the details of the chat or the actual conversation). Or, you may have an input field that uses Angular’s two-way data binding to keep your markup in sync with your Javascript. Or, at the most elementary level, you can have a component that substitutes with an HTML template with no special functionality just because you wanted to break down something complex into smaller, more manageable parts.

Now, I don’t believe too much in learning something by only reading about it, so let’s get our hands dirty and write our own component to see some sample usage. I will assume that you already have Typescript installed and have done the initial configuration required for any Angular 2 app. If you haven’t you can check out how to do so by [clicking on this link.](https://angular.io/docs/ts/latest/quickstart.html)

You may have already seen a component at its most basic level:

```javascript
import {Component} from 'angular2/core';

@Component({
  selector: 'my-app',
  template: '<h1>{{ title }}</h1>'
})

export class AppComponent {
  title = 'Hello World!';
}
```

That’s it! That’s all you really need to have a component. Three things are happening here:

1. We are importing the `Component` class from our Angular 2 core package.

2. We are using a Typescript **decorator** to attach some **metadata** to our `AppComponent` class. If you don’t know what a decorator is, it is simply a function that extends our class with Angular code so that it becomes an Angular component. Otherwise, it would just be a plain class with no relation to the Angular framework. In our options, we defined a selector, which is the tag name we use in our HTML so Angular can find where to insert our component, and a template, which becomes to inner contents of our selector tag. You may notice we are also using **interpolation** to bind our component data and display the value of our public variable in our template.

3. We export our `AppComponent` class so that we can import it elsewhere (in this case, we would import it in our main script so we can bootstrap our application).

That’s a good start, but let’s get into a more complex example that showcases other powerful features of Angular and Typescript/ES2015. In the following example, I've decided to stuff everything into one component. However, if you'd like to stick to best practices and divide the code into different components and services, or if you get lost at any point you can [check out the finished/refactored example here](https://github.com/david-meza/angular2-products/tree/master). Without any further ado, let’s make a quick page that displays a list of products. Let’s start with the index:

```html
<html>
  <head>
    <title>Products</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">    

    <script src="node_modules/es6-shim/es6-shim.min.js"></script>
    <script src="node_modules/systemjs/dist/system-polyfills.js"></script>

    <script src="node_modules/angular2/bundles/angular2-polyfills.js"></script>
    <script src="node_modules/systemjs/dist/system.src.js"></script>
    <script src="node_modules/rxjs/bundles/Rx.js"></script>
    <script src="node_modules/angular2/bundles/angular2.dev.js"></script>

    <link rel="stylesheet" href="styles.css">

    <script>
      System.config({
        packages: {        
          app: {
            format: 'register',
            defaultExtension: 'js'
          }
        }
      });
      System.import('app/main')
            .then(null, console.error.bind(console));
    </script>

  </head>

  <body>
    <my-app>Loading...</my-app>
  </body>

</html>
```

Nothing out of the ordinary going on here. We are just importing all the necessary scripts for our application to work as demonstrated in the quick-start.

Our `app/main.ts` should already look somewhat like this:

```javascript
import {bootstrap} from ‘angular2/platform/browser’
import {AppComponent} from ‘./app.component’

bootstrap(AppComponent);
```

We are importing the bootstrap function from the Angular 2 package, and an AppComponent class from the local directory. Then we initialize the application.

First, we will create a product class which will define the constructor and type definition of any products we make. Create `app/product.ts`:

```javascript
export class Product {
  id: number;
  price: number;
  name: string;
}
```

Next, we will create an `app.component.ts` file which is where the magic happens. I've decided to stuff everything in here for demonstration purposes, but ideally you would want to extract the products array into its own service, the HTML template into its own file, and the product details into its own component. This is how the component will look like:

```javascript
import {Component} from 'angular2/core';
import {Product} from './product'

@Component({
  selector: 'my-app',
  template: `
  <h1>{{title}}</h1>
  <ul class="products">
    <li *ngFor="#product of products"
      [class.selected]="product === selectedProduct"
      (click)="onSelect(product)">
      <span class="badge">{{product.id}}</span> {{product.name}}
    </li>
  </ul>
  <div *ngIf="selectedProduct">
    <h2>{{selectedProduct.name}} details!</h2>
    <div><label>id: </label>{{selectedProduct.id}}</div>
    <div><label>Price: </label>{{selectedProduct.price | currency: 'USD': true }}</div>
    <div>
      <label>name: </label>
      <input [(ngModel)]="selectedProduct.name" placeholder="name"/>
    </div>
  </div>
  `,
  styleUrls: ['app/app.component.css']
})

export class AppComponent {
  title = 'My Products';
  products = PRODUCTS;
  
  selectedProduct: Product;
      
  onSelect(product: Product) { this.selectedProduct = product; }
}

const PRODUCTS: Product[] = [
  { "id": 1, "price": 45.12, "name": "TV Stand" },
  { "id": 2, "price": 25.12, "name": "BBQ Grill" },
  { "id": 3, "price": 43.12, "name": "Magic Carpet" },
  { "id": 4, "price": 12.12, "name": "Instant liquidifier" },
  { "id": 5, "price": 9.12, "name": "Box of puppies" },
  { "id": 6, "price": 7.34, "name": "Laptop Desk" },
  { "id": 7, "price": 5.34, "name": "Water Heater" },
  { "id": 8, "price": 4.34, "name": "Smart Microwave" },
  { "id": 9, "price": 93.34, "name": "Circus Elephant" },
  { "id": 10, "price": 87.34, "name": "Tinted Window" }
];
```

And `app/app.component.css`:

```css
.selected {
  background-color: #CFD8DC !important;
  color: white;
}
.products {
  margin: 0 0 2em 0;
  list-style-type: none;
  padding: 0;
  width: 15em;
}
.products li {
  position: relative;
  min-height: 2em;
  cursor: pointer;
  position: relative;
  left: 0;
  background-color: #EEE;
  margin: .5em;
  padding: .3em 0;
  border-radius: 4px;
  font-size: 16px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  color: #3F51B5;
  display: block;
  width: 100%;

  -webkit-transition: all 0.3s ease;
  -moz-transition:    all 0.3s ease;
  -o-transition:      all 0.3s ease;
  -ms-transition:     all 0.3s ease;
  transition:         all 0.3s ease;
}
.products li.selected:hover {
  background-color: #BBD8DC !important;
  color: white;
}
.products li:hover {
  color: #607D8B;
  background-color: #DDD;
  left: .1em;
  color: #3F51B5;
  text-decoration: none;
  font-size: 1.2em;
  background-color: rgba(0,0,0,0.01);
}
.products .text {
  position: relative;
  top: -3px;
}
.products .badge {
  display: inline-block;
  font-size: small;
  color: white;
  padding: 0.8em 0.7em 0 0.7em;
  background-color: #607D8B;
  line-height: 1em;
  position: relative;
  left: -1px;
  top: 0;
  height: 2em;
  margin-right: .8em;
  border-radius: 4px 0 0 4px;
}
```

I'll explain what is happening:

1. We import from Component so that we can decorate our new component, and we import Product so we can create an array of products and have access to Typescript type infererences.

2. We decorate our component with a selector property 'my-app' that finds `<my-app></my-app>` tags and inserts our component there. I decided to define the template in this file instead of using a URL so I can demonstrate how handy is the ES2015 template string syntax (no more long strings or plus-separated strings). Finally, the styleUrls property uses an absolute file path, and any styles applied will only affect the template in this scope.

3. The actual component only has a few properties outside of the decorator configuration: It has a `title` that we can bind to our template, a `products` array that we will iterate in our markup, a `selectedProduct` that is a scope variable that will initialize as undefined, and an `onSelect` method that will be run every time we click on a list item.

4. Finally, we define a constant (`const` because I've hard-coded it in and won't change in runtime) `PRODUCTS` to mock an object that is usually returned by a service after an external request.

Also worth noting:

* Since we are using Typescript we can make inferences about what type of data will our variables hold. For example, you may have noticed I defined type `Product` whenever I know that this the only kind of object I want to allow for that variable or to be passed to a function.

* Angular 2 has different property prefixes and if you would like to learn when to use each one, you can check out [this Stack Overflow question](http://stackoverflow.com/questions/35944749/what-is-the-difference-between-parentheses-brackets-and-asterisks-in-angular2?answertab=votes#tab-top).

And that's it! We now have a bit more complex component that has a particular functionality. As I previously mentioned, this could be refactored and that would look something like this:

```javascript
import {Component, OnInit} from 'angular2/core';
import {Product} from './product';
import {ProductDetailComponent} from './product-detail.component';
import {ProductService} from './product.service';

@Component({
    selector: 'my-app',
    templateUrl: 'app/app.component.html',
    styleUrls: ['app/app.component.css'],
    directives: [ProductDetailComponent],
    providers: [ProductService]
})

export class AppComponent implements OnInit {
    title = 'Products';
    products: Product[];
    selectedProduct: Product;
    
    constructor(private _productService: ProductService) { }
    
    getProducts() {
        this._productService.getProducts().then(products => this.products = products);
    }
    ngOnInit() {
        this.getProducts();
    }
    onSelect(product: Product) { this.selectedProduct = product; }
}
```

In this example, we get our product data from a service and separate our product detail template into a child component, which is much more modular.

Hope you've enjoyed reading this post. I spent a lot of time reading the Angular docs and tried to make a concise post out of what I learned. Let me know if there's anything I can do to improve it!

