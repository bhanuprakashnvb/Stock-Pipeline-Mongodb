# Anish R Khatavkar & Bhanuprakash Narayana
# Data Pipelining Project - ADT 2024

## Project Outline

Our plan is to stream real time data using Kafka. We captured the last open day's data using AlphaVantage's API and captured the records closest to the current day's time. For example, if its 11AM on the 23rd of November, we select the record corresponding to 11AM on the 22nd of November to send to the consumer. 

We have used an EC2 Instance to host Kafka. This has been performed to stimulate a real production environment, where there is a reliance on cloud servers to run services such as this. We have hosted both producer and consumer on EC2. We have created only a single topic to reduce confusion. 

The data being captured from the AlphaVantage API is cleaned (removal of needless columns, renaming of columns and creation of new columns), and pre-processed. After this, it is sent to the consumers listening to the topics that the producer is broadcasting onto. 

Our final goal was to recreate the graphs that we find on Google whenever we search for stock market data. 

![WhatsApp Image 2024-11-25 at 2 28 34 PM](https://github.com/user-attachments/assets/a29e88d7-198c-4dbd-8d26-d26de976230c)


## Using EC2 Instance to Host Kafka
![WhatsApp Image 2024-11-25 at 2 28 32 PM](https://github.com/user-attachments/assets/d52ed71e-c2ce-475b-8586-9f324deb03b2)

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
![WhatsApp Image 2024-11-25 at 2 28 33 PM](https://github.com/user-attachments/assets/232a4139-4597-4c84-8707-d3a0d9b0eb3d)
![WhatsApp Image 2024-11-25 at 2 28 33 PM-3](https://github.com/user-attachments/assets/746f6b3e-cb13-4618-8478-e354a7b283ad)
![WhatsApp Image 2024-11-25 at 2 28 33 PM-2](https://github.com/user-attachments/assets/0825010d-5c5c-41cd-a3da-f3ae89e08c73)
![WhatsApp Image 2024-11-25 at 2 28 32 PM-3](https://github.com/user-attachments/assets/73fbbe38-2240-4790-a128-8c858b71293a)
![WhatsApp Image 2024-11-25 at 2 28 32 PM-2](https://github.com/user-attachments/assets/096b8f83-1448-4c02-a75f-687e6555a9f7)


## Using Python to Run a Consumer
![WhatsApp Image 2024-11-25 at 2 28 34 PM-3](https://github.com/user-attachments/assets/9b93891f-b136-45fe-84a3-dbeb09451dd2)
![WhatsApp Image 2024-11-25 at 2 28 34 PM-2](https://github.com/user-attachments/assets/ce4eced6-c527-4685-a147-9635c77cd403)
![WhatsApp Image 2024-11-25 at 2 28 33 PM-4](https://github.com/user-attachments/assets/ea42f0ca-6003-42ae-9d2c-1586f2a6bf12)



## Final Results

![WhatsApp Image 2024-11-25 at 2 28 34 PM-5](https://github.com/user-attachments/assets/7fff7925-aa0c-4817-9418-f174e1c701aa)
![WhatsApp Image 2024-11-25 at 2 28 34 PM-4](https://github.com/user-attachments/assets/0c0b70dc-c845-4a29-856c-82d2f4383116)
![WhatsApp Image 2024-11-25 at 2 28 34 PM-3](https://github.com/user-attachments/assets/a7dde8e9-8c13-4885-94bd-d34fb3bcaa2a)
![WhatsApp Image 2024-11-25 at 2 28 34 PM-2](https://github.com/user-attachments/assets/01099da8-aaec-42d3-96c1-4bdb29ac854e)
![WhatsApp Image 2024-11-25 at 2 28 35 PM](https://github.com/user-attachments/assets/8cef77a7-24c1-4dd3-b15f-bc68a462c36d)
![WhatsApp Image 2024-11-25 at 2 28 33 PM](https://github.com/user-attachments/assets/993d6c02-ac79-4607-a654-b7a3fa03cc2f)



