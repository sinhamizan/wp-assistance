# WP Assistance

### Add li class in wp_nav_menu
In functions.php 
```ruby
function add_additional_class_on_li($classes, $item, $args) {
    if(isset($args->add_li_class)) {
        $classes[] = $args->add_li_class;
    }
    return $classes;
}
add_filter('nav_menu_css_class', 'add_additional_class_on_li', 1, 3);
```
In html file
``` ruby

wp_nav_maneu(array(
  .......
  'add_li_class' => 'your-class-name1 your-class-name2',
));

```

### Add li a class in wp_nav_menu
In functions.php 
```ruby
function add_additional_class_on_a($classes, $item, $args)
{
    if (isset($args->add_a_class)) {
        $classes['class'] = $args->add_a_class;
    }
    return $classes;
}
add_filter('nav_menu_link_attributes', 'add_additional_class_on_a', 1, 3);

```
In html file
```ruby

wp_nav_maneu(array(
  .......
  'add_a_class' => 'your-class-name1 your-class-name2',
));

```

### Get Current Category
```ruby
$currCat = get_category(get_query_var('cat'));
$cat_name = $currCat->name;  
$cat_id   = get_cat_ID( $cat_name );
```

### show pagination in category page
```ruby
  $paged = (get_query_var('paged')) ? get_query_var('paged') : 1;
  $temp = $wp_query;
  $wp_query = null;
  $wp_query = new WP_Query();
  $wp_query->query('showposts=1&post_type=post&paged='.$paged.'&cat='.$cat_id);
  ```
  
  ### Change Next/Prev text in pagination
  ```ruby
  global $wp_query;
 
  $big = 999999999; // need an unlikely integer
  echo '<div class="paginate-links">';
    echo paginate_links( array(
    'base' => str_replace( $big, '%#%', esc_url( get_pagenum_link( $big ) ) ),
    'format' => '?paged=%#%',
    'prev_text' => __('<<'),
    'next_text' => __('>>'),
    'current' => max( 1, get_query_var('paged') ),
    'total' => $wp_query->max_num_pages
    ) );
  echo '</div>';
  ```
### Moving the Comment Text Field to Bottom
```ruby
function wpb_move_comment_field_to_bottom( $fields ) {
$comment_field = $fields['comment'];
unset( $fields['comment'] );
$fields['comment'] = $comment_field;
return $fields;
}
add_filter( 'comment_form_fields', 'wpb_move_comment_field_to_bottom' );
```

### Removing the Website URL Field From WordPress Comment Form
```ruby
add_filter('comment_form_default_fields', 'unset_url_field');
function unset_url_field($fields){
    if(isset($fields['url']))
       unset($fields['url']);
       return $fields;
}
```

### Change "Leave a reply" text in comment
```ruby
function change_reply_title($arg) {
	$arg['title_reply'] =__('Leave a Comment');
	return $arg;
}
add_filter('comment_form_defaults','change_reply_title');
```

### Display Custom post type category

```ruby
$cats = get_terms(array(
          'taxonomy' => 'service-category',
          'hide_empty' => false,
        ));
	```
