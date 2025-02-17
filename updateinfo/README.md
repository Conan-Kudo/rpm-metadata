updateinfo.xml
==============

Purpose
-------

The optional `updateinfo.xml` meta-data file in a `yum` repository describes
package updates that are present in the repository. This meta-data can be used
by a package manager to provide a way for a user to direct the package manager
to do things such as install updates fixing a specific issue, or class of issue
such as a security update.

While initially designed just for the `yum` package manager, many third party
security tools use the `updateinfo.xml` file to learn what type of updates are
available for a particular repository, and provide functionality such as
evaluating the patching status of a machine or OS image (such as a container
image).

Representation in repomd.xml
----------------------------

The top level `repomd.xml` file will reference the updateinfo file. See the
(err... non-existent) documentation for `repomd.xml` for how this works.

History
-------

The first `updateinfo.xml` files started to appear circa 2006, and the format
has seen both evolution and variants appear.

In SuSE 10.x (released 2006, EoL 2016), a different format was used,
described as `patches.xml` (see https://en.opensuse.org/openSUSE:Standards_Rpm_Metadata_Patches ).
It is obsolete, and has not been used since SuSE 10.

Tooling to produce `updateinfo.xml` appears to vary greatly between different
Linux distributions, with the distinct possibility that no two use the same
tool. Thus, there have evolved numerous quirks to know about if constructing
generic tooling to parse `updateinfo.xml` successfully for all known `yum`
repositories.

This documentation aims to cover both how to produce an `updateinfo.xml` file
and verify its correctness, and how to parse them.

Schema
------

There are currently two defined schemas provided as XML Schema Definition (XSD) documents.
The permissive schema will validate all known real-world updateinfo files going
as far back as Fedora Core 5 era (2006). The transitional schema differs in
that its goal is to be representitive of what would be reasonable to expect
in modern (2024) repositories.

See [Permissive XML Schema for updateinfo.xml](updateinfo-permissive.xsd) and
[Transitional XML Schema for updateinfo.xml](updateinfo-transitional.xsd).

In future, a strict schema will further clarify what the content of an
updateinfo file should be and the meaning of each element and attribute.

It is always a good idea to be permissive in what you parse and strict in
what you emit.