# Frequently Asked Questions

 * [How can I remove the hyperlink of the title of the post?](#no_link)
 * [How can I use the shortcode in a Widget?](#widget)
 * [How to insert the shortcode on the theme and not a post or page](#shortcode-theme)
 * [How to display lists in columns](#columns)
 * [How do I display the Thumbnail next to the title?](#thumbnail)
 * [How to not display the title](#no-title)
 * [How do I remove the bullets from the list?](#bullets)
 * [The plugin doesn't work on servers with PHP < 5](#php5)
 * [Plugin could not be activated because it triggered a fatal error](#fatal-error)
 * [If a post has many categories, categorypage=yes only detects one of them](#categorypage)

## <a name="no_link"></a>How can I remove the hyperlink of the title of the post?

Add `link_titles=false` to your shortcode.

## <a name="thumbnail"></a>How do I display the Thumbnail next to the title?

To see the thumbnail next to the title, you can add a class to it like
this:

`[catlist id=1 thumbnail=yes thumbnail_class=lcp_thumbnail]`

Then in your theme's stylesheet add this code:

```
.lcp_thumbnail{
  float: left;
}

.lcp_catlist li{
  clear: both;
}
```

If you want the thumbnail to the right, just change the `float: left`
attribute to `float: right`.


## <a name="no-title"></a>How to not display the title

Add `no_post_titles=yes` to your shortcode.

## <a name="shortcode-theme"></a>How to insert the shortcode on the theme and not a post or page

You can use this code on your theme (sidebar, footer, or wherever you like):
`<?php echo do_shortcode("[catlist id=3]"); ?>`

## <a name="columns"></a> How to display lists in columns

You don't need a template for this. You can write something like this when editing your page/post (in the "Text" text-editor):

```html
<table>
  <tr>
    <td>
    [catlist id=3 numberposts=5 excludeposts=this]
    </td>
    <td>
    [catlist id=3 numberposts=5 excludeposts=this offset=5]
    </td>
  </tr>
</table>
```

The offset should equal the number of posts (`numberposts`) times the number of column - 1. So if you had a third column, the code would look like this:
```html
<table>
  <tr>
    <td>
    [catlist id=3 numberposts=5 excludeposts=this]
    </td>
    <td>
    [catlist id=3 numberposts=5 excludeposts=this offset=5]
    </td>
    <td>
    [catlist id=3 numberposts=5 excludeposts=this offset=10]
    </td>
  </tr>
</table>
```
## <a name="widget"></a>How can I use the shortcode in a Widget?

Since WordPress 4.9, you can use a shortcode in a widget.
If you’re using a previous WordPress version, add this code to your theme’s functions.php file:
```php
add_filter('widget_text', 'do_shortcode');
```

Then just add a new text widget to your blog and use the shortcode there
as the widget's content.

## <a name="bullets"></a>How do I remove the bullets from the list?

By default the posts will be displayed inside a ul tag with the
`lcp_catlist` CSS class. So to make the bullets disappear, just add
this CSS code to your theme's stylesheet:

```css
.lcp_catlist li{
  list-style: none;
}
```

## <a name="php5"></a>Does not work on servers with PHP < 5

This is true since version 0.18. If you're still using PHP 4 on your webhost, you should consider upgrading to PHP 5. WordPress 3.1 was the last version to support PHP 4, from 3.2 and forward, only PHP 5 is supported. You can still [download an older version of the plugin](https://wordpress.org/extend/plugins/list-category-posts/download/ "download an older version of the plugin") if you're using PHP 4.

## <a name="fatal-error"></a>Plugin could not be activated because it triggered a fatal error

Something like this:

```
Parse error: syntax error, unexpected T_STRING, expecting
T_OLD_FUNCTION or T_FUNCTION or T_VAR or '}' in
/.../wp-content/plugins/list-category-posts/include/CatListDisplayer.php
on line 10*
```

It's probably due to the webhost using PHP 4. CatListDisplayer.php
declares private attributes. PHP 4 doesn't have public, private or
protected accessors. Try updating your server or using an [older version](http://wordpress.org/plugins/list-category-posts/download/).

Please check:
http://wordpress.stackexchange.com/questions/9338/list-category-posts-plugin-upgrade-fails-fatal-error/9340#9340

## <a name="categorypage"></a>If a post has many categories, categorypage=yes only detects one of them

This is how it works in the current implementation, there are no shortcode parameters to change this behavior.
We have already received feature requests to make `categorypage=yes` work with multiple categories and it should be
implemented at some stage.
