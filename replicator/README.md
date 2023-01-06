![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)

# Replicator

-----

**Abstract**

A replicator finds and syncs with other database peers. Many replicators can be used for one database. Replicators allow remote peers to affect the local database.

# Table of Contents

- [Introduction](#introduction)
- [Implementations](#implementations)

## Introduction

Replicators handle syncing database replicas between peers. The database replica includes the manifest, entries, and identities. However replicators are mainly concerned with the latter two as the manifest is needed before replication, and does not get updated.

## Implementations

- [IPHE](./IPHE)
