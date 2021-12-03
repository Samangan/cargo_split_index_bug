# Cargo Build git Split Index Bug

Cargo build is breaking when a build.rs file is present in a project with a git repo using [split indexes](https://github.com/git/git/blob/b46013950aff31b6626af96ccbf2c48469e36c66/Documentation/git-update-index.txt#L393-L416).

This repo reproduces the issue.

## Steps to Reproduce Bug
* `git config --local include.path ../.gitconfig`
* `git reset` (to trigger the index to be built using a split index)
* `cargo build`

```
error: failed to determine package fingerprint for build script for split_index_bug v0.1.0 (/.../split_index_bug)

Caused by:
  failed to determine the most recently modified file in /.../split_index_bug

Caused by:
  failed to determine list of files in /.../split_index_bug

Caused by:
  failed to open git index at /.../split_index_bug/.git/

Caused by:
  unsupported mandatory extension: 'link'; class=Index (10)
```
