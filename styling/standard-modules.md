# Standard modules

Python comes with a library of standard modules, described in a separate document, the Python Library Reference (“Library
Reference” hereafter). 

https://docs.python.org/3/library/

Some modules are built into the interpreter; these provide access to operations that are not part of the core of the language but are nevertheless built in, either for efficiency or to provide access to operating system primitives such as system calls.

## Very short overview of main modules

* OS-level
    * `os, sys, io, argparse, optparse, logging, curses, platform`
    * `ctypes, time, multiprocessing, threading, subprocess`
* String services:
    * `string, StringIO, datetime, collections, pprint`
* Numbers/calculation:
    * `numbers, math, decimal`

* Cryptographic:
    * `hashlib, hmac`
* FP:
    * `functools, operator`
* Serializing and compression:
    * `pickle, cPickle, shelve, marshal, dbm`
    * `sqlite3, json, zlib, bz2, zipfile, tarfile`

* Internet:
    * `email, mailbox, mimetools, base64, uu`
* Network:
    * `socket, selectors, asyncore, asyncio`
* Structured Markup Processing Tools
    * `HTMLParser, sgmllib, htmllib, xml.etree, xml.dom`
    * `urllib(2), (http|smtp|ftp|imap|ntp)lib`
* Development:
    * `pydoc, doctest, unittest, 2to3`
