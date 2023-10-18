# LAB 01 - Event Streams

This document serves as a resource accompanying the presentations and Proof of Technology event around IBM Event Automation. It is designed to provide insights and hands-on experience for the Event Streams capability, which acts as the backbone of our event-driven architecture.

As you explore this documentation, you'll gain a deeper understanding of Event Streams, its pivotal role as a Kafka broker, and its significance within our overall architecture. We encourage you to delve into the details to fully comprehend the foundation on which our Kafka solutions are built.

## Event Streams: Introduction

Event Streams is an event-streaming platform based on the [Apache Kafka®](https://kafka.apache.org/) project and incorporates the open-source [Strimzi](https://strimzi.io/) technology.

Event Streams uses Strimzi to deploy Apache Kafka in a resilient and manageable way, and provides a range of additional capabilities to extend the core functionality.

**Event Streams capabilities:**

- Apache Kafka deployed by Strimzi that distributes Kafka brokers across the nodes of a Kubernetes cluster, creating a highly-available and resilient deployment.

- An administrative user interface (UI) focused on providing essential features for managing production clusters, in addition to enabling developers to get started with Apache Kafka. The Event Streams UI facilitates topic lifecycle control, message filtering and browsing, client metric analysis, schema and geo-replication management, connection details and credentials generation, and a range of tools, including a sample starter and producer application.

- A command-line interface (CLI) to enable manual and scripted cluster management. For example, you can use the Event Streams CLI to inspect brokers, manage topics, deploy schemas, and manage geo-replication.

- Geo-replication of topics between clusters to enable [disaster recovery](https://ibm.github.io/event-automation/es/georeplication/disaster-recovery).

- A REST API for producing messages to Event Streams topics, expanding event source possibilities.

- A schema registry to support the definition and enforcement of message formats between producers and consumers. Event Streams includes the open-source [Apicurio Registry](https://www.apicur.io/registry/docs/apicurio-registry/2.3.x/index.html) for managing schemas.

- Health check information to help identify issues with your clusters and brokers.

- Secure by default production cluster templates with authentication, authorization and encryption included, and optional configurations to simplify proof of concept or lite development environments.

- Granular security configuration through Kafka access control lists to configure authorization and quotas for connecting applications.

> To learn more about Event Streams and its capabilities, navigate to the documentation page: [Event Streams Documentation](https://ibm.github.io/event-automation/es/about/overview/)

## Event Streams: Lab Introduction

In this lab, we are going to introduce you to IBM Event Streams. After this lab, you should be able to:

- Explore the User Interface
- Create a Kafka Topic
- Generate credentials
- Produce a message
- Browse a message
- Monitor messages

For this lab, we already provided the necessary environments and user credentials to access the environments. The details for accessing the provided environments will be shared with you separately.

---

### 1. Explore the User Interface

#### Logging in to IBM Event Streams UI

The _URL_ for Event Streams should have been provided seperately. Navigate to the user interface and you should be navigated automatically to the login page, if you didn't login previously.

> <font size="1">**[Event Streams URL]**</font>

![Log In](resources/Log_In.png)

Select _IBM provided credentials_ and enter the provided _username & password_ and click Log in.

> <font size="1">**[Event Streams Username]**</font><br><font size="1">**[Event Streams Password]**</font>

You should now be logged in and see the _Welcome to Event Streams_ page. You are now ready to start the lab.

#### Explore Event Streams UI

![Event Streams Home Page](resources/Event_Streams_Home.png)

Welcome to **IBM Event Streams**. Let's explore the user interface.

On the home page, you will see some tiles that allow you to quickly navigate to the desired functionality or documentation.

Let's explore a couple of tiles:

1. The **Try the starter application** will generate boilerplate Java code to quickly start using Event Streams. The project will contain a Kafka producer and consumer. It will also help you generate the credentials and properties files, required for the Java application to run properly.

2. The **Documentation** tile will navigate you to the official documentation page of IBM Event Streams.

3. **Connect to this cluster** will open a modal on the page, allowing you to quickly generate credentials, download necessary certificates and list the Kafka bootstrap URL and other information for connecting to the Kafka cluster.

4. **Kafka basics, Connector basics & Schema basics** will give you a basic and quick introduction to Kafka. Each of those tiles will take you through a quick learning guide about the topic and give you a quickstart for understanding Kafka and Event Streams.

5. **Find more in the Toolbox** will give you the tools for quickly start building Kafka applications. It will provide you boilerplate code to start interacting with your cluster, give you access to information about Kafka Connect and how to set up connectors.

In the upper-right corner, you will see a small round icon. If you click on this icon you can either navigate to your profile settings or log out.

On the left side of the screen you will see the navigation menu. By default the menu is collapsed, and you will only see icons. If you want to show the full menu with text, click on the arrow (**>**) in the bottom-left corner of the page.

> Next, click **Topics** in the menu.

![Topics](resources/Topics.png)

The **Topics** page allows you to manage your topics. Here, you will be able to create a topic, manage topics, view more details about a topic, find more information about how to connect to your cluster and topic, generate credentials for accessing the topic and set-up geo-replication. We will dive deeper on topics in a later stage.

> Next, click **Consumer groups** in the menu.

![Consumer Groups](resources/Consumer_Groups.png)

In the **Consumer groups** page you will see more information about your consumers groups, the amount of consumer groups accessing the cluster, active members, status and unconsumed partitions.

Click on a _Consumer group ID_. You should now see more information about the consumer group, like the Current offset, Log end offset and Offset lag. This can give you more insights in how the consumer group is behaving and detect issues early.

> Next, click **Schema Registry** in the menu.

![Schema Registry](resources/Schema_Registry.png)

Apache Kafka can handle any data, but it does not validate the information in the messages. However, efficient handling of data often requires that it includes specific information in a certain format. Using schemas, you can define the structure of the data in a message, ensuring that both producers and consumers use the correct structure.

Schemas help producers create data that conforms to a predefined structure, defining the fields that need to be present together with the type of each field. This definition then helps consumers parse that data and interpret it correctly. Event Streams supports schemas and includes a schema registry for using and managing schemas.

It is common for all of the messages on a topic to use the same schema. The key and value of a message can each be described by a schema.

**Schema Registry**

Schemas are stored in internal Kafka topics by the Apicurio Registry, an open-source schema registry. In addition to storing a versioned history of schemas, Apicurio Registry provides an interface for retrieving them. Each Event Streams cluster has its own instance of Apicurio Registry providing schema registry functionality.

Your producers and consumers validate the data against the specified schema stored in the schema registry. This is in addition to going through Kafka brokers. The schemas do not need to be transferred in the messages this way, meaning the messages are smaller than without using a schema registry.

**Schemas**

Schemas are defined using [Apache Avro](https://avro.apache.org/), an open-source data serialization technology commonly used with Apache Kafka. It provides an efficient data encoding format, either by using the compact binary format or a more verbose, but human-readable JSON format.

The schema registry in Event Streams uses Apache Avro data formats. When messages are sent in the Avro format, they contain the data and the unique identifier for the schema used. The identifier specifies which schema in the registry is to be used for the message.

Avro has support for a wide range of data types, including primitive types (null, boolean, integer, long, float, double, bytes, and string) and complex types (record, enum, array, map, union, and fixed).

**Schema versioning**

Whenever you add a schema, and any subsequent versions of the same schema, Apicurio Registry validates the format automatically and warns of any issues. You can evolve your schemas over time to accommodate changing requirements. You simply create a new version of an existing schema, and the registry ensures that the new version is compatible with the existing version, meaning that producers and consumers using the existing version are not broken by the new version.

> Next, click _Add schema +_

Here you will be able to enter all the necessary information for adding a schema. You can upload the schema definition from a file and give your schema a relevant name and version.

> Next, click _Cancel_

On the **Schema Registry** page, you should see one or more schemas that where preconfigured for you. You should see the schema name, version and Data Format.

If you click on the arrow pointing down, you will see the whole schema definition in JSON format. If you click on the schema name, you will be navigated to the configuration page of that schema.

Here you can:

- Add a new Schema version
- Manage a schema version (deprecate, disable or remove)
- Configure message encoding (JSON, Binary)
- Find all the relevant information to connect to the schema registry, use the schema, generate credentials, etc...

> For more information on schemas and how to use them, navigate to: [Schemas overview](https://ibm.github.io/event-automation/es/schemas/overview/)

Let's have a view at the monitoring page.

> Next, click **Monitoring** in the menu

The Monitoring page allows you to quickly see important information about your Kafka cluster.

At the top, you can choose the timeframe of the data that is displayed (from 1 hour until 1 month). The data refreshes every 15 seconds.

You will see data about incoming and outgoing message size, partitions and replicas.

This data allows you to quickly monitor your cluster usage and detect problems with partitions and replicas.

> Next, click **Toolbox** in the menu

As discussed above, the toolbox will give you the tools for quickly start building Kafka applications and for interacting with your Kafka cluster.

---

### 2. Create a Kafka Topic

Now, we will create our own Kafka topic using the IBM Event Streams user interface. This topic will be used to produce and consume messages, generate access credentials and browse incoming messages

> Select **Topics** from the menu

![Create Topic](resources/Create_Topic.png)

> Select **Create Topic**

![Topic Name](resources/Topic_Name.png)

Choose a unique and recognizable topic name. For this lab, we'd recommend using your **initials** followed by a **.** and ending by **POT**.

For real use-cases, we would typically choose a relevant and meaningful topic name.

> e.g. If my name would be John Doe, I would call my topic: **JOD.POT**

> Fill in your **Topic name**, and click **Next**

![Partitions](resources/Partitions.png)

Here, you can choose the number of partitions for your topic.

By having multiple partitions distributed across the brokers, the scalability of a topic is increased. If a topic has more than one partition, it allows data to be fed through in parallel to increase throughput by distributing the partitions across the cluster.

For the purpose of this lab, you can keep the default of **1 partition**.

> Click **Next**

![Retention](resources/Retention.png)

Now, you need to choose the retention period, meaning the amount of time the Kafka Cluster will keep your messages. After this period, messages will be deleted.

You can keep the default of **a week**.

> Click **Next**

![Replication](resources/Replication.png)

To improve availability and resiliency, each topic can be replicated onto multiple brokers. For each partition, one of the brokers is the leader, and the other brokers are the followers.

You can select **Replication factor: 1, Minimum in-sync replicas: 1** for the purpose of this lab.

![Topic Created](resources/Topic_Created.png)

You will be navigated to the topics page, and hopefully your newly created topic will be displayed in the list of topics.

**Congratulations**! You have just created your first Kafka topic.

### 3. Generate Credentials

Now that we created our very first Kafka topic, let's move on and put our Kafka topic to use. To be able to actually reach our topic from outside and put messages on the topic, we need to connect to our cluster in a secure way.

Each Kafka listener exposing an authenticated connection to Event Streams requires credentials to be presented when connecting. SCRAM-SHA-512 and Mutual TLS authentication credentials are created by using a KafkaUser custom resource

Let's create the credentials for reaching our cluster securely.

From the **Topics** page, locate your previously created topic.

> Navigate to **Topics** and click on your **Topic**

![Connect Topic](resources/Connect_Topic.png)

> Click on **Connect to this topic**

The topic connection information should now display.