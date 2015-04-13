collectd-softirqs
=================

collectd-softirqs is a [Python plugin](http://collectd.org/documentation/manpages/collectd-python.5.shtml) for [Collectd](https://collectd.org) that measures the number of softirqs handled by the kernel

Install
-------

1. Deploy the `softirqs.py` plugin into collectd's Python plugin directory (e.g. `/usr/lib/collectd/plugins/python`)
2. Configure the plugin (see below)
3. Restart collectd

Configuration
-------------

Add the following to your collectd config

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
