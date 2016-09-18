#Todo:
- add default attribute.
- setup the default flag.
- unit testing




/* draft list */


#Theme Manager vs normal variables

Theme manager, powered by sass maps, provides awesome features you can use to better structure your css!

* variables lack structure.
* variable names are too verbose, long and hard to remember.
* variables are not descriptive enough.
* centralizing component theme makes it easier to use and 


@include theme("colors", (
  primary: white,
  secondary: red
));
@include theme("color-variations", (
  dark: 
))

color(primary, dark)


$theme-setup: (
  variations: "-variation"
)

@include theme-setup($theme-setup)



-variation

theme("colors", primary, dark)

```scss
$color__primary--xxdark: #302844;
$color__primary--xdark: #342C52;
$color__primary--dark: #322161;
$color__primary--darkmid: #3B2772;
$color__primary--lightmid: #462E85;
$color__primary--light: #65519A;

// Neutral tones - greys
$color__neutral--xxdark: #52595E;
$color__neutral--xdark: #58646E;
$color__neutral--dark: #8C9296;
$color__neutral--darkmid: #D1D5D9;
$color__neutral--mid: #C9CED5;
$color__neutral--lightmid: #D8DDE2;
$color__neutral--light: #E5E7EA;
$color__neutral--xlight: #EFF1F2;
$color__neutral--xxlight: #F7F8F8;
```


##Loops
$typography: (
  headings: (
    sizes: (
      h1:                2.5rem,
      h2:                2rem,
      h3:                1.75rem,
      h4:                1.5rem,
      h5:                1.25rem,
      h6:                1rem
    ),
    margin-bottom:       (1rem / 2),
    font-family:         inherit,
    font-weight:         500,
    line-height:         1.1,
    color:               inherit
  )
)
@include theme((typography: $typography))
 
@each $heading, $size in theme("global", typography, headings, sizes)  {
  #{heading} .#{heading} {
    font-family: theme("global", typography, headings, font-family);
    font-size: $size;
    margin-bottom: theme("global", typography, headings, margin-bottom);
 }
}



















@function list-slice($list, $start, $end: length($list)) {
  @if $start > length($list) {
    @return ();
  }
  $new-list: ();
  @for $i from $start through $end {
     $new-list: append($new-list, nth($list, $i), list-separator($list));
  }
  @return $new-list;
}
@function nested-map-get($map, $keys...) {
  @return if(length($keys) == 1,
             map-get($map, nth($keys, 1)),
             nested-map-get(map-get($map, nth($keys, 1)), list-slice($keys, 2)...));
}

$example-map: (
  foo: (
    baz: (
      qux: (
        quux: (
          garply: (
            waldo: "Hello world"
          )
        )
      )
    ) 
  ) 
);
.result {
  deep-access: nested-map-get($example-map, foo, baz, qux, quux, garply, waldo);
}