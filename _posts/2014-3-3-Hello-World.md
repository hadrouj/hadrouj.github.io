---
layout: post
title: START A BLOG WITH GITHUB AND HUGO
published: true
---

Well well Well… this is my first post using Hugo and a really quick intro to setup it up, and publish a blog (for free) on Github.

### Hugo
Hugo is a lightning fast and simple static web pages generator, suitable for blogs, documentation pages, portfolios, etc. It has been developed with Golang, and runs on MacOs X, Windows and Linux. Pages built with Hugo can be deployed on S3, GitHub Pages, Dropbox or any web host. It’s made for people who don’t mind using a CLI to write blog posts, or to manage their website.

The full Hugo documentation is at this page: https://gohugo.io/overview/introduction/

### Installation
This tutorial doesn’t aim to replace the official install tutorial, here is the short and simplest method on MacOs X :

Install brew on your system if it’s not already there:
	$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Update Homebrew and install Hugo:
	$ brew update && brew install hugo

and… that’s it! You’re all set to run Hugo. To check Hugo’s version, just type:
	$ hugo version

### Setting Up Your Blog
Now, let’s get the most interesting part, which is creating your site and adding content to it. To create a typical site structure (scaffolding), use the subcommand ‘new site’:

	$ hugo new site myblog
We need to add a new theme (Hugo is not shipped with a default theme). So, you could start by picking one on https://themes.gohugo.io

Change your current directory to themes:

	$ cd myblog/themes
Then create a directory that contains your choosen theme :

 	$ git clone https://github.com/parsiya/hugo-octopress/
Edit your new blog configuration by changing config.toml file, present in the root of your generated site. Don’t forget to add the following line:

  	baseurl = "https://<your username>.github.io/blog"
  	languageCode = "en-us"
  	title = "Random Thoughts"
  	theme = "hugo-octopress"
Eventually customize your theme by editing theme.toml in myblog/themes/hugo-octopress directory.

### Adding new posts
Change your current directory to your site root then run:

  	$ hugo new post/new-article-title.md
Edit the file in myblog/content/post/new-article-title.md and add the content of your article in the body section (after the second +++). Here is a page to help you use the Markdown syntax in order to put your post in a desirable shape. Save the file then exit your editor.

The article you’ve just wrote will not be viewable publicly until you Undraft it:
	
    $ hugo undraft content/post/new-article-title.md
  
### Run the server

	$ hugo server -w
Fire up your favourite browser and point to http://localhost:1313, you should see your blog homepage shining with one glorious article :)

Notice the -w flag that asks hugo to watch filesystem for change and reload the site if necessary.

if you’d like to serve all posts including the ones in draft state, set the flag buildDrafts to hugo server command:

	$ hugo server --buildDrafts

### Deploy to GitHub
First off we need to generate the site content that will be published on GitHub.

	$ hugo
    Started building site
  	0 draft content
  	0 future content
  	1 pages created 
  	0 non-page files copied
  	0 paginator pages created
  	0 tags created
  	0 categories created
  	in 120 ms

Create a new directory and copy the public content from myblog/public to it:

	$ mkdir ~/myblog-public
    $ cp -r myblog/public/ myblog-public

Then initiate a Git repo, switch to gh-pages branch and set a remote:

	$ cd ~/myblog-public
    $ git init
    $ git checkout -b gh-pages
    $ git add --all
    $ git commit -m 'first article'
    $ git remote add origin https://github.com/<your username>/blog.git
    $ git push origin gh-pages

Your new blog should appear within few minutes in https://<your username>.github.io/blog
