## Control Template
Many controls in WPF use a ControlTemplate to define the control's structure and appearance, which separates the appearance of a control 
from the functionality of the control. You can drastically change the appearance of a control by redefining its ControlTemplate.
For example, suppose you want a control that looks like a stoplight. This control has a simple user interface and functionality. 
The control is three circles, only one of which can be lit up at a time. After some reflection, you might realize that 
a RadioButton offers the functionality of only one being selected at a time, but the default appearance of the RadioButton looks 
nothing like the lights on a stoplight. Because the RadioButton uses a control template to define its appearance, 
it is easy to redefine the ControlTemplate to fit the requirements of the control, and use radio buttons to make your stoplight.

See: [Control Template Details](http://www.wpftutorial.net/templates.html)
