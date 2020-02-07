# vue-scheduler-component

Simple Personal Library - MIT

## DEMO

### Every Day
<img src="https://github.com/RyanDaDeng/vue-scheduler-component/blob/master/31581052959_.pic.jpg" width="280" height="350" />

### Every Week
<img src="https://github.com/RyanDaDeng/vue-scheduler-component/blob/master/21581052950_.pic.jpg" width="280" height="350" />

## Installation

 This is not NPM distribution file, so you just need to copy/paste the file into your project and treat it as a normal vue component.
 The default CSS class is using bootstrap.
 
## Usage

````vue
  <scheduler-setting v-model="schedulerSetting" ></scheduler-setting>
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
