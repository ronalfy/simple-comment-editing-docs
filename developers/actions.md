---
description: There are common actions for Comment Edit Lite.
---

# Actions

{% hint style="info" %}
**Don't want to mess with code?** [Comment Edit Pro](https://dlxplugins.com/plugins/comment-edit-pro/) provides a user interface for the commonly-requested features.
{% endhint %}

### sce\_save\_after - Triggered via Ajax after a comment has been saved

Useful for custom comment fields

```php
/**
* Action: sce_save_after
*
* Allow third parties to save content after a comment has been updated
*
* @since 1.4.0
*
* @param object $comment_to_save The Comment Object
* @param int $post_id The Post ID
* @param int $comment_id The Comment ID
*/
```

