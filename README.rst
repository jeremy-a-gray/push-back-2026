.. ***************************************************************************
..
.. push-back-2026, VRC V5 2026 competition code
..
.. Copyright 2024-2026 Oakman Robotics.
..
.. All rights reserved.
..
.. ***************************************************************************

================
 Push Back 2026
================

This repo contains the competition code and supporting documents for
the Oakman Robotics entry in VEX VRC 2024-2026 Push Back
competition.

Installation
============

Create virtual environment and activate it::

  python -m venv --upgrade-deps --prompt push-back .venv
  source .venv/bin/activate

Install the project dependencies::

  poetry update

Inspect the project dependencies::

  poetry show --latest

Out of date dependencies should be scrutinized regularly for security
problems and to determine which dependencies are blocking upgrades.

The primary project dependency is ``pros-cli``, which orchestrates
compilation and transfer of all robot code, as well as configuration
of its supporting  libraries.

Building with PROS
==================

These instructions are for building the robot program with PROS on a
Linux computer.  Similar facilities exist on Windows and Mac.

Installing an ARM Cross Compiler
--------------------------------

`Download <https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads>`_
the ARM cross compiler for your platform and install it somewhere on
your path.  You probably should be using `x86_64 Linux AArch32 bare-metal
compiler (arm-none-eabi) <https://developer.arm.com/-/media/Files/downloads/gnu/13.2.rel1/binrel/arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz?rev=e434b9ea4afc4ed7998329566b764309&hash=CA590209F5774EE1C96E6450E14A3E26>`_ to cross compile from a Linux PC (x86-64) to ARM32 VEX brain.  Download the files (the first file is large):

* arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz
* arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz.asc
* arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz.sha256asc

Verify the files authenticity with::

  md5sum --check arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz.asc

or::

  sha256sum --check arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz.sha256asc

Finally, unpack the toolchain in a directory like ``${HOME}/.arm``::

  mkdir ${HOME}/.arm
  tar xJf arm-gnu-toolchain-13.2.rel1-x86_64-arm-none-eabi.tar.xz -C ${HOME}/.arm

This will unpack the toolchain into a subdirectory of
``${HOME}/.arm``.  Move the contents of that subdirectory to
``${HOME}/.arm`` and add ``${HOME}/.arm/bin`` to your path::

  export PATH=${PATH}:${HOME}/.arm/bin

Adjust the above commands to your platform and file system as
necessary.  This installation will require about 1.2 GB of space.

Creating a PROS Project
-----------------------

Use the ``pros-cli`` conductor mode to create a new project in your
(preferably empty) source directory::

  pros conductor new-project . v5 3.8.3

We will continue to use version 3 of the PROS kernel until 4 is stable
and better documented.  The above command will overwrite some existing
files so create the project first with PROS-CLI and then copy any
templates.  The initial yearly repository will have this step
completed when it is created.

Updating a PROS Project
-----------------------

Update the PROS kernel and libraries with::

  pros conductor upgrade

Stay on the current version branch of the kernel and test that the
project compiles, passes tests, uploads, and actually works on the
robot before committing.  Upgrades are best done on a new branch.

Compiling and Uploading
-----------------------

Compile the program with::

  pros make

This will fail if you do not have your ARM cross compiler installed or
in your path.  Connect either the brain or controller to the computer
via USB cable and execute::

  pros upload

Large updates, like kernel upgrades, need to be done over USB cable to
the brain while small updates (program changes) can be done wirelessly
with only the controller connected via USB cable.

Competition Notes
=================

Autonomous Mode
---------------

The following conditions must be met by an alliance to win the
autonomous win point:

#. Move from the starting line so that the robot is not touching the
   line.
#. Touch the ladder.
#. Score three rings on a stake.
#. Score rings on two different stakes.

Driver Mode
-----------

Observations from the game manual about driver control mode:

* Rings may be removed from neutral stakes.
* Rings beyond the limit for the stake are not scored.
* Climbing levels are worth 3, 6, and 12 points, respectively.
* One portable stake can be carried per robot.  There are five
  portable stakes.  Assuming every (good) robot carries one, ensure
  that the remaining one is not in your negative spot.
* Two rings can be carried per robot.  Rings on stakes do not count
  for this total.
* Robots are expandable on one side horizontally.
* Robots cannot extend vertically to cross two ladder rungs.

Copyright and License
=====================

Push Back 2026, VEX VRC 2024-2026 Competition Code.

Copyright (C) 2024-2026 `Jeremy A Gray`_ and
Oakman Robotics.

All rights reserved.

Author
======

`Jeremy A Gray`_ and Oakman Robotics 2024-2026.

.. _Jeremy A Gray: grayj2@wcslive.com
