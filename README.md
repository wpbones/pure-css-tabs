# Pure CSS tabs for WP Bones

Pure CSS tabs for WordPress/WP Bones

## Installation

You can use composer to install this package:

    $ composer require wpbones/pure-css-tabs

You may also to add in your plugin `composer.json` file:
 
```json
  "require": {
    "php": ">=5.5.9",
    "wpbones/wpbones": "~0.8",
    "wpbones/pure-css-tabs": "^1.0"
  },
```

Remember to add the following script to your main `composer.json` file in order to get any next update via composer:

```js
  "scripts": {
    "install-pure-css-tabs": [
      "cp -R vendor/wpbones/pure-css-tabs/src/public/css/*.css public/css/",
      "cp -R vendor/wpbones/pure-css-tabs/src/resources/assets/less/*.less resources/assets/less/"
    ],
    "post-update-cmd": [
      "@install-pure-css-tabs"
    ]
  }
```

Alternatively, you can get the `.less` and then compile it, or get directly the `.css` files.    

## Enqueue for Controller

```php
public function index()
{
  wp_enqueue_style( 'wpbones-tabs', WPKirk()->getPublicCssUri() . '/wpbones-tabs.min.css',
                      [],
                      WPKirk()->Version );
}
```

## HTML markup

```html
<!-- main tabs container -->
<div class="wpbones-tabs">

  <!-- first tab -->
  <label for="tab-1" tabindex="0"></label>
  <input id="tab-1" type="radio" name="tabs" checked="checked" aria-hidden="true">
  <h2><?php _e( 'Database' ) ?></h2>
  <div>
    <h3>Content</h3>
  </div>
  
  <!-- second tab -->
  <label for="tab-2" tabindex="0"></label>
  <input id="tab-2" type="radio" name="tabs" aria-hidden="true">
  <h2><?php _e( 'Posts' ) ?></h2>
  <div>
    <h3>Content</h3>
  </div>  
  
  <!-- son on... -->
  
</div>
```

Of course, you may use the **fragment** feature to include the single tabs:

```html
<!-- main tabs container -->
<div class="wpbones-tabs">

  <!-- first tab -->
  <?php echo WPkirk()->view( 'folder.tab1' ) ?>
  
  <!-- second tab -->
  <?php echo WPkirk()->view( 'folder.tab2' ) ?>
  
  <!-- son on... -->
  
</div>
```
 In `/folder/tab1.php` you just insert the following markup:
 
 ```html
<!-- first tab -->
<label for="tab-1" tabindex="0"></label>
<input id="tab-1" type="radio" name="tabs" checked="checked" aria-hidden="true">
<h2><?php _e( 'Database' ) ?></h2>
<div>
  <h3>Content</h3>
</div>
```
