# Tutorial Overview

## Scenario

In this tutorial, connect a smart electric meter to EnOS Cloud and ingest the meter reading data. Then, develop stream processing jobs to aggregate the origin meter reading data to get the calculated data that can be used for analysis. Both the origin data and calculated data will be stored in TSDB by the configured storage types and storage time. The stored data can be retrieved with the TSDB Data Service APIs.

The scenario is as depicted in the following chart:

.. image:: media/scenario_stream_tsdb_api.png

This tutorial walks you through a typical path of processing and storing the stream data of your devices, that is: 

- Registering and connecting an electric meter to EnOS Cloud.
- Configuring storage policy for the reading data of the electric meter.
- Developing a stream data processing job to calculate the maximum and minimum values of the meter reading data in every 10 minutes .
- Developing a stream data processing job to get the difference between the maximum and minimum values of the reading data in every 10 minutes.
- Invoking EnOS TSDB Data Service APIs to get the stored meter reading data and calculated data.

### [Start >](modelling_device)

## Prerequisites

You have completed the [Connecting a Simulated Device into EnOS](/docs/device-connection/en/2.0.8/tutorial/connecting_device_simulated/index.html) tutorial to understand how to connect a device to EnOS and upload simulated device data to EnOS Cloud.

You understand how real-time data flows through the engines, the storage, and the applications. For more information, see [Real-time Data Flow](/docs/data-asset/en/2.0.8/learn/data_flow). 

## Units

This tutorial includes the following units:

> [Unit 1. Modelling the Device](modelling_device)
>
> 10 minutes

> [Unit 2. Configuring Storage Policy for the Device Data](configuring_storage_policy)
>
> 10 minutes

> [Unit 3. Registering and Connecting Device into EnOS](connecting_device)
>
> 20 minutes

> [Unit 4. Developing Stream Data Processing Jobs](developing_streams)
>
> 20 minutes

> [Unit 5. Getting Stored Data with EnOS APIs](getting_stored_data)
>
> 30 minutes

