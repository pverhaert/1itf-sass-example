# 1ITF - SASS example

## Requirements

- Node.js
    - `npm install -g sass live-server`
- PhpStorm

## This example requires some knowledge of SCSS:

- Basic knowledge: variables, nesting, partials, mixins  
  (see course [ITF - Full Stack Essentials](https://itf-full-stack-essentials.netlify.app/))
- Advanced knowledge: maps, for loops, sass:color (color.scale)  
  (not covered in the course, but recommended to better understand how
  to [customize Bootstrap with SASS](https://github.com/twbs/bootstrap/) needed for the project)

## How to run this example

- Open a terminal window in PhpStorm and run the command `npm run sass` to compile the SCSS files to CSS.
- Open another terminal window in PhpStorm and run the command `npm run watch` to start a local server.

## Cheat Sheet

### Table of Contents

- [Variables](#variables)
- [Nesting](#nesting)
- [Partials](#partials)
- [Mixins](#mixins)
- [Maps](#maps)
- [For Loops](#for-loops)
- [sass:color (color.scale)](#sasscolor-colorscale)

### Variables

- Variables are defined using the `$` symbol.
- Variables can be used to store colors, font stacks, or any CSS value you think you'll want to reuse.

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

### Nesting

- Nesting is a way of nesting CSS selectors within one another.
- It allows for easier reading and better organization of your code.
- Use the `&` to **append** the parent selector to a nested selector.

```scss
$color: red;
$color-hover: orange;

nav {
  ul {
    list-style: none;

    li {
      display: inline-block;
    }
  }

  a {
    color: $color;
    text-decoration: none;

    &:hover {
      color: $color-hover;
    }
  }
}
```

### Partials

- Partials are used to modularize your code and make it more maintainable.
- A partial is simply a SCSS file named **with a leading underscore**.
- You might name it something like `_partial.scss`.
- You can import partials into other Sass files using the `@import("path/to/partial")` directive.
- Import **ONLY the name of the partial**, without the leading underscore or file extension.
    - good: `@import 'path/to/partial';`
    - bad: `@import 'path/to/_partial.scss';`

```scss
// _reset.scss
* {
  margin: 0;
  padding: 0;
}

// base.scss
@import 'reset';
body {
  font-family: Helvetica, sans-serif;
  background-color: #efefef;
}
```

### Mixins

- Mixins allow you to define styles that can be re-used throughout your stylesheet.
- They make it easy to avoid using the same code over and over again.
- You can pass in variables (with default values) to make your mixins more flexible.

```scss
@mixin button($color: #fff, $background-color: #2196F3) {
  background-color: $background-color;
  color: $color;
  padding: 10px 20px;
  border: 1px solid $color;
  border-radius: 5px;
  cursor: pointer;
}

.primary-button {
  @include button();
}

.secondary-button {
  @include button(#2196F3, #fff);
}
```

### Maps (advanced)

- Maps are a collection of key-value pairs.
- They can be used to store related data.
- You can access one value of a key in a map using the `map-get` function.
- You can also loop through a map using the `@each` directive.
  - use the `#{$}` interpolation syntax to get **the name** of the key.
  - use the `$` symbol to get **the value** of that key.
- Info: [Sass: Maps](https://sass-lang.com/documentation/values/maps/)
- 
```scss
$colors: (
        "primary": #333,
        "secondary": #666,
);

.primary {
  color: map-get($colors, "primary");
}

@each $name, $color in $colors {
  .#{$name} {
    color: $color;
  }
}
```

### For Loops (advanced but handy)

- For loops allow you to generate styles based on a range of values.
- You can use the `@for` directive to loop through a range of values.
  - use the `#{$x}` interpolation syntax to generate class names dynamically.
- You can also perform arithmetic operations within the loop.
- Info: [Sass: for loop](https://sass-lang.com/documentation/at-rules/control/for/)

```scss
@for $i from 1 through 12 {
  .p-#{$i} {
    padding: $i * .25rem;
  }
}
```

### sass:color (color.scale) (advanced)

- `sass:color` is one of the built-in modules in Sass.
- The `sass:color` function provides a set of color manipulation functions.
- You can use the `scale-color` function to adjust the lightness of a color.
    - a **positive** value for `$lightness` will make the color **lighter**.
    - a **negative** value for `$lightness` will make the color **darker**.
- Info: [sass:color](https://sass-lang.com/documentation/modules/color)

```scss
@use 'sass:color';

$red: #900;

a {
  color: $red;

  &:hover {
    color: scale-color($red, $lightness: 20%);
  }
}
```