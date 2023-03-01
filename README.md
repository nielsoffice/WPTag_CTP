# WPTag_CTP
Add Tag functionality for Custom Post Type WordPress support 6.1 ++

```PHP

if ( ! function_exists( 'ns_register_team_category' ) ) {
	function ns_register_team_category() {
	
	   $labels = array(
		'name' => __( 'Tags', 'ns' ),
		'singular_name' => __( 'Tag', 'ns' ),
		'search_items' =>  __( 'Search Tags' ),
		'popular_items' => __( 'Popular Tags' ),
		'all_items' => __( 'All Tags' ),
		'parent_item' => null,
		'parent_item_colon' => null,
		'edit_item' => __( 'Edit Tag' ),
		'update_item' => __( 'Update Tag' ),
		'add_new_item' => __( 'Add New Tag' ),
		'new_item_name' => __( 'New Tag Name' ),
		'separate_items_with_commas' => __( 'Separate tags with commas' ),
		'add_or_remove_items' => __( 'Add or remove tags' ),
		'choose_from_most_used' => __( 'Choose from the most used tags' ),
		'menu_name' => __( 'Tags' ),
	   );
	
	   $args = array(
		'label' => __( 'Tag', 'ns' ),
		'labels' => $labels,
		'public' => true,
		'publicly_queryable' => true,
		'hierarchical' => true,
		'show_ui' => true,
		'show_in_menu' => true,
		'show_in_nav_menus' => true,
		'query_var' => true,
		'rewrite' => array( 'slug' => 'tag', 'with_front' => false, ),
		'show_admin_column' => false,
		'show_in_rest' => true,
		'rest_base' => 'tag',
		'rest_controller_class' => 'WP_REST_Terms_Controller',
		'show_in_quick_edit' => true,
		'update_count_callback' => '_update_post_term_count',
	);
	
	register_taxonomy( 
  
   'tag',  // tag_name | base on CPT < 'taxonomies' => array( 'blog', 'category', 'tag'), >
   array( 'blog' ), // CPT
   
   $args );

	}
  
	add_action( 'init', 'ns_register_team_category', 0 );
	
	}


```

```PHP
// Fetch and Loop doesn't matter
$tags = get_terms([
          'taxonomy'  => 'YOUR_CUSTOM_TAXONOMY',
          'hide_empty'    => false
        ]);
var_dump($tags);

```

```PHP
  // Base on post ID or Object ID
  $tags = wp_get_post_terms(get_the_ID(), 'post_tag' );

  var_dump( $tags );		

  foreach(  $tags as $tag ) 
		
  { print('<li class="cat_'.$tag->ID.'">' . $tag->name . '</li> '); }
  
```

Reference: <br />

<a href="https://developer.wordpress.org/reference/functions/wp_get_post_terms/">reference/functions/wp_get_post_terms</a><br />
<a href="https://nielsoffice197227997.wordpress.com/2021/09/06/tag-box-for-specific-custom-post-type-wordpress/">Tag box for specific custom post type – WordPress</a><br />
<a href="https://wordpress.stackexchange.com/questions/62260/how-to-add-tags-to-custom-post-type">Nuno Sarmento</a><br />
<a href="https://www.sanwebe.com/snippet/create-custom-tags-for-custom-post-types-wordpress">Create Custom Tags for Custom Post Types (WordPress)</a><br />
<a href="https://stackoverflow.com/questions/29230243/wordpress-get-all-tags-from-custom-post-type">Mahafuz : Fetch and loop Tags for Custom Post Types (WordPress)</a><br />


