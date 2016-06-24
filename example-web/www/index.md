---
title: Knocker
---

    Nix + Docker = Knocker

Build (ideally) minimal docker images for deployment. Knocker copies
only the runtime dependencies of your app into the docker image. No
package manager, no shell, no glibc. Nothing else is copied unless
your application depends on it.

# Normal Mode

Docker really preferes that you have a shell available, so by
default knocker includes busybox in every image.

# Interactive Mode

Drops busybox and adds bash. Also adds some scripts to be sourced
by bash which set up a bunch of important environment variables such
as `CLASSPATH` and `PYTHONPATH`.
