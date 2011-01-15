---
title: Macro reference
layout: default
---

## Core macros

### BT_INIT: Initialise Build Tools autotools support

<code>BT_INIT</code>

This macro should be used at the start of your <code>configure.ac</code>,
immediately after <code>AC_INIT</code>. 

### BT_DETECT_VERSION: Automatically update package version number

<code>BT_DETECT_VERSION</code>

This macro conditionally updates the package version number based upon
version-control system information.

If the package version (<code>$PACKAGE_VERSION</code>) is not set to "trunk"
when this macro is invoked, no changes will be made at all.

If a file named <code>.release</code> exists in <code>$srcdir</code>, then
the package version will be set to its contents.

Otherwise, if the name of the version-control branch the source tree is
checked out from (if any) is not <code>master</code> or <code>trunk</code>,
the package version will be set to the name of the branch.

Alternatively, if possible, the package version will be set to the
version-control revision number or identifier.

In other words if the package version is <code>trunk</code>, <code>BT_DETECT_VERSION</code> will attempt, in order, <code>$srcdir/.release</code>, branch name (if not <code>trunk</code> or <code>master</code>), revision identifier, and finally leaving the version unchanged as <code>trunk</code>.

Currently only the Git version-control system is supported. Support for other
systems may be added in the future.

## Build configurations

### BT_CONFIG_INIT: Allow use of build configurations

<code>BT_CONFIG_INIT</code>

Build configurations are script files, stored in a <code>config</code>
directory relative to the root of the project, which pre-define sets of
<code>configure</code> options.

A build configuration file is specified on the <code>configure</code>
command line by way of the <code>--config=<em>NAME</em></code> option. The
build configurations logic will attempt to locate the named configuration
file first in <code>$builddir/config/<em>NAME</em></code> followed by
<code>$srcdir/config/<em>NAME</em></code> if the former does not succeed.

For example, a build configuration file might be named <code>DEBUG</code>, and
specify the configuration options required to generate a debugging build of
a project. Given this, you could invoke:

<code>../my-project-sources/configure --config=DEBUG</code>

If this were specified, <code>config/DEBUG</code> would be searched for
relative to the current (build) directory, and if that did not succeed,
<code>../my-project-sources/config/DEBUG</code>. If neither exists, an error
message is printed and the <code>configure</code> script is aborted.

The configuration files themselves are shell script fragments sourced by
<code>configure</code>. The following functions are defined:

<code>enable <em>OPTION</em> [<em>VALUE</em>]</code> – equivalent to <code>--enable-<em>OPTION</em>[=<em>VALUE</em>]</code>

<code>disable <em>OPTION</em></code> – equivalent to <code>--disable-<em>OPTION</em></code>

<code>with <em>PACKAGE</em> [<em>VALUE</em>]</code> – equivalent to <code>--with-<em>PACKAGE</em>[=<em>VALUE</em>]</code>

<code>without <em>PACKAGE</em></code> – equivalent to <code>--without-<em>OPTION</em></code>
