[//]: #@corifeus-header

  [![Build Status](https://travis-ci.org/patrikx3/angular-compile.svg?branch=master)](https://travis-ci.org/patrikx3/angular-compile)  [![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/patrikx3/angular-compile/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/angular-compile/?branch=master)  [![Code Coverage](https://scrutinizer-ci.com/g/patrikx3/angular-compile/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/patrikx3/angular-compile/?branch=master) 

  
[![NPM](https://nodei.co/npm/p3x-angular-compile.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/p3x-angular-compile/)
---

 
# Angular Dynamic Compile service and directive

## Issues / Support
This is an open source project. Time is a precious thing, so I have rarely time to give support and fix issues for someone else. I fix a bug, when I have an error that I need. If you got an issue, error or bug, I hope someone will have time to do it for you, otherwise, you are on your own.

Though, if I know the solution, I will tell you. Besides, core errors will be fixed by me.

***If you want to extend, fix bugs or add in new features, I promptly merge pull requests or you can become a ```patrikx3``` member.***

### Node Version Requirement 
``` 
>=7.8.0 
```  
   
### Built on Node 
``` 
v7.10.0
```   
   
The ```async``` and ```await``` keywords are required.

Install NodeJs:    
https://nodejs.org/en/download/package-manager/    
  
# Description  

                        
[//]: #@corifeus-header:end

# Use case
Dynamic compile components by a string template for Angular. You can provide a context, that you can use with anything (for clicking for free etc..) 

**The old ```angular-compile-html```.**

## NPM & Version
It is a ```CommonJS``` bundle.
The version reflects the Angular version (```AngularMajor.AngularMinor.Build-Commit```).

## Install
  
```bash
npm install --save p3x-angular-compile
# or
yarn add p3x-angular-compile
```

## AOT + JIT
It is not working out of the box (the default is either JIT or AOT, not both), but the apps become 10 folds faster. The ``@ngtools/webpack`` is AOT and the ```awesome-typescript-loader``` is JIT only. 
  
The solution can be architect with the ```@angular/compiler``` and the ```awesome-typescript-loader``` together. A miracle!

Example here:
[More info about AOT + JIT](https://pages.corifeus.tk/github/corifeus-builder-angular/artifacts/readme/skeleton.html)

### Size
If you want very small bundle, use ```gzip```.

## Usage

```typescript
// the module settings
@NgModule({
    imports: [
        CompileModule.forRoot({
            module: {
                schemas: [CUSTOM_ELEMENTS_SCHEMA],
                declarations: [MyDynamicElement ]
            }
        })
    ],
    declarations: [
        Page,
    ],
    providers: [
    ],
    bootstrap: [ Page ]
})
export class Module { };
```
  
```html
 <div *ngIf="true" [p3x-compile]="data" [p3x-compile-ctx]="this"></div>
```

```typescript
// a page example
export class Page {

    data: string = "<div (click)="context.alert()">It is working</div>";

    alert() {
        alert('ok');
    }
}
```

#### Actual used dynamic compiler
I use a dynamic Markdown page with ```p3x-angular-compile```:
[Module](https://github.com/patrikx3/corifeus-app-web-pages/blob/master/src/angular/module.ts) , [Example page](https://github.com/patrikx3/corifeus-app-web-pages/blob/master/src/angular/modules/cory-page.ts)

#### Service
[Please refer to use an a service](https://github.com/patrikx3/angular-compile/blob/master/test/angular-webpack/angular/page.ts)

### Options
[Reference for the Angular module settings.](
https://github.com/angular/angular/blob/master/packages/core/src/metadata/ng_module.ts)

The templates are cached.
```typescript
export interface CompileOptions {   
    // cached by template
    template: string;
    container: ViewContainerRef;
    context?: any,
    
    // you can customize here any you want to
    // CommonModule, BrowserModule are auto added 
    // (like *ngIf and angular default directives)
    // though CompileModule.forRoot is usually enough
    // so you do not need to use it
    module?: NgModule;
    
    onCompiled?: Function,
    onError?: Function;

}
```


### Deployed example
[Corifeus Pages (JIT + AOT at once)](https://pages.corifeus.tk)
  
[https://github.com/patrikx3/corifeus-app-web-pages/blob/master/src/angular/modules/cory-page.ts](https://github.com/patrikx3/corifeus-app-web-pages/blob/master/src/angular/modules/cory-page.ts)

## Dev environment end test
   
```bash
npm install -g yarn
git clone https://github.com/patrikx3/angular-compile.git
cd angular-compile
yarn install
grunt run|default
```

[http://localhost:8080](http://localhost:8080)




[//]: #@corifeus-footer

---
[**P3X-ANGULAR-COMPILE**](https://pages.corifeus.tk/angular-compile) Build v4.1.441-62

[Corifeus](http://www.corifeus.tk) by [Patrik Laszlo](http://patrikx3.tk)


[//]: #@corifeus-footer:end
