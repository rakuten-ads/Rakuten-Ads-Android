# Release Checklist

Use this checklist when publishing a new RUNA SDK version. It combines the
version bump and documentation sync into a single, repeatable flow so both
steps are requested and completed together.

## 1. Gather inputs
- [ ] Confirm the new version number (e.g. `1.14.1` → `1.14.2`).
- [ ] Collect the release notes / changelog for the new version.

## 2. Bump the version
- [ ] Update the version reference(s) in `README.md`
      (e.g. `implementation 'com.rakuten.android.ads:runa:x.y.z'`).
- [ ] Confirm the new artifact exists under `maven/com/rakuten/android/ads/`
      for the bumped version.

## 3. Sync manual documentation
- [ ] Review the release notes for any API, behavior, or setup changes.
- [ ] Update the relevant pages under `doc/` (English) to reflect those
      changes.
- [ ] Update the matching pages under `doc/ja/` (Japanese) to keep both
      locales in sync.
- [ ] Only touch documentation (`.md`) files for doc-sync-only requests —
      do not modify unrelated files (e.g. maven artifacts) unless the task
      explicitly requires a version bump too.

## 4. Review
- [ ] Diff the change set and confirm only the intended files
      (version references and/or `.md` docs) were modified.
- [ ] Open a PR summarizing the version bump and the doc updates together.

## Tips
- Request the version bump and doc sync in the same task so both are
  handled in one pass instead of separate follow-up sessions.
- State file-scope constraints (e.g. "only edit `.md` files") up front to
  avoid unintended edits to non-doc files.
