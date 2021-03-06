# Ngx Material DatetimePicker, Timepicker for @angular/material 7.x, 8.x

[![Build Status](https://travis-ci.com/h2qutc/ngx-mat-datetime-picker.svg?branch=master)](https://travis-ci.com/h2qutc/ngx-mat-datetime-picker)
[![codecov](https://codecov.io/gh/h2qutc/ngx-mat-datetime-picker/branch/master/graph/badge.svg)](https://codecov.io/gh/h2qutc/ngx-mat-datetime-picker)
[![License](https://img.shields.io/npm/l/ngx-mat-datetime-picker.svg)](https://www.npmjs.com/package/ngx-mat-datetime-picker)
[![npm version](https://badge.fury.io/js/ngx-mat-datetime-picker.svg)](https://badge.fury.io/for/js/ngx-mat-datetime-picker)

## Description

A DatetimePicker like @angular/material [Datepicker](https://material.angular.io/components/datepicker/overview) by adding support for choosing time.

## DEMO
@see [Demo here](https://stackblitz.com/edit/demo-ngx-mat-datetime-picker)

![Alt Text](demo.png)

## Getting started
```
npm install --save ngx-mat-datetime-picker
```

## Setup
Basically the same way the @angular/material Datepicker is configured and imported.

```
import { NgxMatDatetimePickerModule, NgxMatTimepickerModule } from 'ngx-mat-datetime-picker';
@NgModule({
   ...
   imports: [
      BrowserModule,
      HttpClientModule,
      BrowserAnimationsModule,
      MatDatepickerModule,
      MatInputModule,
      NgxMatTimepickerModule,
      FormsModule,
      ReactiveFormsModule,
      MatButtonModule,
      NgxMatDatetimePickerModule,
   ],
   ...
})
export class AppModule { }
```
@see [src/app/app.module.ts](src/app/app.module.ts)

## Using the component

The same API as @angular/material Datepicker (@see [API docs](https://material.angular.io/components/datepicker/api))

Datetime picker using FormControl

```
<mat-form-field>
    <input matInput [ngxMatDatetimePicker]="picker" placeholder="Choose a date" [formControl]="dateControl">
    <mat-datepicker-toggle matSuffix [for]="picker"></mat-datepicker-toggle>
    <ngx-mat-datetime-picker #picker></ngx-mat-datetime-picker>
</mat-form-field>
```

Timepicker

```
<ngx-mat-timepicker [(ngModel)]="date"></ngx-mat-timepicker>
<ngx-mat-timepicker [(ngModel)]="date" [disabled]="disabled"></ngx-mat-timepicker>
<ngx-mat-timepicker [(ngModel)]="date" [stepHour]="2" [stepMinute]="5" [stepSecond]="10"></ngx-mat-timepicker>
<ngx-mat-timepicker [(ngModel)]="date" [showSpinners]="showSpinners"></ngx-mat-timepicker>
<ngx-mat-timepicker [(ngModel)]="date" [disableSecond]="disableSecond"></ngx-mat-timepicker>
<ngx-mat-timepicker [formControl]="formControl"></ngx-mat-timepicker>
```

## Choosing a date implementation and date format settings

The datepicker was built to be date implementation agnostic. This means that it can be made to work with a variety of different date implementations. However it also means that developers need to make sure to provide the appropriate pieces for the datepicker to work with their chosen implementation.

The easiest way to ensure this is to import one of the provided date modules:

* **NgxMatNativeDateModule**
   **Date type**:	Date
   **Supported locales**:	en-US
   **Dependencies**:	None
   **Import from**:	ngx-mat-datetime-picker

* **NgxMatMomentModule**
   **Date type**:	Moment
   **Dependencies**:	Moment.js
   **Import** from**:	[ngx-mat-moment-adapter](https://www.npmjs.com/package/ngx-mat-moment-adapter)

   ```
   npm install --save ngx-mat-moment-adapter
   ```

Please note: NgxMatNativeDateModule is based off the functionality available in JavaScript's native Date object. Thus it is not suitable for many locales. One of the biggest shortcomings of the native Date object is the inability to set the parse format.

We highly recommend using the **NgxMatMomentModule** or a custom **NgxMatDateAdapter** that works with the formatting/parsing library of your choice.

For example:

Creating a custom date adapter:

```
@Injectable()
export class CustomDateAdapter extends NgxMatDateAdapter<D> {...}
// D can be Date, Moment or customized type
```

Creating a custom date adapter module
```
@NgModule({
  providers: [
    {
      provide: NgxMatDateAdapter,
      useClass: CustomDateAdapter,
      deps: [MAT_DATE_LOCALE, MAT_MOMENT_DATE_ADAPTER_OPTIONS]
    }
  ],
})
export class CustomDateModule { }
```


## Theming
- @see @angular/material [Using a pre-built theme](https://material.angular.io/guide/theming#using-a-pre-built-theme)
- Add the Material Design icon font to your index.html
```
<link href="https://fonts.googleapis.com/icon?family=Material+Icons&display=block" rel="stylesheet">
```

## License
MIT