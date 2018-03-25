# Deploying Hyperledger Fabric on Kubernetes

HLF is an open source blockchain framework implementation and one of the Hyperledger projects hosted by The Linux Foundation. It is a platform for distributed ledger solutions.

### Examples of Hyperledger Fabric Use Cases
1. Business to Business(B2B) contract. This technology can be used to automate business contracts in a trusted way.
2. Asset Depository. 


This article mainly aims at simplifying Fabric operations, by use of Kubernetes. This tool is ideal because: 

- It's easy to achieve high availability(HA) with Kubernetes.
- Fabric is built into container images, Kubernetes is thus useful in orchestration, scaling and managing the containers.
- Kubernetes supports multi-tenancy, hence possible to develop and test blockchain applications.

Note: In this article, I assume the reader has basic understanding of Kubernetes, Helm, Docker and Hyperledger Fabric.

I'm going to deploy a network with one peer, one orderer, two organisations and one channel.

#### Definition of Terms

1. Peer - A Peer is a node on the network maintaining state of the ledger and managing chaincodes. Any number of Peers may participate in a network. A Peer can be an endorser or committer. Peers form a peer-to-peer gossip network
2. Orderer - Manages a pluggable trust engine that performs the ordering of the transactions.
3. Cnannel - A data partitioning mechanism to control transaction visibility only to stakeholders. Consensus takes place within a channel by members of the channel. 

#### Configuration Files

All the configuration files of the network can be found here[link github].

1. configtx.yaml - configtxgen tool generates genesis block according to this file, of which is used to boot up orderer and restrict permission of channel creation. The genesis block is generated according to the definition of organizations in crypto-config.yaml file.
2. crypto-config.yaml - The cryptogen tool generates certificates for Fabric members based on this file.

To generate the network artifacts, run ``` sh network-artifacts-gen.sh```. This will create a crypto-config and channel-artifacts folders. Remember to push all the generated to Github. The contents will be as shown below:

image tree of cypto>

image tree of channel-art>

3. fabric-ca.yaml - This is the Kubernetes deployment template for the CA service of the Fabric. It is used for certificate management in the organization.
4. fabric-orderer.yaml - Kubernetes deployment template of orderer.
5. fabric-peer.yaml -  Deployment template of peers. 
