# vue-recurrence-editor-component

Simple Personal Library - MIT

## DEMO

<img src="https://github.com/RyanDaDeng/vue-scheduler-component/blob/master/demo_scheduler.gif"/>

## Installation

 This is not a NPM distribution file, so you just need to copy/paste the file into your project and treat it as a normal vue component.
 
 The default CSS class is using bootstrap.
 
 I will make it as a distribution package in the future with more advanced features.
 
## Usage

````vue
  <recurrence-editor v-model="yourModel" ></recurrence-editor>
 ````
## API

#### Every Week
````js
   {
      repeatOption: {
          type: 'every_week',
          everyWeekPicker: ['1', '2', '3', '4', '5', '6','7']
      },
      repeatAt: '10:00',
  }
````

#### Every Day
````js
   {
      repeatOption: {
          type: 'every_day'
      },
      repeatAt: '10:00',
  }
````


### License
MIT
