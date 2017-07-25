# Azure Data and Analytics Lab
## By David Harris
### 7/25/2017

## Exercise 1
### Create a Cognitive Service

1. Sign on to the [Azure portal](https://portal.azure.com/).
1. Click New > Intelligence + analytics > Cognitive Services.
1. Select Cognitive Services
  * On the Create blade Enter a Name for the service.
  * Choose a Subscription
  * Select Bing Search APIs for API Type
  * Select a Pricing Tier
  * Select Use Existing for Resource group and select the Photosharing
  * Read Policy and click accept.
1. Open the previously created resource.
1. On the Cognitive Services Blade click overview.
1. On the Overview Blade locate the Endpoint address.
  * Should look like this https://api.cognitive.microsoft.com/bing/v5.0
  * Copy this link. It will be used later.
1. On the Overview Blade, Locate the Manage Key section.
  * Click Show Access Keys
  * Copy Key 1. It will be used later.

Here is an example of how to use the bing search cognitive services.

![alt text](https://github.com/bblldave/ISTA-422/blob/master/ResearchPapers/CodePic.png "Bing Search Cognitive Service Code")

1. Place the Key and the Endpoint into your application. You can Use the web client or the HTTP class to get a connection to the internet.


