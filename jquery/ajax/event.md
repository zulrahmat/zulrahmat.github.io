- [ajaxStart](#ajaxstart)
- [ajaxSend](#ajaxsend)
- [ajaxSuccess](#ajaxsuccess)
- [ajaxComplete](#ajaxcomplete)
- [ajaxError](#ajaxerror)
- [ajaxStop](#ajaxstop)


### ajaxStart
Register a handler to be called when the first Ajax request begins
```js
$( document ).on( "ajaxStart", function() {
  $( ".log" ).text( "Triggered ajaxStart handler." );
} );
```
---
### ajaxSend
Attach a function to be executed before an Ajax request is sent. 
```js
$( document ).on( "ajaxSend", function() {
  $( ".log" ).text( "Triggered ajaxSend handler." );
} );
```
---
### ajaxSuccess
 Attach a function to be executed whenever an Ajax request completes successfully.
```js
$( document ).on( "ajaxSuccess", function() {
  $( ".log" ).text( "Triggered ajaxSuccess handler." );
} );
```
---
### ajaxComplete
Register a handler to be called when all Ajax requests have completed.
```js
$( document ).on( "ajaxComplete", function() {
  $( ".log" ).text( "Triggered ajaxComplete handler." );
} );
```
---
### ajaxError
Register a handler to be called when Ajax requests complete with an error
```js
$( document ).on( "ajaxError", function() {
  $( ".log" ).text( "Triggered ajaxError handler." );
} );
```
---
### ajaxStop
Register a handler to be called when all Ajax requests have completed.
```js
$( document ).on( "ajaxStop", function() {
  $( ".log" ).text( "Triggered ajaxStop handler." );
} );
```

