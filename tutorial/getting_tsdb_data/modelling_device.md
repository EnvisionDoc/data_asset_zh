# Unit 1: Modelling the Device

Create a model for the electric meter with the following basic settings:

- **Identifier**: ElectricMeter
- **Model Name**: ElectricMeter
- **Category**: Grid
- **Created From**: No
- **Source Model**: NA
- **Description**: Model for electric meter

Define the measuring points for the model:

.. list-table::
   :widths: auto

   * - Feature Type
     - Name   
     - Identifier   
     - Point Type
     - Description   
   * - Measuring Point
     - Reading
     - Reading
     - AI
     - Original meter reading data
   * - Measuring Point
     - MaxReading10Min
     - MaxReading10Min
     - AI
     - Maximum reading data in 10 minutes
   * - Measuring Point
     - MinReading10Min
     - MinReading10Min
     - AI
     - Minimum reading data in 10 minutes
   * - Measuring Point
     - ReadingDifference
     - ReadingDifference
     - AI
     - Difference between the maximum data and minimum data

See the following example:

.. image:: media/measure_points.png

## Next Unit

[Configuring Storage Policy for the Device Data](configuring_storage_policy)
