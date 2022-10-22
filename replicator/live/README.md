# Live Replicator Specs

**Abstract**

The live replicator uses Libp2p Pubsub and IPFS/IPLD block storage to sync with peers. Head CIDs of the replica, which is a Merkle-DAG, are shared with with peers.
These Head CIDs can then be resolved to entries and traversed until the replicas converge.

##### Versions:

- [1.md](./1.md)
