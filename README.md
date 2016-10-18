# Step by Step guide of using Angular2 with Typescript for ASP.NET MVC in Visual Studio 2015 


During last couple of months, I have received a lot of requests how to use angular2 in ASP.NET MVC in visual studio environment, Its quite easy to integrate angular2 in asp.net core project, so I am publishing step by step guide to integrate Angular 2 in ASP.NET MVC.

- - - -

## Step 1: Create an ASP.NET MVC project

Create the ASP.NET 4.x project as follows:

- In Visual Studio, select File | New | Project from the menu.
- In the template tree, select Templates | Visual C# (or Visual Basic) | Web.
- Select the ASP.NET Web Application template, give the project a name, and click OK.
- Select the desired ASP.NET 4.5.2 template (>= 4.x.x) and click OK.

![screenshot_71](https://cloud.githubusercontent.com/assets/10474169/19492115/0d8e72fc-953b-11e6-8bf8-2b0c1c98116b.png)

![screenshot_8](https://cloud.githubusercontent.com/assets/10474169/19492138/1dadd6a0-953b-11e6-87f9-e0befbc541d3.png)

- Avoid Adding any authorization and authentication at this point of time to keep project quite simple

![screenshot_9](https://cloud.githubusercontent.com/assets/10474169/19492166/31eea5e0-953b-11e6-9475-da8f55f80e62.png)

_Please note all configuration and package versions are according to Angular Quickstart Guide_

- - - -

## Step 2: Create Package.json file

package.json identifies npm package dependencies for the project.

    {
      "name": "ang2demo",
      "version": "1.0.0",
      "scripts": {},
      "license": "ISC",
      "dependencies": {
        "@angular/common": "~2.0.1",
        "@angular/compiler": "~2.0.1",
        "@angular/core": "~2.0.1",
        "@angular/forms": "~2.0.1",
        "@angular/http": "~2.0.1",
        "@angular/platform-browser": "~2.0.1",
        "@angular/platform-browser-dynamic": "~2.0.1",
        "@angular/router": "~3.0.1",
        "@angular/upgrade": "~2.0.1",
        "bootstrap": "^3.3.7",
        "core-js": "^2.4.1",
        "reflect-metadata": "^0.1.8",
        "rxjs": "5.0.0-beta.12",
        "systemjs": "0.19.39",
        "zone.js": "^0.6.25"
      },
      "devDependencies": {
        "@types/core-js": "^0.9.34",
        "typescript": "^2.0.3",
        "typings": "^1.4.0"
      }
    }

![screenshot_4](https://cloud.githubusercontent.com/assets/10474169/19492192/52790454-953b-11e6-8087-f5bde93edbbc.png)

***Note:***

**Please note that @types/core-js are not mentioned in Angular Quickstart Guide in devDepenedcies section, Add this to avoid duplicate identifier error otherwise you are going to get as “Angular 2 can’t find Promise, Map, Set and Iterator”**

- - - -

## Step 3: Create tsconfig.json file

This file defines how the TypeScript compiler generates JavaScript from the project’s files.

For Visual Studio 2015 we must add "compileOnSave": true to the TypeScript configuration (tsconfig.json) file as shown here.

    {
      "compileOnSave": true,
      "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "moduleResolution": "node",
        "sourceMap": true,
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true,
        "removeComments": false,
        "noImplicitAny": false,
        "typeRoots": [
          "node_modules/@types"
        ],
        "types": [
          "core-js"
        ]
      }
    }

![screenshot_12](https://cloud.githubusercontent.com/assets/10474169/19492218/6e478066-953b-11e6-9b33-bbd346c276d8.png)

***Note:***

* On creating this file you will receive alert from Visual Studio such as below, Just Press No:

![screenshot_14](https://cloud.githubusercontent.com/assets/10474169/19492219/6e47daa2-953b-11e6-8b39-f333972bac16.png)

* Please note that below code is not note mentioned in Angular Quickstart Guide in tsconfig.json, Add this to avoid duplicate identifier error otherwise you are going to get as “Angular 2 can’t find Promise, Map, Set and Iterator”

![screenshot_21](https://cloud.githubusercontent.com/assets/10474169/19492220/6e48424e-953b-11e6-8bfd-26e573266b54.png)

- - - -

## Step 4: Create typings.json file

This file provides additional definition files for libraries that the TypeScript compiler doesn’t natively recognize.

    {
      "globalDependencies": {
        "core-js": "registry:dt/core-js#0.0.0+20160725163759",
        "jasmine": "registry:dt/jasmine#2.2.0+20160621224255",
        "node": "registry:dt/node#6.0.0+20160909174046"
      }
    }

![screenshot_31](https://cloud.githubusercontent.com/assets/10474169/19492286/a6a1dc4a-953b-11e6-9097-5747e5597b39.png)

- - - -

## Step 5: Install package.json file

Open CMD and redirect to your application folder and Using npm from the command line, install the packages listed in package.json with the command:

    > npm install

![screenshot_19](https://cloud.githubusercontent.com/assets/10474169/19492287/a6a3300e-953b-11e6-81a8-4da455d54858.png)

After executing command, output will be like this.

![screenshot_20](https://cloud.githubusercontent.com/assets/10474169/19492285/a6a03e80-953b-11e6-8cde-c9c1068dd092.png)

***Note:***

- Error messages—in red—might appear during the install, and you might see npm WARN messages. As long as there are no npm ERR! messages at the end, you can assume success.

- Do not include the node_modules folder in the project. Let it be a hidden project folder.But you may view the hidden folder in Visual Studio using “Show All Files” option in Solution Explorer.

![screenshot_22](https://cloud.githubusercontent.com/assets/10474169/19492284/a69f79a0-953b-11e6-99df-4e19e9f73dea.png)

- - - -

## Step 6: Create Sample Angular 2 Code using Typescript

* Create a folder name “App” in Scripts folder

* Create application module file

Angular itself is split into separate Angular Modules. This makes it possible for you to keep payload size small by only importing the parts of Angular that your application needs.Every Angular application has at least one module: the root module, named AppModule here.

Create the file App/app.module.ts with the following content:

    import { NgModule }      from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent }   from './app.component';
    @NgModule({
      imports:      [ BrowserModule ],
      declarations: [ AppComponent ],
      bootstrap:    [ AppComponent ]
    })
    export class AppModule { }
    
This is the entry point to your application.

Root module needs to import the BrowserModule from @angular/platform-browser to the imports array.

This is the smallest amount of Angular that is needed for a minimal application to run in the browser.

* Create a component & add it to your application

Every Angular application has at least one component: the root component, named AppComponent here.Components are the basic building blocks of Angular applications. A component controls a portion of the screen—a view—through its associated template.

Create the file App/app.component.ts with the following content:

    import { Component } from '@angular/core';
    @Component({
      selector: 'my-app',
      template: 'My First Angular App – Demo' 
    }) 
    export class AppComponent { }

* Create a Start up file

Now we need to tell Angular to start up your application.

Create the file App/main.ts with the following content:

    import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
    import { AppModule } from './app.module';
    const platform = platformBrowserDynamic();
    platform.bootstrapModule(AppModule);

This code initializes the platform that your application runs in, then uses the platform to bootstrap your AppModule.

***Note:***

>> Please note that transplied typescript files will automatically be available in App folder as we have mentioned attribute CompileOnSave is true in tsconfig.json Files visible in Visual Studio:

![screenshot_23](https://cloud.githubusercontent.com/assets/10474169/19492595/e445c5ec-953c-11e6-9cd8-ee66593f12bb.png)

>> Files visible in Folder:

![screenshot_32](https://cloud.githubusercontent.com/assets/10474169/19492594/e4453f00-953c-11e6-88b7-7c42a0942acd.png)

- - - -

## Step 7: Create systemjs.config.js file

This file provides information to a module loader about where to find application modules, and registers all the necessary packages.

Create the file Scripts/systemjs.config.js with the following content:

    /**
     * System configuration for Angular samples
     * Adjust as necessary for your application needs.
     */
    (function (global) {
        System.config({
            paths: {
                // paths serve as alias
                'npm:': '/node_modules/'
            },
            // map tells the System loader where to look for things
            map: {
                // our app is within the app folder
                app: '/Scripts',
                // angular bundles
                '@angular/core': 'npm:@angular/core/bundles/core.umd.js',
                '@angular/common': 'npm:@angular/common/bundles/common.umd.js',
                '@angular/compiler': 'npm:@angular/compiler/bundles/compiler.umd.js',
                '@angular/platform-browser': 'npm:@angular/platform-browser/bundles/platform-browser.umd.js',
                '@angular/platform-browser-dynamic': 'npm:@angular/platform-browser-dynamic/bundles/platform-browser-dynamic.umd.js',
                '@angular/http': 'npm:@angular/http/bundles/http.umd.js',
                '@angular/router': 'npm:@angular/router/bundles/router.umd.js',
                '@angular/forms': 'npm:@angular/forms/bundles/forms.umd.js',
                // other libraries
                'rxjs': 'npm:rxjs'
            },
            // packages tells the System loader how to load when no filename and/or no extension
            packages: {
                app: {
                    main: './main.js',
                    defaultExtension: 'js'
                },
                rxjs: {
                    defaultExtension: 'js'
                }
            }
        });
    })(this);

![screenshot_5](https://cloud.githubusercontent.com/assets/10474169/19492658/332638d6-953d-11e6-937a-b7f1c672711b.png)

Note:

* npm attribute highlighted in red color in above image should point to folder which has all installed packages, in our case it is node_modules folder.

* app attribute highlighted in red color in above image should point to folder which has all application transcript code, in our case it is Scripts folder.

* main attribute highlighted in red color in above image should point to js file which contains angular application startup code, in our case it is main.ts file.

- - - -

## Step 8: Load and Render Angular2 application in ASP.NET MVC Views

![screenshot_15](https://cloud.githubusercontent.com/assets/10474169/19492712/7f0b15f0-953d-11e6-9a67-f71a2c706838.png)

* In order to load angular 2 application in MVC, integrate angular 2 libraries references and system.js configurations in Views/Shared/_Layout.cshtml file
   
   
        @ViewBag.Title - My ASP.NET Application
        @Styles.Render("~/Content/css")
        @Scripts.Render("~/bundles/modernizr")
        http://~/node_modules/core-js/client/shim.min.js
        http://~/node_modules/zone.js/dist/zone.js
        http://~/node_modules/reflect-metadata/Reflect.js
        http://~/node_modules/systemjs/dist/system.src.js
        http://~/Scripts/systemjs.config.js

            System.import('../../Scripts/App/main').catch(function (err)
            {
                console.error(err);
            });
    

![screenshot_72](https://cloud.githubusercontent.com/assets/10474169/19492750/991f4ef2-953d-11e6-9221-3061646a2318.png)

Mention your angular 2 main file reference (file which contains application bootstraping code) in System.import api as a parameter, Note the forward slash at the beginning of the relative path are according to location of main.ts file

    System.import('../../Scripts/App/main')
    
* In order to kickstart angular code in browser, integrate component in Views/Home/index.cshtml file

        @{
            ViewBag.Title = "Home Page";
        }

        Loading...

- - - -

## Step 9: Build and run the app

Click the Run button or press CTRL + F5 to build and run the application.

This launches the default browser and runs the QuickStart sample application.

![screenshot_24](https://cloud.githubusercontent.com/assets/10474169/19492784/c774a216-953d-11e6-8881-3118d8c8d506.png)


Try editing any of the project files. Save and refresh the browser to see the changes.

- - - -
- - - -

###In case of Error such as:###

***Error 1***

**Compiler errors such as “Property map does not exist on type Observable” and “Observable cannot be found” indicate an old release of Visual Studio. Exit Visual Studio and follow the instructions here.**

You’ll be asked to replace the file

    c:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\CommonExtensions\Microsoft\TypeScript.typescriptServices.js
    
This operation requires admin privileges.

***Error 2***

**IDE issues such as ‘component can not be properly resolved, probably its located in an inaccessible module’**

![screenshot_33](https://cloud.githubusercontent.com/assets/10474169/19492825/f350b384-953d-11e6-8067-97bb48629bcf.png)

**occurs when angular2 keyowrd are highlighted red as no intellisense is available for them by Visual Studio 2015 visible in below images**

![screenshot_6](https://cloud.githubusercontent.com/assets/10474169/19492826/f351f6d6-953d-11e6-8e21-11c45a99f1fb.png)

![screenshot_41](https://cloud.githubusercontent.com/assets/10474169/19492827/f3521148-953d-11e6-8619-e656bba6753e.png)

Inorder to resolve them make sure you have Resharper -> Check your Resharper Typescript Language settings. Resharper might be set to older version of typescript 1.6.  Download latest version of resharper and restart Visual Studio. In case it doesnt work try to set Typescript language level to 2.0 under Inspection Tab from Resharper Options menu.
