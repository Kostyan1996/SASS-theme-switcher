# SASS-theme-switcher
## Description
This is a basic project to try SASS in practice (example looks bad in every theme except Light, but it shows main functionality anyway).

Main part is theme.scss, it's a theme switcher in SASS, easy to add new themes without too much hastle of searching through every needed element every time you add a new theme.

After I had an idea, I needed to find out how to implement it. I figured out that I can place theme class on html, then have a SASS map in theme.scss with all required colors at the top, then iterate over it and somehow apply all colors where I need it. Then I found the implementation of @katiemctigue (https://medium.com/@katiemctigue/how-to-create-a-dark-mode-in-sass-609f131a3995) and really liked it so I modified it, though all credits to @katiemctigue.

Body of theme.scss (where all `@include` and `t()` are located) looks verbose, but you only need to add it once for new element and you don't have to worry about this element after that forever, even if you add entire new theme. Feels better every time your .scss file length increases.

## How to use
* Your code needs to set class to `<html>` in format of `class: "theme-NAME"` where NAME is a theme name that you will use in theme map (3rd step below).
* Add `@mixin applyThemes()` and `@function t($key)` from this theme.scss to your .scss file where you will add theme-related styling.
* Add a map (set of themes that contain key-value pairs) that contains required theme-based parameters in this format (THEME# is a theme name that is added to `<html>` (step 1 above), KEY# is key name that will be used in step 4 and VALUE# is a theme-specific value, that will be used in step 4):
```
$themes: (
  THEME1: (
    KEY1: VALUE1,
    KEY2: VALUE2
  ),
  THEME2: (
    KEY1: VALUE1,
    KEY2: VALUE2
  )
);
```
* For every element that needs a different parameter for every theme you use, add this, where PROPERTY is theme-based property you want to add to your element and VALUE_IN_THEME is a key in theme map:
```
@include applyThemes() {
  PROPERTY: t(KEY_IN_THEME);
}
```
* After that generated .css file should contain every element you added in step 4 mapped to every theme you added in map in step 3.

## Project focus
To learn SASS more and practice it. Currently this includes nesting, custom functions, mixins, @each and more.
