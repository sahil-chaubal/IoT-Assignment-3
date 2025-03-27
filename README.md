# IoT-Assignment-3


# CIS600 IoT Assignment 3: Cloud-based IoT System using AWS IoT Core

## Project Description
This project implements a cloud-based IoT system that collects environmental sensor data from virtual sensors using the MQTT protocol. A virtual sensor station (publisher) generates random sensor readings for temperature, humidity, and CO₂ levels, and publishes these readings as JSON messages. The cloud-based backend (subscriber) running on AWS IoT Core securely receives these messages, stores the data, and provides functions to:
- Display the latest sensor data for a specified environmental station.
- Display sensor data values collected over the last five hours for a specified sensor type.

## Setup Instructions

### Prerequisites
- **Python 3.x**: Ensure that Python 3 is installed on your machine.
- **paho-mqtt Library**: Install the MQTT client library by running:
  ```bash
  pip install paho-mqtt

    AWS Account: Access to an AWS account to configure AWS IoT Core.

AWS IoT Core Configuration

    Create a Thing:

        Log in to the AWS Management Console and navigate to AWS IoT Core.

        Under Manage → Things, click Create things and choose Create a single thing.

        Provide a unique name (e.g., IoT) and complete the setup.

    Generate and Download Certificates:

        After creating the thing, generate a device certificate.

        Download the following files:

            Device certificate (e.g., certificate.pem.crt)

            Private key (e.g., private.pem.key)

            Amazon Root CA (e.g., AmazonRootCA1.pem)

    Attach a Policy:

        Create a policy that permits the following actions: iot:Connect, iot:Publish, iot:Subscribe, and iot:Receive.

        Example policy JSON:

        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "iot:Connect",
                        "iot:Publish",
                        "iot:Subscribe",
                        "iot:Receive"
                    ],
                    "Resource": "*"
                }
            ]
        }

        Attach this policy to your certificate.

    Obtain the AWS IoT Endpoint:

        In the AWS IoT Core console, navigate to Settings.

        Copy the Endpoint value (e.g., a1b2c3d4e5f6-ats.iot.us-west-2.amazonaws.com).

Local Environment Setup

    Clone this repository to your local machine.

    Place your AWS IoT certificate files in a secure directory.

    Update the file paths and AWS IoT endpoint in both the publisher and subscriber scripts as needed.

Running the Code
Publisher Script

The publisher script simulates a virtual sensor station that:

    Generates random sensor data for temperature (–50°C to 50°C), humidity (0% to 100%), and CO₂ (300ppm to 2000ppm).

    Publishes the data to an MQTT topic using TLS on AWS IoT Core.

To run the publisher:

python publisher.py

Subscriber Script

The subscriber script:

    Connects securely to AWS IoT Core.

    Subscribes to the MQTT topic to receive sensor data.

    Processes incoming messages, stores them, and provides functions to display:

        The latest sensor data for a specified station.

        The sensor data from the last five hours for a specified sensor type.

To run the subscriber:

python subscriber.py
