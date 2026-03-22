# Advocates Close

Native macOS software built on Apple frameworks — SwiftUI, SwiftData, XPC Services, TextKit 2 — with nothing in between.

## Redliner

A multi-process macOS application. The main app handles UI and state. Document conversion and redline generation run in dedicated XPC services — separate processes with independent memory spaces, managed by `launchd`, created and destroyed on demand. No document content crosses the XPC boundary. The app passes file paths; the services read, process, and write directly to the filesystem.

The redline engine implements a word-level Myers diff algorithm and uses `NSFileCoordinator` to coordinate concurrent reads and writes across processes. Multiple redlines execute in parallel — each with its own XPC connection, its own handler instance, its own coordinated file access — orchestrated by Swift structured concurrency.

Four named CSS stylesheets — switchable at runtime — cover the range from web-grade minimalism to raw EDGAR appearance. A Handlebars-style template engine resolves variables, conditionals, loops, and computed financial expressions against structured data persisted in SwiftData. Pandoc handles format conversion over XPC.

macOS 15.0+. Xcode 16+. Swift 6.

## Atlas

The document infrastructure beneath Redliner. Atlas captures the drafting process itself — not just the finished document, but every intermediate state.

Every keystroke in an Atlas editor triggers an `NSTextStorageDelegate` callback that produces a timestamped `EditTransaction`: operation type, affected range, post-edit text. Transactions accumulate in memory during the session and are encrypted with AES-GCM before being written to the `.atlas` document package on save.

```
[0] t=09:14:01.003  insert   {0,0}   "T"
[1] t=09:14:01.087  insert   {1,0}   "h"
[2] t=09:14:01.142  insert   {2,0}   "e"
[3] t=09:14:02.450  insert   {3,0}   " plaintiff avers"
[4] t=09:14:05.700  delete   {15,5}
[5] t=09:14:06.100  replace  {15,0}  "alleges"
```

From this log, every intermediate state of the document can be reconstructed. Deliberation time between edits can be measured. Revision patterns — write-then-delete-then-rewrite — can be identified and classified.

| Package | Description |
|---|---|
| **AtlasDocumentKit** | Document model. An `.atlas` file is a macOS package bundle containing rich text, encrypted edit transactions, semantic tags, metadata, and versioned snapshots. |
| **AtlasTextStorage** | `NSTextStorage` subclass backing every Atlas document. The `backingStore` and the standard `replaceCharacters(in:with:)` interface that TextKit requires. |

## Frameworks

Everything listed here is an Apple framework or a first-party Swift package. This is a deliberate choice.

| | |
|---|---|
| **UI** | SwiftUI, AppKit, WebKit |
| **IPC** | NSXPCConnection, NSXPCListener |
| **File Coordination** | NSFileCoordinator |
| **Concurrency** | Swift structured concurrency |
| **Persistence** | SwiftData |
| **Text** | TextKit 2 |
| **Subscriptions** | StoreKit 2 |
| **Markdown** | swift-markdown |

---

*Named after [Advocates Close](https://en.wikipedia.org/wiki/Advocates_Close), an alley off the Royal Mile in Edinburgh, adjacent to the old courts where Scottish advocates once kept their chambers.*
