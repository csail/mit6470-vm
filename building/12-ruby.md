# Ruby Setup

This document describes installing [Ruby](http://www.ruby-lang.org/), together
with commonly used Web frameworks such as [sinatra](http://www.sinatrarb.com/)
and [Ruby on Rails](http://rubyonrails.org/), as well as commonly used Ruby
gems, such as the [Sass](http://sass-lang.com/) compiler.


## Ruby, Web frameworks, and Sass

1. Install the Ruby and [Rubygems](http://rubygems.org/) packages.

```bash
sudo apt-get install -y ruby ruby-dev
```

1. Install the Ruby on Rails and Sinatra gems, for Web development.

```bash
sudo gem install rails sinatra
```

1. Install the Sass compiler and the [Compass](http://compass-style.org/)
   low-level CSS framework.

```bash
sudo gem install compass sass
```

### Commentary

Installing Rails automatically installs [bundler](http://gembundler.com/),
which is very useful for deploying Ruby code. If you skip on Rails for your
server setup, definitely install the `bundler` gem.


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
