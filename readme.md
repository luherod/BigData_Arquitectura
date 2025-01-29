# Hadoop Cluster configuration

## Project objective

Configuring a Hadoop cluster on Google Cloud and integrating it with an Elasticsearch server plus  Kibana for seamless data ingestion and analysis.

## Tools:

* Google Cloud Platform

## Process:

1. **Build a Dataproc Cluster**: Create a standalone or standard Dataproc cluster to run Hadoop.

    *Screenshot was provided after finalizing configuration*

2. **Download and Upload JARs**: Retrieve the ES-Hadoop and commons-httpclient JARs, then place them in a Google Storage bucket.

3. **Copy JARs to Cluster**: Use `gsutil cp` from the master node to pull the JARs into the cluster filesystem.

4. **Elasticsearch VM**: Spin up a separate VM for Elasticsearch, open firewall ports 9200 and 5601 for both cluster and local access.

    *Screenshot was provided once the `elasticsearch.yml` configuration is visible*  

5. **Check Connectivity**: From the cluster, run `curl -I http://IP_Elastic_server:9200` to confirm the Hadoop node can reach Elasticsearch.

6. **Configure Hive**: Edit `hive-site.xml` to add the Elasticsearch connection properties and point `hive.aux.jars.path` to the ES-Hadoop JARs.

    *Screenshot was provided after applying changes*

7. **Restart Services**: Restart Hive (e.g., `sudo service hive-server2 restart`) so that the new settings and JARs are loaded.

8. **Create an ES Index**: On the Elasticsearch VM, create an index (e.g., `alumnos`) and optionally add a document via a `POST` request.

9. **Insert Data via Hadoop**: Perform a bulk insert from the Hadoop cluster and validate with `curl -X GET "http://IP-SERVER-ELASTIC:9200/alumnos/_search?pretty"`.

    *Screenshot was provided showing the query result*

10. **Kibana Dashboard**: Access Kibana (port 5601), create a data view for `alumnos` and build a basic dashboard.

    *Screenshot was provided showing a simple visualization* 


## Author

Lucía Herrero Rodero.
