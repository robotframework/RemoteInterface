========================
Remote library interface
========================

This project exists to give a high level introduction to `Robot Framework
<http://robotframework.org>`_ remote library interface and to list the
`available remote servers`_.

.. contents:: Table of contents:
   :local:
   :depth: 2

Introduction
============

The remote library interface allows `Robot Framework`_ test libraries to
be run as external processes. An important use case for this support is
running test libraries on different machines than where Robot Framework itself
is executed. This allows interesting possibilities for distributed testing.

Another big use case is implementing test libraries using other languages that
Robot Framework supports natively. In practice test libraries can be
implemented using any language that supports the `XML-RPC protocol
<http://www.xmlrpc.com>`_ that the remote interface uses for communication.
Many `languages and platforms`__ are supported already, and implementing
support for new languages or for new usages is pretty straightforward.

__ `Available remote servers`_

Architecture
============

The remote interface consists of the Remote library, remote servers and
actual test libraries running behind these servers. The high level architecture
is illustrated in the picture below.

.. image:: remote.png

The Remote library is one of Robot Framework's standard libraries and thus
automatically installed with the framework. It does not have any keywords of
its own, but instead works as a proxy between Robot Framework and remote
servers.

Remote servers expose the keywords provided by the actual test libraries
to the Remote library. The Remote library and remote servers communicate
using a simple remote protocol on top of an `XML-RPC <http://www.xmlrpc.com>`_
channel. The remote protocol and the whole remote library interface are
described in detail in the `Robot Framework User Guide
<http://robotframework.org/robotframework/#user-guide>`_.
The default port used by the remote protocol is 8270 and it has been
`registered by IANA`__ for this purpose.

How remote servers interact with the actual test libraries depends on the
language and the remote server design. See the implementation of the
`available remote servers`_ below for concrete examples.

It is also possible to create solutions that combine a remote server and
one or more libraries together into a single distribution. For example,
`RemoteSwingLibrary <https://github.com/robotframework/remoteswinglibrary>`_
bundles `SwingLibrary <https://github.com/robotframework/swinglibrary>`_,
jrobotremoteserver_ and also the Remote library itself, and its users do
not even need to know that they use the remote interface.

__ http://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml?search=8270

Available remote servers
========================

Following generic remote servers are available as separate projects. See
the project pages for installation and usage instructions.

===================  =============================
Language / Platform          Remote Server
===================  =============================
Python               `PythonRemoteServer <https://github.com/robotframework/PythonRemoteServer>`_
Java                 `jrobotremoteserver <https://github.com/ombre42/jrobotremoteserver>`_
Ruby                 `robot-remote-server-rb <https://github.com/semperos/robot-remote-server-rb>`_
.NET                 `nrobotremote <https://github.com/claytonneal/nrobotremote>`_
Clojure              `robot-remote-server-clj <https://github.com/semperos/robot-remote-server-clj>`_
Clojure              `RoboZ <https://github.com/cneira/RoboZ>`_
Perl                 `plrobotremoteserver <https://github.com/daluu/plrobotremoteserver>`_
node.js              `node-robotremoteserver <https://github.com/comick/node-robotremoteserver>`_
PHP                  `phrrs <https://github.com/daluu/phrrs>`_
===================  =============================

Please submit an issue and/or pull request to this project if you have
created a new remote server or existing information needs to be updated.
