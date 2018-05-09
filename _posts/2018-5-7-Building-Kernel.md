---
layout: post
title: Building Linux Kernel
---

Linux v4.17 dosen't build in a breeze


Install the following packages first
    `sudo apt-get install build-essential bison flex libelf-dev libssl-dev`

To make an individual module
1. make module_prepare
2. make modules SUBDIRS=drivers/the_module_directory



