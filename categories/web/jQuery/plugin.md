# Plugin

create jQuery namespace

	(function($) {

Single function plugin
	
	$.myPlugin = function () { ... };
	
Iterator plugin

	$.fn.myFunc = function(opts) {
		var options = $.extend({}, $.fn.myFunc.defaults, opts);
		return this.each(function () {
			$(this).css(...);
		};
	};

	$.fn.myFunc.defaults = {
		...
     
Traversal plugin

	$.fn.column = function() {
     
Subselector plugin

	$.extend(jQuery.expr[':'], {
		filterName: function (element, index, matches, set) {
			return true;
		}
	});
