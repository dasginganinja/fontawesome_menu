# Font Awesome Menu

This Drupal 7 module provides an icon field when configuring menu links that implements a helpful icon widget picker. The icon element is processed in using theme_menu_link().

This module does not implement any assets such as css or fonts to your theme front-end, but does provide libraries integration for fontawesome and fontawesome-iconpicker on menu link configuration page.

Keep in mind, since the fontawesome css and font assets themselves are not included in your theme's front-end you will want to be sure that the library version that you are using on the admin side matches the version you use on your theme's front-end side. You can get library version numbers at `admin/reports/libraries`.

## Dependencies
- [Libraries API](https://www.drupal.org/project/libraries)

## Installation
See fontawesome_menu_libraries_info() for specific library assets.

1. Install the "Font Awesome" library.
    - LIBRARY should be at libraries/fontawesome.
      - https://github.com/FortAwesome/Font-Awesome
    - CSS should be at libraries/fontawesome/css.
    - JS should be at libraries/fontawesome/js.
2. Install the "Font Awesome Icon Picker" library.
    - LIBRARY should be at libraries/fontawesome-iconpicker.
      - https://github.com/itsjavi/fontawesome-iconpicker
    - CSS should be at libraries/fontawesome-iconpicker/dist/css.
    - JS should be at libraries/fontawesome-iconpicker/dist/js.
3. Enable the fontawesome_menu module.

## Custom menu link implmentations
Other modules may implement their own custom menu links. For example the superfish module implements a custom theming function `theme_superfish_menu_item_link`. The icon gets returned as part of the $link item. For example, if you call `menu_link_load($mlid)` you would find the defined icon as `$link['fa_icon']`. You could override the custom menu link theming by getting the fa_icon and returning it back as part of the link markup. Here is an implementation for overriding a superfish menu item link:
```php
function hook_superfish_menu_item_link($variables) {
  $menu_item = $variables['menu_item'];
  $link_options = $variables['link_options'];
  if (!empty($menu_item['link']['fa_icon'])) {
    $link_options['html'] = TRUE;
    $icon = '<i class="fa ' . $menu_item['link']['fa_icon'] . '"></i>';
    $title = $icon . '<span class="menu-link-title">' . $menu_item['link']['title'] . '</span>';
  }
  else {
    $title = $menu_item['link']['title'];
  }

  return l($title, $menu_item['link']['href'], $link_options);
}
```
