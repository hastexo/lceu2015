## OverlayFS


An in-kernel
### filesystem
merged in Linux 3.18

Note: 3.18 landed in November 2014. OverlayFS was previously already
available in Ubuntu 14.04.


### Union mount
filesystem
Note: OverlayFS isn't the *only* union mount filesystem in existence,
among its predecessors were UFS and AUFS. OverlayFS is just the first
one that made it upstream.


#### OverlayFS
## &uarr;
#### upperdir
## &uarr;
#### lowerdir
Note: In OverlayFS we always deal with three directories directly, and
one more is internal to OverlayFS' workings.

The **OverlayFS** is the union mount at the top of the stack.

The **lowerdir** is our template or baseline directory.

The **upperdir** is a directory that stores all the files by which the
union mount differs from the lowerdir.

And finally, there's also a **workdir** that OverlayFS uses
internally, but that is not exposed to users.

In **reads**, all data that exists in the upperdir is served from
there, and anything that only exists in the lowerdir transparently
passes through.


#### OverlayFS
## &darr;
#### upperdir
## &times;
#### lowerdir

Note:
**Writes**, in contrast, never hit the lower directory, they always go
to the upper directory.

What this means is that our template lowerdir stays pristine, it is
only the upperdir that the OverlayFS mount physically modifies.


<iframe data-autoplay src="https://asciinema.org/api/asciicasts/0m3ox7hteicnxmf6woys1o4h8?speed=2&amp;size=big&amp" id="asciicast-iframe-0m3ox7hteicnxmf6woys1o4h8" name="asciicast-iframe-0m3ox7hteicnxmf6woys1o4h8" scrolling="yes"></iframe>
