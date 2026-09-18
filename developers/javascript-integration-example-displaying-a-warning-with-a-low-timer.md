---
description: Add some text when the timer is low.
---

# JavaScript Integration Example: Displaying a Warning With a Low Timer

In this example integration, we'll add some text to the timer when the timer is low. This will involve some PHP, a bit of JavaScript, and will show you how to use some of the hooks that are built into Comment Edit Core.

First, we'll use a Comment Edit Core hook called `sce_scripts_loaded`.

<pre class="language-php" data-title="cec-add-timer-low-text.php"><code class="lang-php"><strong>&#x3C;?php
</strong>/**
 * Plugin Name:       Comment Edit Core - Add Timer Low Text
 * Plugin URI:        https://github.com/DLXPlugins/cep-add-timer-low-text/
 * Description:       Add a timer low text to the comment edit core timer section.
 * Version:           1.0.0
 * Requires at least: 5.9
 * Requires PHP:      7.2
 * Author:            DLX Plugins
 * Author URI:        https://dlxplugins.com
 * License:           GPL v2 or later
 * License URI:       https://www.gnu.org/licenses/gpl-2.0.html
 * Text Domain:       cep-add-timer-low-text
 *
 * @package CEPAddTimerLowText
 */

namespace DLXPlugins\CEPAddTimerLowText;

// Hook into Comment Edit Core and output our scripts.
add_action( 'sce_scripts_loaded', __NAMESPACE__ . '\enqueue_scripts' );

/**
 * Enqueue our scripts.
 */
function enqueue_scripts() {
	wp_enqueue_script(
		'cec-add-timer-low-text',
		plugins_url( 'cec-add-timer-low-text.js', __FILE__ ),
		array( 'wp-hooks', 'simple-comment-editing' ), /* Need `wp-hooks` to use `addFilter` */
		'1.0.0',
		true
	);
}
</code></pre>

You'll note that dependency scripts `wp-hooks` and `simple-comment-editing` are set as dependencies for the script file we'll be loading in next.

In the JavaScript, we'll use the `wp-hooks` package to hook into the filter `sce.comment.timer.text`.

{% code title="cec-add-timer-low-text.js" %}
```javascript
/**
 * Set up the timer low text by hooking into the event system.
 */

// Import the addFilter function.
const { addFilter } = wp.hooks;

// Set the low timer text.
const sceLowTimerText = 'Low Timer';

/**
 * Hook into document.load.
 */
document.addEventListener( 'DOMContentLoaded', () => {

	/**
	 * JSFilter: sce.comment.timer.text
	 *
	 * Filter triggered before a timer is returned
	 *
	 * @since 1.4.0
	 *
	 * @param  string comment text
	 * @param  string minute text,
	 * @param  string second text,
	 * @param  int    number of minutes left
	 * @param  int    seconds left
	 */
	addFilter( 'sce.comment.timer.text', 'sce-add-timer-low-text', ( text, minuteText, secondText, numMinutesLeft, numSecondsLeft ) => {

		if ( numMinutesLeft === 0 && numSecondsLeft <= 30 ) {
			text += ' (' + sceLowTimerText + ')';
		}
		return text;
	}, 11 );
} );

```
{% endcode %}

The JavaScript function `addFilter` hooks into Comment Edit Core's filter for modifying the timer text.

Now, when the timer is less than thirty seconds, a warning will show the user that the timer is low.

The full code for this [example is on GitHub](https://github.com/DLXPlugins/cec-add-timer-low-text).
