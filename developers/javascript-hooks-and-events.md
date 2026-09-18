---
description: There are common JavaScript hooks for Comment Edit Lite.
---

# JavaScript Hooks and Events

{% hint style="info" %}
**Don't want to mess with code?** [Comment Edit Pro](https://dlxplugins.com/plugins/comment-edit-pro/) provides a user interface for the commonly-requested features.
{% endhint %}

Here are the common JavaScript hooks available in Comment Edit Core.

## `sce.comment.timer.text` Filter

The `sce.comment.timer.text` filter allows developers to modify the text displayed by a timer before it is returned to the user interface. This filter is particularly useful for customizing the display of countdowns or time-related information in comments.

### Since

Introduced in version 1.4.0.

### Parameters

This filter receives the following parameters:

1. **commentText** (`string`): The original text of the comment.
2. **minuteText** (`string`): Text representation of minutes.
3. **secondText** (`string`): Text representation of seconds.
4. **numMinutesLeft** (`int`): The number of minutes remaining.
5. **numSecondsLeft** (`int`): The number of seconds remaining.

### Usage

To modify the timer text, add a filter function using `wp.hooks.addFilter`. Here's an example:

```javascript
const { addFilter } = wp.hooks;

function modifyTimerText( commentText, minuteText, secondText, numMinutesLeft, numSecondsLeft ) {
    // Custom logic to modify the timer text
    return commentText;
}

addFilter(
    'sce.comment.timer.text',
    'your-custom-namespace',
    modifyTimerText,
    11 /* priority of filter */
);
```

### Example

```javascript
const { addFilter } = wp.hooks;

function addLowTimerWarning( commentText, minuteText, secondText, numMinutesLeft, numSecondsLeft ) {
    if (numMinutesLeft === 0 && numSecondsLeft <= 30) {
        return commentText + ' (Time is running out!)';
    }
    return commentText;
}

addFilter(
    'sce.comment.timer.text',
    'your-custom-namespace',
    addLowTimerWarning
);
```

## `sce.comment.save.data` Filter

The `sce.comment.save.data` filter allows developers to modify the parameters sent during an AJAX request to save a comment. This filter is useful for adding or modifying data before the comment is saved.

### Since

Introduced in version 1.4.0.

### Parameters

This filter receives the following parameter:

* **ajaxSaveParams** (`object`): An object containing the parameters for the AJAX request. The default properties include:
  * `action` (`string`): The action identifier for the AJAX request, typically `'sce_save_comment'`.
  * `comment_content` (`string`): The content of the comment to be saved.
  * `comment_id` (`int`): The ID of the comment being saved.
  * `post_id` (`int`): The ID of the post associated with the comment.
  * `nonce` (`string`): A nonce for security purposes.

### Usage

To modify the AJAX save parameters, add a filter function using `wp.hooks.addFilter`. Here's an example:

```javascript
const { addFilter } = wp.hooks;

function modifyAjaxSaveParams( ajaxSaveParams ) {
    // Custom logic to modify the AJAX save parameters
    return ajaxSaveParams;
}

addFilter(
    'sce.comment.save.data',
    'your-custom-namespace',
    modifyAjaxSaveParams
);
```

### Example

```javascript
const { addFilter } = wp.hooks;

function addCustomParam( ajaxSaveParams ) {
    ajaxSaveParams.custom_param = 'custom_value';
    return ajaxSaveParams;
}

addFilter(
    'sce.comment.save.data',
    'your-custom-namespace',
    addCustomParam
);
```

## `sceCommentSavePost` Custom Event

The `sceCommentSavePost` event is a custom JavaScript event triggered after a comment save action is initiated. This event is dispatched to provide additional hooks for custom functionality or integrations when a comment is being saved.

### Event Details

The event carries a `detail` object with the following properties:

* **button** (`Element`): The button element that initiated the save action.
* **textarea** (`Element`): The textarea element containing the comment content.
* **commentId** (`int`): The ID of the comment being saved.
* **postId** (`int`): The ID of the post associated with the comment.
* **ajaxData** (`object`): The data object returned from the AJAX save request.

### Usage

To listen to the `sceCommentSavePost` event, add an event listener to the `document` object. Here's an example:

```javascript
document.addEventListener('sceCommentSavePost', function(event) {
    const { button, textarea, commentId, postId, ajaxData } = event.detail;

    // Custom logic to handle the event
});
```

## `sceTimerLoaded` Custom Event

The `sceTimerLoaded` event is a custom JavaScript event that is triggered when a timer associated with a comment is loaded. This event provides a hook for developers to add custom functionality or integrations at the moment a comment timer is initialized.

### Event Details

The event includes a `detail` object containing the following properties:

* **button** (`Element`): The button element related to the comment timer.
* **commentId** (`int`): The ID of the comment for which the timer is loaded.
* **postId** (`int`): The ID of the post associated with the comment.

### Usage

To handle the `sceTimerLoaded` event, you need to add an event listener to the `document` object. Here's an example of how to do this:

```javascript
document.addEventListener('sceTimerLoaded', function(event) {
    const { button, commentId, postId } = event.detail;

    // Implement custom logic upon timer loading
});
```

## `sceTimerCountdown` Custom Event

The `sceTimerCountdown` event is a custom JavaScript event that is triggered during the countdown of a comment timer. This event is designed to provide developers with a hook for implementing custom functionality or integrations that respond to the progression of the timer.

### Event Details

The event carries a `detail` object with the following properties:

* **button** (`Element`): The button element associated with the comment timer.
* **commentId** (`int`): The ID of the comment for which the timer is counting down.
* **postId** (`int`): The ID of the post associated with the comment.
* **timer\_seconds** (`int`): The current number of seconds remaining in the timer.
* **timer\_minutes** (`int`): The current number of minutes remaining in the timer.

### Usage

To listen to the `sceTimerCountdown` event, add an event listener to the `document` object. Here's an example:

```javascript
document.addEventListener('sceTimerCountdown', function(event) {
    const { button, commentId, postId, timer_seconds, timer_minutes } = event.detail;

    // Custom logic to handle the countdown event
});
```

## `sceEditTextareaShow` Custom Event

The `sceEditTextareaShow` event is a custom JavaScript event that is triggered when the text area for editing a comment is displayed. This event provides a hook for developers to add custom functionality or integrations at the moment the text area for editing a comment becomes visible.

### Event Details

The event includes a `detail` object containing the following properties:

* **textarea** (`Element`): The textarea element that is used for editing the comment.
* **commentId** (`int`): The ID of the comment being edited.
* **postId** (`int`): The ID of the post associated with the comment.

### Usage

To handle the `sceEditTextareaShow` event, you need to add an event listener to the `document` object. Here's an example of how to do this:

```javascript
document.addEventListener('sceEditTextareaShow', function(event) {
    const { textarea, commentId, postId } = event.detail;

    // Implement custom logic when the edit textarea is shown
});
```

## `sceCommentSavePre` Custom Event

The `sceCommentSavePre` event is a custom JavaScript event that is triggered just before a comment save action is initiated. This event provides developers with an opportunity to implement custom logic or integrations immediately before the comment saving process begins.

### Event Details

The event includes a `detail` object containing the following properties:

* **button** (`Element`): The button element that initiates the save action.
* **textarea** (`Element`): The textarea element containing the comment content.
* **commentId** (`int`): The ID of the comment being saved.
* **postId** (`int`): The ID of the post associated with the comment.

### Usage

To handle the `sceCommentSavePre` event, add an event listener to the `document` object. Here's an example:

```javascript
document.addEventListener('sceCommentSavePre', function(event) {
    const { button, textarea, commentId, postId } = event.detail;

    // Custom logic to execute before saving the comment
});
```
