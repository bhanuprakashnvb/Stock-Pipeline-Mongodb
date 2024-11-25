# Anish R Khatavkar & Bhanuprakash Narayana
# Data Pipelining Project - ADT 2024

## Project Outline

Our plan is to stream real time data using Kafka. We captured the last open day's data using AlphaVantage's API and captured the records closest to the current day's time. For example, if its 11AM on the 23rd of November, we select the record corresponding to 11AM on the 22nd of November to send to the consumer. 

We have used an EC2 Instance to host Kafka. This has been performed to stimulate a real production environment, where there is a reliance on cloud servers to run services such as this. We have hosted both producer and consumer on EC2. We have created only a single topic to reduce confusion. 

The data being captured from the AlphaVantage API is cleaned (removal of needless columns, renaming of columns and creation of new columns), and pre-processed. After this, it is sent to the consumers listening to the topics that the producer is broadcasting onto. 

Our final goal was to recreate the graphs that we find on Google whenever we search for stock market data. 

![Google Stocks](image-6.png?raw=true)

## Using EC2 Instance to Host Kafka

![EC2 Image](image.png?raw=true)

## Running Kafka on EC2 Instance

> This is the file which includes all commands related to running Kafka

1. Open folder in which AWS Certificates are stored.

2. Start EC2 Instance and after all checks are completed, navigate to the `Connect` tab. Copy the last command on the page and 
    enter on your open terminal to connect to the EC2 Instance

3. Re-check if the conif/server-properties file has the EC2 Instance's public address listed under listener name. If not, change.
    * Run:
        cd kafka <press tab to autocomplete>
        nano config/server.properties 
        scroll down to find `advertised.listener.....` line. Replace the IP address with your EC2 machine's address. 

3. Start Zookeeper ------------------------>
    cd kafka <press tab to autocomplete>
    bin/zookeeper-server-start.sh config/zookeeper.properties


4. Start Kakfka --------------------------->
    * Open a new terminal in the same folder as the AWS Certificates
    * Connect to your EC2 Instance
    * Run:
        export KAFKA_HEAP_OPTS="-Xmx256M -Xms128M"
        cd kafka <press tab to autocomplete>
        bin/kafka-server-start.sh config/server.properties


5. Create a topic and Start Producer ------>
    * Open a new terminal in the same folder as the AWS Certificates
    * Connect to your EC2 Instance
    * Run:
        cd kafka <press tab to autocomplete>
        bin/kafka-topics.sh --create --topic stocks --bootstrap-server 18.219.236.123:9092 --replication-factor 1 --partitions 1

        bin/kafka-console-producer.sh --topic stocks --bootstrap-server 18.219.236.123:9092

        here <stocks> is the topic names


6. Create Consumer ------------------------>
    * Open a new terminal in the same folder as the AWS Certificates
    * Connect to your EC2 Instance
    * Run:
        cd kafka <press tab to autocomplete>
        bin/kafka-console-consumer.sh --topic stocks --bootstrap-server 18.219.236.123:9092




## Using Python to Run a Producer

![Producer-1](image-1.png?raw=true)
![Producer-2](image-2.png?raw=true)
![Producer-3](image-3.png?raw=true)
![Producer-4](image-4.png?raw=true)
![Producer-5](image-5.png?raw=true)

## Using Python to Run a Consumer

![Consumer-1](image-7.png?raw=true)
![Consumer-2](image-8.png?raw=true)
![Consumer-3](image-9.png?raw=true)


## Final Results

![Res-6](image-15.png?raw=true)
![Res-5](image-14.png?raw=true)
![Res-1](image-10.png?raw=true)
![Res-2](image-11.png?raw=true)
![Res-3](image-12.png?raw=true)
![Res-4](image-13.png?raw=true)
<img width="1394" alt="Screenshot 2024-11-24 at 2 37 57 PM" src="https://github.com/user-attachments/assets/493c4466-934e-4a73-88e1-8da4fcd09838">



