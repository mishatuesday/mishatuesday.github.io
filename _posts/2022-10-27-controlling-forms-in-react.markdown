---
layout: post
title:  "Controlling Forms in React: Dropdowns, Checkboxes, and Radio Buttons"
date:   2022-10-27 16:15:00 -0400
categories: jekyll update
---
# Controlling text inputs is simple, but checkboxes and radio buttons are not alike...

OK, you already know how to control a text field... wait, maybe you don't. Maybe you came here because you were searching for that and this blog came up because I mentioned it.

OK, review of how to control a text field (scroll sideways to see all the code):

{% highlight javascript %}
// you'll need useState
import React, {useState} from 'react'
// set up a state variable to hold the value of the field, initialized to blank
const [formField, setFormField] = useState("")
// in your JSX, you use the state variable and function to set and change the field's value as the user types
<form>
<input type="text" value={formField} onChange={e => setFormField(e.target.value)}></input>
</form>
{% endhighlight %}

Of course, if you need to use that field value in a different component, you'll have to pass down a function as props to get it there... but I digress.

## The real input types I wanted to blog about:

# Select (dropdown), radio, and checkbox

**Checkboxes** are simple. They're boolean and you just add the word "checked" if true (the boolean is a state variable of course):

`<input type="checkbox" name="colors" value="red" id="red" {isRed ? "checked" : null} onChange={e => setIsRed{!isRed}}>`

Go ahead and open your dev tools *right now* (command-option-j) and see what happens when you check and uncheck this box:

<input type="checkbox" name="test-box" onChange="console.log('the checkbox changed')">
<label for="test-box">Try it!</label>

Notice how it changes when you click it AND when you unclick it... you'll notice a difference when we do radio buttons.
<hr />

**Selects** (which most people call dropdowns) are different in React than in HTML. In HTML you put the default selection in the `<option>` tag, but in React it has to go in the `<select>` tag's value attribute (which, since you're setting it from a state variable, makes it a controlled input):

{% highlight javascript %}
import {useState} from 'react'
const [size, setSize] = useState("Small")
...
  <select 
    className="form-control" 
    name="size" 
    value={size} 
    onChange={e => setSize(e.target.value)}>
    <option value="Small">Small</option>
    <option value="Medium">Medium</option>
    <option value="Large">Large</option>
  </select>
{% endhighlight %}

<hr />

I had fun figuring out **radio buttons**. Try it. Open your dev tools console (really! do it!) and click these radio buttons. I have console logs in the `onChange` attribute for each radio button:

<form>
<input type="radio" name="kingdom" id="Animal" value="Animal" onChange="console.log('Animal changed!')">
<label for="Animal">Animal</label>
<input type="radio" name="kingdom" id="Vegetable" value="Vegetable" onChange="console.log('Vegetable changed!')">
<label for="Animal">Vegetable</label>
<input type="radio" name="kingdom" id="Mineral" value="Mineral" onChange="console.log('Mineral changed!')">
<label for="Animal">Mineral</label>
</form>


Each radio button comes from a stand-alone `<input>` tags, and unlike select options they are not wrapped in any containing tag. But they *are* interrelated (due to sharing the same 'name' attribute), so unlike a checkbox, `onChange` only happens for each button when they are selected, not deselected.

To control radio buttons in React, you set a boolean for the `checked` attribute, based on your state variable. In our example:

{% highlight javascript %}
<form>
<input type="radio" name="kingdom" id="Animal" value="Animal" checked={kingdom === "Animal" ? true : false} onChange={e => setKingdom("Animal")} >
<label for="Animal">Animal</label>
<input type="radio" name="kingdom" id="Vegetable" value="Vegetable" checked={kingdom === "Vegetable" ? true : false} onChange={e => setKingdom("Vegetable")}>
<label for="Animal">Vegetable</label>
<input type="radio" name="kingdom" id="Mineral" value="Mineral" checked={kingdom === "Mineral" ? true : false} onChange={e => setKingdom("Mineral")}>
<label for="Animal">Mineral</label>
</form>
{% endhighlight %}

<hr />

The fact that every input type is handled differently in HTML and controlled differently in React can be a bit confusing, but if you play with them you
will get the hang of it. And when you do, some other, more internally-consistent language will replace HTML and all the old websites will vanish in the night, like Adobe Flash or Swatch Time.

We could complain about the inevitable obsolescence of any tech skill, but I'd rather not complain. **I'd rather be coding.**