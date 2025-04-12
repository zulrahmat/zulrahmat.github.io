### .get()
Load data from the server using a HTTP GET request.
```js
$.get( "ajax/test.html", function( data ) {
  $( ".result" ).html( data );
  alert( "Load was performed." );
});
```
### .post()
 Send data to the server using a HTTP POST request.
 ```js
$.post( "ajax/test.html", function( data ) {
  $( ".result" ).html( data );
});
 ```
### .load()
Load data from the server and place the returned HTML into the matched elements.
```js
$( "#result" ).load( "ajax/test.html", function() {
  alert( "Load was performed." );
});
```
### .getJSON()
 Load JSON-encoded data from the server using a GET HTTP request.
```js
$.getJSON( "ajax/test.json", function( data ) {
  var items = [];
  $.each( data, function( key, val ) {
    items.push( "<li id='" + key + "'>" + val + "</li>" );
  });
 
  $( "<ul/>", {
    "class": "my-new-list",
    html: items.join( "" )
  }).appendTo( "body" );
});
```
### .getScript()
Load a JavaScript file from the server using a GET HTTP request, then execute it.
 ```js
 
$.getScript( "ajax/test.js", function( data, textStatus, jqxhr ) {
  console.log( data ); // Data returned
  console.log( textStatus ); // Success
  console.log( jqxhr.status ); // 200
  console.log( "Load was performed." );
});
 ```

