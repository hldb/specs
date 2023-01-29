# Manifest

-----

**Abstract**

HLDB databases all have an immutable setup document called a manifest.
The manifest contains information needed to run a database.
This information specifies protocols, formats and their configuration.

# Table of Contents

- [Introduction](#introduction)
- [Versions](#versions)
- [Validity Constraints](#validity-constraints)

## Versions

> list of spec'd manifest versions

- [1](./1.md)

## Validity Constaints

A manifest must pass all validity constraints of the manifest version.
If one of these constaints is not satisfied the manifest is invalid.
Invalid manifests cannot be used to open a database.
