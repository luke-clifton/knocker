Knocker
=======

Knocker lets you build a Docker container for your project using
Nix to define all the dependencies. Only the runtime dependencies
of your project are included in the final container, so it should
be fairly minimal.

The final image is **NOT** a NixOS container. It is nothing but your
application. It does not include the package manager, or anything
else.

Dependencies
------------

In order to run knocker you will need bash, nix, and docker installed.

Usage
-----

Knocker supports ad-hoc image creation from the command line, or
you can specify everying in a `Knockerfile`.

Simply copy the `knocker` script onto your path and set it as executable.

    $ knocker --help

    USAGE:
        knocker [OPTIONS | PACKAGE]

        PACKAGE
            Attribute of the Nix package you want to include.

        OPTIONS
            -f KNOCKERFILE
                Read this file like it was a Knockerfile. Overrides any settings
                set before it.

            -d DERIVATION
                Add a derivation directly from the store (or a symlink to one)

                Useful if you have a default.nix, and you just did a nix-build
                and would like to include the result.

                    nix-build && knocker -d result

            -i
                Set up the shell environment for interactive work.
                This includes setting up PYTHONPATH and other such things.
                
                This will cause bashInteractive to be installed instead of
                busybox.

                You will need to start programs via bash, rather than sh.

                Instead of
                    -e python
                You will need to do
                    -e '["bash", "-c", "python"]'
                or if you are lazy and don't care about two shells being launched
                    -e 'bash -c python'

            -e CMD
                Specify the command to execute when the docker image is run.
                Uses the same syntax as the CMD command in Docker.

                    -e '["ls","-l"]'
                    -e 'ls *'

            -n NIXPKGS
                Which Nixpkgs. Defaults to '<nixpkgs>'

            -w WORKDIR
                Set the working directory. Will also create the specified
                directory.

            -U USER
                Add USER to the list of users. (UID > 1000)

            -S USER
                Add system USER to the list of users (UID < 1000)

            -c SRC DST
                Copy SRC on the host to DST in the image.


Examples
--------

The `examples-*` directories demonstrate some usage examples of knocker.

Simply `cd` into the directory and run `knocker`.
