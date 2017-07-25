# Azure Data and Analytics Lab
## By David Harris
### 7/25/2017

## Exercise 1
## Task 1
### Create a Bing Search Console App

1. Open Visual Studio.
1. Click File then select new project.
1. Select Windows Classic and then Select Console App
1. Name the project BingSearchLab.
1. Right click the BingSearchLab project and click Add then select class.
1. Name the class NewsSearch.cs
1. Right click on the BingSearchLab and Select Manage nuget packages.
1. Click Browse and type newtonsoft.json in the search box.
1. Click Newtonsoft.Json package. Click Install. Click ok when box opens.
1. Add the following code to the NewsSearch class

    ``` 
    class NewsSearch
    {
            public string _type { get; set; }
            public string readLink { get; set; }
            public int totalEstimatedMatches { get; set; }
            [JsonProperty(PropertyName = "value")]
            public List<NewsResult> NewsResult { get; set; }
    }

        public class NewsResult
        {
            [JsonProperty(PropertyName = "name")]
            public string Headline { get; set; }
            public string url { get; set; }
            public Image image { get; set; }
            [JsonProperty(PropertyName = "description")]
            public string Summary { get; set; }
            public Provider[] provider { get; set; }
            [JsonProperty(PropertyName = "datePublished")]
            public DateTime DatePublished { get; set; }
            public string category { get; set; }
        }

        public class Image
        {
            public Thumbnail thumbnail { get; set; }
        }

        public class Thumbnail
        {
            public string contentUrl { get; set; }
            public int width { get; set; }
            public int height { get; set; }
        }

        public class Provider
        {
            public string _type { get; set; }
            public string name { get; set; }
        }
    ```

1. Right click BingSearchLab project and select add class.
1. Name the class Search.cs
1. Add the following using statements to the Search class

    ``` 
   using Newtonsoft.Json;
   using System.IO;
   using System.Net.Http;
    ```

1. Add the following code to the Search Class

    ```  
	public static async Task<List<NewsResult>> GetHikingNews()
        {
            var results = new List<NewsResult>();
            var webClient = new HttpClient();
            webClient.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "Add Your Key here");
            byte[] searchResults = await webClient.GetByteArrayAsync("https://api.cognitive.microsoft.com/bing/v5.0/news/search?q=hiking&mkt=en-us");
            var serializer = new JsonSerializer();
            using (var stream = new MemoryStream(searchResults))
            using (var reader = new StreamReader(stream))
            using (var jsonReader = new JsonTextReader(reader))
            {
                results = serializer.Deserialize<NewsSearch>(jsonReader).NewsResult;
            }
            return results;
        }
    ```

1. In the solution explorer, double click Program.cs.
1. Add the following code to the Main Meathod.
    ``` 
        var results = Search.GetHikingNews().Result;
        for (int i = 0; i < results.Count; i++)
        {
            Console.WriteLine(results[i].Headline);
        }

        Console.ReadLine();
    ```

1.This should display the headlines for each result.




## Task 2
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

1. Place the Key into your console application. It needs to go in the search class here.
'webClient.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "Add Your Key here");'

1. Run your application and view the results.

## Task 3
### Delete the Cognitive Service

1. Ensure your cognitive service is open in the Azure portal.
1. On the Overview Blade click Delete at the top left.
1. You successfully deleted the resource. 
1. Congrats!


