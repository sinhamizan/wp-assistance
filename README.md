# WP Assistance
### Add class in li in wp_nav_menu
In functions.php 

function add_additional_class_on_li($classes, $item, $args) {
    if(isset($args->add_li_class)) {
        $classes[] = $args->add_li_class;
    }
    return $classes;
}
add_filter('nav_menu_css_class', 'add_additional_class_on_li', 1, 3);

In html file

wp_nav_maneu(array(
  .......
  'add_li_class' => 'your-class-name1 your-class-name2',
));
