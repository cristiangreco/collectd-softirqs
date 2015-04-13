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

Options
-------

The following options may be specified in the `Module` configuration stanza:

Option|Type|Default|Description
------|----|-------|-----------
`Verbose`|Boolean|False|Enable verbose logging (not recommended)

How it works
------------

The `collectd-softirqs` plugin is very similar to the builtin [IRQ](https://collectd.org/wiki/index.php/Plugin:IRQ) plugin. It works by parsing the `/proc/softirqs` file to extract data about the number softirq handled by the kernel.

Graph example
-------------

This is an example graph created using [rrdgraph](https://oss.oetiker.ch/rrdtool/doc/rrdgraph.en.html)

![events/sec](https://github.com/cristiangreco/collectd-softirqs/raw/master/graph.png)

