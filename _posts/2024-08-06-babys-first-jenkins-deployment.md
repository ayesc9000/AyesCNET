---
layout: post
title: Baby's first Jenkins deployment with Jekyll
category: Development
tags:
tagline: total automation
---

Recently I have taken up an interest in managing my own deployments because of my
stubborn reasoning, but maybe that's a rant for another day. The important part
is that I decided to move my website back onto my VPS and automate its deployment
using Jenkins. I also have plans to deploy some more software in the near future
but since I'm relatively new to Jenkins I decided to start a bit smaller for now.

The plan is to use Jenkins to pull changes from my git repository containing my
website's code, build the site on the server automatically, and then deploy the
artifacts to a local nginx web server.

## What the hell is this website even made of

I wanted to avoid dealing with massive headaches caused by massive frameworks,
especially a lot of the popular JavaScript frameworks that have plagued the
internet as of recent. I also wanted to make sure this website could run in as
many places as possible, so I ended up using Jekyll to build this site.

Jekyll being a static site generator means I can just dump the resulting files
after building onto any old web server and call it a day. It does not need to
rely on a specific operating system or specific version of NodeJS or other
nonsense. However, one major downside (depending on what you use your website
for) is that being a static site generator, Jekyll cannot dynamically modify
the contents of a page in real time. In my case I don't care though so let's
continue on.

## Configuring the Jenkins project

I chose to start with a freestyle project since this project won't be very
complicated. I configured the git repository under *Source Code Management* to
point to my website's git repository.

(Image of git repository settings)

However, the problem is that Jenkins doesn't
know when the repository has been updated. If you are using GitHub, it is possible
to set up a webhook and use the GitHub Jenkins plugin to automatically trigger
a new build, but I am not able to use that here since my Jenkins is set up in such
a way that GitHub cannot talk to it. The solution? SCM polling.

Under *Build Triggers*, there is an option called *Poll SCM*. Turning it on will
display a text box where you can write a schedule to poll the repository for changes.
The schedule uses cron syntax, so you can use a website to automatically generate
you a schedule if you are too lazy to figure it out on your own, or you can steal
mine from the image below which polls every hour.

(Image of SCM polling settings)

The benefit of doing this over just rebuilding the site periodically is that
Jenkins will only start a new build if the current head has changed since the last
build took place. This means that you can poll far more often while being far
more efficent with how often you build your website.

While I am configuring the project, I also turned on *Delete workspace before build
starts* under *Build Environment* just to make sure that the workspace would always
be fresh on every build.

Lastly, I wrote up a shell script using the *Execute shell* build script to perform
the actual building of my website. Jenkins does not currently have a plugin to
manage Ruby for you at the moment, so you will need to install Ruby onto your server
and make sure all users have access to it. You will also need to install bundler
manually since Jenkins by default usually will not have permission to install gems.

```shell
sudo apt install ruby-full
gem install bundler
```

I'm using Debian 12 Bookworm here, but you can consult the (Ruby docs)[https://www.ruby-lang.org/en/documentation/installation/]
for assistance on installing Ruby on other distros.

The shell script I wrote for the build step is below:

```shell
# Build
bundle config path 'vendor/bundle' --local
bundle install
bundle exec jekyll build

# Deploy
rm -rf /var/www/html/*
cp -r $WORKSPACE/_site/. /var/www/html
```

The build portion first sets up bundle to install dependencies into a folder
named *'vendor'* in the workspace, rather than system-wide. This just avoids
having to deal with permissions problems related to bundle/gem trying to install
to a root-owned directory without giving the Jenkins user root/sudo permissions.
Afterwards, we install all the dependencies as usual.

The final part tells Jekyll to build the website. The resulting artifacts are

Note the deployment section. This deploys the site pretty primitively, but I don't
yet know if there is a better way. ^w^

Actually, speaking of deploying,

## I hate permissions

In reality, I am just bad at dealing with permissions on Linux (I grew up on Windows)
but once I got them working my third eye opened just a little more. The solution?
Restart the server.

I did not want to give Jenkins ownership over `/var/www`, so instead I used
the `www-data` group and added the Jenkins user as a member. I then set the owner
of the web directory to the `www-data` group, set the permissions accordingly,
but no dice.

Turns out that I forgot that users need to log out, then back in for the changes
to take effect, so I spent over an hour diagnosing a problem that didn't actually
exist. After a quick reboot, everything worked fine. Definately felt a little
silly there...
