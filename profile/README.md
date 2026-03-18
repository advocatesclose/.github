# Advocates Close

**Machine learning infrastructure for law firms, built on the editing process itself.**

Advocates Close is a suite of Swift packages that capture, encrypt, and persist every keystroke made during legal document drafting. The premise is simple: the value of an AI trained on legal work depends entirely on the quality of the data it is trained on. Garbage in, garbage out. We capture the drafting process — not just the finished product — because the process is where the intelligence lives.

When an attorney writes "plaintiff avers," pauses, deletes "avers," and types "alleges," that sequence is data. When a senior associate restructures a clause three times before settling on the final version, the intermediate states and the time between them are data. When two attorneys draft the same type of provision and one takes four revisions while the other takes one, the difference is data.

We capture all of it.

## How it works

Every keystroke in an Atlas document editor triggers an `NSTextStorageDelegate` callback. Each callback produces a timestamped `EditTransaction` recording the operation type (insert, delete, replace), the affected range, and the post-edit text. Transactions accumulate in memory during the editing session and are encrypted with AES-GCM before being written to `Transactions.json` inside the `.atlas` document package when the user saves.

```
[0] t=09:14:01.003  operation=insert   range={0,0}   afterText="T"
[1] t=09:14:01.087  operation=insert   range={1,0}   afterText="h"
[2] t=09:14:01.142  operation=insert   range={2,0}   afterText="e"
[3] t=09:14:02.450  operation=insert   range={3,0}   afterText=" plaintiff avers"
[4] t=09:14:05.700  operation=delete   range={15,5}  afterText=nil
[5] t=09:14:06.100  operation=replace  range={15,0}  afterText="alleges"
```

From this log, every intermediate state of the document can be reconstructed. Deliberation time between edits can be measured. Revision patterns — write-then-delete-then-rewrite — can be identified and classified. Training pairs of (context, next edit) can be generated at any granularity. The attorney's drafting process becomes a structured dataset, captured at the resolution of individual keystrokes.

There is no expectation of privacy on firm devices. All users are attorneys who know — or will know — that this infrastructure exists for the purpose of converting their drafting expertise into a trainable model.

## Packages

### [AtlasDocumentKit](https://github.com/advocatesclose/AtlasDocumentKit)

The document model. An `.atlas` file is a macOS package bundle containing:

| File | Contents |
|------|----------|
| `Current.rtfd` | The document's rich text content |
| `Transactions.json` | Edit history, AES-GCM encrypted |
| `Tags.json` | Semantic annotations (Title, EffectiveDate, etc.) |
| `Records.json` | File metadata |
| `Info.plist` | Display name, timestamps |
| `Versions/` | Timestamped RTFD snapshots with index |

`AtlasDocument` is a `ReferenceFileDocument` that conforms to SwiftUI's document architecture. It owns the `AtlasTextStorage` (an `NSTextStorage` subclass), the transaction log, semantic tags, version history, and the encryption pipeline. It handles serialization to and from the `.atlas` package format.

### [AtlasDocumentView](https://github.com/advocatesclose/AtlasDocumentView)

The editor. Four source files:

- **`AtlasViewControllerRepresentable`** — an `NSViewRepresentable` that wraps `NSTextView.scrollableTextView()`. Connects the document's `textStorage` through TextKit 2's `NSTextContentStorage` and installs the transaction logger. Drop it into any SwiftUI view.
- **`EditTransactionLogger`** — an `NSTextStorageDelegate` that converts every `didProcessEditing` callback into an `EditTransaction` and appends it to the document's log. Classifies edits as insert, delete, or replace. Ignores attribute-only changes.
- **`AtlasSemanticReader`** — scans an `NSTextStorage` for ranges annotated with semantic tags and returns structured values for display in sidebars and inspectors.
- **`AtlasAttributes`** — `NSAttributedString.Key` extensions for Atlas-specific attributes.

### [AtlasTextStorage](https://github.com/advocatesclose/AtlasTextStorage)

The `NSTextStorage` subclass that backs every Atlas document. Provides the `backingStore` (`NSMutableAttributedString`) and the standard `replaceCharacters(in:with:)` / `setAttributes(_:range:)` interface that TextKit requires.

## Integration

```swift
import AtlasDocumentKit
import AtlasDocumentView

@main
struct MyApp: App {
    var body: some Scene {
        DocumentGroup(newDocument: { AtlasDocument() }) { file in
            AtlasViewControllerRepresentable(
                document: file.document,
                selection: .constant(nil)
            )
        }
    }
}
```

## Requirements

- macOS 15.0+
- Swift 6.2+

## Status

Active development. The edit transaction pipeline is complete and tested. Current focus areas:

- Semantic tagging UI (annotating ranges with structured labels)
- Transaction replay and visualization
- Training data export pipeline
- Version diffing and comparison

---

*Advocates Close is named after [Advocates Close](https://en.wikipedia.org/wiki/Advocates_Close), an alley off the Royal Mile in Edinburgh, adjacent to the old courts where Scottish advocates once kept their chambers.*
