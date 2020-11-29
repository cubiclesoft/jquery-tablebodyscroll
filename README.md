jQuery Table Body Scroll
========================

This jQuery plugin heavily modifies table bodies into slick vertical scrolling solutions.  Ugly scrollbars are hidden out of sight, relying on visual indicators.  Native keyboard, scroll wheel, and touch support.

Combined with [TableCards](https://github.com/cubiclesoft/jquery-tablecards), traditional tables can be displayed on all devices in a neat, compact format.

[![Donate](https://cubiclesoft.com/res/donate-shield.png)](https://cubiclesoft.com/donate/) [![Discord](https://img.shields.io/discord/777282089980526602?label=chat&logo=discord)](https://cubiclesoft.com/product-support/github/)

Usage
-----

```html
<link rel="stylesheet" href="jquery.tablebodyscroll.css" type="text/css" media="all" />
<script type="text/javascript" src="jquery.tablebodyscroll.js"></script>
<script type="text/javascript">
$(function() {
	$('#mytable').TableBodyScroll();

	// Some optional custom event handlers.
	$('#mytable').TableBodyScroll(options).on('table:columnschanged', function() {
		$(this).trigger('tablebodyscroll:columnschanged');
	}).on('table:datachanged', function() {
		$(this).trigger('tablebodyscroll:resize');
	}).on('tablebodyscroll:sizechanged', function() {
		$(this).trigger('table:resized');
	});

	// A custom resize/visibility event handler ('child:visibility' is a custom FlexForms Extras handler emitted by an Accordion callback).
	var resizefunc = function() {
		var obj = $('#mytable');

		if (!obj.length)  $(window).off('resize', resizefunc).off('child:visibility', resizefunc);
		else  obj.trigger('tablebodyscroll:resize');
	};

	$(window).resize(resizefunc).on('child:visibility', resizefunc);
});
</script>
```

There are several live examples under "Add Entry" in the [Admin Pack Demo](http://barebonescms.com/demos/admin_pack/admin.php).

Options
-------

The following options may be passed to TableBodyScroll:

* height - An integer containing the height (Default is 60).
* heightunit - A string containing one of the standard CSS units of measurement (Default is '%').
* percentelem - An object to reference for the height measurement when heightunit is '%' (Default is window).
* postinit - A callback function to run after each TableCards initialization is run (Default is null).

To destroy the instance and restore the table to its initial state, simply call:  `$('#mytable').TableBodyScroll('destroy');`

Events
------

The following custom events may be listened for:

* tablebodyscroll:sizechanged - Notifies after resizing the table's most immediate parent.

The following custom events may be manually triggered:

* tablebodyscroll:resize - Notifies TableBodyScroll that the table has been resized.
* tablebodyscroll:columnschanged - Notifies TableBodyScroll that the table columns have changed and to rebuild any headers and footers.
