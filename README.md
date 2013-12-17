duckbill
========

Duckbill is a thread-pool system for Ettercap to facilitate platypus (by pierce) to more efficiently steal creds from your targets via browser same-origin exploits.  Keeping a MitM on general purpose hardware for a whole /23 or larger heavily used network (think convention wifi) is expensive and slow.  This will almost certainly ellicit concern from users.

Instead, we use a thread-pool system to keep a small pool of ettercap instances active against a subset of the network.  duckbill will call back to platypus to determine whether it has received credentials from the target, in which case duckbill will cylce the ettercap instance for a new IP on the network.  After some timeout, duckbill will just release the ettercap instance and move onto a new target.

Requirements
============

* Ruby >= 1.9.3
* Ettercap
* arp-scan

Gems

* thread

Usage
=====

The most basic usage of duckbill uses the following syntax, it assumes that platypus is listening on localhost:8000 with a 5 second wait between call-backs and a time-to-Mitm per host of 60 seconds.  The interface flag is the only required option.

./duckbill.rb -i [Network interface]

Other options:

* -v | --verbose		Enable the verbose flag for extra messaging
* --manager [HOST]:[PORT]	Your running platypus instance for marking hosts to target for exploitation 
* --sleep			Amount of time (in seconds) to wait before calling back to platypus to determine whether or not to move to the new target
* --ttl				Amount of time (in seconds) to run a MitM against a single host

Future work
===========

Assuming this is a worhtwhile exercise, this is something that deperately needs to be optimized; either by rewriting this in pure C or as a proper extension to ettercap.
