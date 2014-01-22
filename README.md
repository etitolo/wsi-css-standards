# Williams-Sonoma CSS/SASS Style Guide 

Welcome to the Williams-Sonoma CSS Styleguide. Before reading this, you should have a general understanding of [specificity](http://css-tricks.com/specifics-on-css-specificity/), [SASS syntax](http://sass-lang.com/docs/yardoc/file.INDENTED_SYNTAX.html), and [OOCSS Code Standards](https://github.com/stubbornella/oocss-code-standards).

##Coding Style

* Use soft-tabs with a four space indent.
* Put spaces after ```:``` in property declarations.
* When declaring HEX values, use uppercase and shorthand (where possible).  Use RGB and RGBA where necessary.
* Use ```//``` for comment blocks (instead of /* */).

```
// This is a good example!
.styleguide-mediablock 
    border: 1px solid #0F0
    color: #000
    background: rgba(0,0,0,0.5)

 /* This is a bad example */
 .styleguide-mediablock
    border:1px solid #0F0
    color:000
```

* All font sizes must be specified using pixels. Do not use percentages, ems, or rems. We are looking into using rems with a px fall back. For now please stick to px.
* Do not use units with zero values
* Do not use units on line-height 
```
// Good
.cell-display
    font-size: 11px
    margin: 0
    line-height: 1.2

// Bad
.cell-display
    font-size: 1.1em
    margin: 0px
    line-height: 12px
```

### Classes and IDs

* Class names should use dashes for styling purposes. 

* When you are using selectors for JavaScript interaction, use camelCase. *Do not* style against these selectors.

* Do not write IDs in your markup for styling purposes. This leads to overspecificity that is not welcome in our code.

* Try not to use 2 or more IDs in your definitions. You will see this in lots of places in our code and this is unfortunate. It has created serious specificity issues that will cause you headaches. Please do not follow this multiple ID selector pattern. Instead, try to take this opportunity to refactor this old code and think about ways you can avoid using IDs.

* Do not use !important at any time. That being said, there are a few exceptions to this, however none of the exceptions can be used without consulting your FED team members. Do not even think about using the xpath to resolve a specificity issue. That would be bad.

```
// Good
.registry-aside .cell-display .cell-media
    width: 300px
    float: right

// Bad
#registry-aside #cell_display #cellMedia
    width: 300px !important
```

Use semantic naming conventions. This means selectors should derive their meaning from context, not presentation or style. 

```
// Good
.registry-vanity-header
    color: #9329D1

//Bad (never use color in your selector names)
.purple-vanity-header
    color: #9329D1
```

Do not over-qualify class name selectors with an element type unless you are specifying exceptions to the default styling of a particular class.

```
// Good
.cell-display
    width: 20px

// Bad
div#cell-display
    width: 20px
```
### Clearfix

Please try using ```overflow: hidden``` as your first option for a clearfix. Otherwise, try a [micro clearfix](http://nicolasgallagher.com/micro-clearfix-hack/).

```
.clearfix-micro:before,
.clearfix-micro:after 
    content: " "
    display: table

.clearfix-micro:after
    clear: both
}

//For IE7 only
.ie7 .clearfix-micro
    zoom: 1
```


###common styles:
please be sure to look in general/_common.sass before building a separate css definition. The examples below are some common definitions in _common.sass

```
.offscreen 
.hide, .hidden  
.invisible 
.alert, .error
```

### Vendor-Prefixed Properties

When using vendor-prefixed properties, always use the standard property as well. The standard property must always come after all of the vendor-prefixed versions of the same property.

```css
.header
    -moz-border-radius: 4px
    -webkit-border-radius: 4px
    border-radius: 4px
```

Vendor-prefixed classes should align to the left with all other properties.

```css
/* Good */
-webkit-border-radius: 4px
-moz-border-radius: 4px
border-radius: 4px

/* Bad - colons aligned */
-webkit-border-radius:4px
   -moz-border-radius:4px
        border-radius:4px
```


###SASS Style

If any ```$variable``` is *used in multiple file*, it should be put in base/_vars.sass. Others should be put at the top of the file where they're used.

If a ```@mixin``` is being *used in more than only file* it should be placed either in the context that it's being used (only used in checkout). If the ```@mixin``` is useful site wide, please put it base/_functions.sass. 

As a rule of thumb, *don't nest further than 3 levels deep*. If you find yourself going further, think about every selector and the specificity that has been added to each rule. Your goal is to eliminate as much specificity as possible before moving forward. 

Spaces. While indentation, property, and definition spacing is controlled by the Sass compiler, property declarations are not. Please put a space after commas. Example:

```
Good:
.calendar-header
    font-family: comic-sans, Arial, Helvitica, Verdana

Bad:
.comic-sans-rocks
    font-family: comic-sans,Arial,Helvitica,Verdana
```

When using a url() value, always use quotes around the URL. 

```
//Good
.reg-header 
    background: url("img/logo.png")


// Bad - missing quotes
.reg-header
    background: url(img/logo.png)
}
```

####Internet Explorer Hacks

We use Paul Irish's [Conditional Stylesheets](http://www.paulirish.com/2008/conditional-stylesheets-vs-css-hacks-answer-neither/) over property hacks. Please do not user property hacks. Instead do this:

```
.cell-display
    width: 300px
    .ie7 &, .ie8 &
        width: 298px
```

####Shorthand properties. 

Please use shorthand property wherever you can. Sass is very verbose on some of its properties. Example:

```
Good:
.enfuago
    font: italic small-caps bold 12px comic-sans 

Bad:
.enfuago
    font:
        family: comic-sans
        variant: small-caps
        weight: bold
        style: italic
        size: 12px

Compiles to bad:

.enfuago
    font-family: comic-sans
    font-variant: small-caps
    font-weight: bold
    font-style: italic
    font-size: 12px

```

####Partials
We use partials whenever possible. Don't be shy to make a partial. Please create new partials wherever there are logical semantic breaks in styleing or sass functions.

```
Good:
_accordion.sass
_hero.sass
_price.sass
_swatch.sass
_tabs.sass

Bad:
_big-giant-bucket.sass
_more-unoganized-styles.sass
```


