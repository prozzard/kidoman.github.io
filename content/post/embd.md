---
categories: ["framework"]
date: 2014-04-24 06:00:00+05:30
title: "Introducing EMBD"
description: "A superheroic embedded programming framework."
tags:
  - golang
  - embedded
  - hardware
  - raspberry-pi
  - bbb
  - hal
aliases:
  - /framework/embd.html
disqus_url: http://kidoman.io/framework/embd.html
---

**[EMBD](https://github.com/kidoman/embd)** is a framework for **Go** which does **GPIO** (General Purpose I/O), talks the **I²C** protocol (+ many more) and provides the drivers necessary to interact with **many hardware sensors** (eg. gyroscope, magnetometer, barometer, etc.) It's non-intrusive API allows you to quickly prototype solutions (see below for example) without sacrifising production-worthiness. And the best part? The code will run on a multitude of supported hosts (like the Raspberry Pi, and the BeagleBone Black) without change!

http://embd.kidoman.io<br>
https://github.com/kidoman/embd

{{< vimeo 92990437 >}}

Although the framework started its life as **go-rpi**, we soon realized the potential of making it even more useful. The driver code we had written to talk to a [plethora of sensors](https://github.com/kidoman/embd#sensors-supported) were not really dependent on the Raspberry Pi. They expected a I²C bus and not much else. So we immediately started thinking of ways in which we could allow people to leverage all that code in other platforms which Golang ran on (which turned out to be [quite a few](https://github.com/kidoman/embd#platforms-supported).)

## API Design

We spent a bunch of time fine tuning the "feel" of the API. We have aimed to provide both **real world usability** (we did not want a toy feel to the API) and the ability to be be used for quick/rapid hardware prototyping.

For example, it leans towards rapid prototyping when needed:

```go
func main() {
  for {
    embd.LEDToggle("LED0")
    time.Sleep(250 * time.Millisecond)
  }
}
```

Or, gives you the control when necessary:

```go
func main() {
  panicIf(embd.InitLED())
  defer embd.CloseLED()

  led, err := embd.NewLED("LED0")
  if err != nil {
    panic(err)
  }
  defer led.Off()

  // Cleanly exit if someone hits Ctrl-C
  quit := make(chan os.Signal, 1)
  signal.Notify(quit, os.Interrupt, os.Kill)

  for {
    select {
    case <-time.After(250 * time.Millisecond):
      panicIf(led.Toggle())
      fmt.Println("Toggled")
    case <-quit:
      return
    }
  }
}

```

It currently has good support for the Raspberry Pi and the BeagleBone Black, with support for other platforms coming in the near future. This should almost guarentee that the particular combination of prototyping board, sensors, etc. would most probably work OOTB with EMBD.

## Summary

**EMBD** is a bold attempt at creating a cross platform embedded programming library. A lot of work is needed to flesh out the sensor library and to bring in support for new hosts. The [ROADMAP](https://github.com/kidoman/embd/blob/master/ROADMAP.md) lists some of the short/long terms goals we have ahead of us, but we won't get too far down that list without the support of the community. So looking forward to those [pull requests](https://github.com/kidoman/embd/pulls)! Also, while we have done our best, if you do come across a bug, please [let us know](https://github.com/kidoman/embd/issues) so that we can tackle it in the best way possible. And if you need any help, we will be hanging around [here](https://groups.google.com/forum/#!forum/go-embd).

To read the backstory, read [this]({{< relref "post/embd-behind-the-scenes.md" >}}) article as well.

## Links

Homepage: http://embd.kidoman.io/<br/>
Github: https://github.com/kidoman/embd
