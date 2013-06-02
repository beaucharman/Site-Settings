# Site Settings

> Easily create and manage a WordPress site settings page

## Usage

```php
/* Declare the Site Settings options
   ======================================================================== */
$group     = 'lt3_site_settings';
$name      = 'lt3_settings';
$menu_name = 'Site Settings';
$title     = get_bloginfo('name') . ' Site Setings';

/* Declare the Site Settings fields
   ======================================================================== */
$args = array(
  array(
    'id'          => 'google_analytics',
    'type'        => 'text',
    'description' => 'Define the Google Analytics tracking code for the site here.',
    'placeholder' => 'UA-XXXXX-X'
  )
  // add more options here
);

/* Declare a new instance of the Site Settings class
   ======================================================================== */
new LT3_Site_Settings_Page($group, $name, $args, $menu_name, $title);

/* Create a global variable of the Site Settings
   ======================================================================== */
if (!is_admin())
{
  $lt3_site_settings = get_option($name);
}
```

Also, for the use of the file upload option, the following script is required - also alter the reference to it within the site-settings.php class ('path/to/script/cmfb-file-upload.js'):

```javascript
/**
 * Custom Meta Field Boxes File Upload
 * ========================================================================
 * cmfb-file-upload.js
 * @license MIT license
 * ======================================================================== */
(function ($) {
  $('.custom_upload_file_button').click(function () {
    var $formField = $(this).siblings('.custom_upload_file');
    tb_show('Select a File', 'media-upload.php?type=image&TB_iframe=true');
    window.send_to_editor = function (html) {
      var $fileUrl = $(html).attr('href');
      $formField.val($fileUrl);
      tb_remove();
    };
    return false;
  });

  $('.custom_clear_file_button').click(function () {
    $(this)
      .parent()
      .siblings('.custom_upload_file')
      .val('');
    return false;
  });
}(jQuery));
```

#### Dependencies
- jQuery