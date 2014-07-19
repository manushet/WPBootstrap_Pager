WPBootstrap_Pager
=================

Fully-Featured, customizable class for creating Bootstrap-style pagination links for many page types in WordPress.

The WPBootstrap_Pager class provides a consistent interface for creating Bootstrap-style pagination elements
across several WordPress page types.

It was originally designed as a rewrite of [wp_link_pages()](http://codex.wordpress.org/Function_Reference/wp_link_pages) to allow for additional styling,
but has since been expanded to offer the same interface for archive-type pages (similar to what
[paginate_links()](http://codex.wordpress.org/Function_Reference/paginate_links) does).  I have tried
to keep the arguments consistent with the arguments used in the WordPress function calls.

This implementation is left as open-ended as possible.  There are no hard-coded tags, except for anchors (`<a>` tags), which are still created by WordPress.  All other HTML tags are provided through arguments, so there might be uses for this class beyond Bootstrap.  The default arguments, however, are designed to work with Bootstrap with little or no customization required.

Usage
-----

First, include class-wpbootstrap-pager.php in your template's functions.php file:

```php
require_once 'class-wpbootstrap-pager.php';
```

### Post-Type Pager

In a WordPress post or page template (like single.php), the following code would be placed __inside__ the loop:

```php
<?php wpbootstrap_post_pager( $args ); ?>
```

This will create a pagination element for paging through multiple pages in a single post.

This usage is a replacement for calls to [wp_link_pages()](http://codex.wordpress.org/Function_Reference/wp_link_pages),
and is called in a similar manner (with additional arguments that provide extra customization).

### Archive-Type Pager
    
In a WordPress archive-type template (archive.php, category.php, tag.php, etc.), the following code would
be placed __before or after__ the loop:

```php
<?php wpbootstrap_archive_pager( $args ); ?>
```

This will create a pagination element for paging through multiple pages of posts.
    
This usage is a replacement for calls to [paginate_links()](http://codex.wordpress.org/Function_Reference/paginate_links),
although it is called with a different set of arguments that is more similar to those from
[wp_link_pages()](http://codex.wordpress.org/Function_Reference/wp_link_pages).  

The argument structure for both functions is identical, and described below.

### Default Arguments

```php
$defaults = array(
	'before'           => '<ul class="pagination">',
	'after'            => '</ul>',
	'link_before'      => '<li>',
	'link_after'       => '</li>',
	'next_or_number'   => 'number',
	'nextpagelink'     => '&raquo;',
	'previouspagelink' => '&laquo;',
	'pagelink'         => '%',
	'echo'             => true,
	'current_before'   => '<li class="active">',
	'current_after'    => '</li>',
	'currentlink'      => '% <span class="sr-only">'. __( '(current)', 'wp_bootstap_pager' ) . '</span>',
	'disabled_before'  => '<li class="disabled">',
	'disabled_after'   => '</li>',
	'previous_before'  => '<li class="previous">',
	'previous_after'   => '</li>',
	'next_before'      => '<li class="next">',
	'next_after'       => '</li>',
	'show_all'         => false,
	'end_size'         => 1,
	'mid_size'         => 2,
	'hellip'           => '<li class="disabled"><a>&hellip;</a></li>',
);
```

### Parameters

The `$args` parameter is not required.  If omitted, a default Bootstrap pagination element will be created.

#### before

* (string) Text to put before all the links. Defaults to `<ul class="pagination">`.

#### after 

* (string) Text to put after all the links. Defaults to `</ul>`.

#### link_before

* (string) Text that goes before the text of the link. Defaults to `<li>`.

#### link_after 

* (string) Text that goes after the text of the link. Defaults to `</li>`.

#### next_or_number 

* (string) Indicates whether page numbers should be used. Valid values are:
    * `number` (Default) - Display page numbers.
    * `next` - Display previous/next links only.

#### nextpagelink 

* (string) Text for link to next page. Defaults to `&raquo;` (&raquo;)

#### previouspagelink

* (string) Text for link to previous page. Defaults to `&laquo;` (&laquo;)

#### pagelink

* (string) Format string for page numbers.  % in the string will be replaced with the number, so Page % would generate "Page 1", "Page 2", etc. Defaults to `%`.

#### echo

* (boolean) Toggles whether to echo or return the result. The default is `true`. Valid values:
    * 1 (True) - Default
    * 0 (False)

#### current_before

* (string) Text that goes before link for the current page only. Defaults to `<li class="active">`.  This default

#### current_after

* (string) Text that goes after link for the current page only. Defaults to `</li>`.

#### currentlink

* (string) Format string for current page number only.  % in the string will be replaced with the number. Defaults to `% <span class="sr-only">(current)</span>`.

#### disabled_before

* (string) Text that goes before the disabled links.  When `next_or_number = 'number'`, the previous and next links are disabled on the first and last page, respectively.  Applies only to this scenario.  Defaults to `<li class="disabled">`.

#### disabled_after

* (string) Text that goes after the disabled links.  When `next_or_number = 'number'`, the previous and next links are disabled on the first and last page, respectively.  Applies only to this scenario.  Defaults to `</li>`.

#### previous_before

* (string) Used only when `next_or_number = 'next'`.  Text that goes before the previous page link.  Defaults to `<li class="previous">`.  This default class causes the previous page link to left align.

#### previous_after

* (string) Used only when `next_or_number = 'next'`.  Text that goes after the previous page link.  Defaults to `</li>`.

#### next_before

* (string) Used only when `next_or_number = 'next'`.  Text that goes before the next page link.  Defaults to `<li class="next">`.  This default class causes the next page link to right align.

#### next_after

* (string) Used only when `next_or_number = 'next'`.  Text that goes after the next page link.  Defaults to `</li>`.


#### show_all

* (boolean) If set to `true`, then it will show all of the pages instead of a short list of the pages near the current page. By default, `show_all` is set to `false` to prevent the pagination element from becoming too large.  When `show_all = false`, the size of the pager is controlled by the `end_size` and `mid_size` arguments.  Defaults to `false`.

#### end_size

* (integer) Used only when `showall = false`.  Number of pages displayed on either the start and the end list edges.  Defaults to `1`.

#### mid_size

* (integer) Used only when `showall = false`.  Number of pages displayer to either side of current page, but not including current page.  Defaults to 2.

#### hellip

* (string) Text to replace omitted page numbers with, usually some form of ellipses (&hellip;).  Defaults to `<li class="disabled"><a>&hellip;</a></li>`.


### Example Usage
<link href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">

#### Default Post-Type Pagination

```php
<?php
if ( have_posts() ) {
  while ( have_posts() {
     the_post();
     //
     // Post content here
     //
     ?>
     
     <div class="text-center"><?php wpbootstrap_post_pager( ); ?></div>
     
     <?php
  }
}
```

Use `<div class="text-center">` to center the pagination element on the page.

<div class="text-center"><ul class="pagination"><li class="disabled"><a href="#">&laquo;</a></li><li class="active"><a href="#">1 <span class="sr-only">(current)</span></a></li><li><a href="#">2</a></li><li><a href="#">3</a></li><li><a href="#">&raquo;</a></li></ul></div>

#### Default Archive-Type Pagination

```php
<?php
if ( have_posts() ) {
  while ( have_posts() {
     the_post();
     //
     // Post content here
     //
  }
}
?>
<div class="text-center"><?php wpbootstrap_archive_pager( ); ?></div>
```

![archive-type](https://cloud.githubusercontent.com/assets/8201912/3633601/0e08304e-0eea-11e4-92a2-b024893491b4.PNG)

#### Next/Previous Post-Type Pager

```php
<?php
if ( have_posts() ) {
  while ( have_posts() {
     the_post();
     //
     // Post content here
     //

     $args = array(
	'next_or_number'   => 'next',
	'before'           => '<ul class="pager">',
	'previouspagelink' => __( 'Previous Page', 'text-domain' ),
	'nextpagelink'     => __( 'Next Page', 'text-domain' ),
     );
     
     wpbootstrap_post_pager( $args );
  }
}
```

This pager element does not need to be centered, as the default `previous_before` and `previous_after` arguments will right- and left-align the buttons automatically.

![prev-next](https://cloud.githubusercontent.com/assets/8201912/3633605/913d6dbc-0eea-11e4-9f49-324ef307ac70.PNG)

#### Older/Newer Archive-Type Pager

```php
<?php
if ( have_posts() ) {
  while ( have_posts() {
     the_post();
     //
     // Post content here
     //
  }
}

$args = array(
  'next_or_number'   => 'next',
  'before'           => '<ul class="pager">',
  'previouspagelink' => __( 'Newer Posts', 'text-domain' ),
  'nextpagelink'     => __( 'Older Posts', 'text-domain' ),
);
     
wpbootstrap_archive_pager( $args );
```

Note that archives are in reverse chronological, so the previous page contains newer posts and the next page contains older posts.

![newer-older](https://cloud.githubusercontent.com/assets/8201912/3633620/366267ca-0eeb-11e4-880b-7ab22ca38ace.PNG)

#### Centered Previous/Next Pager

```php
<?php
if ( have_posts() ) {
  while ( have_posts() {
     the_post();
     //
     // Post content here
     //

     $args = array(
	'next_or_number'   => 'next',
	'before'           => '<ul class="pager">',
	'previouspagelink' => __( 'Previous Page', 'text-domain' ),
	'nextpagelink'     => __( 'Next Page', 'text-domain' ),
	'previous_before'  => '<li>',
	'previous_after'   => '</li> ',
	'next_before'      => '<li>',
     );
     ?>
     
     <div class="text-center"><?php wpbootstrap_post_pager( $args ); ?></div>
     
     <?php
  }
}
```

Remove the classes from the `previous_before` and `next_before` arguments to prevent them from left- and right-aligning.  Also, a space is added to the end of `previous_after` to keep the two elements from touching.

![centered-prev-next](https://cloud.githubusercontent.com/assets/8201912/3633692/f50ea670-0ef0-11e4-8568-b413e856e6b2.PNG)

#### Pagination Size

The default behavior is to omit pages from large pagination elements, based on the `end_size` and `mid_size` arguments:

![large-pagination](https://cloud.githubusercontent.com/assets/8201912/3633705/b3b85368-0ef2-11e4-8910-37441e25cb49.PNG)

