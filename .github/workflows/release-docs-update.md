---
on:
  pull_request:
    types: [opened, synchronize, reopened]

if: startsWith(github.event.pull_request.head.ref, 'release/')

permissions:
  contents: read
  pull-requests: read

engine:
  id: copilot
  # Pin an explicit model: the `auto` alias cannot be resolved when the model
  # catalog request is rejected, which aborts the agent before it starts.
  model: gpt-5.6-sol

tools:
  github:
    toolsets: [repos, pull_requests]

network: defaults

safe-outputs:
  push-to-pull-request-branch:
    target: "triggering"
    if-no-changes: "ignore"
    allowed-files:
      - "README.md"
      - "doc/**/*.md"
    protected-files:
      exclude:
        - "README.md"

---

# Release Docs Update

This workflow keeps the published RUNA SDK version references in the documentation in
sync whenever a release branch is opened for review.

## Context

- The pull request's head branch name follows the pattern `release/<version>`, for
  example `release/1.14.4`. The `<version>` segment is the default SDK version being
  released; individual modules in a release may have their own version.
- The documentation embeds the current published version in Gradle dependency snippets,
  for example:

  ```groovy
  implementation 'com.rakuten.android.ads:runa:1.14.3'
  ```

  These snippets currently exist in `README.md` and in several files under `doc/`
  (including the Japanese translation under `doc/ja/`).

## Instructions

1. Inspect the current pull request diff and determine every published Maven module
   whose version was changed by this release (for example `runa`,
   `runa-gad-adapter`, `runa-extension`, or `normalizer`). For each module, determine
   its new release version from the diff or the release metadata. Do not assume that
   the branch version applies to every module.
2. Search `README.md` and every Markdown file under `doc/` (including `doc/ja/` and
   all nested directories) for dependency coordinates matching
   `com.rakuten.android.ads:<module>:<version>`.
3. For each changed module, update only occurrences whose version differs from that
   module's new release version. Leave dependencies for modules that were not changed
   in this release untouched. Do not modify any other content, and do not touch files
   outside `README.md` and `doc/**/*.md`.
4. If all relevant occurrences already match their modules' release versions, make no
   changes.
5. Only push changes when at least one file was actually updated.

## Notes

- Keep edits minimal and scoped strictly to the version string inside the dependency
  coordinate; do not reformat surrounding
  text or unrelated documentation.
- Run `gh aw compile` after editing this file to regenerate the GitHub Actions workflow.
- See https://github.github.com/gh-aw/ for complete configuration options and tools
  documentation.
