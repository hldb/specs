![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)

# Store

-----

**Abstract**

Store protocols define the operations and state index for a specific store.

# Table of Contents

- [Introduction](#introduction)
- [Operations](#operations)
- [Index](#index)

## Introduction

Stores are used to derive a database state from the database replica. They provide an api for reads and writes to the database. Different stores can be used to represent very different structures.

## Operations

Operations are used to update database states. They are added to entry operations and read by the store to derive state. An operation is a map with an `op` field that has a string value. The operation encoding and additional fields are defined by the store specification.

```
{
  op: type 3
}
```

#### Example Kvstore Put Operation:

```
  {
    op: 'PUT',
    key: 'example',
    value: 123
  }
```

## Index

The Index defines the structure of the database state. Indexes read the entry log from the replica to derive the index state. It reads the entry log

TODO: example definition for reducing an index from operations
