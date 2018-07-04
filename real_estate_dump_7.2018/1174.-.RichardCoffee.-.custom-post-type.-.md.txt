This repository has evolved from just a CPT class into more of a collection of boiler plate plugin files.
Most of the information below is primarily for the custom post base class.  Some of it no longer applies.
Work continues...





# Custom Post Type

This is a base class for WordPress custom post types.  For something that might be easier to use,
try [Post Types Creator](https://github.com/pelmered/post-types-creator) or [Extended CPTs](https://github.com/johnbillion/extended-cpts).
This is -not- a UI, nor is it intended to be.  If you are looking for that, then try [Custom Post Type UI](https://github.com/WebDevStudios/custom-post-type-ui).

Other good resources: [Custom Post Type Permalinks](https://github.com/torounit/custom-post-type-permalinks),
[Simple Post Type Permalinks](https://wordpress.org/plugins/simple-post-type-permalinks/)


I have seen quite a few different ways of how people handle custom post types in wordpress, but was
never really happy with any of them.  They all did what they were designed to, but never really seemed
to cover the things that I needed.  So I set out to make my own.  It is still very much a work in
progress.  Please drop me a note if you find it useful in your own projects.

The basis for a lot of the code originated from different places on the web.  I have tried to give
credit where I can.  My coding style can not be considered 'orthodox' in any way, shape, form, or fashion.

WARNING:  Use a permalink of `/%category%/%post_name%/` otherwise this thing may not work at all...8-(  It is something I am working on.

## Update:

I have started adding plugin components to the repo, working under the assumption that a CPT
should always be in a plugin.  I also plan on splitting out portions of the code into more
governable components.  Just about everything is in line for a rewrite.

## Features

* Provides a base class for easier CPT creation.
* Control whether the CPT show ups on the Blog page along with regular posts.
* Assign custom 'single'/'archive' templates for displaying the CPT.
* Assign a folder, or list of folders to look for templates in.
* Show a column on the admin Users screen, providing an author count.
* Add taxonomy columns to CPT admin dashboard.
* Stop a user from deleting a custom taxonomy term, either permanently or if in use.
* Prevent editing of custom taxonomy term slugs.
* Stop a CPT with a specific taxonomy term from showing up on queries.
* Automatically generate custom capabilites, suitable to be used for custom roles.
* Generate log messages using your own logging function.

## Install

Requires PHP 5.3+
Requires jQuery, mainly for the ready() function.  If someone makes vanilla javascript versions
of the two js files, I would be happy to take a pull request.

Tested up to 4.7.3

You need four files out of the repository:
```
  classes/Post/Post.php
  classes/Trait/Logging.php
  js/slug_noedit.js
  js/tax_nodelete.js
```
Simply copy these to where you need them.  `Logging.php` is a dependency of
`Post.php`.  If the js files are located anywhere other than `plugin_dir/js`
then the js_path class property will need to be set.

Note:  tcc_plugin.php has an example of an autoload function, which utilizes
the classes/Post/Post.php file.  Hmmm, that file is, well, old.


## Usage

Create your own class extending this one.

### Example 1

A bare minumum child class could look like this:
```
class Simple_Custom_Post_Type extends TCC_Post_Post {

	protected $type = 'simple';
	protected $main_blog = true;

	public function __construct() {
		$args = array(
			'label'     => __( 'Simple',  'text-domain' ),
			'plural'    => __( 'Simples', 'text-domain' )
		);
		parent::__construct( $args );
	}

}
```
### Example 2

A more complicated class might start like this:
```
class Property extends TCC_Post_Post {

	public function __construct() {
		$data = array(
			'type'       => 'my-property',
			'label'      => _x( 'Property', 'single plot of land', 'text-domain' ),
			'plural'     => _x( 'Properties', 'multiple plots of land', 'text-domain' ),
			'descrip'    => __( 'Real Estate Property', 'text-domain' ),
			'menu_position' => 6,
			'menu_icon'  => 'dashicons-admin-home',
			'taxonomies' => array(
				'category'
			),
			'templates'  => array(
				'single'  => plugin_dir_path( __FILE__ ) . '../page-templates/single-property.php',
				'archive' => plugin_dir_path( __FILE__ ) . '../page-templates/archive-property.php',
			),
			'slug_edit'  => false,
		);
		parent::__construct( $data );
		if ( is_admin() ) {
			add_action( 'admin_enqueue_scripts', array( $this, 'admin_enqueue_scripts') );
		}
		add_action( 'tcc_custom_post_' . $this->type, array( $this, 'create_taxonomies' ) );
		add_action( 'add_meta_boxes_' . $this->type,  array( $this, 'add_meta_boxes' ) );
		add_action( 'save_post_' . $this->type,       array( $this, 'save_meta_boxes' ) );
		add_filter( 'tcc_register_post_property',     array( $this, 'register_property' ) );
	}

	public function register_property( $args ) {
		$args['show_in_nav_menus'] = false;
		return $args;
	}


}
```
Look in Post.php for a list of all available arguments, and what
they do.  The method that registers the CPT uses only a subset of arguments
available for the WordPress [register_post_type()](http://codex.wordpress.org/Function_Reference/register_post_type)
function.  If you need to utilize more, there is a filter `tcc_register_post_{post-type}`
that allows you to modify the $args array.  I seem to be adding something with
every project, so it may have the full set at some point.  :)  I have tried to
use what I consider reasonable defaults.  There are some examples in the
`examples\` directory.  They may not work with the current version of `Post.php`.

## General Guidelines

#### Capabilities

While defaulting to using standard Wordpress capabilities, the class can generate
unique ones, based on the slug for the CPT.  Also, adds the expected caps to the
default WordPress user roles. For a listing of those caps, look in `$GLOBALS['wp_post_types'][post type]['cap']`.

#### Labels
The class generates a default array of strings for the labels based upon the
singular and plural labels.  This array can be altered using the filter action
`tcc_post_label_{post-type}`.  See the 'Text domain' and 'Text strings' sections
below for related information.

#### List columns
Custom columns can be added/removed via the plugin.  This can be done utilizing the columns property like so:
```
$this->columns = array('add' => array('taxslug' => __('Header text','text-domain')));
```
The display of taxonomies is handled automatically, while you may need to override the internal method, display_custom_post_column, to display other data:
```
$this->columns = array('add' => array('taxslug' => __('Header text','text-domain'),
                                      'postid'  => __('Post ID','text-domain')));

public function display_custom_post_column($column,$post_id) {
  switch($column) {
    case 'postid':
      echo $post_id;
      break;
    default:
      parent::display_custom_post_column($column,$post_id);
  }
}
```
Optionally, a custom display callback can be specified.  It would be used instead of the plugin method:
```
$this->columns = array('add' => array( 'index1' => __('Header One','text-domain'),
                                       'index2' => __('Header Two','text-domain'))
                       'callback' => 'callable_function');
```
If you want a column to be sortable, then add a 'sort' index, like so:
```
$this->columns = array('add'  => array('taxslug' => __('Header text','text-domain'),
                                       'postid'  => __('Post ID','text-domain'))
                       'sort' => array('taxslug'));
```
To style the column use '.column-{slug}' in your css file.

#### Taxonomies
After the post type has been created, an action hook is run named `tcc_custom_post_{post-type}`.
Hook there to run code such as registering a taxonomy.  See the 'Taxonomies' sections
below.  The class provides its own taxonomy_registration() method.  When used,
it provides the ability to prevent term deletion for the taxonomy.  There is
also a mechanism in place to prevent specified term deletion.  See the
'Term Deletion' section below for slightly more information.

#### Template
A template file can be assigned for 'single' and 'archive' templates.  A template
'folder' can also be specified.  The filter, `tcc_assign_template_{$this->type}`,
can also be used.  I think this still needs more work.  If anyone runs into use
cases that this doesn't handle properly, please let me know.

#### Term Deletion
In order to make this work, the taxonomy must be created using the internal class
method taxonomy_registration(), with `'nodelete'=>true` being passed as a
construction argument.  If you want to prevent specific taxonomy terms from
being deleted, append an array of the term slugs and/or names to the class property tax_keep array, like so:

`$this->tax_keep['taxonomy-slug'] = array('term-slug-one',__('Term Name Two','text-domain'))`

#### Text Domain
All the strings the class uses are defined in the method translated_text().
Redefine the method in the child class to change the text-domain and/or
wording of the strings, but be sure to duplicate the array structure
__exactly__.  Alternately, you could change the Post.php text
 domain to your domain.  If you are comfortable with the linux command
line you could use this command:  `sed -i 's/tcc-custom-post/your-domain-name-here/' path-to/Post.php`.
Or you could just do a search and replace in your favorite text editor.

#### Text strings
the method translated_text() provides default strings for both cpt and taxonomy
labels.  The methods utilizing the strings are post_type_labels(), taxonomy_labels(),
and post_type_messages().  The latter generates CPT specific messages which are
displayed in place of the standard WordPress messages.

## Taxonomies

Frankly, this is kind of a mess.  It is on my TODO list.

$this->taxonomy_registration($args)

$args must be either an associative array or a string.  If it is a string then
it must be parsable by the WordPress [wp_parse_args()](http://codex.wordpress.org/Function_Reference/wp_parse_args)
function.  Accepted arguments are:
```
tax      => string ** the taxonomy slug (required)
taxargs  => array --- passed as the third argument to the WordPress register_taxonomy() function if present
single   => string ** single label name, same as `$taxargs['labels']['singular_name']`
                      (one of the two is required)
plural   => string ** plural label name, same as `$taxargs['labels']['name'] or $taxargs['label']`
                      (one of the three is required)
admin    => boolean - same as `$taxargs['show_admin_column']`
rewrite  => string -- same as `$taxargs['rewrite']['slug']`, defaults to taxonomy slug if either is not set
nodelete => boolean - true indicates that a term in this taxonomy cannot be deleted if the term is
                      associated with a post. default: false
terms    => array --- terms to populate the taxonomy with.  Only happens if the taxonomy is completely
                      devoid of terms.  The 'terms' array can be in structured as `array('Term Name One',
                      'term-slug-two'=>'Term Name Two')`.  It does not handle 'alias_of','description', or
                      'parent' at this time.
func     => string -- function/method name - if the 'terms' array is empty, this function will be used to
                      populate the terms array, default function called: '$this->default_{tax-slug}'
                      set to false to disable.
omit     => array --- array of terms not to display in searches. ie:  if a post has this term, that post
                      will be omitted from query results.
```

# Change Log

No formal release yet.  Code still subject to change without notice.  If anyone uses this, please let me know, and I will start being more structured in a release schedule.
