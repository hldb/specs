![](https://img.shields.io/badge/status-wip-orange.svg?style=flat-square)

# Opal Manifest

-----

**Abstract**

Opal databases all have an immutable setup document called a manifest.
The manifest contains information needed to run a database.
This information specifies protocols, formats and their configuration.

# Table of Contents

- [Introduction](#introduction)
- [Manifest Format](#manifest-format)
  - [Example Manifest](#example-manifest)
- [Manifest Address](#manifest-address)
  - [String Format](#address-string-format)
  - [Binary Format](#address-binary-format)

## Introduction

The manifest must contain relevant information to running the database in agreement with other participants. Many of the manifest's fields specify contain protocol anda protocol or format, sometimes with configuration. These module types and versions are used by the implementation to load the neededThis type, which is just a string, is used by the implementation to load the correct software and version needed for running that piece of the database.

All information needed for Opal to run the database must be included with the manifest, not just referenced. This rule makes it easy to know whether a database can be opened or not.

## Manifest Format

An Opal manifest is a data structure, encoded using dag-cbor [[spec](https://github.com/ipld/ipld/blob/master/specs/codecs/dag-cbor/spec.md)], containing the following fields:

- **version** (uint64)
  - The version of the manifest
  - This document specifies version 1 of the Opal protocol
  - Set to `1`


- **name** (utf8)
  - The name of the database
  - Chosen by the user
  - Does not need to be unique
  - No *default* value


- **store** (utf8)
  - The protocol and config of the database store to be used. Read more about [database stores](./store)
  - Contains a protocol id and optionally a config.
  - No *default* value


- **access** (map)
  - The protocol and config of the database access to be used. Read more about [access modules](./access)
  - Contains a protocol id and optionally a config.
  - *default*: `{ protocol: '/opal/access/ipfs/1.0.0' }`


- **entry** (utf8)
  - The entry format and options to be used. Read more about [entry formats](./entry).
  - Contains a format id and sometimes options.
  - *default*: The default entry format type is `'/ipfs-log/entry/3.0.0'`


- **identity** (utf8)
  - The identity format and options to be used. Read more about [identity formats](./identity).
  - Contains a format id and sometimes options.
  - *default*: `{ format: '/opal/identity/2.0.0' }`


- **meta** (map) [optional]
  - An optional user-space field for including any information to keep immutable and associated with the database.
  - Linked data inside this field will not be fetched automatically.


- **tag** (bytes) [optional]
  - A way to refer to the database without revealing the manifest.
  - Should be unique to the database. Best if random data.



###### see cbor [encoding specification](https://www.rfc-editor.org/rfc/rfc8949.html#name-specification-of-the-cbor-e) and [tag 42](https://github.com/ipld/cid-cbor/)

```
  {
    version: type 0
    name: type 3
    store: {
      protocol: type 3
      config?: tag 42
    }
    access: {
      protocol: type 3
      config?: tag 42
    }
    entry: {
      format: type 3
      options?: tag 42
    }
    identity: {
      format: type 3
      options?: tag 42
    }
    meta?: type 5
    tag?: type 2
  }
```

#### Example Manifest:

```js
  {
    version: 1,
    name: 'example',
    store: {
      protocol: '/opal/keyvalue/1.0.0'
    },
    access: {
      protocol: '/opal/access/static/1.0.0',
      config: CID(bafyreidaqbln54tc6zg2n2oylgx7l5nqnbua7lelsvg3zuoxadr4rqvfiq)
    },
    entry: {
      format: '/opal/entry/basal/3.0.0',
      options: CID(bafyreibzyfs4xxtpuxsphpq2xaz7rrhqwtsjyrxpq6qsk4mepbbdiezkb4)
    },
    identity: {
      format: '/opal/identity/basal/2.0.0',
    },
    meta: { user: 'space' }
  }
```

## Manifest Address

  Also known as the database address, these are used as reference to the database and for potential database peers to fetch the manifest. They are made of the protocol prefix for Opal and a manifest CID.

#### Address String Format

  `/opal/<manifest CID>`

  This is the manifest address string format. The version and encoding for the CID are not specified. Here are some examples of valid addresses:

  - `/opal/QmWDUfC4zcWJGgc9UHn1X3qQ5KZqBv4KCiCtjnpMmBT8JC`
  - `/opal/zdpuArEpCPwqpgQVMYrFSDQKhHLq5L6Es8HQkhWfhrad5oYdK`
  - `/opal/bafybeidpga2xwiiseib3tcsp33wodu3itunwj2su624yygdx6av3s4f5f4`

#### Address Binary Format

  `<opal prefix><manifest CID>`

  This is the manifest address binary format. The prefix code for opal is `0xdb`. This byte must be prefixed to the manifest CID for it to be valid. Here are some examples using the same CIDs from the string section:

  - `0xdb1220750710ddc61a99b8604fc77e4067b53c24d0488cd28fda4cb344ffee95a73191`
  - `0xdb01711220566d493416aee3a6585402934b8544468b5d040935cb1dcb43830057966a0a46`
  - `0xdb017012206f30357b21122203b98a4fdeece1d3689d1b64ea54f6b98c1877f02bb970bd2f`