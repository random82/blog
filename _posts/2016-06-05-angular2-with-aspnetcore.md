---
layout: post
title:  Configuring Angular2 with ASP.NET Core 
date:   2016-06-05 02:26:18 +1100
categories: angular2, visual studio, dotnet core, ASP.NET Core
---

# Angular2 with ASP.NET Core - Step-by-step guide

## Intro

This guide is created on a basis of [Angular 2 - Quickstart](https://angular.io/docs/ts/latest/quickstart.html#)
You can refer to the **Angular2 - Quickstart** guide to check exact contents of application and configuration files.

I was using following versions
```
λ node -v 
v5.1.0
λ npm -v
3.3.12
λ dotnet --version
1.0.0-preview1-002702
```


For this guide I was using Visual Studio 2015 Update 2. Given how quickly **dotnetcore** changes some steps may look diffrently


## Create new ASP.NET Core MVC application

![Create project with Visual Studio](~/img/Angular2-CreateProject.PNG)


TODO: Images here


## Modify gulpfile.js in the project folder

### Add npm folders to gulpfile

```javascript
var paths = {
    js: webroot + "js/**/*.js",
    minJs: webroot + "js/**/*.min.js",
    css: webroot + "css/**/*.css",
    minCss: webroot + "css/**/*.min.css",
    concatJsDest: webroot + "js/site.min.js",
    concatCssDest: webroot + "css/site.min.css",

    npmLibSrc: "./node_modules/",
    npmLibDest: webroot + "lib/npm"
};
```

### Add clean task for npm folders

```javascript
gulp.task("clean:npmlib", function (cb) {
    rimraf(paths.npmLibDest, cb);
});
```

### Add new clean task as a global clean task dependency

```javascript
gulp.task("clean", ["clean:js", "clean:css", "clean:npmlib"]);
```

### Add copy tasks for Angular modules and dependencies

```javascript
gulp.task("copy:systemjs", function () {
    return gulp.src(paths.npmLibSrc + '/systemjs/dist/**/*.*', { base: paths.npmLibSrc + '/systemjs/dist/' })
        .pipe(gulp.dest(paths.npmLibDest + '/systemjs/dist/'));
});

gulp.task("copy:angular2", function () {
    return gulp.src(paths.npmLibSrc + '/@angular/**/*.js', { base: paths.npmLibSrc + '/@angular/' })
        .pipe(gulp.dest(paths.npmLibDest + '/@angular/'));
});

gulp.task("copy:core-js", function () {
    return gulp.src(paths.npmLibSrc + '/core-js/**/*min.js', { base: paths.npmLibSrc + '/core-js/' })
        .pipe(gulp.dest(paths.npmLibDest + '/core-js/'));
});

gulp.task("copy:rxjs", function () {
    return gulp.src(paths.npmLibSrc + '/rxjs/**/*.js', { base: paths.npmLibSrc + '/rxjs/' })
        .pipe(gulp.dest(paths.npmLibDest + '/rxjs/'));
});

gulp.task("copy:zone.js", function () {
    return gulp.src(paths.npmLibSrc + '/zone.js/dist/*.*', { base: paths.npmLibSrc + '/zone.js/dist/' })
        .pipe(gulp.dest(paths.npmLibDest + '/zone.js/dist/'));
});

gulp.task("copy:angular-in-memory", function () {
    return gulp.src(paths.npmLibSrc + '/angular2-in-memory-web-api/*.js', { base: paths.npmLibSrc + '/angular2-in-memory-web-api/' })
        .pipe(gulp.dest(paths.npmLibDest + '/angular2-in-memory-web-api/'));
});

gulp.task("copy:reflect-metadata", function () {
    return gulp.src(paths.npmLibSrc + '/reflect-metadata/*.*', { base: paths.npmLibSrc + '/reflect-metadata/' })
        .pipe(gulp.dest(paths.npmLibDest + '/reflect-metadata/'));
});
```

### Group Angular copy tasks and create publish task

```javascript
gulp.task('copy-dep',
    ['copy:rxjs',
    'copy:angular2',
    'copy:systemjs',
    'copy:core-js',
    'copy:zone.js',
    'copy:reflect-metadata',
    'copy:angular-in-memory']);

gulp.task("publish", ["min", "copy-dep"]);
```


### Upgrade project.json file with new tasks

```javascript
{
    /* Removed for brevity */
    "scripts": {
        "prepublish": [ "npm install", "bower install", "gulp clean", "gulp publish" ],
        "postpublish": [ "dotnet publish-iis --publish-folder %publish:OutputPath% --framework %publish:FullTargetFramework%" ]
    }
}
```

## Configure SystemJS

```javascript
/**
 * System configuration for Angular 2 samples
 * Adjust as necessary for your application needs.
 */
(function(global) {
// map tells the System loader where to look for things

var libFolder = 'lib/npm/';

var map = {
    'app':                        'app', // 'dist',
    '@angular':                   libFolder + '@angular',
    'angular2-in-memory-web-api': libFolder + 'angular2-in-memory-web-api',
    'rxjs':                       libFolder + 'rxjs'
};

/* Removed for brevity */
})(this);
```

## Create Angular2 application

### app.component.ts

```typescript
import { Component } from '@angular/core';
@Component({
    selector: 'my-app',
    template: '<h1>My First Angular 2 App</h1>'
})
export class AppComponent { }
```

### main.ts

```typescript
import { bootstrap }    from '@angular/platform-browser-dynamic';
import { AppComponent } from './app.component';
bootstrap(AppComponent);
```

## Configure TypeScript transpiler

Create a **tsconfig.json** file in the root directory of your web application project

```typescript
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "moduleResolution": "node",
        "sourceMap": true,
        "emitDecoratorMetadata": true,
        "experimentalDecorators": true,
        "removeComments": false,
        "noImplicitAny": false
    }
}
```

Rebuild the project with Visual Studio. If everything is configured correctly, you should be able to see generated JS files in the VIsual Studio

TODO: Image

## Put you Angular2 application inside your ASP.NET Core MVC app

### Modify Views\\Shared\\_Layout.cshtml

```razor
<body>
    @RenderBody()

    <environment names="Development">

        <!-- Polyfill(s) for older browsers -->
        <script src="~/lib/npm/core-js/client/shim.min.js"></script>
        <script src="~/lib/npm/zone.js/dist/zone.js"></script>
        <script src="~/lib/npm/reflect-metadata/Reflect.js"></script>
        <script src="~/lib/npm/systemjs/dist/system.src.js"></script>
        <!-- 2. Configure SystemJS -->
        <script src="systemjs.config.js"></script>
        <script>
            System.import('app').catch(function(err){ console.error(err); });
        </script>
    </environment>
    <environment names="Staging,Production">

    </environment>

    @RenderSection("scripts", required: false)
</body>
```

### Modify Views\\Home\\Index.cshtml

```razor
@{
    ViewData["Title"] = "Home Page";
}

<my-app>Loading my app</my-app>
```

## Troubleshooting

If you application does not appear correctly, check if NPM dependencies are properly loaded.
Try running `gulp publish` from the root folder of your web application after VS rebuild. Sometimes Visual Studio build does not execute gulp tasks correctly