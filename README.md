# FarmBeats Hackathon

The FarBeats Hackathon provides a series of challanges to learn about the [Azure FarmBeats](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoftfarmbeats.microsoft_farmbeats?tab=Overview) service through hands-on experimentation.


## Challenge #1 - Partner Simulation - Collect Telemetery with FarmBeats 


### Indoor-m1 kit


1. Assemble the FarmBeats Business Kit:

   https://github.com/farmbeatslabs/studentkit/blob/master/Indoor-m1/1b_Assemble_your_FarmBeats_Student_Kit_Hardware.md
   
### Azure Iot Dev Kit

1. Connect an MXChip IoT DevKit device to your Azure IoT Central application:

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

1. Create Sensor Models

##### Example POST Requests

```json
POST /SensorModels

{
   "type":"Digital",
   "productCode":"Grove-Air-Tempurature-001",
   "name":"Grove Air Tempurature",
   "SensorMeasures":[
      {
         "name":"tempurature",
         "dataType":"Double",
         "type":"AmbientTemperature",
         "unit":"Fahrenheit"
      }
   ]
}

```

```json
POST /SensorModels

{
   "id":null,
   "type":"Digital",
   "productCode":"Grove-Soil-Moisture-001",
   "name":"Grove Soil Moisture",
   "SensorMeasures":[
      {
         "name":"reading1",
         "dataType":"Double",
         "type":"SoilMoisture",
         "unit":"Percentage"
      },
      {
         "name":"reading2",
         "dataType":"Double",
         "type":"SoilMoisture",
         "unit":"Percentage"
      }
   ]
}

```

2. Create Device Model

##### Example POST Request
```json
POST /DeviceModels

{
   "type":"Node",
   "manufacturer":"Microsoft FarmBeats Business Kit",
   "name":"Indoor-M1",
   "description":"Raspberry Pi with Light, Soil Moisture, Air Temperature, Humidity, and Barometric Pressure sensors.",
   "sensorModels":[
      "Grove Soil Moisture",
      "Grove Ambient Light",
      "Grove Air Pressure",
      "Grove Air Humidity",
      "Grove Air Tempurature"
   ]
}

```


#### 3. Create Device and Sensor entities for deployed Indoor-m1 instance

1. Create Device

```json

TBD

```

2. Create Sensor

```json

TBD

```

#### 4. Add data export in IoT Central to event hub

1. Create event hub
2. Capture the connection string
3. Add export to event hub in IoT Central

#### 5. Create Azure Function to transform and forward into FarmBeats Service

See Reference Implementation:

    https://github.com/rutzsco/farmbeats-partner-accelerator/tree/develop


## Challenge #4 - Experiment with AI and Analytics via DataHub

Leverage the Timeseries Insights, Blob storage, and DataHub API to create advanced analytics.



