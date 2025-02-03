# MQTT Broker and Client Configuration Lab

## Objectives
- Configure an MQTT Broker on a PC.
- Set up MQTT subscribers and publishers on both the PC and IoT devices.

## Equipment
- Computer / Laptop
- M5StickC Plus

## Introduction
MQTT (Message Queue Telemetry Transport) is a lightweight, open, easy-to-implement messaging transport protocol, making it ideal for Internet of Things (IoT) contexts with limited network bandwidth and small code footprint requirements. It operates over TCP/IP or similar network protocols, providing ordered, lossless, bidirectional connections.

### MQTT Components
- **MQTT Broker**: A program that relays messages between clients, requiring each message to be associated with a topic.
- **Topic**: A namespace for categorizing messages on the broker.
- **MQTT Client**: A device that either publishes to or subscribes to a topic on the broker. Clients can publish, subscribe, unsubscribe, and disconnect from the broker.

![image](https://github.com/drfuzzi/CSC2106_MQTT/assets/108112390/1f809798-135f-4cdc-be7e-0085df0b452f)

Figure 1: An Example of a MQTT Implementation

## Setup Instructions

### 1. Setting Up MQTT Broker (on your laptop)
We will use Mosquitto MQTT broker [version 2](http://www.steves-internet-guide.com/download/6-bit-mosquitto-v2/). After unzipping, update the configuration file (`mosquitto.conf`) to allow network address listening.

![overview](https://github.com/user-attachments/assets/ccd7d55a-ce37-42c3-99f8-d6a004bc2fe9)
Figure 2: Overview of the Lab Excercise

#### Steps:
- Update `mosquitto.conf` as shown in below.
- Start the broker with `mosquitto -c mosquitto.conf -v` in the command prompt. Default port is 1883.

```
listener 1883
allow_anonymous true
```

### 2. Setting Up MQTT Client - Subscriber (on your laptop)
Use the following command to start the client as a subscriber:
`mosquitto_sub -h 192.168.x.x -t csc2006`
Replace `192.168.x.x` with the broker’s IP and `csc2006` with your chosen topic.

### 3. Setting Up MQTT Client – Publisher (on your laptop)
Start the client as a publisher using:
`mosquitto_pub -h 192.168.x.x -m “This is CSC2006” -t csc2006`
Ensure the broker's IP and topic match the subscriber's settings (`-h` to specify the IP for the broker and `-t` to specify the topic).

### 4. Setting Up MQTT Client (on the M5StickC Plus)
Configure the MQTT client on M5StickC Plus using API libraries and the provided sample code [mqtt.ino](mqtt.ino). Ensure correct SSID, password, and broker IP. Test communication with the PC subscriber.

## Common Problems and Solutions
- **Mismatched Topics**: Ensure both publisher and subscriber are using the same topic name.
- **Incorrect Broker IP**: Verify the IP address of the MQTT broker.
- **Network Issues**: Check for proper network connectivity and firewall settings.

## Lab Assignment
1. **Node Interaction Using MQTT**
   - Configure two M5StickC devices (Node A and Node B).
   - Node A should toggle Node B's LED (and vice-versa) upon button press.
   - Implement and propose appropriate topic names for this interaction.

## References
1. [Mosquitto Install Guide](http://www.steves-internet-guide.com/install-mosquitto-broker/)
2. [Mosquitto Broker Guide](http://www.steves-internet-guide.com/mosquitto-broker/)
3. [Mosquitto Client Publish & Subscribe Guide](http://www.steves-internet-guide.com/mosquitto_pub-sub-clients/)
4. [Arduino MQTT Client Code](https://github.com/m5stack/M5StickC-Plus/blob/master/examples/Advanced/MQTT/MQTT.ino)
5. [Thingsboard MQTT Integration](https://thingsboard.io/docs/user-guide/integrations/mqtt/)
6. [Thingspeak MQTT Basics](https://www.mathworks.com/help/thingspeak/mqtt-basics.html)
