# gitoxide-1361-regeneration-notes

This relates to regenerating archives for https://github.com/Byron/gitoxide/pull/1361.

Note that, in spite of being unfortunately named noble-x64, the system this was done on was actually an Ubuntu 22.04 LTS (Jammy Jellyfish) system, not an Ubuntu 24.04 LTS (Noble Numbat) system. The naming was originally a mistake related to an initial plan to set up 24.04 LTS. This is not a problem, just a confusing hostname shown in the log. In particular, the version of Git used is from the git-core PPA and is a build of the latest stable version of Git (as of when this is being done).

The branch name freebsd relates to an original motivating reason for wanting the compatibility improvement conferred by changing the #! lines (see the PR). The system the archives were regenerated on is not FreeBSD either.

The actual run that regenerated the archives (which were then staged and committed, as also show) began at https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-gitoxide-regenerate-archives-log-L8455. Everything before that was just some pre-runs to verify some assumptions.

### Post-testing on Ubuntu

#### Re-running on Ubuntu, using generated archives

After regenerating the archives and committing, I [did a `gix clean -xde` and ran the tests again](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-log) (with the same command). One archive was changed:

```text
ek@noble-x64:~/repos/gitoxide (freebsd *=)$ git diff
diff --git a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz
index 2602d5df0..ef4c40b7f 100644
Binary files a/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz and b/gix-diff/tests/fixtures/generated-archives/make_diff_repo.tar.xz differ
```

I'm not sure why. I believe that's one of the ones that came up like that when the tests were run on the main branch, too, though.

#### Re-running on Ubuntu, not using generated archives

Rerunning on Ubuntu [without using pre-generated archives](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-rerun-ignore-archives-log) also passed. It modified a number of archives that don't seem to need regeneration, but I think it is common for archives that are forced to be regenerated by `GIX_TEST_IGNORE_ARCHIVES=1` to differ and thus show as modified.

### Post-testing on Windows

#### Running on Windows, using generated archives

[Running the tests on Windows after the regenerated archives were in place](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-txt) worked, all tests passing and no tracked files modified.

#### Running on Windows, not using generated archives

[Running the tests on Windows again, but without using pre-generated archives](https://gist.github.com/EliahKagan/e83322aba8687589df874943ad203e9f#file-post-regeneration-windows-run-ignore-archives-log) produced 16 failures.

Running with `GIX_TEST_IGNORE_ARCHIVES=1` has never passed all tests on Windows, so the goal here is to compare to what was failing before, as seen in https://github.com/Byron/gitoxide/issues/1358.

The failures this time were:

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

### Post-testing on macOS

My access to interactively usable macOS systems is limited. I can eventually test this if necessary.