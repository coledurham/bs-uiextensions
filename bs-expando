! function($, window, undefined) {
  'use strict';

	/**
   * Expando BS Plugin Object
   * @constructor
   * @param {objet} element - Element to turn into Expando object
   * @param {object} options - Configuration object reperesenting options to the Expando instance/object.
   */
  var Expando = function(element, options) {
    this.options = options;
    this.$body = $(document.body);
    this.$element = $(element);

    this.init(options);
  };

  Expando.VERSION = '1.0.1';

  Expando.TRANSITION_DURATION = 1500;
  Expando.OPEN = 'open';
  Expando.COLLAPSE = 'collapse';
  Expando.COLLAPSED = 'collapsed';
  Expando.TRANSITIONS = 'transitionend webkitTransitionEnd oTransitionEnd MSTransitionEnd';

  Expando.DEFAULTS = {
    transition: 1500,
    state: 'closed'
  };
  
  Expando.prototype.open = function(element){
  	return new Promise(function (resolve, reject){
     	element.removeClass('collapse');
			setTimeout(function(){
        resolve(true);
      }, 0);
    });
  };
  
  Expando.prototype.uncollapse = function(element){
  	return new Promise(function (resolve, reject){
    	element.removeClass('collapsed');
			setTimeout(function(){
        resolve(true);
      }, 0);
    });
  };
  
  Expando.prototype.close = function(element){
  	return new Promise(function (resolve, reject){
    	element.addClass('collapse');
			setTimeout(function(){
      	resolve(true);
      }, 0);
    });
  };
  
  Expando.prototype.collapse = function(element){
  	return new Promise(function (resolve, reject){
    	element.addClass('collapsed');
			setTimeout(function(){
      	resolve(true);
      }, 0);
    });
  };
  
  /**
  * Toggle individual function that closes the current expando element/s; e.g. does not toggle other expando objects states
  * @param {object} el - Current element to toggle independently
  */
  Expando.prototype.toggleIndividual = function(el) {
    var self = this;
    
		if(el.hasClass('collapse')){
    	self
    	.uncollapse(el)
      .then(self.open.bind(self, el));
    }
    else{
    	self
    	.close(el);
    }
  }

	 /**
  * Toggle singular function that closes the current expando element/s and toggles other expando elements with data-singular=true attribute
  * @param {object} element - Current element/s to target and close.
  */
  Expando.prototype.toggleSingular = function(el) {
    var els = $('[data-singular="true"]:not(.collapse)').not(el),
      self = this,
      transitionCount = 0;
      
    if(els.length){
    	//Attach one off listner for the set of existing siblings that need to be closed; avoids having to do off().on()
    	els.one(Expando.TRANSITIONS, function(curr){
				++transitionCount;
        
        if(transitionCount == els.length){
          self.toggleIndividual(el);
					transitionCount = 0;
        }
      });
      
    	self
      	.close(els);
    }
    else{
    	self.toggleIndividual(el);
    }
  }
  
	Expando.prototype.toggle = function(element){
  
  	var self = this,
      el = element || this.$element;

    if (el.attr('data-singular') && Boolean(el.data('singular')) === true) {
      this.toggleSingular(el);
    } else {
      this.toggleIndividual(el);
    }

    return true;
  };
  
  Expando.prototype.registerEvents = function(element){
  	var el = element || $('body');
    var self = this;
    
    $('.expando').on(Expando.TRANSITIONS, function(){
    	if($(this).hasClass('collapse')){
				self.collapse($(this));
      }
    });
  };

	/**
  * Init function that initializes expando plugin on element specified
  * @param {object} element - Current element to bind expando plugin to
  */
  Expando.prototype.init = function(options) {
    var $expando = this.$element,
      self = this;

		//Update transition duration if set and not equal to default.
    if (options.TRANSITION_DURATION && options.TRANSITION_DURATION != Expando.TRANSITION_DURATION) {
      var duration = (parseFloat(options.TRANSITION_DURATION / 1000).toFixed(1) + 's');
      $('.expando').css('transitionDuration', duration);
    }

		self.registerEvents();

    $expando.siblings('a.toggle').on('click', function(e) {
      //Prevent propagation and default so we can expand/close element
      e.preventDefault();
      e.stopPropagation();

      self.toggle();
    });
  };

  // expando PLUGIN DEFINITION
  // =========================

  function Plugin(option) {

    return this.each(function() {
      var $this = $(this);
      var data = $this.data('bs.expando');
      var options = $.extend({}, Expando.DEFAULTS, $this.data(), typeof option == 'object' && option);

      if (!data && /destroy|hide/.test(option)) return; //Test if no data and destroy; return
      if (!data) $this.data('bs.expando', (data = new Expando(this, options))); //If no data then creat new instance of Expando and attach
      if (typeof option === 'string') data[option](); //If option is string then execute that method;
    })
  }

  var old = $.fn.expando;

  $.fn.expando = Plugin;
  $.fn.expando.Constructor = Expando;

}(jQuery, window);
