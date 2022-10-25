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

# The real topic I wanted to blog about:

## Input types select (dropdown), radio buttons, and checkboxes.

Checkboxes are easy. They're boolean and you just add the word "checked" if true: