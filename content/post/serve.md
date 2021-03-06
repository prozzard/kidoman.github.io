---
categories: ["software"]
date: 2014-04-10 06:00:00+05:30
description: "A simple command line file/directory server built with Go."
title: "Introducing Serve"
tags:
  - golang
  - webserver
  - simple
  - elegant
  - homebrew
  - cli
  - software
aliases:
  - /software/serve.html
disqus_url: http://kidoman.io/software/serve.html
---

Sometimes, it takes a great deal of effort to create something simple.

* What is the smallest feature set you can support and still be useful?
* How elegant should the implementation be?

These are the typical questions which would come to your mind when aiming for simplicity.

Well, here is my dedication to the shrine of [simplicity](http://www.infoq.com/presentations/Simple-Made-Easy).

## What is this?

**Serve** makes serving static content out of directories **simple**.

Why would you want to do this?

```
python -m SimpleHTTPServer 8080
```

When you can just do this:

```
serve .
```

**Serve** is a single binary. Easy installed via [Homebrew](http://brew.sh/) with a single command:

```
brew install kidoman/tools/serve
```

(there are a few other ways of installing Serve, including but not limited to precompiled binaries. But they are much better documented at the [Github repo](https://github.com/kidoman/serve))

## How to use

Provided you have ```serve``` under your $PATH somewhere:

```
serve .
```

This will serve the current directory at ```http://localhost:5000/```

```
serve -p 9999 ~/my-awesome-blog
```

Will serve the contents of the folder ```~/my-awesome-blog``` at ```http://localhost:9999/```

```
serve -x /my ~/precious
```

You guessed it, ```http://localhost:5000/my``` is now wired up to ```~/precious```

```
serve -o ~/sesame
```

Wires up ```http://localhost:5000``` to ```~/sesame``` and opens the URL in your favorite browser while it is at it.

## Next Steps

The next logical thing would be to allow the ```serve``` functionality to be used by simply importing the package. But it totally depends on the simplicity of the change! Happy serving.
