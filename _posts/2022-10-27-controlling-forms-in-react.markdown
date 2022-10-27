---
layout: post
title:  "Controlling Forms in React: Dropdowns, Checkboxes, and Radio Buttons"
date:   2022-10-27 16:15:00 -0400
categories: jekyll update
---
# Controlling text inputs is simple, but checkboxes and radion button are not alike...

OK, you already learned how to control a text field... wait, maybe you don't. Maybe you came here because you were searching for that and I came up because I mentioned it.

OK, review of how to control a text field:

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

Of course, if you need to use that field value in a different componenet, you'll have to pass down a function as props to get it there... but I digress.

## The real input types I wanted to blog about:

# Select, radio, and checkbox

Checkboxes are easy. They're boolean and you just add the word "checked" if true (the boolean is a state variable of course):

`<input type="checkbox" name="colors" value="red" id="red" {isRed ? "checked" : null} onChange={e => setIsRed{!isRed}}>`

Selects are different in React than in HTML. In HTML you put the default selection in the `<option>` tag, but in React it has to go in the `<select>` tag:

{% highlight javascript %}
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

I had fun figuring out radio buttons. Try it. Open your console (command-option-j). You should see console logs when you click these buttons:

<form>
<input type="radio" name="kingdom" id="Animal" value="Animal" onChange="console.log('Animal changed!')">
<label for="Animal">Animal</label>
<input type="radio" name="kingdom" id="Vegetable" value="Vegetable" onChange="console.log('Vegetable changed!')">
<label for="Animal">Vegetable</label>
<input type="radio" name="kingdom" id="Mineral" value="Mineral" onChange="console.log('Mineral changed!')">
<label for="Animal">Mineral</label>
</form>

They are independent `<input>` tags, but they are interrelated, so unlike a checkbox, `onChange` only happens for each button when they are selected, not deselected.

To control radio buttons in React, you set a boolean for the `checked` attribute, based on your state variable. In our example:

{% highlight javascript %}
<form>
<input type="radio" name="kingdom" id="Animal" value="Animal" onChange={e => setKingdom("Animal")} checked={kingdom === "Animal" ? true : false}>
<label for="Animal">Animal</label>
<input type="radio" name="kingdom" id="Vegetable" value="Vegetable" onChange={e => setKingdom("Vegetable")} checked={kingdom === "Vegetable" ? true : false}>
<label for="Animal">Vegetable</label>
<input type="radio" name="kingdom" id="Mineral" value="Mineral" onChange={e => setKingdom("Mineral")} checked={kingdom === "Mineral" ? true : false}>
<label for="Animal">Mineral</label>
</form>
{% endhighlight %}

The fact that every input type is handled differently in HTML and controlled differently in React can be a bit confusing, but if you play with them you
will get the hang of it. And when you do, some other, more internally-consistent language will replace HTML and all the old websites will vanish in the night, like Adobe Flash or Swatch Time.

We could complain about the inevitable obsolescence of any tech skill, but I'd rather not complain. **I'd rather be coding.**