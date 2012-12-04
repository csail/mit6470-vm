# Ruby Setup

This document describes installing [Ruby](http://www.ruby-lang.org/), together
with commonly used Web frameworks such as [sinatra](http://www.sinatrarb.com/)
and [Ruby on Rails](http://rubyonrails.org/), as well as commonly used Ruby
gems, such as the [Sass](http://sass-lang.com/) compiler.


## Ruby Runtime

1. Install the Ruby and [Rubygems](http://rubygems.org/) packages.

```bash
sudo apt-get install -y ruby ruby-dev
```

### Commentary

Many Ruby users use [rbenv](https://github.com/sstephenson/rbenv) or
[rvm](https://rvm.io/). Ubuntu 12.10 bundles a reasonably recent MRI 1.9.3
build, so we decided to stick with it, over concerns that the indirection layer
added by `rbenv` and `rvm` will make debugging harder for beginners.

More and more forums recommend using RVM. We might end up including it, just so
that students won't think it solves whatever application problem they're having
and waste installing it on their own.


## Ruby Libraries

1. Install commonly used Ruby gems.

```bash
sudo gem install rails sinatra foreman compass sass
```

### Commentary

Installing Rails automatically installs [bundler](http://gembundler.com/),
which is very useful for deploying Ruby code. If you skip on Rails for your
server setup, definitely install the `bundler` gem.

[Compass](http://compass-style.org/) is a low-level CSS framework and can be
used in a SCSS lecture. The [foreman](http://ddollar.github.com/foreman/) gem
is used for production deployments in the Ruby lessons.


## Mechanize

1. Install libraries for processing XML and XSLT.

```bash
sudo apt-get install -y libxml2-dev libxslt-dev
```

1. Install the [Mechanize](http://mechanize.rubyforge.org/) gem.

```bash
sudo gem install mechanize
```

### Commentary

Mechanize is very useful for scraping data off of Web sites. Asides from that,
its dependency, `nokogiri`, is hard to install on its own, because it requires
`libxml` and `libxslt` headers. We pre-install both of them so students don't
have to figure them out.


## Rmagick

1. Install the [ImageMagick](http://www.imagemagick.org/) library.

```bash
sudo apt-get install -y libmagickwand-dev
```

1. Install the [Rmagick](http://rmagick.rubyforge.org/) gem.

```bash
sudo gem install rmagick
```

### Commentary

The libraries required by Rmagick are really heavy in terms of dependencies. It
is included because many tutorials reference it, and we want to spare students
the effort of figuring out how to install it correctly. Rmagick has
[many alternatives](https://www.ruby-toolbox.com/categories/image_processing),
and we might consider them in the future. A production setup should definitely
consider alternatives, as it seems that Rmagick can leak memory.
