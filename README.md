This relates to regenerating archives for https://github.com/Byron/gitoxide/pull/1361.

Note that, in spite of being unfortunately named noble-x64, the system this was done on was actually an Ubuntu 22.04 LTS (Jammy Jellyfish) system, not an Ubuntu 24.04 LTS (Noble Numbat) system. The naming was originally a mistake related to an initial plan to set up 24.04 LTS. This is not a problem, just a confusing hostname shown in the log. In particular, the version of Git used is from the git-core PPA and is a build of the latest stable version of Git (as of when this is being done).

The branch name freebsd relates to an original motivating reason for wanting the compatibility improvement conferred by changing the #! lines (see the PR). The system the archives were regenerated on is not FreeBSD either.

The actual run that regenerated the archives (which were then staged and committed, as also show) began at https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-gitoxide-regenerate-archives-log-L8455. Everything before that was just some pre-runs to verify some assumptions.

After regenerating the archives and committing, I did a `gix clean -xde` and ran the tests again (with the same command). One archive was changed:

```text
ek@noble-x64:~/repos/gitoxide (freebsd *=)$ git diff
diff --git a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
index 2602d5df0..ef4c40b7f 100644
Binary files a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz and b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz differ
```

I'm not sure why. I believe that's one of the ones that came up like that when the tests were run on the main branch, too, though.