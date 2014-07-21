---
layout: post
title: "Tailing remote log files on OS X"
date: 2014-07-21 12:18:27 -0400
comments: true
categories: osx ssh logs
---

I wanted to share how I deal with watching remote log files on our production server.

First, I ssh to the server, tail the log, and pipe the output to a file on my local machine.

``` bash
$ ssh server "tail -f /path/to/production.log" >> ~/Library/Logs/prod.log &
[1] 87094
```

The ```&``` at the end of the command will run the process in the background so you don't have to keep a terminal
window open with no output. When you run the command it will return a process id you can use to kill the process
later.

``` bash
$ kill -9 87094
```

Now that we have a local log file updating in real time, we can use the built-in Console.app to watch the log.
In Console.app, open your local log file by going to _File > Open Quickly > Files > ~/Library/Logs > prod.log._

I usually drag Console.app to my second monitor and give it a desktop of it's own. Since I will typically keep
higher priority apps up on my second monitor it's useful to know when the log is being written to. Console.app
has a preference to do this, just goto _Console.app > Preferences_ and check _Animate the application icon_ or
_Bring log window to front, send back after:_ (whichever is least annoying for you).


