---
layout: post
title: First Post
date: 2022-09-26 04:41:33 -0400
categories: test
---

**Read the documentation. Read the error message.**

Getting this up and running was a lot of fun. Deploying a themed Jekyll page used to be automatic through github itself, but the functionality was removed due to security issues a few weeks ago or something, so the documentation on the github site was wrong. Figuring out how to get this page up and running in a way that allowed me to actually modify it took much longer than it should have. The problem:

```
  /opt/hostedtoolcache/Ruby/3.0.4/x64/bin/bundle install --jobs 4
  Your bundle only supports platforms ["x64-mingw-ucrt"] but your local platform
  is x86_64-linux. Add the current platform to the lockfile with
  `bundle lock --add-platform x86_64-linux` and try again.
  Took   1.62 seconds
Error: Error: The process '/opt/hostedtoolcache/Ruby/3.0.4/x64/bin/bundle' failed with exit code 16
```

Why? Who knows why. The message above the error told me how to fix it though. It would have been easier to find if it wasn't in a block of text that was collapsed above the actual error though. At least it's fixed, and here I am.

Test