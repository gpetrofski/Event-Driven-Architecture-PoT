# LAB 01A MQ to EventStreams

> [!WARNING] >**DRAFT** still under work

![](resources/images/2023-11-02-12-56-42.png)

[info on MQ Streaming](https://www.ibm.com/docs/en/ibm-mq/9.3?topic=scenarios-streaming-queues)

### Create a Queue

1. Open the MQ Web UI:

[MQ Console](https://mq-demo-rest-cp4i-mq.apps.melch.coc-ibm.com/ibmmq/console)
![](resources/images/2023-11-01-20-09-52.png)

2. Click on Manage in the left menu

![](resources/images/2023-11-01-20-11-01.png)

3. Click on the **Local Queue Manager** (see previous screenshot)

In the local queue manager, the queue manager **QMGRDEMO** is listed
![](resources/images/2023-11-01-20-11-26.png)

4. Click on the queue manager **QMGRDEMO**

You have a view of all the queues that are available on this queue manager.
You will create a queue for your application.

5. Click **Create**

![](resources/images/2023-11-01-20-12-15.png)

6. Choose a **LOCAL** queue

![](resources/images/2023-11-01-20-12-41.png)

7. Provide a queue name

> [!NOTE]
> For this lab, follow the following pattern for the queue name: \*LQ.APP.USER**\*X**. Where X is the number that has been assigned to you: **LQ.APP.USER1**.

8. Click Create

![](resources/images/2023-11-01-20-13-42.png)

9. Click on your queue

![](resources/images/2023-11-01-20-17-48.png)

You will see that the queue is empty.
![](resources/images/2023-11-01-20-27-49.png)

### Send/receive MQ message

We have exposed a REST API to send and receive MQ messages.  
The REST API is available on the developer portal of API Connect.

1. Navigate to the API Connect Developer portal

Navigate to the developer portal and you should be navigated automatically to the login page, if you didn't login previously.

[API Connect Developer Portal](https://apim-demo-ptl-portal-web-cp4i-apic.apps.melch.coc-ibm.com/melch-admin-porg/sandbox)

1. Enter the provided _username & password_ and click **Sign in**.

> [!IMPORTANT]  
> UserName have the following pattern: devuser**x**  
> where x is the number that has been provided to you. It is not possible to have two sessions opened as the same time with the same user. Please take the user that has been provided.  
> The password should be provided by the assistant.

You should now be logged in and see the _API Connect Developer Portal_.

3. Select the **MQ Utils** product.

![](resources/images/2023-11-01-20-20-02.png)

4. Select the **MQ-QMGRDEMO** API

![](resources/images/2023-11-01-20-20-45.png)

5. Select the **POST /stringMessafe**

![](resources/images/2023-11-01-20-21-42.png)

6. Click on **Try it**

![](resources/images/2023-11-01-20-22-12.png)

7. Provide the **QueueName** and a **message**

The queue name should be the name of the queue that you created.  
For the message, please use a JSON message with a content that you can recognize. In the example user, the user name has been provided to easily identify your message.

![](resources/images/2023-11-01-20-23-50.png)

8. Click on **send**

The response is provided here with a status code 201.
![](resources/images/2023-11-01-20-24-12.png)

> [!NOTE]
> Don't close the page as we will use it to send and receive other messages.

9. Navigate back to the MQ console and select your queue

[MQ Console](https://mq-demo-rest-cp4i-mq.apps.melch.coc-ibm.com/ibmmq/console)

![](resources/images/2023-11-01-20-25-14.png)

You message should be visible.

> If you left your MQ UI on the queue view, you can refresh the content using the refresh button located just on the left of the create button.

![](resources/images/2023-11-01-20-25-32.png)

10. Navigate back to the API Connect developer portal
11. Select the **GET /stringMessage** to get MQ messages and **tryIt**

Provide the QueueName that you have used previously.  
![](resources/images/2023-11-01-20-26-41.png)

12. Click **Send**
    The message is get out from the queue and displayed in the UI.

![](resources/images/2023-11-01-20-26-58.png)

> [!NOTE]
> The message has been read destructively from the queue (default behavior)

13. Navigate back to the MQ console and select your queue

Verify that the message has been removed from the queue. You might need to click on the refresh button.  
![](resources/images/2023-11-01-20-27-30.png)

### Configure MQ Streaming

1. Select the queue that you created

![](resources/images/2023-11-01-20-27-49.png)

2. Select in **Actions** the option **view configurations**
   ![](resources/images/2023-11-01-20-29-21.png)

3. Select the **EDit**
   ![](resources/images/2023-11-01-20-29-59.png)

4. Select **Storage** in the right side menu

![](resources/images/2023-11-01-20-30-41.png)

5. Add the streaming queue

Provide as queue name **LQ.KAFKA.SOURCE**.  
De MQ Kafka Connect has been configured to get messages from **LQ.KAFKA.SOURCE**. Any messages that arrives on this queue will be get by the kafka connect and put in the EventStreams Topic **MQ.SOURCE**.

![](resources/images/2023-11-01-20-31-48.png)

6. Click **Save**

7. Go back to your queue view
   ![](resources/images/2023-11-01-20-32-56.png)

8. Send back a message to your queue **LQ.APP.USERX** (X been your assigned number)

In API Connect developer portal, select POST:  
![](resources/images/2023-11-01-20-26-41.png)

Provide your queue name **LQ.APP.USERX**

> [!IMPORTANT]
> Its **not** the Kafka queue that you have to use here.

Send a message that you can easily identify:  
![](resources/images/2023-11-01-20-26-58.png)

12. Click **Send**
    The message is get out from the queue and displayed in the UI.

13. Navigate to the EventStreams UI

[EventStreams UI](https://cpd-cp4i.apps.melch.coc-ibm.com/integration/kafka-clusters/cp4i-eventstreams/es-demo/)

14. Select **topic** in the left menu and select topic **MQ.SOURCE**

![](resources/images/2023-11-01-20-37-49.png)

15. Your message should be there !!
    ![](resources/images/2023-11-01-20-39-30.png)

---

### Next Lab

| Lab                       | Location                                          | Description                                                                                                   |
| ------------------------- | ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Event Endpoint Management | [LAB 02](../../Lab_02_Event_Endpoint_Management/) | Learn how to describe and catalog your Kafka topics as event sources, and how to securely subscribe to topics |
