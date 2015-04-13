collectd-softirqs
=================

`collectd-softirqs` is a [Python plugin](http://collectd.org/documentation/manpages/collectd-python.5.shtml) for [Collectd](https://collectd.org) that measures the rate at which the Linux kernel handles softirqs.

Install
-------

1. Deploy the `softirqs.py` plugin into collectd's Python plugin directory (e.g. `/usr/lib/collectd/plugins/python`)
2. Configure the plugin (see below)
3. Restart collectd

Configuration
-------------

Add the following to your collectd configuration file:
```xml
<LoadPlugin python>
    Globals true
</LoadPlugin>
    
<Plugin python>
    ModulePath "/usr/lib/collectd/plugins/python"
    Import "softirqs"

    <Module softirqs>
        Verbose false
    </Module>
</Plugin>
```

Options
-------

The following options may be specified in the `Module` configuration stanza:

Option|Type|Default|Description
------|----|-------|-----------
`Softirq`|String|-|Select this softirq to be collected (may appear multiple times)
`IgnoreSelected`|Boolean|False|If this is set to `true`, all selected softirqs are ignored and all others are collected
`Verbose`|Boolean|False|Enable verbose logging (not recommended)

How it works
------------

The `collectd-softirqs` plugin is very similar to the Collectd's builtin [IRQ](https://collectd.org/wiki/index.php/Plugin:IRQ) plugin. It works by parsing the `/proc/softirqs` file to extract data about the number of softirqs handled by the kernel since boot time.

Manual run
----------

You can run `collectd-softirqs` from the command line as a simple python script. It will output something like this and exit immediately:

```
$ python softirqs.py 
HRTIMER:4949
SCHED:1834967
BLOCK_IOPOLL:21
NET_TX:2920
RCU:1985467
TIMER:2095671
HI:68181
NET_RX:936
TASKLET:2829290
BLOCK:93491
```

This could be useful to get an idea of the values the plugin parses and dispatches to collectd.

Graph example
-------------

This is an example graph (a mostly idle system) created using [rrdgraph](https://oss.oetiker.ch/rrdtool/doc/rrdgraph.en.html):

![events/sec](https://github.com/cristiangreco/collectd-softirqs/raw/master/graph.png)

