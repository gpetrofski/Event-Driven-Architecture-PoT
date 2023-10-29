# LAB 03 - Event Processing

![IBM Event Processing](resources/images/Event_Processing.png)

## Event Processing: Introduction

**Event Processing** is a scalable, low-code event stream processing platform that helps you transform and act on data in real time.

Event Processing transforms event streaming data in **real time**, helping you turn events into **insights**. You can define flows that connect to event sources which bring event data (messages) from Apache Kafka into your flow, combined with processing actions you want to take on your events.

The flows are run as [Apache Flink](https://flink.apache.org/) jobs. Apache Flink is a framework and a distributed processing engine for stateful computations over event streams. In addition to being the processing engine for Event Processing, Flink is also a standalone engine you can run custom Flink SQL workloads with.

### Features

Event Processing features include:

- A user interface (UI) designed to provide a low-code experience.
- A free-form layout canvas to create flows, with drag-and-drop functionality to add and join nodes.
- The ability to test your event flow while constructing it.
- The option to import and export flows in JSON format to reuse across different deployment instances.
- The option to export the output of the flow processing to a CSV file.

> [!NOTE]
> IBM Event Processing is part of IBM Event Automation. To read more about Event Automation, navigate to: [Event Automation](https://www.ibm.com/products/event-automation). For more information on Event Processing: [Event Processing](https://ibm.github.io/event-automation/ep/).

## Event Processing: Lab Introduction

In this lab you will discover the main capabilities provided by Event Processing.

- Part 1 - Create an **Event Processing flow** and connect to an **event source** to bring events into your flow
- Part 2 - **Filter** event sources to discard events in the stream that don't match a specific condition
- Part 3 - **Join** events by combining two streams of events that match a condition within a time window
- Part 4 - **Transform** events by renaming and removing properties in events and create new properties
- Part 5 - **Aggregate** events to perform calculations on groups of events within a time window
- Part 6 - Connect to an **event destination** and write your (processed) events to it, allowing others to work with those events

### Part 1 - Create a flow and connect to an event source

#### 1. Logging in to the Event Processing platform

The _URL_ for Event Processing should have been provided seperately. Navigate to the user interface and you should be navigated automatically to the login page, if you didn't login previously.

> <font size="1">**[Event Processing URL]**</font>

<div style="text-align:center;margin:25px;">
  <img src="resources/images/Event_Processing_Login.png" alt="Event Processing Login" width="400"/>
</div>

1. Fill in the Event Processing _username_ anc click **Continue**
2. Fill in the Event Processing _password_ and click **Log In**

> <font size="1">**[Event Processing Username]**</font><br><font size="1">**[Event Processing Password]**</font>

You should now be logged in and see the _Welcome to Event Processing_ page.

![Event Processing Landing Page](resources/images/Event_Processing_Landing.png)

On the Event Processing dashboard, you will see different tiles. The most important tile if for creating or importing flows. The other tiles will guide you to Event Processing [tutorials](https://ibm.github.io/event-automation/tutorials/) and product [documentation](https://ibm.github.io/event-automation/) pages.

Below, we have an overview of all the flows we created. We can find flows by entering a search or by filtering by date or status, or create or import a flow.

Now that we are logged in, let's start by creating our first Event Processing flow!

---

#### 2. Creating an Event Processing flow

1. Click on **Create +**

<div style="text-align:center;margin:25px;">
  <img src="resources/images/Event_Processing_Create_Flow.png" alt="Event Processing Create Flow" width="300"/>
</div>

2.

<div style="text-align:center;margin:25px;">
  <img src="resources/images/Event_Processing_Create_Flow_Details.png" alt="Event Processing Create Flow Details" width="300"/>
</div>

<div style="text-align:center;margin:25px;">
  <img src="resources/images/Event_Processing_Empty_Flow_Canvas.png" alt="Event Processing Empty Flow Canvas"/>
</div>
