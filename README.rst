Suri-stats
==========

Introduction
------------

suri-stats is a small script based on ipython and matplotlib. It enables you to
load a suricata stats.log file. Once this is done, it is possible to graph things.

Usage
-----

Let's assume we've gota stats.log in /tmp/. Being in the suri-stats directory, one
can run ::

  ipython --pylab qt suri-stats

You will be given a shell.

First thing to do is to create on Stats object ::

  In [1]: ST=Stats("long run")
  In [2]: ST.load_file("/tmp/stats.log")


This can take some time if the file is big.

Now, it is possible to list the retrieve counters ::

  In [3]: ST.list_counters()
  Out[3]: 
  ['decoder.udp',
   'decoder.avg_pkt_size',
   'tcp.memuse',
   'tcp.segment_memcap_drop',
   'defrag.ipv6.fragments',
   'decoder.sctp',
   'tcp.reassembly_gap',
   ...
   'decoder.pppoe',
   'capture.kernel_drops',
   'tcp.synack',
   'flow_mgr.closed_pruned',
   'decoder.ipv6',
   'decoder.pkts',
   'decoder.ipv4',
   'tcp.reassembly_memuse',
   'capture.kernel_packets']

And you can now graph the value you want, successive call to plot will result in adding the graph on the output ::

  In [4]: ST.plot('tcp.reassembly_memuse')
  In [5]: ST.plot('capture.kernel_drops')
  
You can even save the file in a file ::

  In [6]: savefig("correl.png")

In fact, you can use any function of matplotlib.

The plot function
-----------------

The stats are merged by default. But it is possible display on graph per-thread ::

  In [7]: ST.plot("detect.alert", merge=False)

It is also possible to plot for one single thread ::

  In [8]: ST.plot('tcp.sessions', 'AFPacketeth310')

To get the list of threads you can use ::

  In [9]: ST.list_threads('tcp.sessions')

To start a new graph, you can use the clf() function or close the graph window.