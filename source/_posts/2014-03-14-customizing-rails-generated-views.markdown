---
layout: post
title: "Customizing Rails Generated Views"
date: 2014-03-14 11:06:33 -0400
comments: true
categories: rails
---
One of my favorite things about rails is how easy it is to get simple scaffolding setup. I find in
particular that I've been using it to create administration forms for my websites. I'm working in
within an agile framework so getting a basic implementation up and running first is the priority
an rails generators are perfect for this, it creates just about everything I need to get this
basic implementation working, I can then go back with future user stories and clean stuff up.

The only downside of the rails generators is that the default styling doesn't work with the way I've customized my pages.
At first I was manually adjusting the code of the generated views to match the rest of
the views I'd already created. It wasn't that much work, but still a very tedious process and
as we are all aware most of us developers hate tedious work. One day when I was finally fed up
with this process (it didn't take long) I decided that there had to be a better way and I started looking into
creating my own generators. However, as I started looking into this I quickly discovered that rails
made simple customizations to it's generators really easy.

<!-- more -->

All you have to do to adjust the view templates is to add your own templates to `lib/erb/scaffold/` and rails generators
will start using these templates for you. To get started it's probably easiest to copy the existing templates, you can
find them in your rails gem directory within: `lib/rails/generators/erb/scaffold/templates`. If you don't know where
the rails gem directory is you can find it with this command `gem which rails` I use rvm and so for me it was located at
`~/.rvm/gems/ruby-2.0.0-p195/gems/railties-4.0.1`

Once you have those files copied into your app specific directory, it's pretty easy to figure out how to modify the files,
plus you can always check the rails docs for more information. Now whenever I run `rails generate scaffold ...` I get
views with my custom templating, saving me some tedious manual work.
