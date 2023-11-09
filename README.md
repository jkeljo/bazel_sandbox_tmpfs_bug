This reproduces what I believe to be a bug in Bazel where --sandbox_tmpfs_path
has no effect.

To repro, install Bazelisk and run `bazelisk build -s //:test`. I did this on 
Ubuntu 20.04.

Bazel will fail with "ls: cannot access '/var/tmp': No such file or directory".

Adding a `--sandbox_add_mount_pair=/var/tmp` allows this to succeed, and indeed
mounts an empty directory at `/var/tmp` rather than your real one, but it seems
like that should not be necessary.
