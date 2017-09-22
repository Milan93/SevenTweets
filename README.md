The idea of this project is to build a network of mini services that are similar to Twitter. In this network, node is a separate service with it's own storage (database) and username which serves as a unique identifier.

Every node in the network knows address of other nodes in order to communicate with them. All of the nodes have same API, but implementation might differ.

Nodes can run on its own, without joining network. To join network, request to /join_network is issued with address of at least one other node. This initiates protocol for joining. New node sends request with its own name and address to existing node and receives list of other nodes in network as result. Existing node adds him to his own list and new node registers itself to all other nodes by sending its info to /register. When node is being shut down, it sends /unregister request to all other nodes.

If node is killed violently before it has a chance to unregister itself from network, other nodes will remove it from list upon unsuccessful contact with it.

Basic node functionality is to:

create tweets,
create retweets (references to other nodes by name, not address, since we allow address to change),
list tweets,
delete tweets,
local search (only one node),
distributed search (search on all nodes in network and return aggregated results0).
SevenTweets is written in Python 3 with Flask framework and PostgreSQL database.

Build packages source into Docker image and automated deploy is implemented using fabric3.
