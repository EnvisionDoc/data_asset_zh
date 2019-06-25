# Unit 3: Registering and Connecting Device into EnOS

After your device model is created and data storage policy is configured based on the device model, you can start to register the electric meter on the EnOS Console and perform device-end development so that the device connects to EnOS Cloud and transmits data with EnOS.

## Create a product for the electric meter

Create a product with the following basic settings:

- **Product Name**: SmartElectricMeter
- **Asset Type**: Device
- **Model**: ElectricMeter
- **Data Type**: Json
- **Certificate-based bi-directional authentication**: Disabled
- **Description**: Smart Electric Meter

## Register the electric meter device

Create a smart electric meter device with the following basic settings:

- **Product**: SmartElectricMeter
- **Device Name**: Meter01
- **Use DST**: No
- **timezone**: UTC+08:00
- **Device Key**: Optional (it can be generated automatically by the system)

## Perform device-end development and initialize connection

The *Connecting a Simulated Device into EnOS* tutorial describes detailed steps for how to perform device-end development. You can follow the same steps to connect the smart electric meter for this tutorial.

## Next Unit

[Developing Stream Data Processing Jobs](developing_streams)

<!--end-->