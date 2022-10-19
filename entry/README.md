# Entry

-----

**Abstract**

Entries are used to append updates in an immutable and conflict free way. Peers share them with each other and add them to their local replica.
Before new entries can be checked for access and added to the replica; their tag, digital signature, and writer identity need to be verified.

# Table of Contents

- [Introduction](#introduction)
- [Formats](#formats)
- [Validity Constraints](#validity-constraints)

## Introduction

Entries are immutable and reference previous entries by [content-address](https://docs.ipfs.io/concepts/content-addressing) also called CID; creating causal and traversable links.

Beside references to previous entries, entries include:

 - version
 - database tag
 - payload
 - identity

## Formats

> List of spec'd entry formats

- [basal](./basal)

## Validity Constraints

An entry must pass all validity constraints of the entry format.
If one of these constaints is not satisfied the entry is invalid. Invalid entries cannot be added to the replica.

