# Pure CSS tabs for WP Bones

Pure CSS tabs for WordPress/WP Bones

[![Latest Stable Version](https://poser.pugx.org/wpbones/pure-css-tabs/v/stable)](https://packagist.org/packages/wpbones/pure-css-tabs)
[![Total Downloads](https://poser.pugx.org/wpbones/pure-css-tabs/downloads)](https://packagist.org/packages/wpbones/pure-css-tabs)
[![License](https://poser.pugx.org/wpbones/pure-css-tabs/license)](https://packagist.org/packages/wpbones/pure-css-tabs)

## Installation

You can install third party packages by using:

```sh
php bones require wpbones/pure-css-tabs
```
   
I advise to use this command instead of `composer require` because doing this an automatic renaming will done.  

You can use composer to install this package:

```sh
composer require wpbones/pure-css-tabs
```

You may also to add `"wpbones/pure-css-tabs": "^1.0"` in the `composer.json` file of your plugin:
 
```json
  "require": {
    "php": ">=7.2",
    "wpbones/wpbones": "~1.0",
    "wpbones/pure-css-tabs": "~1.0"
  },
```

and run 

```sh
composer install
```
    
Alternatively, you can get the `src/resources/assets/less/wpbones-tabs.less` and then compile it, or get directly the `src/public/css/wpbones-tabs.css` files.    
Also, you can get pre-compiled minified version `src/public/css/wpbones-tabs.min.css`.

## Enqueue for Controller

You can use the provider to enqueue the styles.

```php
public function index()
{
  // enqueue the minified version
  PureCSSTabsProvider::enqueueStyles();
  
  // ...
  
}
```

## PureCSSTabsProvider

This is a static class autoloaded by composer. You can use it to enqueue or get the styles path:

```php
// enqueue the minified version
PureCSSTabsProvider::enqueueStyles();

// enqueue the flat version
PureCSSTabsProvider::enqueueStyles( false );
    
// return the absolute path of the minified css
PureCSSTabsProvider::css();

// return the absolute path of the flat css
PureCSSTabsProvider::css();   
```

## HTML markup

```html
<!-- main tabs container -->
<div class="wpbones-tabs">

  <!-- first tab -->
  <input id="tab-1" type="radio" name="tabs" checked="checked" aria-hidden="true">
  <label for="tab-1" tabindex="0"><?php _e( 'Database' ) ?</label>
  <div class="wpbones-tab">
    <h3>Content</h3>
  </div>
  
  <!-- second tab -->
  <input id="tab-2" type="radio" name="tabs" aria-hidden="true">
  <label for="tab-2" tabindex="0"><?php _e( 'Posts' ) ?></label>
  <div class="wpbones-tab">
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
<input id="tab-1" type="radio" name="tabs" checked="checked" aria-hidden="true">
<label for="tab-1" tabindex="0"><?php _e( 'Database' ) ?></label>
<div class="wpbones-tab">
  <h3>Content</h3>
</div>
```

## Customize

Of course, you can edit both of CSS or LESS files in order to change the appearance of tabs.
In the LESS file, you'll find the color variable as well.

```less
@wpbones-tab-border-color : #aaa;
@wpbones-tab-responsive-accordion-border : #ddd;
@wpbones-tab-disabled : #ddd;
@wpbones-tab-content-color : #fff;
```

> :pushpin:
>
> Anyway, the best way to customize your tabs is override the default styles. Otherwise, when an update will be done you'll lose your customization.

## Helper

In addition, you can use some methods provided by `PureCSSTabsProvider` class.
In your HTML view you might use:

```php
    /**
     * Display tabs by array
     *
     *     self::tabs(
     *       'tab-1' => [ 'label' => 'Tab 1', 'content' => 'Hello', 'selected' => true ],
     *       'tab-2' => [ 'label' => 'Tab 1', 'content' => 'Hello' ],
     *       ...
     *     );
     *
     * @param array $array
     */
    WPKirk\PureCSSTabs\PureCSSTabsProvider::tabs(
      'tab-1' => [ 'label' => 'Tab 1', 'content' => 'Hello', 'selected' => true ],
      'tab-2' => [ 'label' => 'Tab 1', 'content' => 'Hello' ],
      ...
    );
```

Also, you can use `openTab()` and `closeTab()` methods:

```php
  /**
   * Display the open tab.
   *
   * @param string $label    The label of tab.
   * @param null   $id       Optional. ID of tab. If null, will sanitize_title() the label.
   * @param bool   $selected Optional. Default false. TRUE for checked.
   */
   public static function openTab( $label, $id = null, $selected = false ) {}
```

```html
<div class="wpbones-tabs">

  <?php WPKirk\PureCSSTabs\PureCSSTabsProvider::openTab( 'Tab 1', null, true ) ?>
    <h2>Hello, world! I'm the content of tab-1</h2>
  <?php WPKirk\PureCSSTabs\PureCSSTabsProvider::closeTab ?>
    
  <?php WPKirk\PureCSSTabs\PureCSSTabsProvider::openTab( 'Tab 2' ) ?>
    <h2>Hello, world! I'm the content of tab-2</h2>
  <?php WPKirk\PureCSSTabs\PureCSSTabsProvider::closeTab ?>
    
</div>    
```
> :pushpin:
>
> Remember, in the example above I have used `WPKirk` base namespace. You should replace it with your own namespace.

