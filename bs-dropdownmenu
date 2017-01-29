!function($, window, undefined){
	'use strict';
  
  var SubMenu = function (element, options) {
    this.options             = options;
    this.$body               = $(document.body);
    this.$element            = $(element);
    
    this.init(options);
  };
  
  SubMenu.VERSION  = '1.0.0';

  SubMenu.TRANSITION_DURATION = 300;
  SubMenu.BACKDROP_TRANSITION_DURATION = 150;
  SubMenu.OPEN = 'open';

  SubMenu.DEFAULTS = {
    keyboard: true,
    show: true
  };
  
  SubMenu.prototype.toggle = function(element){
  	var self = this,
    	_element = element || this.$element;
      
    console.log('self is :: ', self);
    
    self.$element.toggleClass(SubMenu.OPEN);
  };
  
  SubMenu.prototype.init = function(options){
  	var $submenu = this.$element,
    	self = this;
    
		$submenu.siblings('a.toggle').on('click', function(e){
    	//Prevent propagation and default so we can expand/close element
      e.preventDefault();
      e.stopPropagation();

      self.toggle();
    });
  };
  
    // TOOLTIP PLUGIN DEFINITION
  // =========================

  function Plugin(option) {
    return this.each(function () {
      var $this   = $(this)
      var data    = $this.data('bs.tooltip')
      var options = typeof option == 'object' && option

      /*if (!data && /destroy|hide/.test(option)) return
      if (!data) $this.data('bs.tooltip', (data = new SubMenu(this, options)))
      if (typeof option == 'string') data[option]()*/
      
      new SubMenu(this,options);
    })
  }

  var old = $.fn.tooltip

  $.fn.submenu = Plugin;
  $.fn.submenu.Constructor = SubMenu;
  
}(jQuery, window);

$(document).ready(function(e){
	$('.submenu').submenu({});
});
