<img align="left" width="80" height="80" src="/Images/lildrone.png" alt=">Drone icon">

# PrestaCop
This project is realized within the course **Functional Data Programming** at the **Efrei Paris**.

## Problem Description
**PrestaCop** is a company that wants to create a drone service to help the police make parking tickets.

Each drone sends messages regularly, with:
- drone location
- time
- drone id

And if a violation occured, with the two following additional fields:
- violation code
- image id

When the drone's message violation code indicates that human interaction is required (1% of the time), an alarm must be send to a human operator.

With all the data, PrestaCop wants to make statistics and improve their services. To improve those statistics, NYPD historical data should be used. However, NYPD poses two constraints:
- The computers are old and not very powerful
- The data is stored in a large CSV

## Architecture
The basic part of this project consists of the following 5 Services, a stream and a storage solution:
- **csv-to-stream**: Reads the NYPD CSV and publishes the rows as messages to the stream
- **drone-simulator**: Simulates a drone, sends messages of different forms to the stream
- **alert-system**: Consumes stream messages, raises an alarm when human interaction is required
- **stream-to-storage**: Consumes stream messages, stores them
- **analysis**: Reads messages out of storage, performs the analysis

The following picture depicts how the components work together:
![Architecture](/Images/Architecture_v1.png)

The following picture depicts our current AWS architecture:
![Architecture](/Images/AWS_Architecture_v2.png)

## Data Model
As described above, the drone sends messages wit 3 or 5 fields. We used a Scala case class **Message** to realize this data format:
```scala
case class Message(
                    location: String,
                    time: String,
                    droneId: String,
                    violationCode: Option[String] = None,
                    violationImageId: Option[String] = None
                  )
```

## Launch the project

Because our project runs on AWS, there is an infrastructure to create. You should start with the create-infrastructure readme.md.  

Everything will run automatically. See the analysis readme for the analysis part.