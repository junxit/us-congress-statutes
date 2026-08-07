# What this repository leaves out

Everything below is an upstream fact or a deliberate scope decision,
not a build failure. It is written down because an unexplained absence
reads as a build that quietly went wrong.

## Treaties, proclamations and executive agreements

The Statutes at Large prints these alongside the session laws --
13,387 of them across the 137 volumes read so far --
and none of them are here. A treaty is made by Senate ratification and
a proclamation by the President alone; neither is an act of Congress
passed by both chambers and presented for signature, which is what this
repository holds.

### Volumes that print nothing else

2 of the volumes read so far contain no session law
at all. They are not missing and they did not fail to build:
volume 7 is the Indian treaties and volume 8 the foreign treaties
and international agreements. They have no commit and no tag,
because a commit with an empty tree would say nothing and a tag
without one would point at the previous volume's text.

| Volume | Treaties and proclamations |
|---|---|
| 7 | 262 |
| 8 | 79 |

## Laws with no date

4,212 laws carry no usable date of approval anywhere in the
source: not in `<meta>`, not on the `<approvedDate>` printed in the
margin. They are committed with the rest of their volume and their
frontmatter simply has no `approved:` line, rather than being given
a guessed one.

A handful carry a date that is recorded but impossible -- volume 32
dates a law to 16 April 1110 and volume 34 dates three to January and
February 1007, in volumes covering 1901-1903 and 1905-1907. Those are
rejected and counted here rather than published as fact.

A few more are possible but wrong, and those cannot be detected at all.
One resolution in volume 2 is dated 3 March **1845** in a volume that
runs 1799 to 1813, so that commit's subject line reads
*volume 2 (1799-1845)*. The years on a commit are the first and last
dates the volume actually carries, not a correction of them.

## Dates before 1970

**Every commit for a volume that closes before 1970 is timestamped
1970-01-01.** git stores no date earlier than the Unix epoch: `git
commit` refuses `1799-03-03` outright, and writing a negative timestamp
through `fast-import` succeeds only for `git log` to render it as a
blank. That is everything up to volume 82, which is most of this
repository, so most of `git log --date` here is meaningless.

The real dates are not lost. Each commit's subject line carries the
years the volume covers, its message carries the first and last approval
date in it, and every law carries its own `approved:` date in its
frontmatter. The order of the commits is the order of the volumes.

## What is not a gap

Private laws **are** here, under `private/` in each volume. They are not
general law -- a private act relieves one named person or firm -- but
they are law, and in the older volumes they outnumber the public acts.

Marginal notes are here too, collected under a heading of their own
rather than left in the sentence. In the printed volume they sit in the
margin beside the text, and the source XML puts them inline: mid-word in
many cases, so reproducing that position would splice a note into the
middle of a clause.
