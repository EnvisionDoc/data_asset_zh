# Tutorial Overview

## Scenario

In this tutorial, connect a smart electric meter to EnOS and ingest data to the IoT hub. Then, configure and enable data subscription jobs to subscribe the real-time temperature data and alert records of the smart meter. When the data subscription jobs are enabled, program with EnOS SDK to get the subscribed data. In this way, the real-time device data and alert records can be consumed by your application in a timely manner.

The scenario is depicted in the following chart:

.. image:: media/connect_alert_subscribe.png

This tutorial walks you through a typical path of using the data subscription service of EnOS to subscribe to your device real-time data, which is:

- Registering and connecting a smart electric meter to EnOS Cloud
- Simulating temperature data of the smart meter and configuring alerts to monitor the temperature
- Configuring data subscription jobs on EnOS Console
- Getting the subscribed data by programming with EnOS SDK

### [Start >](registering_device)

## Prerequisites

You have completed the *Connecting Devices into EnOS Using SDK* tutorial to understand how to connect a device to EnOS and upload simulated device data to EnOS Cloud.

## Units

This tutorial includes the following units:

> [Unit 1. Registering and Connecting the Device to EnOS](registering_device)
>
> 10 minutes

> [Unit 2. Simulating Device Data and Configuring Alert Settings](setting_alerts)
>
> 20 minutes

> [Unit 3. Configuring Data Subscription](configuring_subscription)
>
> 10 minutes

> [Unit 4. Getting the Subscribed Data](getting_subscribed_data)
>
> 30 minutes
