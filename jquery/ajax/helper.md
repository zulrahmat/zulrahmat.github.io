### .param()
Create a serialized representation of an array, a plain object, or a jQuery object suitable for use in a URL query string or Ajax request. In case a jQuery object is passed, it should contain input elements with name/value properties.
```js
var params = { width:1680, height:1050 };
var str = jQuery.param( params );
$( "#results" ).text( str );

// ouput: width=1680&height=1050
```

### .serialize()

Encode a set of form elements as a string for submission.
```js
$( "form" ).on( "submit", function( event ) {
  event.preventDefault();
  console.log( $( this ).serialize() );
});
```

### .serializeArray()
Encode a set of form elements as an array of names and values.
```js
$( "form" ).on( "submit", function( event ) {
  console.log( $( this ).serializeArray() );
  event.preventDefault();
} );
```