---
layout: post
title:  "Controlling Forms in React: Dropdowns, Checkboxes, and Radio Buttons"
date:   2022-10-24 11:26:00 -0400
categories: jekyll update
---
# Controlling text is easy, but radio buttons are weird...

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

I had fun figuring out radio buttons. Try it. Open your console right now.

<form>
<input type="radio" name="kingdom" id="Animal" value="Animal" onChange="console.log('it changed!')">
<label for="Animal">Animal</label>
<input type="radio" name="kingdom" id="Vegetable" value="Vegetable" onChange="console.log('it changed!')">
<label for="Animal">Vegetable</label>
<input type="radio" name="kingdom" id="Mineral" value="Mineral" onChange="console.log('it changed!')">
<label for="Animal">Mineral</label>
</form>