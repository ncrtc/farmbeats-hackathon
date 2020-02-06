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
   
   *Troubleshooting Notes:*
   
   > Error: Entry not found in cache. View following [Link](https://social.msdn.microsoft.com/Forums/sharepoint/en-US/5ae1d454-c0d6-4a29-9f09-4e9b9f13ab1d/unable-to-deploy-azure-farmbeats) for resolution details.
   
2. Create a Farm:

   https://docs.microsoft.com/en-us/azure/industry/agriculture/manage-farms-in-azure-farmbeats
   
3. Generate Maps:

   https://docs.microsoft.com/en-us/azure/industry/agriculture/generate-maps-in-azure-farmbeats



## Challenge #3 - Implement Partner Integration of Indoor Kit 

Overview: https://docs.microsoft.com/en-us/azure/industry/agriculture/sensor-partner-integration-in-azure-farmbeats


#### 1. Enable device integration with FarmBeats

This step creates a client that has access to your Azure FarmBeats instance as the device partner. Generating your Farm Beats partner will provide your with the following:

- Tenant ID
- Client ID
- Client secret
- EventHub connection string

##### Azure Cloud Shell Access

Grant Azure Cloud Shell Access to Farm Beats API deployment (https://<datahub>.azurewebsites.net)

1. Download the [zip file](https://aka.ms/farmbeatspartnerscriptv2), and extract it to your local drive. There will be one file inside the zip file.

2. Sign in to [Azure Portal](https://portal.azure.com/) and go to Azure Active Directory -> App Registrations

3. Click on the App Registration that was created as part of your FarmBeats deployment. It will have the same name as your FarmBeats Datahub.

4. Click on “Expose an API” -> Click “Add a client application” and enter 04b07795-8ddb-461a-bbee-02f9e1bf7b46 and check "Authorize Scope". This will give access to the Azure CLI (Cloud Shell) to perform the below steps.

##### Generate Partner


1. Open Cloud Shell. This option is available on the toolbar in the upper-right corner of the Azure portal.

![cloud shell bar](/images/navigation-bar-1.png)

2. Make sure the environment is set to PowerShell. By default, it's set to Bash.

![cloud shell bar](/images/power-shell-new-1.png)

3. Upload the file from step 1 in your Cloud Shell instance.

![cloud shell bar](/images/power-shell-two-1.png)

4. Go to the directory where the file was uploaded. By default, files get uploaded to the home directory under the username.
Run the following script. The script asks for the Tenant ID which can be obtained from Azure Active Directory -> Overview page.

```bash
./generatePartnerCredentials.ps1
```

5. Follow the onscreen instructions to capture the values for API Endpoint, Tenant ID, Client ID, Client Secret, and EventHub Connection String.


_Please review the steps on the [Farm Beats Documentation](https://docs.microsoft.com/en-us/azure/industry/agriculture/get-sensor-data-from-sensor-partner#enable-device-integration-with-farmbeats) for additional guiidance._
 

#### 2. Create Device Model and Sensor Models for Indoor Kit

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
POST /Device

{
   "hardwareId":"b827eb2f6557",
   "deviceModelId":"d9b254ed-2531-47b3-bfb8-6007c937fcff",
   "farmId":null,
   "reportingInterval":300,
   "location":{
      "latitude":0.0,
      "longitude":0.0
   },
   "name":"EastChain - Indoor-M1"
}

```

2. Create Sensor

```json
POST /Sensor

{
   "hardwareId":"580cc355-2da0-42e2-8a01-7bc41d6a3725",
   "sensorModelId":"d6a16fc2-26f0-4b8e-88bf-fb27464a55c9",
   "deviceId":"4e4e02bf-261a-429a-b647-51884b350f25",
   "name":"EastChain - Indoor-M1Grove Soil Moisture"
}

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

## Challenge #5 - Set up the FarmBeats IOT simulator to recreate a historical scenario

https://github.com/rutzsco/farmbeats-hackathon/blob/master/FarmBeats_IOTData_Simulator.pdf



