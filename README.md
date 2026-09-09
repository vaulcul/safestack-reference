# SafeStack reference library

This repository publishes the **public clinical reference library** that the SafeStack app reads.
It exists so a correction to that data can reach installed devices without an app-store release.

## What is here

```
reference/v1/version.txt      the version currently published
reference/v1/delta.json       the library itself
reference/v1/delta.json.sig   a signature over delta.json
```

## What is not here, and never will be

**Nothing about any person.** No user data, no health data, no identifiers, no analytics. The app
sends nothing when it fetches these files — it asks for a version number, and if that number is
higher than the one it holds, it asks for the library.

## Integrity

`delta.json` is signed with ECDSA (nistP256 / SHA-256). The app carries the matching public key and
**refuses any payload whose signature does not verify**, so a file altered in transit or at rest is
discarded rather than believed. The version is bound *inside* the signed bytes, so `version.txt` can
only ever say "go look" — it can never relabel an older library as a newer one.

An older version is refused as a replay. A file is never republished under a version number that has
already been used; a correction is published as a **higher** version.

## Sources

The published data derives from US Government works — openFDA and DailyMed drug labels, and the
electronic Code of Federal Regulations. Every row carries a citation a reader can open.

## Contributing

This repository is published output, not a working tree. Corrections belong upstream in the SafeStack
project.
