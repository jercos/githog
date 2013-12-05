githog
======

Rip a git repo quick and dirty over HTTP, without cooperation from the remote.

Githog expects to be run in an existing git repo with basic structures intact,
thus you should git init a repo, cd into it, and then run githog for maximum effectiveness.

Usage: githog http://example.com/gitrepo/.git/ refs/heads/master [bare repo path]

The first argument is a repository path, in the format of a URL to which a ref or
object path can be concatenated to make a valid URL according to LWP::Simple.

The second argument may be a bare commit hash, or a full refspec to a tag or branch,
however this is handled by githog and not by the git utilities, so the referenced object
must itself contain a commit hash, not another refspec, and as such, most cases of using
"HEAD" would not work.

Githog is meant to be run in a normal git repo, with a working tree. If this is not
the case, the bare repo path should be given, and githog should be run from one level
below the bare repo. I don't believe any actual ill would come of running it inside
a bare repo, but then you'd have to give the bare repo path as an empty string, and
that can be rather confusing to the inexperienced.

If not given, bare repo path defaults to ".git/".

After githog completes, you should be sitting in a repo ready to be checked out to
the branch you gave it, or to the commit ID. It should also contain the complete history
before that point, i.e., the parents of that commit back to the beginning of the repo.

The resulting repo from githog's run will not, however, contain any tags, branches, or
other refs save for a copy of HEAD. Githog should be safe to re-run on the same repo with a
different commit ID or refspec to more fully build up the mirror.
