---
layout: post
title:  "Creating a Jekyll Blog for GitHub Pages"
date:   2022-10-06 12:36:00 -0400
categories: jekyll update
---
## A very hand-holding walkthrough...

I make no claims that this is the *only way* or even the *best way* to create a Jekyll blog and post it to GitHub pages. I'm just documenting the method I used as a complete newcomer to Jekyll, Git and GitHub.

### What you need: 
- A local shell terminal (classically bash; I use Zsh) with Ruby and Git installed. Don’t try to do this on your phone.
- A free GitHub account
- Something to say

### Create local site

**First, install Jekyll**

`gem install jekyll bundler`
If your shell doesn't recognize `gem` as a command, you need to install Ruby.

**Then use Jekyll to create a site:**

`jekyll new <sitename>`

Sitename can be anything; it's just a filename, but it should not be `<git-username>.github.io` (you don't want the headaches I had doing this). It also shouldn't have spaces in it; use hyphens. Jekyll will create a new directory with that name that you can now `cd` into. *Note: in this method, the directory just created will not be your blog's final local home. If you're an expert on setting up remotes then my method is beneath you.* When you `ls`, you will see a bunch of files. The parts that are immediately relevant to you are:
`_posts/<date-of-creation>-welcome-to-jekyll.markdown`
and
`_config.yml`

The folder `_posts` is where all your posts will go; the one that’s in there is Jekyll’s default post. For ease of creating your first post, I recommend just going into the default post and replacing the content with your own. But do not remove the part that says: 
{% highlight markdown %}
---
layout: post
title:  "Welcome to Jekyll!"
date:   2022-10-05 11:38:45 -0400
categories: jekyll update
---
{% endhighlight %}
That must be at the top of every post file. Of course you can change the title (and the date if you need to), but don’t change the structure.

**Creating new posts**

When you want to create a new post, create a new file in the _posts/ folder using the filename scheme
`YYYY-MM-DD-<title>.md` where YYYY is the year, MM the month, and DD the day. Title can be anything; it's just a filename; the actual post title is defined inside the Markdown file. Remember to put your header at the top:
{% highlight markdown %}
---
layout: post
title:  "Whatever you want the title to be" 
date:   2022-10-05 11:38:45 -0400 
categories: jekyll update
---
{% endhighlight %}
For your title, the quotation marks are required. For the time, use the actual datetime in `YYYY-MM-DD HH:MM:SS -TMZN` format... the `-TMZN` is your time zone relative to GMT. Jekyll's first post should have yours already listed, so you can just copy that. I'm sure there's a tool that does this header automatically, but I'm telling you how I did it as a complete newcomeer to Jekyll and GitHub.

**Testing**

It's a good idea to see how your posts will look (and whether you did anything wrong) before publishing to GitHub. Jekyll has a live server feature that you invoke by typing:
`bundle exec jekyll serve` (make sure you are in the top-level site directory, not `_posts`)

This assmbles your raw files into an actual web page. By default, Jekyll serves on port 4000, so if you put `http://localhost:4000` into a web browser you should see your blog. You can change the theme template (there are hundreds if not thousands out there), but I haven't done that yet and we're just getting started here. You should be able to make changes to your post's Markdown file and see them by refreshing the page in the browser. When you're done looking, you can ctrl-c to stop the Jekyll server.

### Getting it on GitHub Pages

This was the trickiest part for me because I'm still learning git and GitHub. I had lots of problems that I didn't keep track of, and I'll tell you what I finally did that worked. There's certainly a better way to do this, but if you're as new to git as I was, this 'might' be a safe and easy way to do it. If you already have a GitHub Pages going, you may run into the troubles I did. If you don't already have a repo called `<your-username>.github.io` then this should work for you.

**Create a new repo on GitHub**

Go to GitHub and click on the down arrow by the plus sign at the top right of the page (just to the left of your account avatar) and select 'new repository.'

Give the new repository a name of 'your-username.github.io'. Obviously substitute your username. For example, mine is mishatuesday.github.io

Click on the blue 'Create repository' button at the bottom of the page.

You will see a blue-highlighted section at the top of the page that says 'Quick setup — if you’ve done this kind of thing before'. You want to create a README file by clicking on 'README' below the repo address. You don't have to type anything in, but you need to commit with the blue button at the bottom. You want a placeholder file to be in this repo so you can clone it to your machine. 

Once you've done that, you can click on the blue 'Code' button near the top. You want to copy the address in there. If you've never cloned a repo before, you'll probably have to use the HTTPS tab above the address; SSH is better for security, but if you haven't set that up ahead of time it won't work. Use HTTPS or take a moment to learn [how to set up SSH on GitHub][ssh-setup].

Go to your terminal with your GitHub repo address in your clipboard, make sure you're in a directory where your site can live, and type `git clone <paste address>`. Git will create a directory called `<your-username>.github.io` which will be your blog's final local home.

`cp` (or `mv`) all the files (including the directories `_posts` and `_site`) from the directory Jekyll created to the directory git just created. Then do a commit:

`git commit -am "initial commit of Jekyll blog"`

And you should now be able to `git push` and now all your Jekyll files are in your repo. One more step and it will be published for anyone in the world to see!

**Publish in GitHub pages**

Go back to your GitHub repo, and click on the 'settings' button, in the row of buttons just under the repo name at the top of the page.

On the left-hand navigation menu, click 'Pages.'

Under 'Build and deployment' use the 'Deploy from a branch' dropdown to select 'GitHub Actions.' I know it says Beta, but don't be scared. It's just because Jekyll isn't part of GitHub, so it's considered a third-party item.

Click 'Configure' under 'GitHub Pages Jekyll.' Do not change anything in the file you see. Just click the blue 'Start commit' button, then press the 'Commit new file' button.

You've just created a workflow that will build a static site from the files in your repo every time you push to it.  So the final step is to do another `git push` from your terminal, while in your site/repo directory. Then type your repo name (your-username.github.io) into a browser.

Don't panic if you see a 404 not found page.  It takes a few minutes for the build to happen and for the page(s) to get published. Obsessively refresh for up to 10 minutes until you see your blog.
### Except:

When I created this post (only my second post) and pushed to GitHub, the Jekyll workflow to build and deploy my site failed. I got an error message to the effect that the Ruby bundle failed with exit code 16. Long story short, it seems like a cross-OS issue; typing `bundle lock --add-platform x86_64-linux` in my terminal fixed the problem--thank you Gerard Morera for your answer on [Stackoverflow][stackoverflow]. On a subsequent push, the build worked, and my second post was gloriously visible (or you wouldn't be reading it now!). But I still can't tell you why the build worked the first time and broke when I added a new post. But Gerard's solution worked for me. YMMV.


*Let me know f you find anything in this walkthrough that is wrong or doesn't work as it should. My email is at the bottom of the page*

[ssh-setup]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
[stackoverflow]: https://stackoverflow.com/
