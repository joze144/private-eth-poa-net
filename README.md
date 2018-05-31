# Local Ethereum Network
A set of Docker images to create a local Ethereum network with two mining nodes, bootnode and a monitor. They use Clique protocol (Proof of Authority) consensus mechanism and don't require any computation power for it. Computation power is only needed for the transactions, therefor it runs very efficiently.

Block time is set to 8s, and gasPrice is set to 1 on the mining nodes.

## Usage
Setting up this networks requires you to install Docker. Clone the repository, and run `docker-compose up -d --build` from the repository root. The network should start and synchronize without any further configuration.

## The bootnode
The nodes in the network are connecting with the bootnode. This is a special ethereum node, designed to provide a register of the existing nodes in the network. The parameter `nodekeyhex`in the `docker-compose.yml` is needed to derive the `enodeID` which is later passed to the other nodes. The IP needs to be fixed, as the other nodes need to know where to find the bootnode, and DNS is not supported. The bootnode does not participate in synchronization of state or mining.

## Miners / Geth Nodes
There are two nodes that participate in the network. The state is synchronized between them and they are trying to create blocks with mining. Initially they connect to the bootnode with the information derived from the fixed IP and the nodekeyhex. If you want to interact with the network, you need to connect via RPC. You can attach a geth instance, connect Remix IDE or connect your browser with web3 and build a DApp.

You can connect additional nodes to the network, which can serve as a RPC point and are synchronizing with other nodes. But they can't participate in the mining, since you need to be authorised in the genesis block to do that.

The RPC Ports of the nodes are mapped to your localhost, the addresses are:

* [http://localhost:8502](http://localhost:8502) - geth-miner-1
* [http://localhost:8503](http://localhost:8503) - geth-miner-2

## Monitoring
The monitoring is being provided by two nodes, the monitoring-backend and the monitoring-frontend. The backend connects to the ethereum nodes and retrieves metrics from them. It communicates with the monitoring-frontend with websockets. The frontend can be found under [http://localhost:3000](http://localhost:3000)
