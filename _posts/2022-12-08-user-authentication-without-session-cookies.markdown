---
layout: post
title:  "User Authentication Without Session Cookies"
date:   2022-12-07 13:15:00 -0400
categories: jekyll update
---

## "Why won't this cookie persist?"

I was having trouble getting session cookies to persist in Rails. Then I
stumbled on to localStorage

*Some people will tell you that using localStorage circumvents cookie
consent laws, but this is not the case. This is not legal advice, but
whether you can store data on a user's equipment without asking has nothing to do with what method you're using, and everything to do
with whether it is* necessary *for a service or function that the user
has requested, i.e. setting dark mode or logging in.*

**The beauty of localStorage** 

When a user submits a username/password combination, you create a session
instance in your back end. In Ruby on Rails, it might look something like
this:

{% highlight ruby %}
class SessionsController < ApplicationController

    def create
        params.require(:email, :password)
        user = User.find_by(email: params[:email])
        if user&.authenticate(params[:password])
            render json: user, status: :ok
        else
            render json: {error: "Login invalid"}, status: :not_found
        end
    end
{% endhighlight}

Notice there's no `session[:anything]` in there. So how does my front end (React for instance) know that the user is logged in? 

## Easy 
There are (at least) two ways to set a localStorage key/value pair.
I use `localStorage.email = r.email`.
You can also use brackete notation: `localStorage['email'] = r.email`
When you want to get rid of it, it's `localStorage.removeItem("name")`
Or you can nuke everything in localStorage with `localStorage.clear`
In my opinion, easier than dealing with session cookies. There's no
configuration to worry about, it just works.

So here's my login function in React:

{% highlight javascript %}
    function onLogin() {
        fetch("http://localhost:3000/login", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Accept": "application/json"
            },
            body: JSON.stringify(formData)
        })
        .then(res => res.json())
        .then(r => {
            if (r.email) {
                localStorage.removeItem("error")
                localStorage.email = r.email
            } else {
                localStorage.error = "invalid email/password combination"
            }
            setFormData({email: "", password: ""})
            toggleLoggedIn()
        })
    }
{% endhighlight}

I added `toggleLoggedIn()` which sets a Boolean state variable, because I
needed some components to re-render upon login. `localStorage.error` is so my login form can conditionally render the error message if present.

Finally, my components can conditionally render elements based on whether
or not you are logged in, for instance:

{% highlight javascript %}
    return (
    <div>
        <img src={props.concession.image} alt={props.concession.name}/>
        <div>Name: {concession.name}</div>
        <div>Price: {concession.price}</div>
        {localStorage.email ? 
        <button onClick={() => deleteConcession(concession) }>Delete Concession</button>
        <NavLink to={`/concession/${props.concession.id}/EditForm`} name="Edit Concession">Edit Concession
        </NavLink> 
        : null}
    </div>
    )
{% endhighlight}

As my favorite fake user data account, David Pumpkins, would say: "Any questions?"

Actually, never mind. I probably won't answer any questions, because **I'd rather be coding.**