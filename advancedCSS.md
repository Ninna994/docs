# Advanced CSS CheatSheet

## by Ninna

### Table of Contents

- [Advanced CSS CheatSheet](#advanced-css-cheatsheet)
  - [by Ninna](#by-ninna)
    - [Table of Contents](#table-of-contents)
    - [Sass Features](#sass-features)
    - [Sass Syntax](#sass-syntax)
    - [Sass Functionality](#sass-functionality)
    - [Variables](#variables)
    - [Mixins](#mixins)
    - [Nesting](#nesting)
    - [Extends](#extends)
    - [Functions](#functions)

### Sass Features

1. **Variables**
   * _reusable values_ --> colors, font-sizes, spacing
2. **Nesting**
   * for _nesting selectors_ inside one another for less code
3. **Operators**
   * for _mathematical operations_ inside CSS
4. **Partials and imports**
   * to write CSS in _different files_ and import them all into one single file
5. **Mixins**
   * for writing _reusable pieces_ of CSS code
6. **Functions**
   * similar to Mixins, but its value _can be used later_
7. **Extends**
   * to make different selectors _inherit declarations_ that are common to all of them
8. **Control directives**
   * to write complex code using _conditionals_ and _loops_

### Sass Syntax

1. Sass syntax

   ```sass
   .navigation
     list-style: none
     float: left
     & li
       display: inline-block
       margin-left: 30px
   ```

2. SCSS Syntax

   ```scss
   .navigation {
     list-style: none;
     float: left;
     & li {
       display: inline-block;
       margin-left: 30px;
     }
   }
   ```

### Sass Functionality

1. **Comments**
   * `//` inline comments

### Variables

1. **Declaration** `$name: value;`

### Mixins

1. **Mixin declaration**

   ```scss
   @mixin ime(argument) {
     /* code */
   }
   ```

2. **Mixin call**

   ```scss
   @include ime(argument);
   ```

### Nesting

1. Inside one class declaration we can put nested classes, just **indent** them.
2. When we need deeper nesting we can put the **&** sign which represents all the _path_ to that element.

### Extends

When we have the same principles in multiple selectors:

1. **Declaring it**

   ```scss
   %ime {
     /* code */
   }
   ```

2. **Calling it**

   ```scss
   @extend %ime;
   ```

### Functions

1. **Declaring functions**

   ```scss
   @function ime(arg1, arg2) {
     @return /* value */;
   }
   ```

2. **Function call**

   ```scss
   ime(arg1, arg2) * 1 unit;
   ```

3. **Color functions**
   * `darken(color, percentage);`
   * `lighten(color, percentage);`
