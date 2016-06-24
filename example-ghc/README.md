Demonstrates how to build a docker container for a Haskell binary.

Currently Haskell pulls in many dependencies that it doesn't really
need because the Haskell infrastructure in Nixpkgs doesn't use multiple
outputs yet.

See: https://github.com/NixOS/nixpkgs/issues/4504
