# Actions: How to hide a frame

!!! example "Experimental"
    Actions are released as Experimental.
    This means that you can use them to test out future functionality, but the actual implementation is not final yet.

For basic intro into Actions, look at the [concept](/GraFx-Studio/concepts/actions/) page.

## Intro

A trigger is set to act upon the presence of a value in a variable.

This variable is a text variable, containing the old price for a discounted product.

The action will execute the change, based on the presence of a value in that variable.

![Movie](demo.gif)

### The variable

A text variable "Old price" is defined.

![screenshot](variable.png)

### The trigger

An action is defined (See [Create Actions](/GraFx-Studio/guides/actions/create/) on how to do this)

![screenshot](action-definition.png)

Step 1 is to define the trigger, that will initiate the action.

The trigger is initiated when

- the "Variable value changed", specified by the "Old price" variable, 
- or when the document is loaded (to be sure we check when opening the document)
- or when a layout is changed

![screenshot](action-triggers.png)

### Action

The script (action) executed upon the trigger

![](action.png)

``` js
	// Hide the Old price frame, Old price shape frame, Discount and Discount shape frame if the Old price variable doesn't contain a value, show them when it has a value
	let oldPriceVariable = studio.variables.getValue('Old price').toString();

	if (oldPriceVariable.trim()==="") {
		studio.frames.include('Old price', false);
		studio.frames.include('Old price shape', false);
	} else {
		studio.frames.include('Old price', true);
		studio.frames.include('Old price shape', true);
	}
```

The part starting with double "//" are comments, to give info to your future self, or colleague Template Designers working on the script.

A JavaScript variable **oldPriceVariable** is defined to hold the value of the Variable in the document, and is converted to a string (series of characters).

Then an if-statement checks if the JS variable **oldPriceVariable** contains a value.

If this is NOT the case, we set the "include" property of the frame to "false", basically hiding the frame from sight and output.

If there is content, we enable the inclusion of the frame.

### The result

When the end-user changes the value of the variable, the frame will be hidden or shown, depending on the value's presence.
