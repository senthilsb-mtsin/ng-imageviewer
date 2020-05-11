# ng-imageviewer
Wrapper for viewerjs.js image viewer for Angular 9

fengyuanchen/viewerjs   <a href="https://github.com/fengyuanchen/viewerjs">viewer.js</a>

# Usage

Clone the Repository 

Intstall the node_modules 

```shell
npm install
```
To Run the Demo

```shell
ng serve -o
```



## Getting started

Create new Angular Application or Open Existing Application

### Installation

```shell
npm install viewerjs --add
```
![GitHub Logo](/images/logo.png)

This would install the javascript libary into node_modules into your Angular Application

Add refence to ```viewer.js``` or ```viewer.min.js``` and ```viewer.css``` or ```viewer.min.js``` to the Application from the node_modules
You can add to _angular.json_ ```"styles"``` and ```"scripts"``` sections

Make sure you add the same to all build types *sections* like _build,test,prod_ etc...


 ```json
         "build": {
          "builder": "@angular-devkit/build-angular:browser",
          "options": {
            "outputPath": "dist/xc-imageviewer",
            "index": "src/index.html",
            "main": "src/main.ts",
            "polyfills": "src/polyfills.ts",
            "tsConfig": "tsconfig.app.json",
            "aot": true,
            "assets": [
              "src/favicon.ico",
              "src/assets"
            ],
            "styles": [
              "src/styles.css",
              "./node_modules/viewerjs/dist/viewer.min.css"
            ],
            "scripts": [
              "./node_modules/viewerjs/dist/viewer.min.js"
            ]
          },
```

Modify the ```yourcomponent.component.html``` file; in this demo project it is```xcimageviewer/xcimageviewer.component.html```

Add #_keyword_ before the ```div``` to refenece it from the ```xcimageviewer/xcimageviewer.component.ts```

```html
<div class="docs-galley mb-3" style="width: 800px; height: 600px;">
    <div id="galley" #galley style="visibility: hidden">
      <ul class="pictures">
        <li><img data-original="../assets/images/tibet-1.jpg" src="../assets/images/thumbnails/tibet-1.jpg" alt="Cuo Na Lake"></li>
        <li><img data-original="../assets/images/tibet-2.jpg" src="../assets/images/thumbnails/tibet-2.jpg" alt="Tibetan Plateau"></li>
        <li><img data-original="../assets/images/tibet-3.jpg" src="../assets/images/thumbnails/tibet-3.jpg" alt="Jokhang Temple"></li>
      </ul>
    </div>
</div>
```

Modify the ```yourcomponent.component.ts``` file; in this demo it is project ```xcimageviewer/xcimageviewer.component.ts```
## Usage

 - Import ```AfterViewInit, ElementRef, ViewChild, OnDestroy```

 - Declare reference to ```Viewer```

 - Variable for component class to access ```viewer```
 
 - Implement ```ngAfterViewInit()``` Create viewer 

 - Implement ```ngOnDestroy()``` Destroy viewer

 
 ```ts
import { Component, OnInit, AfterViewInit, ElementRef, ViewChild, OnDestroy } from '@angular/core';

// Reference to JS Viewer
declare var Viewer: any;

@Component({
  selector: 'app-xcimageviewer',
  templateUrl: './xcimageviewer.component.html',
  styleUrls: ['./xcimageviewer.component.css']
})
export class XcimageviewerComponent implements OnInit, AfterViewInit, OnDestroy {
  // variable for viewer
  viewer: any;
  // DOM element reference
  @ViewChild('galley') galley: ElementRef;

  constructor() { }

  ngOnInit(): void {
  }

  ngAfterViewInit(){
    // console.log(this.galley.nativeElement.innerHTML);
    this.viewer = new Viewer(this.galley.nativeElement, {
      inline: true,
      url: 'data-original',
    });

    this.viewer.show();
  }

  ngOnDestroy() {
    this.viewer.destroy()
  }
}

```
