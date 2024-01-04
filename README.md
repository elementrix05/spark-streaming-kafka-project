# spark-streaming-kafka-project

Gets random names from the API. Sends the name data to Kafka topics every 10 seconds using Airflow. Every message is read by Kafka consumer using Spark Structured Streaming and written to Cassandra table on a regular interval.

`kafka_producer_dag.py` -> The DAG script that writes the API data to a Kafka producer every 10 seconds.

`kafka_producer.py` -> The script that gets the data from API and sends it to Kafka topic

`spark_streaming_script.py` -> The script that consumes the data fromo Kafka topic with Spark Structured Streaming

`sample_response.json` -> Sample response coming from the API



## Process

We will have to create a multinode Kafka cluster. We can define the replication factor as 3 since there are 3 nodes (kafka1, kafka2, kafka3). 

We will also create a Cassandra server. Every env variable is located in `docker-compose.yml`. I also defined them in the scripts.

Then, we will create the keyspace `spark_streaming` and the table `random_names` (You can use your own names)

When we turn the OFF button to ON, we can see that the data will be sent to Kafka topics every 10 seconds. We can check from Kafka UI as well.

First of all we should copy the local PySpark script into the container

We should then access the Spark container and install necessary JAR files under jars directory.

We should run the necessary commands to install the necessary JAR files under for latest spark version

While the API data is sent to the Kafka topic `random_names` regularly, we can submit the PySpark application and write the topic data to Cassandra table

After running the commmand, we can see that the data is populated into Cassandra table

## Project Description

This is basic project on spark streaming with kafka. Project flow is basically get data from API -> run a scheduled script with Airflow &amp; send data to Kafka (Producer) -> consume with Spark -> then write to Cassandra
