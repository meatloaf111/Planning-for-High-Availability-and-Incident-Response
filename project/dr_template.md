# Infrastructure

## AWS Zones
Identify your zones here
us-east-2 region:"us-east-2a","us-east-2b"
us-west-1 region:"us-west-1a","us-west-1b"

## Servers and Clusters

| ### Table 1.1 Summary |                                                                      |                                                                        |                                                                 |                                                                                                              |
|-----------------------|----------------------------------------------------------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Asset                 | Purpose                                                              | Size                                                                   | Qty                                                             | DR                                                                                                           |
| Ubuntu Web            | Web Server                                                           | t3.micro                                                               | 1                                                               | Deployed to DR region                                                                                                            |
| EKS Node              | EKS Node                                                             | t3.medium                                                              | 1                                                               | Deployed to DR region                                                                                                            |
| Load Balancer         | Load Balancer                                                        | N/A                                                                    | 1                                                               | Deployed to DR region                                                                                                            |
| RDS                   | Database                                                             | db.t2.small                                                            | 1                                                               | Deployed to DR region and data is replicated                                                                                                            |
| SSH Keys              | SSH keys for administering the EC2 instances                         | N/A                                                                    | 1                                                               | Created in each regions by manual                                                                                                            |
| Monitoring            | Monitoring platform (Grafana and Prometheus) for the web application | N/A                                                                    | 1                                                               | Deployed to DR region                                                                                                            |
| Asset name            | Brief description                                                    | AWS size eg. t3.micro (if applicable, not all assets will have a size) | Number of nodes/replicas or just how many of a particular asset | Identify if this asset is deployed to DR, replicated, created in multiple locations or just stored elsewhere |


### Descriptions
More detailed descriptions of each asset identified above.
・Ubuntsu Web servers hosts flask web applications

・RDS holds data for the above web applications

・EKS nodes hosts monitoring platform(grafana and prometheus) to monitor the web application

・SSH keys are uses to administre web nodes

・Load balancer works to handle the incoming request and allocate them to the Web servers

## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.

・Ensure both sites are configured the same

・Use IaC to do this

## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region

・Point your DNS to your secondary region
This can be done with a name provider like Amazon route 53

・Failover your database replication instances to another region
Manually force the secondary region to become primary at the database level, or
Automatically failover the database by health checks