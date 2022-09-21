## Experiment 1:
### Create LWM2M Objects in your registered client in the Leshan server

**What is LWM2M Object?**
LWM2M objects are functionalities the LWM2M client provides. An Object is a named collection of individual resource definitions which is mapped directly to a device or to a software component for the purpose of data sharing. A Resource is read, written or executed. Resources within Objects are accessed with simple URIs:/{Object ID}/{Object Instance}/{Resource ID}.

After you register the client to leshan page, you can create objects from DietPi terminal using below command

![createobject](https://user-images.githubusercontent.com/112504410/191579708-0ae2e7e5-c00a-4300-b7d5-99b76c986bfa.png)

Information like Object name,Object Id's and thier description can be found at this link [LWM2M Object ID's](https://technical.openmobilealliance.org/OMNA/LwM2M/LwM2MRegistry.html)

I created Air Quality Object and Energy object
|Object|Command|
|:-----:|:-----:|
|Air Quality|`create 3428`|
|Energy|`create 3331`|

![Air quality object](https://user-images.githubusercontent.com/112504410/191582126-510123ff-2f11-4165-be87-d03d8804bc81.png)

![enerygy object](https://user-images.githubusercontent.com/112504410/191582153-3f8d04b9-5339-4e2a-be35-3b0ddb1517ac.png)

## Experiment 2:
### Using Wireshark to Analyse protocols

I downloaded Wireshark 3.6.8 from the link [Wireshark Download](https://www.wireshark.org/download.html). If you are a windows user, click on Windows Installer(64-bit) to begin te download.

Install and open the wireshark 

