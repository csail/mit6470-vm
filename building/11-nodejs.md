# Node.js Setup

This document describes installing [node.js](http://nodejs.org/) and commonly
used node packages, such as the [CoffeeScript](http://coffeescript.org/) and
[less](http://lesscss.org/) compilers.


## Node.js Runtime

1. Add a PPA with up-to-date packages.

```bash
sudo add-apt-repository -y ppa:chris-lea/node.js
sudo apt-get update
```

1. Install node.js and the [npm package manager](https://npmjs.org/).

```bash
sudo apt-get install -y nodejs npm
```

### Commentary

We're not particularly happy to use a PPA instead of official Ubuntu packages.
Unfortunately, Ubuntu 12.10 packages `node.js` 0.6, which is rather old.


## Node.js Libraries

1. Install the CoffeeScript and Less compilers.

```bash
sudo npm install -g coffee-script less watch-less
```

### Commentary

It is unfortunate that users need to learn to update packages from multiple
tools (`apt`, `npm`, `gem`, etc.) We might add a script that performs updates
across all package managers.

`watch-less` is included so it can be used during teaching. Beginners are
particularly prone to wasting a lot of time due to out of date CSS files.
