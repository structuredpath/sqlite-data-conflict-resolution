# Customizable Conflict Resolution for SQLiteData

This repository tracks the effort to support **customizable conflict resolution** for CloudKit sync in [SQLiteData](https://github.com/pointfreeco/sqlite-data). The work started in the umbrella discussion [\#272](https://github.com/pointfreeco/sqlite-data/discussions/272) and has since unfolded across issues, pull requests, and design conversations in the upstream repository, so the discussion no longer reflects the latest state. This page collects the current status of all related work, the queue of planned pull requests, and the open design topics.

## Links

- [CloudKit docs for SQLiteData](https://swiftpackageindex.com/pointfreeco/sqlite-data/main/documentation/sqlitedata/cloudkitsync) — Official documentation for CloudKit synchronization in SQLiteData
- [structuredpath/sqlite-data](https://github.com/structuredpath/sqlite-data) — Fork where the implementation happens
- [sqlite-data-sync-notes](https://github.com/structuredpath/sqlite-data-sync-notes) — Notes on SQLiteData’s current CloudKit sync behavior and a conceptual model for built-in conflict resolution
- [`Mergeable` protocol in Forked](https://drewmccormack.github.io/Forked/Forked/documentation/forked/mergeable) — Merging protocol from the Forked framework
- [Conflict resolution in Ensembles 3](https://mentalfaculty.github.io/Ensembles3/Ensembles/documentation/ensembles/conflictresolution) — Conflict resolution in the Ensembles framework
- [Ensembles 3’s SwiftData integration](https://mentalfaculty.github.io/Ensembles3/Ensembles/documentation/ensembles/swiftdataintegration/) — Conflict resolution in Ensembles’ SwiftData integration

## Activity

| Date | Type | Ref | Title/Description | Status |
|---|---|---|---|---|
| 2025‑10‑23 | Discussion | [\#272](https://github.com/pointfreeco/sqlite-data/discussions/272) | **Customizable conflict resolution for CloudKit sync (umbrella discussion)** | 🔄 Ongoing |
| 2025‑10‑24 | Issue | [\#273](https://github.com/pointfreeco/sqlite-data/discussions/273) | Date equality mismatch due to millisecond rounding differences between SQLite and CloudKit (converted to discussion as #wontfix) | ✅ Fixed in [\#387](https://github.com/pointfreeco/sqlite-data/pull/387) |
| 2025‑10‑24 | Issue | [\#274](https://github.com/pointfreeco/sqlite-data/discussions/274) | Data divergence between devices after concurrent offline edits | 🟠 Open |
| 2025‑11‑30 | Issue | [\#315](https://github.com/pointfreeco/sqlite-data/issues/315) | CloudKit bug with non-atomic saves behaving as atomic | ✅ Workaround implemented |
| 2025‑12‑09 | Comment | [\#244](https://github.com/pointfreeco/sqlite-data/discussions/244#discussioncomment-15203862) | Per-field macros in table types for sync engine configuration (encryption) | ➡️ See [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) |
| 2025‑12‑22 | Comment | [\#336](https://github.com/pointfreeco/sqlite-data/pull/336#issuecomment-3680256359) | Reaction to PR’d support for non-encrypted fields via `SyncEngine.init` | ➡️ See [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) |
| 2026‑01‑01 | Discussion | [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) | Macro-based CloudKit configuration via `@SyncedTable`/`@SyncedField` | ✅ API confirmed |
| 2026‑01‑02 | PR | [\#353](https://github.com/pointfreeco/sqlite-data/pull/353) | ~~Improve MergeConflictTests coverage and naming~~ | ➡️ Superseded by [\#411](https://github.com/pointfreeco/sqlite-data/pull/411) |
| 2026‑01‑02 | Issue | [\#354](https://github.com/pointfreeco/sqlite-data/issues/354) | Violation of “last edit wins” conflict resolution strategy | 🟠 Open |
| 2026‑01‑08 | Slack Post | n/a | Update on my work on customizable conflict resolution | ✅ Answered |
| 2026‑01‑13 | PR | [\#370](https://github.com/pointfreeco/sqlite-data/pull/370) | **Three-way merge model for built-in conflict resolution for CloudKit sync** | 📝 Draft |
| 2026‑01‑28 | Comment | [\#386](https://github.com/pointfreeco/sqlite-data/pull/386#issuecomment-3813266210) | Role of last-known server record & explanation of conflict-on-fetch scenario | ✅ Next step identified |
| 2026‑02‑27 | Slack Post | [Screenshot](slack/2026-02-27-sqlite-data-plans.png) | Discussion about timeline and plans for SQLiteData in 2026 | ✅ Timeline outlined, call offered |
| 2026‑03‑03 | PR | [\#410](https://github.com/pointfreeco/sqlite-data/pull/410) | ~~Fix metadatabase crash in tests on macOS 15~~ | ➡️ Superseded by [\#508](https://github.com/pointfreeco/sqlite-data/pull/508) |
| 2026‑03‑03 | PR | [\#411](https://github.com/pointfreeco/sqlite-data/pull/411) | Set `CKRecord.modificationDate` in `MockCloudDatabase` | 🟠 Open |
| 2026‑03‑04 | PR | [\#412](https://github.com/pointfreeco/sqlite-data/pull/412) | ~~Fix `MockCloudDatabase` record mutation in modify callback~~ | ➡️ Superseded by [\#507](https://github.com/pointfreeco/sqlite-data/pull/507) |
| 2026‑03‑05 | PR | [\#414](https://github.com/pointfreeco/sqlite-data/pull/414) | **Overhaul of merge conflict tests** | 📝 Draft |
| 2026‑05‑19 | Fork PR | [\#1](https://github.com/structuredpath/sqlite-data/pull/1) | Reconciliation for no-ancestor case, contributed by Drew McCormack as a discussion PR on my fork | ✅ Ideas adopted |
| 2026‑07‑23 | Comment | [\#506](https://github.com/pointfreeco/sqlite-data/pull/506#issuecomment-5108352240) | Observations on third-party fix for sync divergence when `userModificationTime` stamps tie | ✅ OP agreed with more structured approach |
| 2026‑07‑23 | PR | [\#507](https://github.com/pointfreeco/sqlite-data/pull/507) | Return copied `CKRecord`s when modifying `MockCloudDatabase` (Brandon’s replacement of [\#412](https://github.com/pointfreeco/sqlite-data/pull/412)) | ✅ Merged |
| 2026‑07‑24 | PR | [\#508](https://github.com/pointfreeco/sqlite-data/pull/508) | Fix in-memory metadatabase creation in `defaultMetadatabase` (reframes [\#410](https://github.com/pointfreeco/sqlite-data/pull/410)) | 🟠 About to be merged |
| 2026‑07‑24 | PR | [\#510](https://github.com/pointfreeco/sqlite-data/pull/510) | Deliver latest record state in `ModifyRecordsCallback` test helper | ✅ Merged |

## Next Steps

- Await merge of [\#508](https://github.com/pointfreeco/sqlite-data/pull/508)
- Await feedback for [\#411](https://github.com/pointfreeco/sqlite-data/pull/411)
- Submit PR for mocking `CKRecord.recordChangeTag` (`pr3`, depends on [\#411](https://github.com/pointfreeco/sqlite-data/pull/411))
- Finalize [\#414](https://github.com/pointfreeco/sqlite-data/pull/414) for review
- Submit PR for reconciliation aka two-way merge test coverage (`pr1`, depends on [\#414](https://github.com/pointfreeco/sqlite-data/pull/414))
- Submit PR fixing conflicts favoring the client over a newer server, addressing #354 (`pr2`, depends on [\#414](https://github.com/pointfreeco/sqlite-data/pull/414))
- Submit PR removing the last-known server record update from the send path (`pr4`, depends on [\#414](https://github.com/pointfreeco/sqlite-data/pull/414) and `pr1`)

## Open Topics

- **Conflict-on-fetch handling.** Agreement is needed on how conflicts detected during fetch should be handled, likely through custom ancestor tracking rather than relying on the parameters of the `.serverRecordChanged` error.
- **Role of the last-known server record.** Does it represent the last confirmed server state, or the most up-to-date record we have, including before we’ve even sent the record to iCloud? Should it serve as the ancestor in a three-way merge? Can we drop the eager store of in-flight records?
- **Macro infrastructure.** Design and implementation of the `@SyncedTable`/`@SyncedField` macros for configuring the sync engine.

## Future Tasks

- Ensure timestamp update for conflicts where both sides remove a value (see `sameFieldRemoval_conflictOnSend_clientNewer` test)
- Ensure the client-newer value wins during reconciliation when no last-known server record exists (see `reconciliation_fetchBeforeSend_clientNewer` and `reconciliation_sendBeforeFetch_clientNewer` tests)
- Align `CKRecord`’s print representation with `RowVersion` (`@123` instead of 📅)
