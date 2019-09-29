# Unit 3: Configuring Data Subscription Jobs

To subscribe to the real-time measuring point data and alert records of the electric meter, you need to configure data subscription jobs on the EnOS Console first. For more information about the features of the Data Subscription service, see [Data Subscription](../../learn/data_subscription_overview).

Follow the instructions below to configure data subscription jobs for the device real-time data and alert records separately.

## Subscribing to Real-Time Data

Take the following steps to configure a subscription job for the real-time measuring point data of the electric meter:

1. Log in EnOS Console and select **Data Subscription > New Subscription**.

2. Configure the subscription job with the following settings:

.. list-table::
   :widths: 20 80

   * - Item
     - Value
   * - Type
     - Select "Real-time Data Subscription".
   * - ID
     - Enter an ID for the subscription job, for example "sub-001".
   * - SA
     - Select your application service account from the drop-down list.
   * - Description
     - Enter short description for the subscription job.
   * - Customers
     - Select the customers whose data are to be subscribed to (typically your own organization).
   * - Model Filter
     - Select the *Grid.TopupAcMeter* model and the *Temperature* measuring point for this tutorial.

3. Click **Save** to complete the configuration.

See the following example of the created data subscription job.

.. image:: media/subscription_config_1.png

For detailed information about configuring subscription jobs for real-time data, see [Subscribing to Real-time Data](../../quickstart/gettingstarted_subscribe_realtime).

## Subscribing to Alert Records

Take the following steps to configure a subscription job for the alerts on the electric meter:

1. Log in EnOS Console and select **Data Subscription > New Subscription**.

2. Configure the subscription job with the following settings:

.. list-table::
   :widths: 20 80

   * - Item
     - Value
   * - Type
     - Select "Alert Data Subscription".
   * - ID
     - Enter an ID for the subscription job, for example "sub-002".
   * - SA
     - Select your application service account from the drop-down list.
   * - Description
     - Enter short description for the subscription job.
   * - Customers
     - Select the customers whose data are to be subscribed to (typically your own organization).
   * - Model Filter
     - Select the *Grid.TopupAcMeter* model for this tutorial.

3. Click **Save** to complete the configuration.

See the following example of the created alert subscription job.

.. image:: media/subscription_config_2.png

For detailed information about configuring subscription jobs for alert records, see [Subscribing to Alert Data](../../quickstart/gettingstarted_subscribe_alerts).

## Authorizing the application service account

The application service account (SA) associated with the data subscription jobs must be authorized to access the asset data and alert records. Otherwise, the data subscription jobs will fail because of authentication failure. Take the following steps to authorize the application service account:

1. Log in EnOS Console with the administrator account and select **IAM > Policy**.

2. Click **New Policy**, enter the policy name and description, and click **Next**.

3. Under the **EnOS Services** tab, click **New Rule**, and select **Asset** from the **Service** drop-down list.

4. For **All Assets**, select `control`, `read`, and `write` permission, and click **Save** to save the authorization policy.

   .. image:: media/authorization_policy.png

5. Select **IAM > Service Account**, find your application from the list, and click the **Authorize** icon from the **Operation** column.

6. On the **Authorize** page, click **Assign Policies**, select the created authorization policy, and click **Save**.

   .. image:: media/authorizing_sa.png

After authorizing the application service account with asset access permission, you can enable the data subscription jobs. For detailed information about authorizing the service account, see [Managing Service Accounts](/docs/iam/zh_CN/2.0.9/howto/service_account/managing_service_account.html).

## Enabling the subscription jobs

When the configuration of the subscription jobs is saved, you can enable the jobs by clicking the **Enable** icon in the **Operations** column of the subscription job list.

.. image:: media/enable_jobs.png

Once the subscription jobs are enabled, the data subscription service will be running to filter device data and alert data according to the settings.

## Next Unit

[Getting the Subscribed Data](getting_subscribed_data)

<!--end-->
