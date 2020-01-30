## Testing Vault/Consul Cluster
--------------------------------

This compose file and setup creates a single-node HashiCorp Vault cluster with a 3-node Consul cluster as a backend, as well as a single-node Vault "standby" for High Availability.


I built this out to test out the different DR scenarios that could occur within a Vault cluster to evaluate how to handle and recover.


Obviously this is not the only use case for this setup, so feel free to expand and use it however you need.


### **Setup**
-------------

This setup uses Docker Compose, so in order to create the cluster you'll need to install Docker and Docker Compose on your system.


Please see Docker's own installation guides to accomplish this according to your operating system.


Once Compose has been installed, the cluster can be brought online with the command:


            docker-compose up -d


The containers will come online and be accessible on your local machine at the following ports:


            Master Vault: http://localhost:8200
            Standby Vault: http://localhost:8201
            Consul: http://localhost:8500



### **Vault Init**
------------------

Lastly, you'll need to initialize and unseal the Vault cluster to enable usage. You can do this via the command line (see [Hashi's docs](https://www.vaultproject.io/docs/commands/operator/init.html)), however it's easiest to walk through the steps in the UI by visiting ``http://localhost:8200``.


You'll be prompted to identify the number of *Key Shares* - the number of shards to break the master key into - as well as a *Key Threshold* - the number of key-shares required to reconstruct the master key. These concepts can be further explained via Hashi's [Seal Concepts Page](https://www.vaultproject.io/docs/concepts/seal.html).


Next you'll be given the *Master Key* as well as an initial *Root Token* that you can then use to fully unseal the master Vault node.


To enable the Performance Replica, you will also need to provide the *Master Key* via command-line or the UI to unseal it as well and enable replication.
