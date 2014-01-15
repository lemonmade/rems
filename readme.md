# rems

This project is a collection of [SASS](http://sass-lang.com) functions and mixins for gracefully handling `rem`, `em`, and `px` units in your stylesheets. Its key feature is creating `rem` style declarations with `px` (and, optionally, `em`) fallbacks to handle older browsers (which, as we all know, is merely a pet name for IE).

## Examples

### Create rem styles with px fallback

```(sass)
@import "_rems.scss";

.big-header {
    // We want an effective pixel value of 50px
    @include rems(font-size, 50px);
}
```