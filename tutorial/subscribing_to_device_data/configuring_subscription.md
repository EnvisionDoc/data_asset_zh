# Unit 3: Configuring Data Subscription

To subscribe to the real-time measuring point data and alert records of the electric meter, you need to configure data subscription on the EnOS Console. For more information about the features of the Data Subscription service, see [Data Subscription](https://www.envisioniot.com/docs/data-asset/en/latest/learn/data_subscription_overview.html).

Follow the instructions below to configure data subscriptions for the device real-time data and alert record separately.

## Subscribing to Real-Time Data

Take the following steps to configure a subscription for the real-time measuring point data of the electric meter:

1. Log in EnOS Console and select **Data Subscription > New Subscription**.

2. Configure the subscription with the following settings:

.. list-table::
   :widths: 20 80

   * - Item
     - Value
   * - Type
     - Select "Real-time Data Subscription".
   * - ID
     - Enter an ID for the subscription, for example "sub-001".
   * - SA
     - Select your application service account from the drop-down list.
   * - Description
     - Enter short description for the subscription.
   * - Customers
     - Select the customers whose data are to be subscribed to (typically your own device data).
   * - Model Filter
     - Select the *Grid.TopupAcMeter* model and the *Temperature* measuring point for this tutorial.

3. Click **Save** to complete the configuration.

See the following example of the created data subscription.

.. image:: media/subscription_config_1.png

For detailed information about configuring subscriptions for real-time data, see [Subscribing to Real-time Data](https://www.envisioniot.com/docs/data-asset/en/latest/quickstart/gettingstarted_subscribe_realtime.html).

## Subscribing to Alert Records

Take the following steps to configure a subscription for the alerts on the electric meter:

1. Log in EnOS Console and select **Data Subscription > New Subscription**.

2. Configure the subscription with the following settings:

.. list-table::
   :widths: 20 80

   * - Item
     - Value
   * - Type
     - Select "Alert Data Subscription".
   * - ID
     - Enter an ID for the subscription, for example "sub-002".
   * - SA
     - Select your application service account from the drop-down list.
   * - Description
     - Enter short description for the subscription.
   * - Customers
     - Select the customers whose data are to be subscribed to (typically your own device data).
   * - Model Filter
     - Select the *Grid.TopupAcMeter* model for this tutorial.

3. Click **Save** to complete the configuration.

See the following example of the created data subscription.

.. image:: media/subscription_config_2.png

For detailed information about configuring subscriptions for alert record, see [Subscribing to Alert Data](https://www.envisioniot.com/docs/data-asset/en/latest/quickstart/gettingstarted_subscribe_alerts.html).

## Enabling the subscriptions

When the configuration of the subscriptions is saved, you can enable the jobs by clicking the **Enable** icon in the **Operations** column of the subscription list.

.. image:: media/enable_jobs.png

Once the subscriptions are enabled, the data subscription service will be running to filter device data according to the settings.

## Next Unit

[Getting the Subscribed Data](getting_subscribed_data)

<!--end-->
