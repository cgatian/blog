---
title: Building Material Themed Components
date: 2017-05-15 10:39:49
tags: Angular, Material
---

If you've pulled in [Material Design Components](https://material.angular.io) into your Angular application, 
you inevitability will find youself wanting to keep your component's colors consistant with the theme of the rest of you application.
In this post I will show you how to create themed components using the existing theme mixins provided by Material. 
This will not work if you're using one of the built-in themes.

If you already know the basics you can skip down to [Building a Themed Component](#building-theme)

### Setup
For this project we are going to use the [Angular CLI](https://github.com/angular/angular-cli) to build your project. However, this tutorial will work with any project.

To start create a fresh Angular CLI project and follow the [Getting Started Guide](https://material.angular.io/guide/getting-started) **steps one through three**. 

Next we will create a new file named `theme.scss` file in the `./src` folder of your Angular project. This file will provide the theme for our application.

{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/c_scale,h_474/v1494792370/screen1_rgywut.png %}

Next open `angular-cli.json` and add a reference to `theme.scss`.

{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1494792370/screen2_yzc3ss.png %}

Open `theme.scss` and add the candy-app theme provided in the [material theme guide](https://material.angular.io/guide/theming).

```scss
@import '~@angular/material/theming';

@include mat-core();

$candy-app-primary: mat-palette($mat-indigo);
$candy-app-accent:  mat-palette($mat-pink, A200, A100, A400);
$candy-app-warn:    mat-palette($mat-red);

$candy-app-theme: mat-light-theme($candy-app-primary, $candy-app-accent, $candy-app-warn);
```
Open `app.component.html` and add a button to verify the setup.

```html
<h1>
  {{title}}
</h1>

<button type="button" md-raised-button color="accent">Test</button>
```
Run `npm start` and verify your builds and displays renders the page below.

{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1494792370/screen3_xuq4aq.png %}

### Create A New Component

Now with our application is configured with a Material Theme we can build a component to utilize our theme.

First, create a new component in your project called `UserComponent`.
This component is simply going to take an `Input` of `name` and display it within a `span` element.

**user.component.ts**
```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.scss']
})
export class UserComponent {
  @Input() name: string;
}
```
**user.component.html**
```html
<div class="user">
  <span>Name: {{name}}</span>
</div>
```
**user.component.scss**
```css
.user {
  padding: 10px;
  border: 1px solid green;
}

```
Update `app.module.ts` to include your new component, and drop your component into `app.component.html`.
**app.component.html**
```html
<h1>
  {{title}}
</h1>

<app-user name="Dawson"></app-user>
<button type="button" md-raised-button color="accent">Test</button>
```
The result:

{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1494792370/screen4_rwa6rn.png %}

### <a name="building-theme"></a> Building a Themed Component

So far we've added Material and created a new compnent that has some styles defined.
Next we are going to add the secondary color from our Material Theme and add it as the background to the component.

First, create a new file called `user.component-theme.scss`. 
It's important to note we are not using the existing `user.component.scss` file.
Understand that we are seperating the concerns of the stylesheets, the `user.component.scss` will be responsible all our **non-theme** CSS styles, and the `user.component-theme.scss` is used for all **themed** CSS styles, defined by our Material theme.

Just to reitterate, it's fine to have color properties in `user.component.scss` but just not ones specific to your material theme, e.g. a green border from our example.

Open `user.component-theme.scss` and add the following:
```scss
// Import Material Mixins
@import '~@angular/material/theming';

// Define a custom mixin that takes in the current theme
@mixin user-component-theme($theme) {

  // Parse the theme and create variables for each color in the pallete
  $primary: map-get($theme, primary);
  $accent: map-get($theme, accent);
  $warn: map-get($theme, warn);

  // Create theme specfic styles
  .user-theme {
    background-color: mat-color($accent);
  }
}
```
Open `theme.scss` and import the mixin.
```scss
@import '~@angular/material/theming';
// Imports the custom mixin
@import './app/components/user/user.component-theme';

@include mat-core();

$candy-app-primary: mat-palette($mat-indigo);
$candy-app-accent:  mat-palette($mat-pink, A200, A100, A400);
$candy-app-warn:    mat-palette($mat-red);

$candy-app-theme: mat-light-theme($candy-app-primary, $candy-app-accent, $candy-app-warn);

@include angular-material-theme($candy-app-theme);
// Pass the theme variable to the mixin
@include user-component-theme($candy-app-theme);

```
Success, we now have a Material themed component. 
{% img http://res.cloudinary.com/dk1rn2kmf/image/upload/v1494792370/screen5_z2aynk.png %}

