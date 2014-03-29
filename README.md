Rig Builder
===========
A tool to build OS images in a repeatable fashion. Used primarily to seed Rig
with images that are useful.

How It Works
------------
Builder's primary purpose is to enforce repeatability in the image build
process while maintaining ease of use. It maintains specific versions of its
own dependencies in an effort to minimize the effects of version changes. It
uses [Packer](http://packer.io) for all the heavy lifting and sets constraints
around how Packer is called.

Builder has two directories related to the image build process. These are:

- *templates*: Image templates are stored in subdirectories of this path. Each
  template should have a template.json which Packer will execute. Builder will
  cd to the template's directory before calling Packer easing the use of
  relative paths in the template.json file.

- *images*: When applicable image outputs are placed in this location.

Builder keeps its cached dependencies, as well as a log of the last run, in
_.data_. The Packer cache is also kept under this location.

Calling Builder
---------------
Builder is currently called as follows:

  ./builder TEMPLATE VERSION [NAME=VALUE [...]]

- *TEMPLATE*: This is the name of a subdirectory under _templates_ containin the image definition.

- *VERSION*: This is the version of the image to build. This is passed to Packer as the _version_ user variable.

- *NAME=VALUE*: Additional user variables to pass to Packer.
