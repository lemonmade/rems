# rems

This project is a collection of [SASS](http://sass-lang.com) functions and mixins for gracefully handling `rem`, `em`, and `px` units in your stylesheets. Its key feature is creating `rem` style declarations with `px` (and, optionally, `em`) fallbacks to handle older browsers (which, as we all know, is merely a pet name for IE).

## Examples

### Create `rem` styles with `px` fallback

```scss
@import "_rems.scss";

.big-header {
    // We want an effective pixel value of 50px
    @include rems(font-size, 50px);
}
```

Outputs:

```css
.big-header {
    font-size: 50px;
    font-size: 3.125rem; // baseline defaults to 16px, so 50px / 16px
}
```

### Create `rem` styles with `px` and `em` fallbacks

```scss
@import "_rems.scss";

.parent {
    @include rems(font-size, 20px, 1rem);

    .child {
        @include rems(font-size, 30px, 20px);
    }
}
```

Outputs:

```css
.parent {
    font-size: 20px;
    font-size: 1.25em;
    font-size: 1.25rem;
}

.parent .child {
    font-size: 30px;
    font-size: 1.5em; // 30px (target) / 20px (parent size)
    font-size: 1.875rem; // 30px (target) / 16px (default baseline)
}
```

The definition of `em` sizes requires you to provide the font-size of the parent element, either as a pixel or `rem` value. This is a bit of a pain as it requires you to calculate the size of the parent, but there is no way around this as the mixin can't detect the effects of `em`-based sizing's cascade. However, if you use this mixin to define all sizes of ancestor elements, everything should work out quite nicely.


### Common conversions

```scss
number(30em);               // returns 30
px-to-em(30px, 20px, true); // returns 1.5em
px-to-rem(20px, 16px);      // returns 1.25
rem-to-px(2.5, 16, true);   // returns 40px
```