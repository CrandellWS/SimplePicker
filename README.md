#Overview
SimplePicker is a pure HTML5 Canvas/JavaScript color picker. No external images. No reliance on external frameworks (such as jQuery). No CSS (unless you add your own). Released under the
terms of the MIT License.

Minimal usage requires two HTML 5 Canvas elements (one for hue, one for saturation and lightness) and one arbitrary HTML element to show the selected color (the background color of the element will be set to the chosen color). 

Text fields for displaying the chosen color in RGB and HSL format, and
HTML5 range controls (sliders) can also be specified if desired.

#Basic usage:

	<script src="SimplePicker.js"></script>
	<script type="text/javascript">

	function setupPicker(){
		var mypicker = new SimplePicker("huewell","slwell","resultwell");	
	}

	</script>

	<body onload="setupPicker();">
		<canvas id="huewell" width="200" height="20">></canvas><p />
		<canvas id="slwell" width="400" height="400"></canvas><p />
		<div id="resultwell" width="50" height="50"> </div>
	</body>

#Usage with HTML5 range ("slider") controls:

	<script src="SimplePicker.js"></script>

	<script type="text/javascript">

	function setupPicker(){
		var mypicker = new SimplePicker("huewell","slwell","resultwell");
		mypicker.setRGBRangeControls("red","green","blue");
		mypicker.setHSLRangeControls("hue","saturation","lightness");
	
	}

	</script>

	<body onload="setupPicker();">


		<canvas id="huewell" width="200" height="20">></canvas><p />
		<canvas id="slwell" width="400" height="400"></canvas><p />
		<div id="resultwell" width="50" height="50"> </div> 

		Red: <input type="range" min = "0" max ="255" step="1" id="red"  /><br />
		Green: <input type="range" min = "0" max ="255" step="1" id="green" /><br />
		Blue: <input type="range" min = "0" max ="255" step="1" id="blue" /><br />
		Hue: <input type="range" min = "0" max ="360" step="1" id="hue"  /><br />
		Saturation: <input type="range" min = "0.0" max ="1.0" step="0.01" id="saturation" /><br />
		Lightness: <input type="range" min = "0.0" max ="1.0" step="0.01" id="lightness" /><br />

	</body>

#Usage with HTML5 range controls and text input fields:


	<script src="SimplePicker.js"></script>

	<script type="text/javascript">

	function setupPicker(){
		var mypicker = new SimplePicker("huewell","slwell","resultwell");
		mypicker.setRGBRangeControls("red","green","blue");
		mypicker.setHSLRangeControls("hue","saturation","lightness");
		mypicker.setHSLInput("hslval");
		mypicker.setRGBInput("rgbval");
	
	}

	</script>

	<body onload="setupPicker();">


		<canvas id="huewell"  width="200" height="20">></canvas><p />
		<canvas id="slwell" width="400" height="400"></canvas><p />
		<div id="resultwell" width="50" height="50"> </div> 

		Red: <input type="range" min = "0" max ="255" step="1" id="red"  /><br />
		Green: <input type="range" min = "0" max ="255" step="1" id="green" /><br />
		Blue: <input type="range" min = "0" max ="255" step="1" id="blue" /><br />
		Hue: <input type="range" min = "0" max ="360" step="1" id="hue"  /><br />
		Saturation: <input type="range" min = "0.0" max ="1.0" step="0.01" id="saturation" /><br />
		Lightness: <input type="range" min = "0.0" max ="1.0" step="0.01" id="lightness" /><br />
	
		RGB: <input type="text" id="rgbval" value = "unknown"/> HSL:<input type="text" id="hslval" value = "unknown"/><br />

	</body>

#Styling

You're free to apply any CSS styling that fits into your application's design (but see the note below about the size of the canvas
elements).

#Caveats

You should set the width and height for the canvas elements explicitly in the code, rather than relying on CSS (otherwise you may
run into scaling issues).

There are some unavoidable issues relating to conversion between different color spaces. RGB components are quantized (integers between 0-255 inclusive),
while HSL components are continuous (0-360 degrees for hue, 0.0-1.0 for saturation and lightness). This can produce small rounding errors.

In addition, for certain values of lightness (0% and  100%), hue is essentially meaningless. 0% is black and 100% lightness is white, regardless of the hue. That means that more than one setting of for HSL will correspond to the same screen color, and may produce a hue "jump" under certain conditions.


#API:

**SimplePicker(hueElementId,satvalElementId,wellElementId)**

Constructs a new SimplePicker object. 

Parameters: 

*hueElementId, satvalElementId* should be the ids of HTML5 Canvas elements. 

*wellElementId* should be the id of any HTML element which supports the backgroundColor (JavaScript)/background-color (CSS) property.
	
		
		
**SimplePicker.setRGBInput(rgbInputId)**

Binds a text input field to the current color. It will be updated automatically as the color is changed.


Parameter:

*rgbInputId* should be the id of an HTML text input field

	
		
**SimplePicker.setHSLInput(hslInputId)**

Binds a text input field to the current hue, saturation and lightness. It will be updated automatically as the color is changed.

Parameter:

*hslInputId*  should be the id of an HTML text input field
		
		

**SimplePicker.setRGBRangeControls(redRangeId,greenRangeId,blueRangeId)**

Binds HTML5 range controls ("sliders") to the current RGB values.

Parameters:

redRangeId,greenRangeId,blueRangeId should be the ids of HTML5 range controls with min 0, max 255, and step 1.
		
		

**SimplePicker.setHSLRangeControls(hueRangeId,saturationRangeId,lightnessRangeId)**

Binds HTML5 range controls ("sliders") to the current HSL values.

Parameters:

*hueRangeId,saturationRangeId,lightnessRangeId* should be the ids of HTML5 range controls. *hueRangeId* should have min 0, max 360, and a step
appropriate for the precision you need (1 is a good starting point).

*saturationRangeId* and *lightnessRangeId* should have min 0, max 1.0 and an appropriate step (0.01 is a good starting point)
	
		
		
**SimplePicker.getRGBString()**

Returns the current RGB value as an HTML hex color code (e.g. #FF00FF)

Parameters:

none

	
	
**SimplePicker.getRGB()**

Returns the current RGB values as a three-element JavaScript array (each in the range [0,255]).

Parameters:

none
	
		
		
**SimplePicker.getHSL()**

Returns the current HSL values as a three-element JavaScript array (hue in the range [0,360], saturation and lightness in the range [0,1.0])

Parameters:

none
		
		
		
**SimplePicker.setRGB(red,green,blue)**

Sets the current components in RGB color space. 

Parameters:

*red,green,blue* are the new RGB values in the range 0-255
	
		
		
**SimplePicker.setRed(red)**

Sets the current red value in RGB color space.

Parameters:

*red*: the new red value (range 0-255)
	
		

**SimplePicker.setGreen(green)**

Sets the current green value in RGB color space.

Parameters:

*green*: the new green value (range 0-255)

	

**SimplePicker.setBlue(blue)**

Sets the current blue value in RGB color space.

Parameters:

*blue*: the new blue value (range 0-255)

		

**SimplePicker.setHSL(hue,saturation,lightness)**

Sets the current components in HSL color space.

Parameters:

*hue*: the new hue (range 0-360)

*saturation*: the new saturation (range 0.0-1.0)

*lightness*: the new lightness (range 0.0-1.0)

		
**SimplePicker.setHue(hue)**

Sets the current hue in HSL color space.

Parameters: 

*hue*: the new hue (range 0-360)
	
		
		
**SimplePicker.setSaturation(saturation)**

Sets the current saturation in HSL color space.
	
Parameters: 

*saturation*: the new saturation (range 0.0-1.0)
		
		

**SimplePicker.setLightness(lightness)**

Sets the current lightness in HSL color space.

Parameters:

*lightness*: the new lightness (range 0.0-1.0)

		
