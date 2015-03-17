---
layout: post
title: Debian Backporting Exact Steps
date: 2015-03-17
comments: false
---

I've been trying to learn more about building Debian packages and I've been
learning how to design printed circuit boards.  Hence, I've attempted to
backport a more recent version of kicad to Debian Wheezy!

This is a rough outline of the steps I took to do a backport:

Configure your `~/.devscripts` file to specify the GPG key you want to use by
defining `DEBSIGN_KEYID=` or be sure to pass the proper key identification
switches to `dpkg-buildpackage` or `debsign` as needed later.

Get the sources from Debian testing by adding the testing repo to your
`/etc/apt/sources.list.d directory (just a `deb-src` line as you probably don't
want to actually install packages from testing on your stable).  Then do an
`apt-get update`.  Then you can get the sources from testing with an `apt-get
source $PKGNAME=$VERSION` to get the sources for a given version.

You may need to have the backports archive setup to pull in binary packages if
the thing you're backporting has dependencies on newer libraries or whatnot.
Follow the nice instructions for adding [backports][backports] to your apt.

[backports]: http://backports.debian.org/Instructions/

Now get the build dependencies for the package you're trying to backport with
`apt-get build-dep $PACKAGE=$VERSION`.

Enter into the source directory for your package.  Update the changelog to show
that you're backporting with `dch --bpo` (and if you have dch from wheezy, it'll
show `squeeze-backports` which you should correct to `wheezy-backports`).

Then build the package with `dpkg-buildpackage` and add the `-sa` switch if you
need to include the full sources (aka, this isn't a debian software), and add
the `-j3` (adjust for your machine's number of CPUs) to parallelize the build,
and add the `-v$STABLEVERSION` switch if there has been no backport of this
package yet so that the changes file includes all the changes since the stable
version was released.

If for some reason your package didn't have its dsc and changes files signed by
`dpkg-buildpackage`, then use `debsign` to sign them now (telling `debsign`
which key to use if needed).

Now you have a full set of output .deb files, a changes file, a dsc file, and
both the upstream packaged sources and debian patches in tarballs!

Upload this to [Debian Mentors][mentors] following the
[instructions][mentorsinst] (skip to section 4).

[mentors]: https://mentors.debian.net/
[mentorsinst]: https://mentors.debian.net/intro-maintainers

Once you've uploaded the package to Debian Mentors, ask for someone to review on
the proper mailing list!
