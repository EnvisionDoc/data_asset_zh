# Unit 2: Configuring Storage Policy for the Device Data

EnOS Time Series Database (TSDB) enables you to store important and frequently-accessed business data with a variety of data storage options. Data is stored in TSDB by categories (data types and storage time), thus reducing data storage costs and enhancing data reading efficiency.

Before the reading data of the electric meter is uploaded to EnOS Cloud, you need to configure data storage policy for the uploaded data. Otherwise, the uploaded data will not be stored in EnOS TSDB by default.

In this tutorial, configure storage policy for the following measuring points that have been defined when creating the electric meter model.

| Measuring Point     | Storage Type       | Description                                                  |
| ----------------- | ------------------ | ------------------------------------------------------------ |
| Reading           | AI Raw Data        | When the reading data of the electric meter is uploaded, store the raw data of the *Reading* measuring point in TSDB directly. |
| MaxReading10Min   | AI Normalized Data | Get the maximum value of the reading data every 10 minutes with the stream processing engine, and then store the minute-level normalized data in TSDB. |
| MinReading10Min   | AI Normalized Data | Get the minimum value of the reading data every 10 minutes with the stream processing engine, and then store the minute-level normalized data in TSDB. |
| ReadingDifference | AI Normalized Data | Get the difference between the maximum and minimum values of the reading data with the stream processing engine, and then store the normalized data in TSDB. |

For detailed description of the supported storage types, see [Configuring TSDB Storage](https://www.envisioniot.com/docs/data-asset/en/latest/configuring_tsdb_storage.html).

## Creating a storage policy group

1. Log in EnOS Console and select the **Storage Policy** module.

2. Click **New Group** to create a storage group. Enter the group name, select a group model (select *ElectricMeter* for this tutorial).

3. Click **OK** to save the storage policy group configuration.


## Configuring the storage policy

After the storage group is created, you can see all the TSDB storage policy options listed under the storage group tab. Configure **AI Raw Data** and **AI Normalized Data** policies separately for the *Reading*, *MaxReading10Min*, *MinReading10Min*, and *ReadingDifference* measuring points.

For configuring the **AI Raw Data** storage type, take the following steps:

1. Move the cursor on the **AI Raw Data** storage type and click the **Edit** icon to open the **Edit Storage Policy** page.

2. From the **Storage Time** drop down list, select the storage time for the data (for example, 3 months).

3. Select the *ElectricMeter* model and the *Reading* measuring point.

4. Click **OK** to save the storage policy. See the following example.

   .. image:: media/storage_policy_config_1.png

For configuring the **AI Normalized Data** storage type, take the following steps:

1. Move the cursor on the **AI Normalized Data** storage type and click the **Edit** icon to open the **Edit Storage Policy** page.

2. From the **Storage Time** drop down list, select the storage time for the data (for example, 3 months).

3. Select the *ElectricMeter* model and the *MaxReading10Min*, *MinReading10Min*, and *ReadingDifference* measuring points.

4. Click **OK** to save the storage policy. See the following example.

   .. image:: media/storage_policy_config_2.png

With the storage policies configured, raw data of the electric meter reading will be stored as **AI Raw Data** storage type, and the minute-level normalized data output from the stream processing engine will be stored as **AI Normalized Data** storage type.

## Next Unit

[Registering and Connecting Device into EnOS](connecting_device)

<!--end-->
