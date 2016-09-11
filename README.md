# Sass Theme manager
This tiny sass helper offers a convenient way to manage your styleguide and themes using sass maps.

##Usage
Themes can be set per component basis, and globally for styleguide theme management.

###Locally
```scss
.my-component {
  @include theme((
    header: (
      color: #000
    )
  ));
  &.header {
    color: theme(header, color);
  }
}
```

###Globally
```scss
@include theme((
  headings: (
    h1: 2em,
    h2: 1.8em
  ),
  font-family: 'Roboto'
));

html, body {
  font-family: theme("global", font-family);
}

.my-component h1 {
  font-size: theme("global", headings, h1)
}
```

##Set theme styles
To set a theme for a component, include `theme` mixin inside the component root. The component theme name is binded from the parent selector. Nested styles are supported.

```scss
my-component {
  @include theme($sassMap)
}
```

##Get theme styles

To get a style from the theme use the `theme` function. The theme name is implicitly binded from the scope, or explicitly set as a first parameter. Nested styles are supported.


```scss
my-component {
  @include theme((
    padding: 15px,
    general: (
      bg: #fff
    ),
    header: (
      color: blue,
      background-color: #fff,
      line-height: 1
    ),
    footer: (
      large-text: 16px
    )
  ));

  // current theme scope: "my-component".
  padding: theme(padding); //implicit from "my-component".
  // interpolates nested styles
  background-color: theme(general, bg);
  // explicitly set the theme name to get the styles from.
  background-color: theme("my-component", general, bg);

  .header {
    // current theme scope: "my-component".
    line-height: theme(header, line-height); //implicit from "my-component".
  }

  @at-root #{&}--footer {
    //current theme scope "". (since @at-root is used)
    font-size: theme("ys-card", footer, large-text); //must use explicit theme binding.
  }
}
```

##Global themes
To set global themes, include `theme` mixin in the global scope.

```scss
@include theme((themeMap))

h1 {
  font-size: theme("global", h1, font-size);
}
```