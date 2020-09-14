# SwatchBook
 A tutorial about how to create a swatch book like component that let's you open and rotate the single swatches revealing some details. We will be using CSS transforms and transitions and create a simple jQuery plugin.
 
 In this tutorial we will be using an icon font that was created with Fontello.

We will omit vendor prefixes in this tutorial. But you’ll of course find them in the files.

The Markup
For the markup we’ll have a simple structure with several divisions where each one contains an icon span and a h4:

<div id="sb-container" class="sb-container">

	<div>
		<span class="sb-icon icon-cog"></span>
		<h4><span>All Settings</span></h4>
	</div>
	
	<div>
		<span class="sb-icon icon-flight"></span>
		<h4><span>User Modes</span></h4>
	</div>	
	
	<div>
		<!-- ... -->
	</div>	
	
	<!-- ... -->
	
	<div>
		<h4><span>Profile</span></h4>
		<h5><span>We ♥ color</span></h5>
	</div>
	
</div><!-- sb-container -->
The last division will not have an icon span but instead an h4 and an h5 element. This last division will be our “cover”, the top most layer of the swatch book.

Let’s take a look at the style.

The CSS
First, let’s define the style for the containing wrapper. We’ll make it the same width like one of the swatches (although they will take up more space) so that we can easily center it:

.sb-container {
	position: relative;
	width: 150px;
	height: 400px;
	margin: 30px auto 0 auto;
}
Our aim is to create a swatch book like structure with several swatch “sheets”. Each one will be rotated using the CSS transform property (JS). So, let’s give the swatches a realistic width and height and make them absolute. Our initial state is that all swatches are stacked on top of each other. The transform-origin will define how our swatches will be rotated. Since we’ll want to use the bottom left corner for that, we’ll set a value of 25% 90%. The backface-visibility hidden will help avoiding a jagged looking text when rotating:

.sb-container div {
    position: absolute;
	top: 0;
	left: 0; 
	width: 130px;
	background: #fff;
	height: 400px;
	border-radius: 5px;
	cursor: pointer;
	text-align: center;
	background-image: url(../images/fabric.png);
	transform-origin: 25% 90%;
	backface-visibility: hidden;
}
Let’s define a different background color and box shadow for each division:

.sb-container div:nth-child(1){
	background-color: #ea2a29;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 1px 1px 1px rgba(0,0,0,0.1);
}
.sb-container div:nth-child(2){
	background-color: #f16729;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 2px 2px 1px rgba(0,0,0,0.1);
}
.sb-container div:nth-child(3){
	background-color: #f89322;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 3px 3px 2px rgba(0,0,0,0.2);
}
.sb-container div:nth-child(4){
	background-color: #ffcf14;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 4px 4px 4px rgba(0,0,0,0.2);
}
.sb-container div:nth-child(5){
	background-color: #ffea0d;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 5px 5px 6px rgba(0,0,0,0.3);
}
.sb-container div:nth-child(6){
	background-color: #87b11d;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 6px 6px 8px rgba(0,0,0,0.3);
}
.sb-container div:nth-child(7){
	background-color: #008253;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 7px 7px 10px rgba(0,0,0,0.4);
}
.sb-container div:nth-child(8){
	background-color: #3277b5;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 8px 8px 12px rgba(0,0,0,0.4);
}
.sb-container div:nth-child(9){
	background-color: #4c549f;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 9px 9px 14px rgba(0,0,0,0.4);
}
.sb-container div:nth-child(10){
	background-color: #764394;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 10px 10px 16px rgba(0,0,0,0.4);
}
.sb-container div:nth-child(11){
	background-color: #ca0d86;
	box-shadow: -1px -1px 3px rgba(0,0,0,0.1), 11px 11px 18px rgba(0,0,0,0.4);
}
We want to make it look as realistic as possible, so we’ll give the bottom most element, which is our first child, a very subtle shadow. For every following element we’ll increase that second shadow.

The last swatch will serve as a cover, so we’ll give it a special background and box shadow:

.sb-container div:last-child{
	background: #645b5c url(../images/cover.jpg) repeat center center;
	box-shadow: 
		-1px -1px 3px rgba(0,0,0,0.2),
		12px 12px 20px rgba(0,0,0,0.6),
		inset 2px 2px 0 rgba(255, 255, 255, 0.1);
}
Let’s add a little brass fastener. For that we’ll use the pseudo-class :after. It will have a gradient and a box shadow to make it look like as if it’s from metal. The position depends on the transform-origin of the swatches and since we’ve chosen the bottom left corner, we’ll set the according position of the brass fastener to be there, too:

.sb-container div:last-child:after{
	content: '';
	position: absolute;
	bottom: 15px;
	left: 15px;
	width: 20px;
	height: 20px;
	border-radius: 50%;
	background: #dddddd;
	background: linear-gradient(135deg, #dddddd 0%,#58535e 48%,#889396 100%);
	box-shadow: -1px -1px 1px rgba(0,0,0,0.5), 1px 1px 1px rgba(255,255,255,0.1);
}
Let’s style the headings:

.sb-container div h4{
	color: rgba(255,255,255,0.9);
	text-shadow: 1px 1px 1px rgba(0,0,0,0.2);
	font-weight: 700;
	font-size: 16px;
	text-transform: uppercase;
	border-top: 1px dashed rgba(0,0,0,0.1);
	border-bottom: 1px dashed rgba(0,0,0,0.1);
	margin: 5px;
	padding: 5px;
	user-select: none;
}
.sb-container div:last-child h4{
	background: rgba(0,0,0,0.2);
	box-shadow: 0 1px 1px rgba(255,255,255,0.1);
}
The big heading on the cover will be rotated and translated into the right position. This depends on the size of it, so if we were to use other words, we’d need to adjust these values:

.sb-container div:last-child h5{
	font-size: 50px;
	white-space: nowrap;
	text-align: left;
	margin: 0;
	padding: 0;
	position: absolute;
	line-height: 50px;
	top: 0px;
	left: 0px;
	color: #111;
	text-shadow: -1px -1px 1px rgba(255,255,255,0.1);
	text-transform: uppercase;
	transform: rotate(-90deg) translateX(-157%) translateY(73px);
	transform-origin: 0 0;
	user-select: none;
}
Last, but not least, let’s style the icon class. We’ll use an icon font that we have generated with Fontello (Entypo icon set). We’ll style the span and the :before pseudo-element, which will contain the characters of the icon font:

span.sb-icon{
	display: block;
	height: 70px;
	width: 70px;
	margin: 20px auto;
	user-select: none;
}
span.sb-icon:before {
	font-family: 'icons';
	font-style: normal;
	font-weight: normal;
	speak: none;
	display: block;
	text-decoration: inherit;
	text-align: center;
	text-shadow: 1px 1px 1px rgba(127, 127, 127, 0.3); 
	line-height: 64px;
	width: 100%;
	font-size: 60px;
	color: #000;
	text-shadow: 0 0 1px #000;

}
.icon-cog:before { content: '35'; } /* '5' */
.icon-flight:before { content: '37'; } /* '7' */
.icon-eye:before { content: '34'; } /* '4' */
.icon-install:before { content: '39'; } /* '9' */
.icon-bag:before { content: '36'; } /* '6' */
.icon-globe:before { content: '38'; } /* '8' */
.icon-picture:before { content: '32'; } /* '2' */
.icon-video:before { content: '30'; } /* '0' */
.icon-download:before { content: '41'; } /* 'A' */
.icon-mobile:before { content: '42'; } /* 'B' */
.icon-camera:before { content: '33'; } /* '3' */
And that’s all the style! Now, let’s make some magic!

The JavaScript
Let’s first take a look at our plugin options:

$.SwatchBook.defaults = {
	// index of initial centered item
	center : 6,
	// number of degrees that is between each item
	angleInc : 8,
	speed : 700,
	easing : 'ease',
	// amount in degrees for the opened item's next sibling
	proximity : 45,
	// amount in degrees between the opened item's next siblings
	neighbor : 4,
	// animate on load
	onLoadAnim : true,
	// if it should be closed by default
	initclosed : false,
	// index of the element that when clicked, triggers the open/close function
	// by default there is no such element
	closeIdx : -1,
	// open one specific item initially (overrides initclosed)
	openAt : -1
};
The options mean the following:

center: The index of the “centered” item, the one that will have an angle of 0 degrees when the swatch book is opened
angleInc: The space between the items (in degrees)
speed & easing: The speed and transition timing functions
proximity: The distance from the opened item to its next sibling
neighbor: The distance from the opened item’s next siblings
onLoadAnim: If true the swatch book will open with a transition on load, otherwise it will be opened by default
initclosed: If true the swatch book will be initially closed
closeIdx: The index of the item that will trigger the swatch book’s close function when clicked
openAt: The index of the item that will be opened initially
We will start by executing the _init function:


_init : function( options ) {
			
	this.options = $.extend( true, {}, $.SwatchBook.defaults, options );

	this.$items = this.$el.children( 'div' );
	this.itemsCount = this.$items.length;
	this.current = -1;
	this.support = Modernizr.csstransitions;
	this.cache = [];
	
	if( this.options.onLoadAnim ) {
		this._setTransition();
	}

	if( !this.options.initclosed ) {
		this._center( this.options.center, this.options.onLoadAnim );
	}
	else {

		this.isClosed = true;
		if( !this.options.onLoadAnim ) {
			this._setTransition();
		}

	}

	if( this.options.openAt >= 0 && this.options.openAt < this.itemsCount ) {
		this._openItem( this.$items.eq( this.options.openAt ) );
	}
	
	this._initEvents();
	
}

Here we are basically caching some elements and initializing some variables to be used later.
Also, we need to check if the swatch book will be initially opened or closed. If it should be closed, we need to set the CSS transitions for the items (_setTransition function).

Finally we load the click events on the items.


_setTransition : function() {

	if( this.support ) {
		this.$items.css( { 'transition': 'all ' + this.options.speed + 'ms ' + this.options.easing } );
	}

}

When we click on one of the items, the item will rotate so it has 0 degrees. We also need to rotate its siblings, in such way that we can read the opened item's content:


_initEvents : function() {

	var self = this;
	
	this.$items.on( 'click.swatchbook', function( event ) {
		self._openItem( $( this ) );
	} );

}

_openItem : function( $item ) {
	
	var itmIdx = $item.index();
	
	if( itmIdx !== this.current ) {

		if( this.options.closeIdx !== -1 && itmIdx === this.options.closeIdx ) {

			this._openclose();
			this._setCurrent();

		}
		else {

			this._setCurrent( $item );
			$item.css( { 'transform' : 'rotate(0deg)' } );
			this._rotateSiblings( $item );

		}

	}

}

The _rotateSiblings looks as follows:


_rotateSiblings : function( $item ) {

	var self = this,
		idx = $item.index(),
		$cached = this.cache[ idx ],
		$siblings;

	if( $cached ) {
		$siblings = $cached;
	}
	else {

		$siblings = $item.siblings();
		this.cache[ idx ] = $siblings;
		
	}

	$siblings.each( function( i ) {

		var rotateVal = i < idx ? 
			self.options.angleInc * ( i - idx ) : 
			i - idx === 1 ?
				self.options.proximity : 
				self.options.proximity + ( i - idx - 1 ) * self.options.neighbor;

		var transformStr = 'rotate(' + rotateVal + 'deg)';

		$( this ).css( { 'transform' : transformStr } );

	} );

}

Basically, we are rotating the item's next siblings in a way that these leave space for us to read the content of the item. The amount itself is defined in the options (proximity and neighbor).

If we want the swatch book to be initially closed and/or we specify an item to trigger the open/close function, the click event on that item will open/close the swatch book, depending on its current status:


_openclose : function() {

	this.isClosed ? this._center( this.options.center, true ) : this.$items.css( { 'transform' : 'rotate(0deg)' } );
	this.isClosed = !this.isClosed;

}

And that's all, I hope you like it and find it inspiring!
