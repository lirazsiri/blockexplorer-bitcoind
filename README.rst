This repository contains pre-compiled binaries of legacy bitcoin-qt
versions with a special "getblock" patch that allows bitcoin's
blockupdate.php script to get a dump of raw block data.

Why does this exist?
====================

The getblock patch was needed for older versions of bitcoin-qt because
until bitcoin-qt 0.8.X support was missing for getting raw block data.

Unfortunately the output format and RPC API for getblock in bitcoin-qt
0.8.X is substantially different from the output format produced by the
older patched bitcoin-qt, which means blockexplorer still depends on
the old patched bitcoind.

The plan is to update blockexplorer code so that it can use bitcoin-qt
0.8.X instead. Then we will no longer need this repository. Until that
happens, the older patched version is still a dependency.

Note that a workaround is required for the older patched bitcoind to be
compatible with newer versions:

http://bitcoin.org/may15.html

::

	cat /var/local/lib/bitcoin-qt/DB_CONFIG
	set_lk_max_locks 537000

	cat /var/local/lib/bitcoin-qt-testnet/testnet3/DB_CONFIG 
	set_lk_max_locks 537000
