*@sivel did a terrific job on speedtest-cli.py -- thank you very much!*

Thought it would be helpful to have a **wrapper which creates one-line results for a log file. It is formatted as CSV** for analysis and graphing. Here's a sample output:

```
$ speedtest --log
2015-03-13, 21:21, 24.761, 0.57, 0.30
2015-03-14, 08:30, 24.862, 0.50, 0.26
2015-03-14, 11:05, 23.887, 0.49, 0.29
```

With no arguments or with --simple, we would have seen:

```
$ speedtest
2015-03-14, 11:05, 23.887, 0.49, 0.29

$ speedtest --simple 
Ping: 22.602 ms
Download: 0.62 Mbit/s
Upload: 0.25 Mbit/s
```

The wrapper script, written in Bash, is available here: [https://github.com/rsvp/speedtest-linux](https://github.com/rsvp/speedtest-linux) -- and *it always uses the most current version of speedtest-cli.py.*

Feel free to incorporate it into the main repo.

