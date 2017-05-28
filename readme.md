# skaware-void-sysdeps

This is a bundle of sysdeps directories to allow cross compilation of skalibs
on Void Linux.  The only platform for which I do not yet have sysdeps
is i686-musl.
Void doesn't distribute i686-musl packages anyway, so that's no big deal.

## Versioning

The version number of the bundle stays in sync with the
version number and revision of the Void skalibs package, to
unforeseen complications.
E.G., the first version of this bundle will be 2.5.1.1r2.
skalibs is at version 2.5.1.1, and revision 2 of the Void package
will be the first to support cross compilation.

## Process for Constructing Sysdeps

I have hosts (either native or virtual) for several platforms already,
so for those, I just run ./configure in the skalibs source directory,
and then copy over the resulting sysdeps.
If I did not have a host for a platform, I built a chroot for it from
a rootfs tarball containing both the base Void system and the base-devel
package.  I have the binfmt-support and qemu-user-static packages installed,
so I can run binaries for foreign architectures.  For each chroot,
I copy the relevant qemu-*-static binary to its usr/bin, so the
foreign binaries will run in the chroot.  Then, inside the chroot, I
create a normal user and give it a password.  I su to that user, and then
fetch and unpack the skalibs source tarball.  From here, just ./configure
in the skalibs source tree and copy, as usual.
