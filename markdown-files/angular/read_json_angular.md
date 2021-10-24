# How To Read Local JSON Files In Angular

Learn how to read local json files

We can import or read local JSON files in Angular,several different ways depending upon the Angular version we are using.

In this post I am listing out different methods with examples on how to read JSON files in Angular.

## Reading local JSON files in Angular 7 and Angular 6.1

Angular framework supports TypeScript 2.9 from 6.1 version onwards.In typescript 2.9 with the help of resolveJsonModule we can import local JSON files just like modules

I have added a sample JSON file in assets folder of Angular App. Have a look at the sample json example

```js
{
"Post": "Angular Json Files",
"CanEdit": true,
"Version": 7
}
```

I have imported sampleJson.json in our ReadingJsonFilesComponent as shown below

```js
import { Component, OnInit } from '@angular/core';
import SampleJson from '../../assets/SampleJson.json';

@Component({
  selector: 'app-reading-json-files',
  templateUrl: './reading-json-files.component.html',
  styleUrls: ['./reading-json-files.component.css']
})

export class ReadingJsonFilesComponent implements OnInit {

constructor() {
 console.log('Reading local json files');
 console.log(SampleJson);
}

ngOnInit() {}

}
```

Now If you build the application you will get the following error

ERROR in src/app/reading-json-files/reading-json-files.component.ts(2,24): error TS2732: Cannot find module ‘../../assets/SampleJson.json’. Consider using ‘–resolveJsonModule’ to import module with ‘.json’ extension

To remove the above error,In tsconfig.json file under compiler options we need to add “resolveJsonModule” and ”esModuleInterop” configurations as true as shown below.

```js
{  "compilerOptions": {  "resolveJsonModule": true, "esModuleInterop": true } }
```

One more thing you need to understand is the the imported JSON file contents are typesafe. In the above json version is a number. So if you tried to change the version to string it will throw error.

```js
SampleJson.Version= "Seven"; //throws error as Version is of type number
```

## Reading local JSON files in Angular 5 or Angular 4

In earlier versions of Angular like Angular 5 or Angular 4 to read local json files, we need to use HttpClient from ‘@angular/common/http’ and Observable from ‘rxjs/Observable’ as shows below.

We need to inject HttpClient in constructor.

```js
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Component({
 selector: 'app-reading',
 templateUrl: './reading.component.html',
 styleUrls: ['./reading.component.css']
})

export class ReadingComponent implements OnInit {
 private _jsonURL = 'assets/SampleJson.json';
 constructor(private http: HttpClient) {
   this.getJSON().subscribe(data => {
    console.log(data);
   });
 }
 public getJSON(): Observable<any> {
   return this.http.get(this._jsonURL);
 }
 ngOnInit() {
 }
}
```

HttpClient is introduced in Angular 4.3, If you are using Angular version 4.3 below use the below method to read the JSON files

## Reading local JSON files in Angular 2+ versions

We need to use Http from “@angular/http” to import JSON files in Angular version 4.3 below and Angular 2 +.

```js
import { Component, Input } from '@angular/core';
import { Injectable } from '@angular/core';
import { Http, Response, Headers, RequestOptions } from '@angular/http';
import {Observable} from 'rxjs/Rx';
import 'rxjs/add/operator/map';
import 'rxjs/add/operator/catch';

@Injectable()
export class ReadingJsonService{

private _jsonURL = 'assets/SampleJson.json';

constructor(private http: Http) {
 var object;
 this.getJSON().subscribe(data => object=data, error => console.log(error));
}

public getJSON(): Observable<any> {
  return this.http.get(_jsonURL)
   .map((response:any) => response.json())
   .catch((error:any) => console.log(error));

}
}
```

## Reading local JSON files in Offline Angular Applications

Angular Http will not work if the application goes offline. In that case we have an alternate way of importing JSON files We need to add a new file json-typings.d.ts in app folder along with index.html file

```js
declare module "*.json" {
  const value: any;
  export default value;
}
```

And then we can import JSON files just like latest versions of Angular

`import * as SampleJson from "../../assets/SampleJson.json";`
