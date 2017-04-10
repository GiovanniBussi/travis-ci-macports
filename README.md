[![Build Status](https://travis-ci.org/GiovanniBussi/travis-ci-macports.svg?branch=master)](https://travis-ci.org/GiovanniBussi/travis-ci-macports)

# Travis-CI MacPorts

[Travis-ci](https://travis-ci.org) is great and allows you to test your [GitHub](https://github.com) projects on OSX.
However, OSX images on Travis-ci only come with Homebrew installed.
If, like me, you want to use [MacPorts](https://www.macports.org/),
you should install it on the fly everytime.
For a few projects I am working on I copied scripts around.
I decided to share here a generic script that could be used in multiple projects.
The script is checked frequently on [Travis-ci](https://travis-ci.org/GiovanniBussi/travis-ci-macports),
so you should be able to see from the status image above whether it is working or not.

Installing MacPorts
-------------------

Put the following commands in your `.travis.yml` file:

     - export COLUMNS=80
     - wget https://raw.githubusercontent.com/GiovanniBussi/travis-ci-macports/master/install.macports
     - ./install.macports

If you prefer, you can directly include the `./install.macports` file in your github repository.
Setting the number of columns is required for MacPorts to
be able to download some distfiles.

The `./install.macports` script can  be run with a few options:

     --prefix=/other/prefix
         Install MacPorts in a different location. Default is `/opt/local`.
     --source
         Install MacPorts from source (slower). It is implicit when
         using `--prefix` with a prefix different from `/opt/local`.
     --binary
         Install MacPorts from a pkg (faster, this is the default).
     --version=2.4.1
         Require a specific MacPorts version. Notice that
         MacPorts is anyway updated with a `selfupdate` command.

Using your local Portfiles
-------------------------------

In case you just need ports to install tools that are used in your project,
you are done. If you want to also setup a 
[local Portfile repository](https://guide.macports.org/chunked/development.local-repositories.html) to test your own Portfiles you might do the following:

     - wget https://raw.githubusercontent.com/GiovanniBussi/travis-ci-macports/master/configure.macports
     - ./configure.macports path/to/port/dir

After this command, you will be able to install packages described in your local Portfiles.
Notice that local Portfiles will take the precedence with respect to official Portfiles.

Feedbacks
---------

In case you find any problem or you think you can improve this script, please open an
[issue](https://github.com/GiovanniBussi/travis-ci-macports/issues/new)
or a [pull request](https://github.com/GiovanniBussi/travis-ci-macports/pulls).



