---
description: Comment Edit Lite has flexible markup for styling.
---

# Styling

{% hint style="info" %}
**Don't want to mess with code?** [Comment Edit Pro](https://dlxplugins.com/plugins/comment-edit-pro/) provides a user interface for the commonly-requested features.
{% endhint %}



## Styling

The plugin doesn’t come with any styles. We leave it up to you to style the interface. It doesn’t look horribly ugly on most themes, but we leave the advanced customization up to you.

### Styling the Edit Interface

The overall editing interface has been wrapped in a `div` with class `sce-edit-comment`.

```css
.sce-edit-comment { /* styles here */ } CSS 
```

### Styling the Edit Button

The edit button and timer have been wrapped in a `div` with class `sce-edit-button`.

```css
.sce-edit-button { /* styles here */ }
.sce-edit-button a { /* styles here */ }
.sce-edit-button .sce-timer { /* styles here */ } CSS 
```

### Styling the Loading Icon

The loading icon has been wrapped in a `div` with class `sce-loading`.

```css
.sce-loading { /* styles here */ }
.sce-loading img { /* styles here */ } CSS 
```

### Styling the Textarea

The textarea interface has been wrapped in a `div` with class `sce-textarea`.

The actual `textarea` has been wrapped in a `div` with class `sce-comment-textarea`. The save/cancel buttons have been wrapped in a `div` with class `sce-comment-edit-buttons`.

```css
.sce-textarea { /* styles here */ }
.sce-textarea .sce-comment-textarea textarea { /* styles here */ }
.sce-comment-edit-buttons { /* styles here */ }
.sce-comment-edit-buttons .sce-comment-save { /* styles here */ }
.sce-comment-edit-buttons .sce-comment-cancel { /* styles here */ } CSS 
```

### Testing the Styles

Since most of the interface is hidden, it’s a little hard to style. Just place this into your stylesheet, and remove when you’re done.

```css
/* todo - remove me when done styling */
.sce-edit-button,
.sce-loading,
.sce-textarea {
	display: block !important;
}
```

