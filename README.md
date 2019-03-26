# solr-zookeeper-ensemble

This is my first try to use Docker Swarm for a simple solr cluster with zookeeper ensemble.

For this at first I created five CentOS 7 VMs in gnome-boxes and installed docker in them. there are 3 managers and 2 workers in the Swarm. Next I launched Portainer docker.

All the job can be done by docker's command line I already tried that with no issues.

this command issues the deploying the services in the swarm:

# docker stack deploy --compose-file=solr-cloud-zk-ensemble.yml solr-zk

Because zookeer ensemble takes sometimes to be fully intialized and solr instances need it to be launched successfully, solr instances won't be not ready to use right away. I tried the "depends_on" attribute and it doesn't work as expected in swarm mode. Also I used different restart policy with no result.

My work around to fix the issue is to run update service on solr service instances after successfull zookeeper ensemble startup as bellow:

# docker service update solr-zk-ensemble_solr-x





