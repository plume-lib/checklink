This directory contains:
 * a slightly modified version of the
   [W3C Link Checker](http://search.cpan.org/dist/W3C-LinkChecker/).
 * the file `checklink-args.txt`, which contains useful command-line
   arguments for the `checklink` program that reduce false positive warnings.
 * the program `checklink-persistent-errors`, which processes multiple runs
   of `checklink` and outputs only the errors that appear in all of the
   runs.  This lets you ignore transient errors due to network flakiness or a
   host being down temporarily.

These are described in more detail below.


# Prerequisites

You need to have CSS/DOM.pm installed (get it from CPAN).


# checklink

The checklink program reports broken links.  You can run it periodically,
and fix any broken links in webpages that you maintain.

This version of checklink uses a locally-cached version of DTDs rather than
requesting them from `www.w3.org`.

Many webpages refer to DTDs that are hosted at `www.w3.org`.  However, that
webserver intentionally throttles requests, which can make the link checker
take hours instead of seconds to run.


# checklink-args.txt

This is a set of command-line arguments to the checklink program, that
suppress spurious warnings and thus make the output easier to scan for real
problems.  Run `checklink` like this:

```
   checklink -q -r `grep -v '^#' checklink-args.txt` MYURL
```

There are certain checklink warning that you do not want to see, because
they are not important or you cannot fix them.  Removing them from the
output enables you to find the interesting results more easily.
Examples include:
 * There is a redirect, but you wish to refer to the original URL rather than the redirected one.
 * A URL is unreadable by a web-crawling robot such as `checklink`, but the URL works from a web browser.
 * Archived, historical data has broken links that you don't care about.
 * A program generates slightly broken webpages, and you do not wish to see the related errors.


# checklink-persistent-errors

This script reports errors that persist over multiple runs of the
checklink program, ignoring transient errors.

If a web server is temporarily down or there is a transient network
failure, `checklink` will report a broken link.  It is a waste of your time
to investigate such reports.  You want to see `checklink` output only when
you need to update your own webpages.

The `checklink-persistent-errors` program lets you run `checklink` multiple
times, and it only reports errors that occurred every time.

There is more
[documentation](https://raw.githubusercontent.com/plume-lib/checklink/master/checklink-persistent-errors)
at the top of file, including examples of commands you could put in your
crontab to run the link checker periodically.
