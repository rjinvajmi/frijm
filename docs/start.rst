##########################
The ``native Lua`` Project
##########################

|version-badge|_ \
|appveyor-badge|_ \
|cirrus-badge|_ \
|azure-badge|_ \
|readthedocs-badge|_ \
|license-badge|_ \
|code-style-black-badge|_

**Lua on the platform you use with the compiler you choose**

`Lua` is multi-paradigm programming language. `Lua` is cross-platform as it is
written in ANSI C. `Lua` is licensed under `MIT`_ license. `native Lua`\ s goal
is to deliver a framework to build `Lua` on any platform with any compiler.

For information on `Lua` see `Lua.org`_.

********
Overview
********

As default `Lua` requires ``gcc`` and ``make`` to be installed to build the
`Lua` binaries, therefore building for e.g., Linux or other POSIX systems where
``gcc`` and ``make`` are natively available is easy. Building `Lua` on Windows
with MinGWs' ``gcc`` and some sort of ``make`` is also straight forward.

But this does not allow a good platform and compiler independent way of
building and testing `Lua`. Especially testing is not that simple as it should
be. Therefore this project tries to implement a platform and compiler
independent way of building **and** testing `Lua`.

******
How-To
******

Building `Lua` with the `native Lua` project requires Python 3.5 or greater and
some C compiler.

.. image:: _static/basic-cmds.gif
   :alt: alternate text

*********************************
Supported Platforms And Compilers
*********************************

The current release supports the following platform/compiler combinations:

+----------+-----------------------+-------------------------------+
| Platform | Official Lua Releases | `native Lua` Releases         |
+==========+=======================+===============================+
| aix      | gcc                   | xlc*, gcc*, clang*            |
+----------+-----------------------+-------------------------------+
| bsd      | gcc                   | see OpenBSD and NetBSD        |
+----------+-----------------------+-------------------------------+
| OpenBSD  | see bsd               | gcc, clang                    |
+----------+-----------------------+-------------------------------+
| NetBSD   | see bsd               | gcc*, clang*                  |
+----------+-----------------------+-------------------------------+
| c89      | gcc                   | all compilers*                |
+----------+-----------------------+-------------------------------+
| FreeBSD  | gcc                   | gcc, clang                    |
+----------+-----------------------+-------------------------------+
| generic  | gcc                   | gcc (not win32), msvc (win32) |
+----------+-----------------------+-------------------------------+
| linux    | gcc                   | gcc, clang, icc*              |
+----------+-----------------------+-------------------------------+
| macOS    | gcc                   | gcc, clang                    |
+----------+-----------------------+-------------------------------+
| MinGW    | gcc                   | see win32                     |
+----------+-----------------------+-------------------------------+
| posix    | gcc                   | TODO                          |
+----------+-----------------------+-------------------------------+
| solaris  | gcc                   | gcc*, clang*                  |
+----------+-----------------------+-------------------------------+
| win32    | see MinGw             | msvc, gcc, clang              |
+----------+-----------------------+-------------------------------+
| cygwin   | no                    | gcc, clang                    |
+----------+-----------------------+-------------------------------+

\* means not or not fully tested.

******************************************
Repository Structure And Code Organization
******************************************

The repository is structured into the parts described below.

Root Directory
==============

The root directory contains the

- general project documentation (``README.md``, ``CHANGELOG.md``)
- build script and build toolchain (``wscript``, ``waf``, ``waf.bat``),
- required Python packages (``requirements.txt``, ``environment.yml``),
- CI scripts (``.appveyor.yml``, ``.cirrus.yml``, ``azure-pipelines.yml``,
  ``readthedocs.yml``),- editor configurations (``.vscode``, ``.editorconfig``),
- coding and general guidelines (``pyproject.toml``),
- licensing information (``LICENSE``),
- and information on the ``native Lua`` project and the lua version
  (``VERSION``).

``demos`` Directory
===================

Some scripts demonstrating what can be done with Lua. These demos should not
use libraries that do not come with the Lua interpreter.

``docs`` Directory
==================

This directory contains the `native Lua` project documentation as well as the
official Lua documentation. The official Lua documentation is found in
``_static/doc``. This documentation is also linked into the project
documentation. The main documentation files ``index.rst``, ``conf.py`` and
``doxygen.conf`` are found here. Contribution guidelines are found in
``contributing.rst``.

`native Lua` uses the `ReadTheDocs Sphinx theme`_ ``sphinx_rtd_theme`` as
layout theme for the documentation.

``src`` Directory
=================

This directory contains the source files downloaded from `Lua.org`_. Trailing
whitespace and additional newlines at the end of the files are removed.
Furthermore the native Lua header is included (see
`_native_lua_config.h <src/_native_lua_config.h>`_).

Changes are indicated by the following comment:

.. code-block:: C

   /* native Lua */

The lua interpreter (``lua.c``) as well as the lua compiler (``luac.c``) have
been changed, to indicate, that they were build based on the `native Lua`
project:

.. code-block:: bash

   $ build/gcc/lua -v
   Lua 5.4.0  Copyright (C) 1994-2017 Lua.org, PUC-Rio [based on native Lua (0.5.0-devel), https://github.com/swaldhoer/native-lua]

``tests`` Directory
===================

This directory contains the source files downloaded from `Lua.org`_. Trailing
whitespace and additional newlines at the end of the files are removed.

..  note::

   The encoding of test files **must not** be changed.

Some tests require changes to the test files in order to work on platforms.
Changes are indicated by the following comment:

.. code-block:: lua

   -- native Lua

Test files for the build toolchain have been added in ``tests/build``.

*****
Links
*****

Documentation
=============

The documentation can be found on `readthedocs.io`_.

Continuous Integration
======================

- Azure Pipelines: Linux (GCC, Clang), MacOS (Clang, GCC), Windows (MSVC, GCC, Clang)
- AppVeyor: Windows (Cygwin GCC, Cygwin Clang)
- Cirrus CI: Linux (GCC, Clang), FreeBSD(Clang, GCC)
- ReadTheDocs.org: Documentation

On Azure Pipelines' Windows build we also run |black|_ and |pylint|_.

*******
License
*******

`native Lua` is licensed under the terms of the MIT license.

----

.. _lua.org: https://www.lua.org/
.. _MIT: https://www.lua.org/manual/5.3/readme.html#license
.. _lua_readme: https://www.lua.org/manual/5.3/readme.html

.. _waf.io: https://www.waf.io

.. _readthedocs.io: https://native-lua.readthedocs.io/en/latest/

.. _ReadTheDocs Sphinx theme: https://github.com/readthedocs/sphinx_rtd_theme

.. |black| replace:: ``black``
.. _black: https://black.readthedocs.io/en/stable/

.. |pylint| replace:: ``pylint``
.. _pylint: https://www.pylint.org/

.. |version-badge| image:: https://img.shields.io/github/v/tag/swaldhoer/native-lua
.. _version-badge: https://github.com/swaldhoer/native-lua/releases/latest

.. |appveyor-badge| image:: https://ci.appveyor.com/api/projects/status/1gtcdi6wslxx3d6u/branch/master?svg=true
.. _appveyor-badge: https://ci.appveyor.com/project/swaldhoer/native-lua/branch/master

.. |cirrus-badge| image:: https://api.cirrus-ci.com/github/swaldhoer/native-lua.svg
.. _cirrus-badge: https://cirrus-ci.com/github/swaldhoer/native-lua

.. |azure-badge| image:: https://dev.azure.com/stefanwaldhoer/native-lua/_apis/build/status/swaldhoer.native-lua?branchName=master
.. _azure-badge: https://dev.azure.com/stefanwaldhoer/native-lua/

.. |readthedocs-badge| image:: https://readthedocs.org/projects/native-lua/badge/?version=latest
.. _readthedocs-badge: https://native-lua.readthedocs.io/en/latest/?badge=latest

.. |license-badge| image:: https://img.shields.io/github/license/swaldhoer/native-lua.svg
.. _license-badge: https://github.com/swaldhoer/native-lua/blob/master/LICENSE

.. |code-style-black-badge| image:: https://img.shields.io/badge/code%20style-black-000000.svg
.. _code-style-black-badge: https://github.com/python/black
