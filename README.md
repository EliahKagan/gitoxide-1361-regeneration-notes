# gitoxide-1361-regeneration-notes

This relates to regenerating archives for https://github.com/Byron/gitoxide/pull/1361.

Note that, in spite of being unfortunately named noble-x64, the system this was done on was actually an Ubuntu 22.04 LTS (Jammy Jellyfish) system, not an Ubuntu 24.04 LTS (Noble Numbat) system. The naming was originally a mistake related to an initial plan to set up 24.04 LTS. This is not a problem, just a confusing hostname shown in the log. In particular, the version of Git used is from the git-core PPA and is a build of the latest stable version of Git (as of when this is being done). The exact package version is 1:2.45.2-0ppa1~ubuntu22.04.1.

The branch name freebsd relates to an original motivating reason for wanting the compatibility improvement conferred by changing the #! lines (see the PR). The system the archives were regenerated on is not FreeBSD either.

License for this gist: [CC0-1.0](https://creativecommons.org/publicdomain/zero/1.0/deed.en)

The following is a guide to the [files in this gist](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#files) as well as some [specific notes](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#specific-notes).

## Files

### Without the shebang change or regeneration

These are on the main branch, using generated archives as usual, to show what archives were already not used, even without any feature branch changes, i.e., to allow which files are modified in such runs to be inspected:

- [`main-branch-run-1-downgraded-git.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-run-1-downgraded-git-log)\
  A run on the main branch, on Ubuntu 22.04 LTS, using git 2.34.1.

- [`main-branch-run-2.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-run-2-log)\
  A run on the main branch, on Ubuntu 22.04 LTS, using git 2.45.2.

- [`main-branch-macos-run.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-macos-run-log)\
  A run on the main branch, on macOS 14.5, with git 2.39.3 (Apple Git-146).

### Regenerating the archives

These are logs from the session where I regenerated the archives:

- [`gitoxide-regenerate-archives-1-prep.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-gitoxide-regenerate-archives-1-prep-log)\
  Some checks and setup for regenerating the logs, such as installing git 2.45.2 from the PPA and testing it.

- [**`gitoxide-regenerate-archives-2-regenerate.log`**](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-gitoxide-regenerate-archives-2-regenerate-log)\
  **Actually regenerating the archives.**

- [`gitoxide-regenerate-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-gitoxide-regenerate-archives-log)\
  The contents of the above two files together. Kept in case it is is use, but it's hard to work with this.

### Post-checks

These are logs of manually initiated test suite runs on the feature branch that has the regenerated archives committed to it, on multiple systems, supplementing the CI checks in https://github.com/Byron/gitoxide/pull/1361:

#### Ubuntu

- [`post-regeneration-rerun-1.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-1-log)\
  On the feature branch, on Ubuntu 22.04 LTS, using the generated archives, with git 2.45.2.

- [`post-regeneration-rerun-2-ignore-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-2-ignore-archives-log)\
  On the feature branch, on Ubuntu 22.04 LTS, with GIX_TEST_IGNORE_ARCHIVES=1, with git 2.45.2.

- [`post-regeneration-rerun-3-downgraded-git.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-3-downgraded-git-log)\
  On the feature branch, on Ubuntu 22.04 LTS, using the generated archives, with git 2.34.1.

- [`post-regeneration-rerun-4-downgraded-git-ignore-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-4-downgraded-git-ignore-archives-log)\
  On the feature branch, on Ubuntu 22.04 LTS, with GIX_TEST_IGNORE_ARCHIVES=1, with git 2.34.1.

#### macOS

- [`post-regeneration-macos-run-1.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-macos-run-1-log)\
  On the feature branch, on macOS 14, using the generated archives, with git 2.39.3.

- [`post-regeneration-macos-run-2-ignore-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-macos-run-2-ignore-archives-log)\
  On the feature branch, on macOS 14, with GIX_TEST_IGNORE_ARCHIVES=1, with git 2.39.3.

#### Windows

- [`post-regeneration-windows-run-1.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-1-log)\
  On the feature branch, on Windows 10, using the generated archives, with git 2.45.1.

- [`post-regeneration-windows-run-2-ignore-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-2-ignore-archives-log)\
  On the feature branch, on Windows 10, with GIX_TEST_IGNORE_ARCHIVES=1, with git 2.45.1.

### Round 2: Regenerating one last archive on macOS

- [**`round2-add-one-macos-specific-1-regenerate.log`**](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-add-one-macos-specific-1-regenerate-log)\
  **Regenerating gix-discover/tests/fixtures/generated-archives/make_exfat_repo_darwin.tar.xz on macOS 14.5.**

### Round 2: Post-checks

#### macOS

The first clean test run on macOS after the round-2 single-archive regeneration had one failing test:

- [`round2-add-one-macos-specific-2-rerun-a-fail.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-add-one-macos-specific-2-rerun-a-fail-log)

That seems to have been due to random events, since three more separate test runs afterwards all passed:

- [`round2-add-one-macos-specific-3-rerun-b-pass.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-add-one-macos-specific-3-rerun-b-pass-log)
- [`round2-add-one-macos-specific-4-rerun-b-pass.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-add-one-macos-specific-4-rerun-c-pass-log)
- [`round2-add-one-macos-specific-5-rerun-b-pass.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-add-one-macos-specific-5-rerun-d-pass-log)

#### Ubuntu

Since only one regenerated archive was committed in round 2, I only did one retest on the original Ubuntu system.

- [`round2-post-regeneration-ubuntu.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-post-regeneration-ubuntu-log)\
  On the fast-forwarded feature branch on Ubuntu 22.04 LTS, using the generated archives, with git 2.45.2.

#### FreeBSD

The one macOS-specific regenerated archive is not releated to FreeBSD, but I had not tested regenerated archives with FreeBSD in round one, so I did it now.

- [`round2-post-regeneration-freebsd-run-1.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-post-regeneration-freebsd-run-1-log)\
  On the fast-forwarded feature branch on FreeBSD 14.0-RELEASE, using the generated archives, with git 2.45.1.

- [`round2-post-regeneration-freebsd-run-2-ignore-archives.log`](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-round2-post-regeneration-freebsd-run-2-ignore-archives-log)\
  On the fast-forwarded feature branch on FreeBSD 14.0-RELEASE, with GIX_TEST_IGNORE_ARCHIVES=1, with git 2.45.1.

## Specific Notes

### Post-testing on Ubuntu

#### Re-running on Ubuntu, using generated archives

After regenerating the archives and committing, I [did a `gix clean -xde` and ran the tests again](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-1-log) (on the same Ubuntu 22.04 LTS system, with the same command). One archive was changed:

```text
ek@noble-x64:~/repos/gitoxide (freebsd *=)$ git diff
diff --git a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
index 2602d5df0..ef4c40b7f 100644
Binary files a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz and b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz differ
```

I'm not sure why. However, this is not new. That is one of the archives that is regenerated even without `GIX_TEST_IGNORE_ARCHIVES=1` even when the tests were run on the main branch, both with the [system-provided git 2.34.1](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-run-1-downgraded-git-log) and [git-core PPA git 2.45.2](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-run-2-log) on Ubuntu as well as the [system-provided git on macOS](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-main-branch-macos-run-log). All three had the same such files:

```text
        modified:   gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
        modified:   gix/tests/fixtures/generated-archives/make_head_repos.tar.xz
        modified:   gix/tests/fixtures/generated-archives/make_status_repos.tar.xz
```

In contrast, only the first one, in `gix-diff`, differs when the tests are rerun on Ubuntu on the feature branch where the shebangs have been made more portable and the archives have been regenerated:

```text
        modified:   gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
```

#### Re-running on Ubuntu, *not* using generated archives

Rerunning on Ubuntu 22.04 LTS [without using pre-generated archives](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-2-ignore-archives-log) also passed. It modified a number of archives that don't seem to need regeneration, but I think it is common for archives that are forced to be regenerated by `GIX_TEST_IGNORE_ARCHIVES=1` to differ and thus show as modified.

### Post-testing on macOS

#### Running on macOS, using generated archives

[Running the tests on macOS 14.5 after the regenerated archives were in place](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-macos-run-1-log) worked, with all tests passing. But two archives were modified:

```text
        modified:   gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
        modified:   gix-discover/tests/fixtures/generated-archives/make_exfat_repo_darwin.tar.xz
```

The first is the one that is also modified in Ubuntu re-runs. The second appears to be modified because it was actually not regenerated at all, due the test that uses it only running on macOS.

#### Running on macOS, *not* using generated archives

[Running the tests on macOS 14.5 again, but without using pre-generated archives](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-macos-run-2-ignore-archives-log) still passes as well. As in Ubuntu, a number of archives are modified when this is done, but I think that is normal.

### Post-testing on Windows

#### Running on Windows, using generated archives

[Running the tests on Windows 10 after the regenerated archives were in place](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-1-log) worked, all tests passing and no tracked files modified.

#### Running on Windows, *not* using generated archives

[Running the tests on Windows 10 again, but without using pre-generated archives](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-2-ignore-archives-log) produced 16 failures.

Running with `GIX_TEST_IGNORE_ARCHIVES=1` has never passed all tests on Windows, so the goal here is to compare to what was failing before, as seen in https://github.com/Byron/gitoxide/issues/1358. The failures this time were:

```text
     Summary [ 805.476s] 2351 tests run: 2335 passed (17 slow, 14 leaky), 16 failed, 9 skipped
        FAIL [   7.350s] gix-glob::glob pattern::matching::compare_baseline_with_ours
        FAIL [   7.628s] gix-pathspec::pathspec parse::baseline
        FAIL [   0.045s] gix-pathspec::pathspec parse::valid::glob_negations_are_always_literal
        FAIL [   0.077s] gix-pathspec::pathspec parse::valid::whitespace_in_pathspec
        FAIL [   6.129s] gix-pathspec::pathspec search::files
        FAIL [  10.753s] gix-pathspec::pathspec search::prefixes_are_always_case_sensitive
        FAIL [ 180.981s] gix-ref-tests::refs packed::iter::performance
        FAIL [   4.751s] gix-submodule::submodule file::baseline::common_values_and_names_by_path
        FAIL [  35.035s] gix-submodule::submodule file::is_active_platform::pathspecs_matter_even_if_they_do_not_match
        FAIL [  28.607s] gix-submodule::submodule file::is_active_platform::submodules_with_active_config_are_considered_active_or_inactive
        FAIL [  21.430s] gix-submodule::submodule file::is_active_platform::submodules_with_active_config_override_pathspecs
        FAIL [  14.781s] gix-submodule::submodule file::is_active_platform::without_any_additional_settings_all_are_inactive_if_they_have_a_url
        FAIL [   9.120s] gix-submodule::submodule file::is_active_platform::without_submodule_in_index
        FAIL [  26.757s] gix::gix object::tree::diff::track_rewrites::copies_in_entire_tree_by_similarity_with_limit
        FAIL [   0.182s] gix::gix revision::spec::from_bytes::regex::find_youngest_matching_commit::regex_matches
        FAIL [   0.088s] gix::gix revision::spec::from_bytes::regex::with_known_revision::contained_string_matches_in_unanchored_regex_and_disambiguates_automatically
error: test run failed
```

Those are the exact same tests that had failed before when run this way, shown in https://github.com/Byron/gitoxide/issues/1358. So I think we are okay there, as far as proceeding with https://github.com/Byron/gitoxide/pull/1361 is concerned.

### Post-testing on FreeBSD?

I don't have the ability to run my FreeBSD system right now. I should be able to try this in the next couple of days. This might not be a blocker for proceeding with https://github.com/Byron/gitoxide/pull/1361, which has justifications beyond FreeBSD compatibility.

If and when this is done, the results should be compared to https://gist.github.com/EliahKagan/ede466f2d3f14ccc021c1c17fabd5015#file-output-txt-L2871 (as the "14 failures remaining" link points to from https://github.com/Byron/gitoxide/pull/1361).