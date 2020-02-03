# FarmBeats Hackathon

The FarBeats Hackathon provides a series of challanges learn about the [Azure FarmBeats](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoftfarmbeats.microsoft_farmbeats?tab=Overview) service through hands-on experimentation.


## Challenge #1 - Partner Simulation - Collect Telemetery with FarmBeats 


### Indoor-m1 kit


1. Assemble the FarmBeats Business Kit

   https://github.com/farmbeatslabs/studentkit/blob/master/Indoor-m1/1b_Assemble_your_FarmBeats_Student_Kit_Hardware.md
   
### Azure Iot Dev Kit

1. Connect an MXChip IoT DevKit device to your Azure IoT Central application

    https://docs.microsoft.com/en-us/azure/iot-central/core/howto-connect-devkit



## Challenge #2 - Deploy and configure FarmBeats Azure Service

1. Use the following guide to deploy the Azure FarmBeats service:

   https://docs.microsoft.com/en-us/azure/industry/agriculture/install-azure-farmbeats
   
2. Create a Farm:

   https://docs.microsoft.com/en-us/azure/industry/agriculture/manage-farms-in-azure-farmbeats
   
3. Generate Maps:

   https://docs.microsoft.com/en-us/azure/industry/agriculture/generate-maps-in-azure-farmbeats



## Challenge #3 - Implement Partner Ingegration of Indoor Kit 

Overview: https://docs.microsoft.com/en-us/azure/industry/agriculture/sensor-partner-integration-in-azure-farmbeats


#### 1. Enable device integration with FarmBeats

1. Follow process for generating credential: 

   https://docs.microsoft.com/en-us/azure/industry/agriculture/get-sensor-data-from-sensor-partner#enable-device-integration-with-farmbeats

2. Follow process for registering:

   TBD

#### 2. Create Device Model and Sensor Models for IndoorM1

TBD

#### 3. Create Device and Sensor enttities for deployed Indoor-m1 instance

TBD

#### 4. Add data export in IoT Central to event hub

1. Create event hub
2. Add export in IoT Central

#### 5. Create Azure Function to transform and forward into FarmBeats Service

See Reference Implementation:

    https://github.com/rutzsco/farmbeats-partner-accelerator/tree/develop


## Challenge #4 - Experiment with AI and Analytics via DataHub

Leverage the Timeseries Insights, Blob storage, and DataHub API to create advanced analytics.



