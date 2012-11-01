#jPanelMenu

jPanelMenu is a [jQuery](http://jquery.com) plugin that creates a paneled-style menu (like the type seen in the mobile versions of [Facebook](http://m.facebook.com) and [Google](http://google.com), as well as in many native iPhone applications).



#How Do I Use This Thing?

Start off by including the jPanelMenu.js file in your page. (Bonus points for using the minified version [jPanelMenu.min.js], or for bundling the jPanelMenu code into your own JavaScript file to reduce size and HTTP requests.)

Build your page as you normally would (the source order does not matter), and instantiate jPanelMenu by calling the plugin constructor function.

	var jPM = $.jPanelMenu();

By default, jPanelMenu will look for an element with an ID of `menu` to use as the menu, and elements with a class of `menu-trigger` to use as the trigger(s). To point jPanelMenu to your menu and trigger elements, pass an object into the constructor function call, as follows:

	var jPM = $.jPanelMenu({
		menu: &rsquo;#custom-menu-selector&rsquo;,
		trigger: &rsquo;.custom-menu-trigger-selector&rsquo;
	});

**Note:** Check out the [options section](#options) for more customization goodness like the above.

After jPanelMenu has been instantiated (and made sure to save the returned object to a variable, as shown above), it&rsquo;s time to turn it on!

	jPM.on();

After that, jPanelMenu will be functioning, and that&rsquo;s it!

If you want to take things to the next level, keep reading.



#How Does This Thing Work?

When jPanelMenu is turned on, two `<div>` elements are created. The menu element (with an id of `jPanelMenu-menu`, and the panel element (with a class of `jPanelMenu-panel`).

The menu, `#jPanelMenu-menu`, contains the elements targeted by the menu selector passed into the jPanelMenu constructor function. The targeted menu element is cloned into `#jPanelMenu-menu`, and is not removed from its original position in the DOM, it is only hidden (using `display: none`).

The panel, `.jPanelMenu-panel`, contains all of the content in the `<body>` element (except for `<style>` tags and `#jPanelMenu-menu`). The selected content is moved, not cloned, into `.jPanelMenu-panel`.

To style or select the menu, use the following selector: `#jPanelMenu-menu`.

To style or select the content panel, use the following selector: `.jPanelMenu-panel`.

When jPanelMenu is turned off, the two `<div>` elements are removed, and all of the content inside `.jPanelMenu-panel` is moved back into the `<body>` element. 


#Does It Animate?

Of course, if you want it to!

Animation is handled by CSS transitions, for browsers with support. CSS transitions are hardware-accelerated on supporting devices, so the animations are silky smooth.

For browsers that do not support CSS transitions, the jQuery animation engine is used as a fallback.



#Options

The following options can be set via an object passed into the constructor function call.

	var jPM = $.jPanelMenu({
		// options...
	});


***


###menu

The selector pointing to the desired menu element.

- **Data Type:** `string`
- **Default Value:** `#menu`


***


###trigger

The selector pointing to the menu-triggering element.

- **Data Type:** `string`
- **Default Value:** `.menu-trigger`


***


###excludedPanelContent

A selector string specifying which tags within the `<body>` element should not be pushed into `.jPanelMenu-panel`.

Generally, `<style>` and `<script>` tags should not be moved from their original location, but in certain circumstances (mostly advertising), `<script>` tags may need to move with the page content.

- **Data Type:** `string`
- **Default Value:** `style, script`


***


###keyboardShortcuts

An option that allows you to control if keyboard shortcuts are enabled, and if they are, which keys do what.

Setting this option to `false` will disable keyboard shortcuts entirely. To enable keyboard shortcuts, pass in an `array` of `objects`. Each enabled key gets its own `object` in the `array` and each object should be structured as follows:

	{
		code: Keycode of enabled key,
		open: Boolean value (true or false), specifying whether or not this key should open the menu,
		close: Boolean value (true or false), specifying whether or not this key should close the menu
	}

- **Data Type:** `array` or `boolean`
- **Accepted Values:** `array` or `false`
- **Default Value:**
	

		[
			{
				code: 27,
				open: false,
				close: true 
			},
			{
				code: 37,
				open: false,
				close: true 
			},
			{
				code: 39,
				open: true,
				close: true 
			},
			{
				code: 77,
				open: true,
				close: true 
			}
		]


***


###openPosition

The measurement value for the open position of the menu. Can be set as a pixel, percentage, or em value.

- **Data Type:** `string`
- **Examples:** `250px`, `75%`, `20em`
- **Default Value:** `250px`


***


###duration

The time, in milliseconds, which it should take to open and close the menu, when animated.

- **Data Type:** `int`
- **Default Value:** `150`


***


###openDuration

The time, in milliseconds, which it should take to open the menu, when animated. If set, this overrides the duration option.

- **Data Type:** `int`
- **Default Value:** Inherited from `duration`


***


###closeDuration

The time, in milliseconds, which it should take to close the menu, when animated. If set, this overrides the duration option.

- **Data Type:** `int`
- **Default Value:** Inherited from `duration`


***


###easing

The easing function to use when animating the opening and closing of the menu.

- **Data Type:** `string`
- **Accepted Values:** `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`
- **Default Value:** `ease-in-out`


***


###openEasing

The easing function to use when animating the opening of the menu. If set, this overrides the easing option.

- **Data Type:** `string`
- **Accepted Values:** `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`
- **Default Value:** Inherited from `easing`


***


###closeEasing

The easing function to use when animating the closing of the menu. If set, this overrides the easing option.

- **Data Type:** `string`
- **Accepted Values:** `linear`, `ease`, `ease-in`, `ease-out`, `ease-in-out`
- **Default Value:** Inherited from `easing`


***


###before

Called before the menu is opened or closed, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`


***


###beforeOpen

Called before the menu is opened, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`


***


###beforeClose

Called before the menu is closed, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`


***


###after

Called after the menu is opened or closed, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`


***


###afterOpen

Called after the menu is opened, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`


***


###afterClose

Called after the menu is closed, regardless of animation state.

- **Data Type:** `function`
- **Default Value:** `function(){ }`



#API

The following are the methods and properties of the object returned by the jPanelMenu constructor function call. In the following example, these would be the methods and properties of `jPM`.

	var jPM = $.jPanelMenu();

###on( )

Initializes a jPanelMenu instance. Sets up the markup, styles, listeners, and interactions, according to the options passed into the constructor function.

- **Returns:** `null`


***


###off( )

Destroys a jPanelMenu instance. Resets the markup and styles, removes listeners and interactions.

- **Returns:** `null`


***


###trigger( `animated` )

Triggers the opening or closing of the menu, depending on the current state (open or closed).

- **Parameters**
	- `animated`
		- A boolean value that determines whether or not to animate the action. The action will animate if `animated` is `true`, and will not animate if `animated` is `false`. If no value is passed in, the action will not be animated.
		- **Data Type:** `boolean`
		- **Accepted Values:** `true`, `false`
- **Returns:** `null`


***


###open( `animated` )

Triggers the opening of the menu.

- **Parameters**
	- `animated`
		- A boolean value that determines whether or not to animate the action. The action will animate if `animated` is `true`, and will not animate if `animated` is `false`. If no value is passed in, the action will not be animated.
		- **Data Type:** `boolean`
		- **Accepted Values:** `true`, `false`
- **Returns:** `null`


***


###close( `animated` )

Triggers the closing of the menu.

- **Parameters**
	- `animated`
		- A boolean value that determines whether or not to animate the action. The action will animate if `animated` is `true`, and will not animate if `animated` is `false`. If no value is passed in, the action will not be animated.
		- **Data Type:** `boolean`
		- **Accepted Values:** `true`, `false`


***


###isOpen( )

Checks the current state of the menu. Returns `true` if the menu is currently open, and `false` if it is closed.

- **Returns:** `boolean`, `true` or `false`


***


###menu

A property equal to the raw selector of the created menu object.

- **Data Type:** `string`


***


###getMenu( )

Returns the created menu object in the form of a `jQuery Object`.

- **Returns:** `jQuery Object`


***


###panel

A property equal to the raw selector of the created panel object.

- **Data Type:** `string`


***


###getPanel( )

Returns the created panel object in the form of a `jQuery Object`.

- **Returns:** `jQuery Object`



#Best Practices, Tips, and Other Good Ideas

###Progressive Enhancement

Users without JavaScript (whether they have turned it off or are using a device without it) will obviously not get the interactions provided by jPanelMenu. It&rsquo;s a good idea to take a [&ldquo;progressive enhancement&rdquo;](http://www.alistapart.com/articles/understandingprogressiveenhancement/) approach, and build your site&rsquo;s navigation to work without JavaScript running.

A good way to do that is to have your site&rsquo;s basic CSS display and style the navigation (or whatever is the content of your jPanelMenu) in an appropriate way, and use JavaScript to apply any styles that are specific to the JavaScript-enabled implementation (maybe have your site&rsquo;s JavaScript write out a `<style>` tag).

###jPanelMenu and jRespond &mdash; Perfect Together

I'm a **huge** fan of [jRespond](https://github.com/ten1seven/jRespond), which is &ldquo;a simple way to globally manage JavaScript on responsive websites.&rdquo;

jRespond and jPanelMenu are the perfect couple &mdash; use jRespond to enable and disable jPanelMenu at appropriate breakpoints, creating a truly great experience. That&rsquo;s how I almost always use jPanelMenu (that&rsquo;s how the [documentation/demo site](http://jpanelmenu.com) works), and I think you should give it a shot, too.

Responsive design is awesome on its own, but add responsive behavior to the mix, and you&rsquo;ve made something incredible.














