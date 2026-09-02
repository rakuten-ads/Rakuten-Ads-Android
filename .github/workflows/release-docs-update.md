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
  model: claude-sonnet-4.5

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

---

# Release Docs Update

This workflow keeps the published RUNA SDK version references in the documentation in
sync whenever a release branch is opened for review.

## Context

- The pull request's head branch name follows the pattern `release/<version>`, for
  example `release/1.14.4`. The `<version>` segment is the SDK version being released.
- The documentation embeds the current published version in Gradle dependency snippets,
  for example:

  ```groovy
  implementation 'com.rakuten.android.ads:runa:1.14.3'
  ```

  These snippets currently exist in `README.md` and in several files under `doc/`
  (including the Japanese translation under `doc/ja/`).

## Instructions

1. Search the repository for every occurrence of dependencies referred in `README.md` and any Markdown file under `doc/` (this includes `doc/ja/` and other subdirectories),
  like `com.rakuten.android.ads:runa:<version>`.
2. If any of those occurrences reference a version different from the release version
   updated in the diff of current PR, update them so the dependency snippet points at the release version. 
   Do not modify any other content in these files, and do not touch files
   outside `README.md` and `doc/**/*.md`.
4. If every occurrence already matches the release version, make no changes.
5. Only push changes when at least one file was actually updated.

## Notes

- Keep edits minimal and scoped strictly to the version string inside the dependency
  coordinate; do not reformat surrounding
  text or unrelated documentation.
- Run `gh aw compile` after editing this file to regenerate the GitHub Actions workflow.
- See https://github.github.com/gh-aw/ for complete configuration options and tools
  documentation.
