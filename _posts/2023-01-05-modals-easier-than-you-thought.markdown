---
layout: post
title:  "Modals: Easier Than You Thought!"
date:   2023-01-05 13:15:00 -0400
categories: jekyll update
---

You've seen this: you click on a button and a form seems to pop up. The rest of the screen goes dark and there's a smallish box in the center of the page with a product view, or a form to fill out, or some breakout detail that you asked for. You click 'done' or whatever, and the box disappears and the screen is no longer dark. THIS WAS NOT A POPUP.

## It was a modal.

Pronounced MODE-ull. Or mo-DOLL. Maybe mode-OWL? No one seems to agree on how to say it, but a modal is a box with content that seems to "pop up" out of nowhere and return to nowhere when you're done with it. And they are INCREDIBLY EASY TO DO!

## It's just conditional rendering and styling.

All it takes to create a modal is:
1) Some content in an element that can be displayed and hidden based on some event
2) Styling to darken the rest of the page and show the content in the middle of the screen.

As an example, let's take a generic example in React. We create a state variable set to Boolean for whether or not the modal should be visible. Then we add event listeners to toggle `showModal` between true and false:

{% highlight javascript %}
    function mainComponent() {
        const [showModal, setShowModal] = useState(false)

        return (
            <>
            <h1>This is the main page we're on</h1>
            <button onClick={() => setShowModal(true)}>show modal</button>
            {
                showModal ?
                <div className="modal">
                    <div className="modal-content">
                        <p>This is the modal! It could be a separate component, but it doesn't have to be!</p>
                        <button onClick={() => setShowModal(false)}>hide modal</button>
                    </div>
                </div>
                :
                null
            }
            </>
        )
    }
{% endhighlight %}

That's it for logic. Just one Boolean state value to either show it or not. The rest is done with styling. Notice there are two class names in the modal element: `modal`, and `modal-content`. You could get fancier than that and have a modal-header, modal-footer, etc. But let's keep it simple for now. The `modal` class takes up the whole page and uses rbga background color to darken the screen, and the `modal-content` class sets the content in the middle of the page:

{% highlight javascript %}
.modal {
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0,0,0,0.8);
  display: flex;
  flex-direction: column;
  align-items: center;
}

.modal-content {
  max-width: 500px;
  background-color: #fff;
  padding: 5px;
  font-size: 12px;
}
{% endhighlight %}

And that's the essentials. Conditional display with modal styling will give you that pop-up feeling without any actual pesky pop-ups. Cuz this is not the 90's.

I'd like to come up with a catchy and funny way to end this blog post, but the truth is, **I'd rather be coding.**