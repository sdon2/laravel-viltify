<p align="center">
    <img src="stubs/resources/src/assets/logo.png" alt="Laravel VILTify">
</p>

<p align="center">
    <a href="https://packagist.org/packages/dalpizzol/laravel-viltify">
        <img src="https://img.shields.io/packagist/dt/dalpizzol/laravel-viltify" alt="Total Downloads">
    </a>
    <a href="https://packagist.org/packages/dalpizzol/laravel-viltify">
        <img src="https://img.shields.io/packagist/v/dalpizzol/laravel-viltify" alt="Latest Stable Version">
    </a>
    <a href="https://packagist.org/packages/dalpizzol/laravel-viltify">
        <img src="https://img.shields.io/packagist/l/dalpizzol/laravel-viltify" alt="License">
    </a>
</p>

# **Laravel VILTify**

**Laravel VILTify** is a heavily opinionated Laravel starter kit. It's intent is to seamlessly integrate [<ins>**V**</ins>ue](https://vuejs.org/), [<ins>**I**</ins>nertia.js](https://inertiajs.com/), [<ins>**L**</ins>aravel](https://laravel.com/), [<ins>**T**</ins>ailwindCSS](https://tailwindcss.com/) and [Vuet<ins>**ify**</ins>](https://vuetifyjs.com/en/), so you don't waste your time learning how to do it and focus on writing your application, **leaving setup behind**.

## Table of contents

* [Requirements](#requirements)
* [Quick start](#quick-start)
* [Troubleshooting](#troubleshooting)
* [Why would I use this instead of Laravel Breeze or Laravel Jetstream?](#why-would-i-use-this-instead-of-laravel-breeze-or-laravel-jetstream)
  
  * [Vue CLI instead of Laravel Mix](#vue-cli-instead-of-laravel-mix)
  * [Vuetify's full power in your hands](#vuetifys-full-power-in-your-hands)
  * [No conflicts between Vuetify and TailwindCSS classes](#no-conflicts-between-vuetify-and-tailwindcss-classes)
  * [Inertia.js conveniences](#inertiajs-conveniences)
    * [The `v-link` global component](#the-v-link-global-component)
    * [Server driven toast notifications](#server-driven-toast-notifications)
  * [Resonable defaults with production builds in mind](#resonable-defaults-with-production-builds-in-mind)
    * [Code Splitting out of the box](#code-splitting-out-of-the-box)
    * [Material Design Icons JS SVG instead of WebFont](#material-design-icons-js-svg-instead-of-webfont)
  * [Separeted builds for different endpoints](#separeted-builds-for-different-endpoints)
  * [Isolated client side environment settings](#isolated-client-side-environment-settings)
* [Drawbacks](#drawbacks)
* [License](#license)

## **Requirements**

* **Operating System**: This package should work on **MacOS** and **Linux**. If you're using **Windows**, you're gonna need **WSL**.

* **Laravel 8, 9**

* **Vue CLI**: Under the hood, this package will call the [**Vue CLI**](https://cli.vuejs.org/) tool. Make sure you have **Vue CLI V5** installed before continuing. If you don't, [**the installation**](https://cli.vuejs.org/guide/installation.html) is fairly simple.

## **Quick Start**

> **HEADS UP**: this package is meant to be used **ONLY ON FRESH LARAVEL INSTALLATIONS**.

```bash
# Create a new Laravel project
composer create-project laravel/laravel my-app

# Enter the project folder
cd my-app

# Install Laravel VILTify
composer require dalpizzol/laravel-viltify

# Create your base tables
php artisan migrate

# Run the installer
php artisan viltify:install

# Remove the package so you don't accidentally run it again in the future
composer remove dalpizzol/laravel-viltify

# Enter the resources folder
cd resources

# Lift the assets devserver
npm run serve

# Lift the PHP server in another terminal
# (if you're not already running one)
php artisan serve
```

> **HEADS UP**:


> Be aware that you're running two servers, just like when you use Laravel Mix. Your PHP application runs at port `80` while the devserver runs at `8080`. So, in your browser, you navigate to your PHP application at port `80`, for instance: `http://localhost`.

## **Troubleshooting**

In some scenarios, if you're using Node.js 17.x.x or higher, you might encounter an `ERR_OSSL_EVP_UNSUPPORTED` error when running the `resources/package.json` scripts, like `npm run serve` or `npm run build`.

This is related to changes introduced by Node.js 17 and you can read more about this [here](https://github.com/vuejs/vue-cli/issues/6770), [here](https://github.com/PassiveDNS/PassiveDNS/pull/24), and [here](https://stackoverflow.com/questions/69394632/webpack-build-failing-with-err-ossl-evp-unsupported).

You don't need to downgrade Node.js. Instead, just prepend `NODE_OPTIONS=--openssl-legacy-provider` to your `resources/package.json` scripts:

```js
// resources/package.json

{
  scripts: {
    "serve": "NODE_OPTIONS=--openssl-legacy-provider vue-cli-service serve",
    "build": "NODE_OPTIONS=--openssl-legacy-provider vue-cli-service build"
  }
}
```

## **Why would I use this instead of Laravel Breeze or Laravel Jetstream?**

This package is actually heavily based on [**Laravel Breeze**](https://github.com/laravel/breeze). A lot of code was simply ripped off from that. But there's some advantages here:

### **Vue CLI instead of Laravel Mix**

This package actually turns your `resources` folder into a Vue app generated by [**Vue CLI**](https://cli.vuejs.org/). This means that inside `resources` you can do things like `vue add some-vue-cli-plugin` which you can't when using [Laravel Mix](https://laravel-mix.com/). Vue CLI is also much more stable than Laravel Mix and much more focused and battle tested for use with Vue, so you are probably going to save some time avoiding common issues related to Laravel Mix.

This also allows you to use [**Vue CLI's GUI**](https://cli.vuejs.org/guide/creating-a-project.html#vue-create) inside `resources`, if that's your thing...

### **Vuetify's full power in your hands**

While official Laravel starter kits delivers a dozen Vue components, they are fairly simple. **Laravel VILTify** comes with [**Vuetify**](https://vuetifyjs.com/) UI component library already installed and configured so you can take advantage of 70+ highly customizable, responsive and beautiful components based on Google's [**Material Design**](https://material.io/design).

### **No conflicts between Vuetify and TailwindCSS classes**

**Laravel VILTify** comes with Vuetify and [**TailwindCSS**](https://tailwindcss.com/) already configured so you can use both without worrying about class collisions. All you have to do is to prefix your tailwind classes with `tw-`.

### **Inertia.js conveniences**

#### **The v-link global component**

**Laravel VILTify** offers a globally registered `v-link` component which is a [**Vuetify `v-btn`**](https://vuetifyjs.com/en/components/buttons/) component wrapped by an [**Inertia.js `Link`**](https://inertiajs.com/links) component. This way you can use Inertia.js links everywhere without having to remember to include the `Link` component locally on every component and they can use every style available to `v-btn` components. Inertia's `Link` component is also registered globally.

```html
<v-link :href="someUrl"
  color="success"
  rounded
  outlined
  x-large
>
  This is an Inertia.js link rendered as a Vuetify Button
</v-link>
```

#### **Server driven toast notifications**

It also ships with a server driven toast notification system specifically crafted to work nicely with Inertia.js. This means you can do things like this:

```php
// Success message
return redirect()
  ->route('dashboard')
  ->toast('Laravel VILTify is awesome');

// Error message
return redirect()
  ->route('dashboard')
  ->toast('You didn\'t give Laravel VILTify a star. =(', 'error');
```

Another cool feature it offers are **validation toasts**. This is usefull when you have some "invisible data" on a form that may not be valid. For instance, a reCaptcha V3 token. Since there's no visible form element for the token, you may want to toast the validation error if the token validation fails.

```php
Toast::validation('recaptcha_token');

request()->validate([
  'recaptcha_token',
  // ...
]);

// It also accepts an array:
// Toast::validation(['recaptcha_token', 'another_field'])
```

> Make sure you call `Toast::validation` before you actually run your validations.

### **Resonable defaults with production builds in mind**

#### **Code Splitting out of the box**

Since we're dealing with SPAs, **Laravel VILTify** makes sure that code splitting takes place. All the files needed by any route are loaded on demand by default.

#### **Material Design Icons JS SVG instead of WebFont**

By default Vuetify comes configured to use @mdi/js instead of a regular WebFont, so it enforces that you only ever load the icons you really need. [**Learn more here**](https://vuetifyjs.com/en/features/icon-fonts/#material-design-icons-js-svg).

### **Separeted builds for different endpoints**

If you need a separate build for an entirely different endpoint, for instance, an **admin area**, follow these steps:

**1.** Duplicate `resources/src/templates/app.blade.php` and rename it to `resources/src/templates/app-admin.blade.php`. This will be your Inertia's `rootView`.

**2.** Create a new entry in the `pages` prop at `resources/vue.config.js`.

```js
  pages: {
    ...page('main', 'app'),
    ...page('admin', 'app-admin')
  },

  // The following disables prefetch links generation for each endpoint
  chainWebpack: config => {
    config.plugins.delete('prefetch-main'),
    config.plugins.delete('prefetch-admin')
  }
```

**3.** Duplicate the `resources/src/main.js` and rename it to `resources/src/admin.js`.

**4.** Then, you need to instruct Inertia to use the `app-admin.blade.php` view when rendering an admin page.

```php
return Inertia::setRootView('app-admin')
  ->render('admin/Dashboard');
```

### **Isolated client side environment settings**

When using Laravel Mix, client side environment settings are put into `MIX_` prefixed variables inside `.env` file. Here, since our `resources` folder is actually a Vue CLI generated app, you can leverage [**the pattern shipped by Vue CLI do deal with environment variables**](https://cli.vuejs.org/guide/mode-and-env.html#environment-variables). **Laravel VILTify** comes out of the box with a `resources/.env.local` for the devserver and a `resources/.env.production` example file, so you can deal with every client side setting separated from Laravel settings.

## Drawbacks

Since the intent here is to use Vuetify, we're still using Vue 2 and Webpack instead of Vue 3 and Vite, since Vuetify support for Vue 3 hasn't released yet.

## **License**

This software is provided free of charge and without restriction under the [MIT License](/LICENSE)
