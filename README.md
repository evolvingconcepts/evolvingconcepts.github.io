

## Api documentation

### Overview

![](/overview.png)


We provide an IOT api with a single interface for each module that supports cross manufacture devices. This way there is no need to implenment every single api from multiple manufactures.
All gateway trafic is handled over sockets, there is no port-forward, vpn requirements. A active internet connection is the only requirement. Without a active internet connection the functionality in the specific house still works due to the local gateway.






Click here for full  [Api Dcoumentation](/api-docs) 


### Capabilities

Each gateway has capabilties (features activated)
Based on the response it is posible to determin what function to use.

&nbsp;

Each gateway has default capabilties and each room can have separate capabilities. This way it is posible to see what devices are added to specific rooms and create your own logic based on this. 



```
{
  "id": "string",
  "capabilities": {
    "motionEnabled": true,
    "thermostatEnabled": true,
    "lightEnabled": true,
    "smokeEnabled": true,
    "energyEnabled": true
  },
  "rooms": [
    {
      "id": "string",
      "name": "string",
      "capabilities": {
        "motionEnabled": true,
        "thermostatEnabled": true,
        "lightEnabled": true,
        "smokeEnabled": true,
        "energyEnabled": true
      }
    }
  ]
}
```

For more information see the openapi spec page linked in the top of this page



## Client SDK

### C#

#### Initilization:

```
using EvolvingConcepts.Client;

var client = new IotClient("mysecret");
```

Examples:

Climate


```
//Get current climate
var currentClimate = await client.GetClimate(result.Id);

//set climate 
await client.SetClimate(result.Id,new Climate { Mode = Climate.Modes.Heat, Temperature = 21 });

//Set climate is specific room
await client.SetClimate(result.Id,new Climate { Mode = Climate.Modes.Heat, Temperature = 21 },"bedroom1");
```

Events:

It is posible to subscribe to specific events of specific iot devices, Each time an manual action on the device (Like a person activating a ac unit or setting a temperature from the location itself, turning on the light etc...) the event will contain the location and the room where it is triggered. 
```
await client.EnableEvents();

client.ClimateChanged += (e,s) => 
{

};

client.MotionChanged += ......

```








