# Customizable Conflict Resolution for SQLiteData

This repository tracks the effort to support **customizable conflict resolution** for CloudKit sync in [SQLiteData](https://github.com/pointfreeco/sqlite-data). The work started in the umbrella discussion [\#272](https://github.com/pointfreeco/sqlite-data/discussions/272) and has since unfolded across issues, pull requests, and design conversations in the upstream repository, so the discussion no longer reflects the latest state. This page collects the current status of all related work, the queue of planned pull requests, and the open design topics.

## Links

- [CloudKit docs for SQLiteData](https://swiftpackageindex.com/pointfreeco/sqlite-data/main/documentation/sqlitedata/cloudkitsync) — Official documentation for CloudKit synchronization in SQLiteData
- [structuredpath/sqlite-data](https://github.com/structuredpath/sqlite-data) — Fork where the implementation happens
- [structuredpath/sqlite-data-sync-notes](https://github.com/structuredpath/sqlite-data-sync-notes) — Notes on SQLiteData’s current CloudKit sync behavior and a conceptual model for built-in conflict resolution
- [`Mergeable` protocol in the Forked framework](https://drewmccormack.github.io/Forked/Forked/documentation/forked/mergeable)
- [Conflict resolution in the Ensembles framework](https://mentalfaculty.github.io/Ensembles3/Ensembles/documentation/ensembles/conflictresolution)
- [Ensembles’ SwiftData integration](https://mentalfaculty.github.io/Ensembles3/Ensembles/documentation/ensembles/swiftdataintegration/)

## Activity

| Date | Type | Ref | Title/Description | Status |
|---|---|---|---|---|
| 2025‑10‑23 | Discussion | [\#272](https://github.com/pointfreeco/sqlite-data/discussions/272) | **Customizable conflict resolution for CloudKit sync (umbrella discussion)** | 🔄 Ongoing |
| 2025‑10‑24 | Issue | [\#273](https://github.com/pointfreeco/sqlite-data/discussions/273) | Date equality mismatch due to millisecond rounding differences between SQLite and CloudKit (converted to discussion as #wontfix) | ✅ Fixed in [\#387](https://github.com/pointfreeco/sqlite-data/pull/387) |
| 2025‑10‑24 | Issue | [\#274](https://github.com/pointfreeco/sqlite-data/discussions/274) | Data divergence between devices after concurrent offline edits | 🟠 **Open** |
| 2025‑11‑30 | Issue | [\#315](https://github.com/pointfreeco/sqlite-data/issues/315) | CloudKit bug with non-atomic saves behaving as atomic | ✅ Workaround implemented |
| 2025‑12‑09 | Comment | [\#244](https://github.com/pointfreeco/sqlite-data/discussions/244#discussioncomment-15203862) | Per-field macros in table types for sync engine configuration (encryption) | ➡️ See [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) |
| 2025‑12‑22 | Comment | [\#336](https://github.com/pointfreeco/sqlite-data/pull/336#issuecomment-3680256359) | Reaction to PR’d support for non-encrypted fields via `SyncEngine.init` | ➡️ See [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) |
| 2026‑01‑01 | Discussion | [\#352](https://github.com/pointfreeco/sqlite-data/discussions/352) | Macro-based CloudKit configuration via `@SyncedTable`/`@SyncedField` | ✅ API confirmed |
| 2026‑01‑02 | PR | [\#353](https://github.com/pointfreeco/sqlite-data/pull/353) | ~~Improve MergeConflictTests coverage and naming~~ | ➡️ Superseded by [\#414](https://github.com/pointfreeco/sqlite-data/pull/414) |
| 2026‑01‑02 | Issue | [\#354](https://github.com/pointfreeco/sqlite-data/issues/354) | Violation of “last edit wins” conflict resolution strategy | 🟠 **Open** |
| 2026‑01‑05 | Issue | [\#356](https://github.com/pointfreeco/sqlite-data/issues/356) | Inconsistent conflict resolution between production and tests due to unpopulated `CKRecord.modificationDate` in mocks | 🟠 **To be fixed by [\#411](https://github.com/pointfreeco/sqlite-data/pull/411)** |
| 2026‑01‑08 | Slack Post | n/a | Update on my work on customizable conflict resolution | ✅ Answered |
| 2026‑01‑13 | PR | [\#370](https://github.com/pointfreeco/sqlite-data/pull/370) | **Three-way merge model for built-in conflict resolution for CloudKit sync** | 📝 Draft |
| 2026‑01‑28 | Comment | [\#386](https://github.com/pointfreeco/sqlite-data/pull/386#issuecomment-3813266210) | Role of last-known server record & explanation of conflict-on-fetch scenario | ✅ Next step identified |
| 2026‑02‑27 | Slack Post | [Screenshot](slack/2026-02-27-sqlite-data-plans.png) | Discussion about timeline and plans for SQLiteData in 2026 | ✅ Timeline outlined, call offered |
| 2026‑03‑03 | PR | [\#410](https://github.com/pointfreeco/sqlite-data/pull/410) | ~~Fix metadatabase crash in tests on macOS 15~~ | ➡️ Superseded by [\#508](https://github.com/pointfreeco/sqlite-data/pull/508) |
| 2026‑03‑03 | PR | [\#411](https://github.com/pointfreeco/sqlite-data/pull/411) | Set `CKRecord.modificationDate` in `MockCloudDatabase` | 🟠 **Awaiting review** |
| 2026‑03‑04 | PR | [\#412](https://github.com/pointfreeco/sqlite-data/pull/412) | ~~Fix `MockCloudDatabase` record mutation in modify callback~~ | ➡️ Superseded by [\#507](https://github.com/pointfreeco/sqlite-data/pull/507) |
| 2026‑03‑05 | PR | [\#414](https://github.com/pointfreeco/sqlite-data/pull/414) | **Overhaul of merge conflict tests** | 📝 Draft, depends on [\#411](https://github.com/pointfreeco/sqlite-data/pull/411) |
| 2026‑05‑19 | Fork PR | [\#1](https://github.com/structuredpath/sqlite-data/pull/1) | Reconciliation for no-ancestor case, contributed by Drew McCormack as a discussion PR on my fork | ✅ Ideas adopted |
| 2026‑07‑23 | Comment | [\#506](https://github.com/pointfreeco/sqlite-data/pull/506#issuecomment-5108352240) | Observations on third-party fix for sync divergence when `userModificationTime` stamps tie | ✅ OP agreed with more structured approach |
| 2026‑07‑23 | PR | [\#507](https://github.com/pointfreeco/sqlite-data/pull/507) | Return copied `CKRecord`s when modifying `MockCloudDatabase` (Brandon’s replacement of [\#412](https://github.com/pointfreeco/sqlite-data/pull/412)) | ✅ Merged |
| 2026‑07‑24 | PR | [\#508](https://github.com/pointfreeco/sqlite-data/pull/508) | Fix in-memory metadatabase creation in `defaultMetadatabase` (reframes [\#410](https://github.com/pointfreeco/sqlite-data/pull/410)) | 🟠 **About to be merged** |
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

- **Conflict-on-fetch handling.** A conflict-on-send arises when the client sends a record that has changed on the server in the meantime and is surfaced through the `.serverRecordChanged` error. A conflict-on-fetch arises when a newer server record is fetched while the local row holds unsynced changes. Agreement is needed on treating the latter as a first-class conflict, detected through custom ancestor tracking, since the error parameters only cover the send case.
- **Role of the last-known server record.** Does it represent the last confirmed server state, or the most up-to-date record we have, including before we’ve even sent the record to iCloud? Should it serve as the ancestor in a three-way merge? Can we drop the eager store of in-flight records?
- **No-ancestor case.** A conflict can arise without a last-known server record, for example when two devices create a row with the same ID. The open questions are how this case should be handled and whether it should be called reconciliation.
- **Timestamp management for opted-out tables.** Should per-field modification timestamps still be maintained and synced for tables that use a custom strategy instead of the default “field-wise last edit wins”? Keeping them would allow switching back to the default strategy later and exposing timestamps to custom resolvers.
- **Record decoding.** Custom resolvers need `CKRecord`s decoded into `@Table` types, which the fork achieves through a synthetic SQL `SELECT` executed on the database. Is this approach acceptable?
- **Macro infrastructure.** Design and implementation of the `@SyncedTable`/`@SyncedField` macros for configuring the sync engine.
- **Built-in merge policies.** Which merge policies should the library ship with beyond `.latest`? The prototype includes `.counter` and `.set` as demonstrations.

## Backlog

- Ensure timestamp update for conflicts where both sides remove a value (see `sameFieldRemoval_conflictOnSend_clientNewer` test)
- Add test coverage for asset-backed fields in the record decoding path
- Align `CKRecord`’s print representation with `RowVersion` (`@123` instead of 📅)
