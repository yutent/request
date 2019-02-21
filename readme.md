# Request.next
Promise based HTTP client for the modern browser(IE10+, chrome 40+, ff 38+, safari 10+).


## Features
- Make `XMLHttpRequests` from the browser 
- Use `fetch` when posible.
- Supports the `Promise` API
- Transform request and response data
- Cancel requests
- Supports RESFUL API


## Browser Support

![Chrome](https://raw.github.com/alrra/browser-logos/master/src/chrome/chrome_48x48.png) | ![Firefox](https://raw.github.com/alrra/browser-logos/master/src/firefox/firefox_48x48.png) | ![Safari](https://raw.github.com/alrra/browser-logos/master/src/safari/safari_48x48.png) | ![Opera](https://raw.github.com/alrra/browser-logos/master/src/opera/opera_48x48.png) | ![Edge](https://raw.github.com/alrra/browser-logos/master/src/edge/edge_48x48.png) | ![IE](https://raw.github.com/alrra/browser-logos/master/src/archive/internet-explorer_9-11/internet-explorer_9-11_48x48.png) |
--- | --- | --- | --- | --- | --- |
Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | Latest ✔ | 10 ✔ |



## Installion

Using npm:
```bash
npm i request.next
```

Download File:
```html
<script src="path of the request.js"></script>
```


## Example

```html
<script src="path of the request.js"></script>
<script>
  request.get('/article?id=123')
    .then(res  => {
      // {
      //   stutus: Number,
      //   statusText: String,
      //   error: Error || NULL,
      //   text: Any,
      //   body: Any
      // }
      console.log(res)
    })
    .catch(err  => {
      console.log(err)
    })

  // or like this
  request.get('/article', {
    data: { id: 123 }
  })
  .then(res  => {
    console.log(res)
  })
  .catch(err  => {
    console.log(err)
  })


  // POST request
  request.post('/article/save', {
    data: { id: 123, title: 'hello', content: 'hello world!' }
  })
  .then(res  => {
    console.log(res)
  })
  .catch(err  => {
    console.log(err)
  })
</script>

```



## APIs

### request.init(param`<Object>`)
> Preset common params for all requests. like auth_token?

```js
request.init({ 
  headers: { token: 'hello' }, 
  datatype: 'json' 
})
```

### request.get(url`<String>`[, param`<Object>`])
> Quick way to launch a GET request.


### request.post(url`<String>`[, param`<Object>`])
> Quick way to launch a POST request.

### request.download(url`<String>`[, param`<Object>`])
> Quick way to launch a GET request and parse the response to a `Blob`.

### request.upload(url`<String>`, param`<Object>`)
> Quick way to launch a POST request, to Send attaches to server.


```js
request.upload('/upload', { 
  data: {
    image: File // fetch form <input type="file">
  }
})
```


### request.open(url`<String>`[, method`<String>`, param`<Object>`])
> Launch a request by self config.
>> - url`<String>`.  
>> - method`<String>`.
>> - param`<Object>`.
>>>  + headers: `<Object>`. 
>>>  + data: `<Object>|<String>|<Number>|<DOM FORM>|<FormData>`.
>>>  + dataType: `<Object>`. Tell what type response should be parsed
>>>  + formType: `<String>`.   form`(default)` | form-data | json | text
>>>  + cache: `<Bollean>`. default `true`
>>>  + withCredentials: `<Bollean>`.  default `false`
>>>  + timeout: `<Number>`. default `0`

```js
request.open('/article', 'GET', { 
  data: {
    id: 1234
  }
})

// same with above
request.open('/article', { 
  data: {
    id: 1234
  }
})
```

 All request config
```js
request.open(
  url,  // The server URL that will be used for the request
  method,  // The request method to be used when making the request
  // all params
  { 
    // custom headers to be sent
    headers: { foo: 'bar' },   

    // custom data to be sent.
    // it can be an object, a tring, a number, a DOM<form>, or a FormData object.
    // eg.
    // { id: 123 }
    // document.querySelector('form')
    data: '', 

    // Tell what type response should be parsed
    // can be  one of these.
    // arraybuffer, blob, document, json, text(default)
    dataType: 'text',


    // request content-type
    // can be one  of these
    // json, text, form-data,  form(default)
    formType: 'form',


    // allow caching?
    // default true
    cache: false,


    // supportCors?
    // if set to true, the server api must response sone headers like these
    // Access-Control-Allow-Credentials
    // Access-Control-Allow-Origin
    // Access-Control-Allow-Headers
    withCredentials: false,


    // timeout
    timeout: 0
  }
)
```


### instance method api

```js
let req  = request.get('/xxxx')

req.abort() // cancel request

req.then(res => {
  // console.log(res)
}).catch(err => {
  console.log(err)
})

```