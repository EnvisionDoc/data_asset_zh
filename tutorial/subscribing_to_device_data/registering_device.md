# Unit 1: Registering the Device on EnOS Console

Before connecting a smart electric meter to EnOS IoT hub, you need to register the electric meter on the EnOS Console, including defining the electric meter model, creating a meter product, registering a meter device.

The *Connecting Devices into EnOS Using SDK* tutorial describes detailed steps for registering a device on EnOS Console. You can follow the same steps to register a smart electric meter, with the following information:

## Creating a model

Create a model with the following basic settings:

- **Identifier**: Grid.TopupAcMeter
- **Model Name**: Grid.TopupAcMeter
- **Category**: Grid
- **Create From**: No
- **Support Passthrough**: No
- **Source Model**: NA
- **Description**: AC meter that has a temperature sensor

Define the "Temperature" measuring point for the model:

.. list-table::
   :widths: auto

   * - Feature Type
     - Name   
     - Identifier   
     - Point Type
     - Data Type   
   * - Measuring Point
     - Temperature
     - Temperature
     - AI
     - double

## Creating a product

Create a product with the following basic settings:

- **Product Name**: Grid.PrepaidElectricityMeter
- **Asset Type**: Device
- **Model**: Grid.TopupAcMeter
- **Data Type**: Json
- **Certificate-based bi-directional authentication**: Disabled
- **Description**: State grid standard electricity meter

## Creating a device

Create a smart electric meter with the following basic settings:

- **Product**: Grid.PrepaidElectricityMeter
- **Device Name**: Demo_meter
- **Use DST**: No
- **timezone**: UTC+08:00
- **Device Key**: Optional (it can be generated automatically by the system)



## Next Unit

[Simulating Device Data and Configuring Alert Settings](setting_alerts)
