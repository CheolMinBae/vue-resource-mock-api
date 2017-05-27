# vue-resource-mock

[![Coverage Status](https://coveralls.io/repos/github/giovanniorigins/vue-resource-mock-api/badge.svg?branch=dev)](https://coveralls.io/github/giovanniorigins/vue-resource-mock-api?branch=dev)

[![npm](https://img.shields.io/npm/v/vue-resource-mock-api.svg)](https://www.npmjs.com/package/vue-resource-mock-api)
[![vue-resource](https://img.shields.io/badge/vue--resource-0.9.x-brightgreen.svg)](https://github.com/pagekit/vue-resource)
[![vue2](https://img.shields.io/badge/vue-1.x-brightgreen.svg)](https://v1.vuejs.org/)
[![vue2](https://img.shields.io/badge/vue-2.x-brightgreen.svg)](https://vuejs.org/)

The plugin for Vue.js provides a mock middleware for vue-resource during unit-testing. This interceptor allows you to make mock API calls within your components.

## Installation

### NPM
```
$ npm install vue-resource-mock-api --save-dev
```

## Example
```
// ./index.js
// Import vue-resource
import VueResource from 'vue-resource';
Vue.use(VueResource);

// import vue-resource-mock-api
import VueResourceMock from 'vue-resource-mock-api'

// import mock API to be used by interceptor
import MockData from './mock-api'
Vue.use(VueResourceMock, MockData);
```
You can also change the <a href="https://github.com/snd/url-pattern#customize-the-pattern-syntax">url-pattern syntax</a> by passing a nested object with the `matchOptions` property

```
Vue.use(VueResourceMock, {
  routes: MockData,
  matchOptions: {
    segmentValueCharset: 'a-zA-Z0-9.-_%' // default
  }
});
```


```
// ./mock-api.js
export default {

    // Get api token
    ['POST *login'] (pathMatch, query, request) {
        // before respond, you can check the path and query parameters with `pathMatch` & `query`
        // powered by 'url-pattern' & 'qs'
        // https://www.npmjs.com/package/url-pattern
        // https://www.npmjs.com/package/qs
        let body = {
            api_token: 'test'
        };
        return {
            body: body,
            status: 200,
            statusText: 'OK',
            headers: { /*headers*/ },
            delay: 1500, // millisecond
        }
    },
    
    // Get list of cars
    ['POST *cars/:car'] (pathMatch, query, request) {
        let body = {
            data: [
            	{
            		Manufacturer: 'BMW',
            		Model: 'M3',
            		color: 'blue
            	},
            ]
        };
        return {
            body: body,
            status: 200,
            statusText: 'OK',
            headers: { /*headers*/ },
            delay: 500, // millisecond
        }
    },
    
      // shorthand mock
      ['PUT */path/to/resource'] = 200 // respond with only status code
    
      ['POST */path/to/resource'] = { /*whatever*/ } // respond with only body, status code = 200

}
```



## :book: Documentation
See [here](http://giovanniorigins.github.io/vue-resource-mock/)

## :scroll: Changelog
Details changes for each release are documented in the [CHANGELOG.md](https://github.com/giovanniorigins/vue-resource-mock-api/blob/dev/CHANGELOG.md).


## :exclamation: Issues
Please make sure to read the [Issue Reporting Checklist](https://github.com/giovanniorigins/vue-resource-mock-api/blob/dev/CONTRIBUTING.md#issue-reporting-guidelines) before opening an issue. Issues not conforming to the guidelines may be closed immediately.


## :muscle: Contribution
Please make sure to read the [Contributing Guide](https://github.com/giovanniorigins/vue-resource-mock-api/blob/dev/CONTRIBUTING.md) before making a pull request.

## :copyright: License

[MIT](http://opensource.org/licenses/MIT)
