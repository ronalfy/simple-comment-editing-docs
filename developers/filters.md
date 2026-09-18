---
description: Extend Comment Edit Lite programatically.
---

# Filters

{% hint style="info" %}
**Don't want to mess with code?** [Comment Edit Pro](https://dlxplugins.com/plugins/comment-edit-pro/) provides a user interface for the commonly-requested features.
{% endhint %}

### sce\_loading\_img - Change the loading image

```phpdoc
/**
* Filter: sce_loading_img
*
* Replace the loading image with a custom version.
*
* @since 1.0.0
*
* @param string  $image_url URL path to the loading image.
*/
```

Example:

```php
//Simple Comment Editing
add_filter( 'sce_loading_img', 'edit_sce_loading_img' );
function edit_sce_loading_img( $default_url ) {
	return 'http://domain.com/new_loading_image.gif';
}
```

### sce\_comment\_check\_errors - Add custom error messages

```phpdoc
/**
* Filter: sce_comment_check_errors
*
* Return a custom error message based on the saved comment
*
* @since 1.2.4
*
* @param bool  $custom_error Default custom error. Overwrite with a string
* @param array $comment_to_save Associative array of comment attributes
*/
```

Here's an example:

```php
add_filter( 'sce_comment_check_errors', 'custom_sce_check_comment_length', 15, 2 );
function custom_sce_check_comment_length( $return = false, $comment = array() ) {
	$comment_content = trim( wp_strip_all_tags( $comment[ 'comment_content' ] ) );
	$comment_length = strlen( $comment_content );
	if ( $comment_length < 50 ) {
		return 'Comment must be at least 50 characters';
	}
	return false;
}
```

### sce\_allow\_delete - Whether to allow comment deletion or not

```phpdoc
/**
* Filter: sce_allow_delete
*
* Determine if users can delete their comments
*
* @since 1.1.0
*
* @param bool  $allow_delete True allows deletion, false does not
*/
```

Example:

```php
// Disable delete functionality
add_filter( 'sce_allow_delete', '__return_false' );
```

### sce\_allow\_delete\_confirmation - Whether to show a delete confirmation or not

```phpdoc
/**
 * Filter: sce_allow_delete_confirmation
 *
 * Boolean to decide whether to show a delete confirmation
 *
 * @since 2.1.7
 *
 * @param bool true to show a confirmation, false if not
 */
```

Example:

```php
add_filter( 'sce_allow_delete_confirmation', '__return_false' );
```

### sce\_get\_comment - Add extra data to the comment object

This is only used when retrieving a comment via Ajax and can be used by third-party plugins who post comments using Ajax

```phpdoc
/**
* Filter: sce_get_comment
*
* Modify comment object
*
* @since 1.5.0
*
* @param object Comment Object
*/
```

### sce\_extra\_fields - Add extra HTML to the editing interface

```phpdoc
/**
* Filter: sce_extra_fields
*
* Filter to add additional form fields
*
* @since 1.4.0
*
* @param string Empty string
* @param int post_id POST ID
* @param int comment_id Comment ID
*/
```

### sce\_buttons - Add extra buttons to the editing interface (aside from Cancel and Save)

```phpdoc
/**
* Filter: sce_buttons
*
* Filter to add button content
*
* @since 1.3.0
*
* @param string  $textarea_buttons Button HTML
* @param int       $comment_id        Comment ID
*/
```

### sce\_content - Modify the edit output HTML

```phpdoc
/**
* Filter: sce_content
*
* Filter to overrall sce output
*
* @since 1.3.0
*
* @param string  $sce_content SCE content 
* @param int       $comment_id Comment ID of the comment
*/
```

### sce\_save\_before - Modify the comment object before saving via AJAX

```phpdoc
/**
* Filter: sce_save_before
*
* Allow third parties to modify comment
*
* @since 1.4.0
*
* @param object $comment_to_save The Comment Object
* @param int $post_id The Post ID
* @param int $comment_id The Comment ID
*/
```

### sce\_can\_edit - Override the boolean whether a user can edit a comment or not

```phpdoc
/**
* Filter: sce_can_edit
*p
* Determine if a user can edit the comment
*
* @since 1.3.2
*
* @param bool  true If user can edit the comment
* @param object $comment Comment object user has left
* @param int $comment_id Comment ID of the comment
* @param int $post_id Post ID of the comment
*/
```

Example: [https://gist.github.com/ronalfy/6b4fec8b3ac55bc47f3f](https://gist.github.com/ronalfy/6b4fec8b3ac55bc47f3f)

### sce\_security\_key\_min - How many security keys will be stored as post meta

```phpdoc
/**
* Filter: sce_security_key_min
*
* Determine how many security keys should be stored as post meta before garbage collection
*
* @since 1.0.0
*
* @param int  $num_keys How many keys to store
*/
```

### sce\_load\_scripts - Whether to load SCE scripts or not

```phpdoc
/**
* Filter: sce_load_scripts
*
* Boolean to decide whether to load SCE scripts or not
*
* @since 1.5.0
*
* @param bool  true to load scripts, false not
*/
```

### sce\_comment\_time - How long in minutes to allow comment editing

```phpdoc
/**
* Filter: sce_comment_time
*
* How long in minutes to edit a comment
*
* @since 1.0.0
*
* @param int  $minutes Time in minutes
*/
```

Example:

```php
//Simple Comment Editing
add_filter( 'sce_comment_time', 'edit_sce_comment_time' );
function edit_sce_comment_time( $time_in_minutes ) {
	return 60;
}
```

### sce\_show\_timer - Show or hide the timer

```phpdoc
/**
 * Filter: sce_show_timer
 *
 * Filter allow you to hide the timer
 *
 * @since 2.3.0
 *
 * @param bool Whether to show the timer or not
 */
```

Example:

```php
//Simple Comment Editing - Disable the timer
add_filter( 'sce_show_timer', '__return_false' );
```

### sce\_edit\_text - Change the "Click to Edit" text.

```phpdoc
/**
* Filter: sce_text_edit
*
* Filter allow editing of edit text
*
* @since 2.0.0
*
* @param string Translated click to edit text
*/
```

Example:

```php
add_filter( 'sce_text_edit', function( $translated_text ) {
	return "Custom Edit Text";
} );
```

### sce\_edit\_save - Change the "Save" button text.

```phpdoc
/**
* Filter: sce_text_save
*
* Filter allow editing of save text
*
* @since 2.0.0
*
* @param string Translated save text
*/
```

Example:

```php
add_filter( 'sce_text_save', function( $translated_text ) {
	return "Custom Save";
} );
```

### sce\_edit\_cancel - Change the "Cancel" button text.

```phpdoc
/**
* Filter: sce_text_cancel
*
* Filter allow editing of cancel text
*
* @since 2.0.0
*
* @param string Translated cancel text
*/
```

Example:

```php
add_filter( 'sce_text_cancel', function( $translated_text ) {
	return "Custom Cancel";
} );
```

### sce\_edit\_delete - Change the "Delete" button text.

```phpdoc
/**
* Filter: sce_text_delete
*
* Filter allow editing of delete text
*
* @since 2.0.0
*
* @param string Translated delete text
*/
```

Example:

```php
add_filter( 'sce_text_delete', function( $translated_text ) {
	return "Custom Delete";
} );
```

### sce\_akismet\_enabled

```
/**
 * Filter: sce_akismet_enabled
 *
 * Allow third parties to disable Akismet.
 *
 * @param bool true if Akismet is enabled
 */
$akismet_enabled = apply_filters( 'sce_akismet_enabled', true );
```

Example:

```
add_filter( 'sce_akismet_enabled', function( $enabled ) {
	return false;
} );
```
