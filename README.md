
## Why CSS Grid AND Flexbox is better than Bootstrap for creating responsive layouts

### Grid Features

### "Automagic" responsive breakdown
Built into the grid is an opinated take on how the different column layouts should reflow and breakdown across the 5 breakpoints. This works nicely for those that want to get up and running quickly, need their content to look great across many screens, and don't need the granualar control over the breakdown of columns for each breakpoint.

In this "automagic" mode, only certain column spanning values are supported out of the box. For example, if you need a column spanning 7 columns in a 24 column layout, you'll need to use the manual class overrides described below.

Column spanning options that are supported "automagically", these will reflow and respond across the different breakpoints without any manual classes:

| Columns |      Spans     |
|:-------:|:--------------:|
|    1    | 1              |
|    2    | 1, 2           |
|    3    | 1, 2, 3        |
|    4    | 1, 2, 3, 4     |
|    5    | 1, 2, 3, 4, 5  |
|    6    | 1, 2 ,3 ,4, 6  |
|    8    | 1, 2, 4, 6, 8  |
|    12   | 1, 2, 4, 12    |
|    24   | 1, 6, 12, 24   |

Example row:
```html
<section class="ms-row">
    <div class="col-3-4 ">
    </div>
    <div class="col-1-4 ">
    </div>
</section>
```

Column breakdown across each breakpoint:

| Columns | < 320px (mf) | > 320px (vp1) XS | > 540px (vp2) S | > 768px (vp3) M | > 1084px (vp4) L | > 1400px (vp5) XL |
|:-------:|:------------:|:-------------:|:-------------:|:-------------:|:-------------:|:--------------:|
|    1    |       1      |       1       |       1       |       1       |       1       |        1       |
|    2    |       1      |       1       |       1       |       2       |       2       |        2       |
|    3    |       1      |       1       |       3       |       3       |       3       |        3       |
|    4    |       1      |       1       |       2       |       4       |       4       |        4       |
|    5    |       1      |       1       |       1       |       5       |       5       |        5       |
|    6    |       1      |       1       |       2       |       3       |       6       |        6       |
|    8    |       2      |       2       |       2       |       4       |       8       |        8       |
|    12   |       2      |       2       |       4       |       4       |       12      |       12       |
|    24   |       6      |       6       |       12      |       24      |       24      |       24       |


### Manual column spanning
Manual column span class overrides are supported for all column counts and all breakpoints.
Here is the pattern for the classes:

viewport - col - # of columns to span - total # of columns

Examples:

`s-col-3-24` - 12.5% of the viewport - At the small(viewport 2) breakpoint and above, this column will span 3 columns of the 24 columns in the row.

`l-col-14-24` - 58.3333333333% of the viewport - At the large(viewport 4) breakpoint and above, this column will span 14 columns of the 24 columns in the row.

### Fluid vs. fixed gutter options
The grid can support fluid, fixed, and zero/no gutter options, all of which is configurable. By default the grid uses fluid gutters. If you want to use fixed gutters, you will add one of three helper classes: `fixed`, `fixed-small`, or `fixed-large`. Zero or no gutter uses the helper class `zero-margin`.

To apply these different gutter options, you place the corresponding helper class on the grid element or an individual row. Place on the grid if you want it to go across that entire grid. Place on an individual row if you'd like to scope the behavior to only that row.

Fluid - this is the default behavior.

`fixed` - stays at one value across all breakpoints, default is 4px.

`fixed-small` - starts at 4px, jumps to 12px at viewport 2, and to 24px at viewport 3.

`fixed-large` - starts at 8px, jumps to 24px at viewport 2, and to 48px at viewport 3.

`zero-margin` - removes all gutters between columns.

### Page margins
The grid supports two flavors of page margins. None or full width and an option with margin.

The default grid's page margins start at 12px, jump to 24px at vp2, 48px at vp3, and 5% at vp4.

The `full` class added on the grid element will enabled the no margin experience.

### Offsets
Using these classes will offset a column by a specified amount.

Here is the pattern for the classes:
viewport - col - total # of columns - offset - # of columns to offset

Example:
`l-col-8-offset-2` - This will offset the column by 2 column widths for an 8 column row above the large(viewport 4) breakpoint.

### Column ordering (push/pull)
Using these classes will allow you to change the built-in column ordering .

Here is the pattern for the classes:
Pull - viewport - col - total #of columns - pull - # of columns to pull over by
Push - viewport - col - total #of columns - push - # of columns to push over by

Example:
If these classes were used in conjunction on two adjacent columns, it would swap them, their order.

`l-col-24-pull-12` - This will pull the column over by 12 column widths for a 24 column row above the large(viewport 4) breakpoint.

`l-col-24-push-12` - This will push the column over by 12 column widths for a 24 column row above the large(viewport 4) breakpoint.


### Centered columns
Putting the `.centered` class on a single column will center it in that row.

### Vertically centering columns
In [browsers that support Flexbox](http://caniuse.com/#search=flexbox), putting the `.vertically-centered` or `.vc` class on a single row will align all items center which will vertically center them. Great for vertically centering text next to images.

### Horizontally centering all columns
In [browsers that support Flexbox](http://caniuse.com/#search=flexbox), putting the `.horizontally-centered` or `.hc` class on a single row will align all items center based on a flex direction of column which will horizontally center all of them.

### No break
Putting the `.nb` class on a column will make it hold it's original width across all breakpoints.

Example:
An element with the classes of `class="col-1-4 nb` will always stay at a width of 25%.

### Prefixing of grid and row classes
The _config file has the variable named `$grid-prefix` where you can specify any prefixing that you would like added to all the `.grid` and `.row` classes. The default is `ms-`.

### Hiding and showing content
Helpers are available to you to hide, show, or make invisible content based on the breakpoints of the grid. Here is an example of the classes output for the default medium breakpoint.
```css
@media screen and (min-width: 768px) {
  .show-m {
    display: block;
    visibility: visible;
  }

  .hide-m {
    display: none;
    visibility: hidden;
  }

  .invisible-m {
    visibility: hidden;
  }
}
```

### jQuery plugin for preceding columns
There is a scenario where the CSS sibling selector, +, fails for the "automagic" mode. This selector only selects siblings that follow after and not preceding siblings. Because of this scenario, when a smaller column span could be used preceding a larger column span, those preceding columns need to be decorated with a class so that they can be selected. If you don't want to use the jQuery plugin, that is fine, but they will need to be decorated with a preceding class. Or add the small jQuery plugin that runs on load to decorate those classes automatically for you.

### RTL Support
The grid has full support for RTL. There are predefined SCSS files and labeled respectively for LTR, RTL, and mixed. Compiliation for direction is controlled by two different config values: `$dir` (ltr or rtl) and `$dirMixed` (boolean, false as a default). These variables then drive `$left` and `$right` variables throughout the SCSS to change as appropriate.

To enable directional support, you need to apply the `dir` attribute to the html tag and link the appropriate CSS file. It should look something like the following.

`<html dir="rtl">` or `<html dir="ltr">`

Mixed language support is enabled through the use of a `dir` attribute override. For example, you could have a default `dir` tag of ltr on the html tag, but than place the 'dir' attribute again where you needed to support the opposite, say on a `row` element to override that specific `row` and make it rtl.
```html
<html dir="ltr">
...
<div class="row" dir="rtl"></div>
```

### IE8 Support
Without doing anything, IE8 will show the mobile first view. If that is not acceptable for your project, full IE8 support is supported by adding [Respond.js](https://github.com/scottjehl/Respond) to your project will allow it to behave as it does in modern browsers. Remember that if you're using any HTML5 elements (like section), you'll also want to add the [HTML5Shiv](https://github.com/aFarkas/html5shiv). Include this JS in the head of your HTML, putting in the conditional comment below will only serve it to browsers below IE9.
```html
<head>
	...
	...

    <!--[if lt IE 9]>
        <script src="/pathto/html5shiv.js"></script>
        <script src="/pathto/respond.js"></script>
    <![endif]-->
</head>
```

### Why do you need flex.css?
```
In the process of Mobile Terminal Development, standard flex is not supported by all versions of all kinds of
browsers, webview, and wechat which basically support  -webkit-box. So flex.css's main purpose is to ensure
that every attribute can be supported by standard version's flex or old-version's -webkit-box.
due to autoprefixer compilation is used by flex.css,it will roll back to old-version's -webkit-box when standard
flex is not supported by some browsers so the effect of layout will be the same.
Then,here comes a magic effient layout tool of mobile terminal development ...
```


###  merits
```
Concise api,
familiar attribute values, makes it easy for you to get started in using flex.css.
In html, the layout is bind with attributes, so it is seperated from css. In this way, it will be easier for you
to maintain and modify your layout without modifying css.
```


### support
```
flex layout is split into three versions: old version: display: box; , transitional version: display:flexbox; ,
and present standard version: display:flex; .
Android
2.3  began to support old version: display: -webkit-box;
4.4 began to support standard version: display: flex;
IOS
6.1  began to support old version: display: -webkit-box;
7.1 began to support standard version: display: flex;
PC
You can use flex.css if you don't need to consider IE10-.
flex.css is compatible with standard version and old version at the same time, so when a browser doesn't support standard version, it will roll back to old version.

```
![Alt text](https://github.com/lzxb/flex.css/raw/master/shot/caniuse.png)

### use
```html
<!--
According to what you need, include css files in the dist directory into your html
flex.css should be matched by flex attribute
data-flex.css should be matched by data-flex attribute(used by React)
If you use webpack to package, after npm is installed, and ES6 compiler is deployed in your project,
flex attribute matching can be implemented in this way:
import 'flex.css';
data-flex attribute matching can be implemented in this way( used by React):
import 'flex.css/dist/data-flex.css';
 -->
<!-- flex attribute matching，a simple example of centering child element ： -->
  <div flex="main:center cross:center" style="width:500px; height: 500px; background: #108423">
    <div style="background: #fff"> to see if this is in the center </div>
  </div>

<!-- data-flex attribute matching，a simple example of centering child element： -->
  <div data-flex="main:center cross:center" style="width:500px; height: 500px; background: #f1d722">
    <div style="background: #fff"> to see if this is in the center </div>
  </div>
```
### collection of flex attributes
```
dir: axis direction
    top：from top to bottom
    right：from right to left
    bottom：from bottom to top
    left：from left to right( default )
```
```
main：axis align
    right：from right to left
    left：from left to right ( default )
    justify：justify align
    center：center align
```
```
cross：cross axis align
    top：from top to bottom ( default )
    bottom：from top to bottom
    baseline：baseline align
    center：center align
    stretch：cover whole area
```
```
box：child element setup
    mean：space is split by child elements equally
    first：spare space is  not given to the first element and split by the rest of child elements equally
    last：spare space is  not given to the last element and split by the rest of child elements equally
    justify：spare space is  not given to both of the first element of each end
	and split by the rest of child elements equally
```

### flex-box attributes description
```
values range ( 0-10 ), how to asign spare space to individual child element: if the value equals 0,there won't
be any spare space for this child element.
spare space assignment = current value of flex-box / the sum of all values of child element's flex-box
```
