## Solution overview ##
<img src="images/dogusvdf/dogusHeader.png" alt="Dogus Teknoloji VDF Fleet Header">

[Doğuş Teknoloji](http://www.d-teknoloji.com.tr) is a technology provider of [Dogus Group](https://www.dogusgrubu.com.tr/en/corporate-profile). They've recently granted an R&D center certification and they would like to provide different user experiences to group companies and customers. [Volkswagen Doğuş Finans (VDF)](http://www.vdf.com.tr/tr/ana-sayfa.aspx) is one of group companies and "VDF Finance and Fleet Team" at Dogus teknoloji is responsible with IT opererations of VDF.

In this project, we've worked with "VDF Finance and Fleet Team" that serves to Automotive vertical of Dogus Group companies. We've worked on a project called "Interactive Assistant", A digital assistant provides a solution to any customer or sale representative to retrieve an offer for fleet & car rental, due to their asks & needs.

This project is the first Conversation-as-a-Platform (CaaP) implementation at “Dogus Teknoloji”.

<img src="images/dogusvdf/photo.jpg" alt="Dogus Teknoloji VDF Fleet Team">

> "After finalizing or solution we showed the solution to our clients, they're amazed with the level of user experience and productivity of the solution. With this work, we got many chat bot use case ideas for our daily job increase our productivity, also these solutions can be expandable to other Dogus Group Companies." - Çiğdem Örer , Project Manager

### Technologies used : ###
- [Microsoft Bot Framework](https://dev.botframework.com)
- [LUIS - Language Understanding Intelligent Service](https://www.luis.ai/)
- [Translator Text API](https://azure.microsoft.com/en-us/services/cognitive-services/translator-text-api/)
- [Custom Vision API](https://customvision.ai/)
- [Azure Web Apps](https://azure.microsoft.com/en-us/services/app-service/web/)
- [Azure CosmosDB](https://azure.microsoft.com/en-us/services/cosmos-db/)
- [Azure Application Insight](https://azure.microsoft.com/en-us/services/application-insights/)

### Core Team ###

- [Ibrahim Kivanc](https://twitter.com/ikivanc) - Senior Technical Evangelist | Microsoft
- Ünal Karakuş - Team Leader | Dogus Teknoloji
- Çağatay Eralp - Software Development Engineer | Dogus Teknoloji
- Çiğdem Örer - Project Manager | Dogus Teknoloji

<img src="images/dogusvdf/photo1.JPG" alt="Dogus Teknoloji VDF Fleet Team">

## Customer profile ##
[Doğuş Teknoloji](http://www.d-teknoloji.com.tr)  began its activities as a part of the [Dogus Group](https://www.dogusgrubu.com.tr/en/corporate-profile) companies in 2012. Since then, it has remained an innovative, solution-oriented and dynamic company ensuring customer satisfaction through high-quality, value-added products and services at the lowest costs possible.

<img src="images/dogusvdf/vdflogo.png" alt="Dogus Teknoloji VDF Fleet Team">


Doğuş Teknoloji works in a huge variety of areas of Information Technology (IT) infrastructures, adapting systems and software products, creating and maintaining products using the latest technologies. The Company treats its customers as strategic partners, working closely with their internal business and IT units. Doğuş Teknoloji creates products that answer to actual demands, and that reflect strong technological and operational experience, and sectorial expertise. In addition, the Company offers effective project management services, and it reviews and continuously improves its methodologies to deliver the best on-time, as-promised solutions, thereby maintaining the highest level of quality and customer satisfaction. It is thanks to these principles of perfection and dependability that Doğuş Teknoloji is able to expand its customer portfolio.

The main areas of Doğuş Teknoloji’s expertise include designing software and information systems, requests for the analysis of business requirements (i.e.; business process automation, reporting, security, etc.), development, installation, updating, maintenance, error fixing and integration of projects into these systems, maintaining security, monitoring performance and reporting abnormalities, consultancy services, and managing all of all these processes.

[About Dogus Group](https://www.dogusgrubu.com.tr/en/corporate-profile) | 
[About Dogus Teknoloji](http://www.d-teknoloji.com.tr/ana-sayfa.aspx)


## Problem statement ##

As Doğuş Teknoloji we develop products for [Dogus Group](https://www.dogusgrubu.com.tr/en/corporate-profile) companies in 9 different sectors. (Automotive, finance, tourism, construction, energy, retail, food & beverage, media, real estate). In our products, we need to communicate with our users through different channels, and improve user experience. The use of chatbots and voice command systems is at the forefront, as the user experience on mobile is different from other devices. As Doğuş Technology, we have a goal of creating an infrastructure that we can spread to our pilot projects and then to our products in all sectors. We intend to use Doğuş Otomotiv's “Diyalog”(Road Assistance) application as a pilot in the B2C field and VDF “Fleet ERP”(Operational Fleet Car Rental) application in the B2B field.

<img src="images/dogusvdf/photo2.JPG" alt="Dogus Teknoloji VDF Fleet Team">

## Solution and steps ##

The proposed solution is to develop a chat bot platform based on the Microsoft Bot Framework.  This project will be the first CaaP implementation at “Dogus Teknoloji” that is providing solutions to different customers. They’ll create a Digital Assistant called "Interactive Assistant" to help sales representatives and customers from different channels. Any customer or sale representative will go to this digital assistant to have an offer for Fleet or Car rental with a guidance.

They have 2 different channels, one from a chat channel (official Microsoft Canvas; Facebook Messenger and Skype) using typing, another usage will be from a native application using text input and voice input, Voice input will be used with Bing Speech API to have a text output this will be active.

Team has created a Bot Application with rule based questions (using Multi Dialog & Chain) and will accept free form questions via typing on a chat window. Users will type in Turkish then Microsoft Text Translator API will be translating Turkish sentences to English to use in LUIS. We’re using LUIS for natural language understanding, to recognize what users say. Every translation will be stored in MongoDB on Azure CosmosDB. To provide a different user experience, users can upload their photos of cars they took, system can recognize which brand and which model it is, for this image recognition team has used Custom Vision Services.

Any query will be ended with a proposal of a fleet or car rental, all business logic will work with retrieved entities from LUIS. Bot business logic will use these entities to retrieve search results from VDF Fleet Backend via Web API.

> "VDF Fleet & Car Rental Bot Application developed with power of Microsoft Bot Framework, with this framework we were able to develop application rapidly and run the application on different channels. While we're developing our solution, we've found that there are many useful tools for monitoring and analizing our Bot to improve quaility." - Çiğdem Örer , Project Manager

## Technical delivery ##
You can find architectural diagram of "Interactive Assistant" Chat bot solution below.

<img src="images/dogusvdf/dogusvdfbotarchitechture.png" alt="Dogus Teknoloji VDF Fleet Header">   

This section includes the following details of how the solution was implemented:

For all details for a chat bot integration
[Bot Framework Documentation](https://docs.botframework.com) and [BotBuilder Samples](https://github.com/Microsoft/BotBuilder-Samples)  are great resources and examples you can benefit. Also you can follow best practices and guidances.

### Bot Patterns
Team has followed below patterns to have interactive assistant.
- [Multi-Dialog Bot](https://github.com/Microsoft/BotBuilder-Samples/tree/master/CSharp/core-MultiDialogs)
- [Chain](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-dialogs#a-iddialog-chainsa-dialog-chains)
- [State](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-state)

### Core Bot Capabilities
- Conversations
- Free Text Questions
- Custom Vision: Image Search

### Bot Intelligence
For Bot intelligence team used Microsoft Cognitive services to make chat bot smarter.

There are three major services helped a lot to make bot smarter:
1. **Luis.ai:**  Used for Natural Language Processing (NLP) to understand free-text questions. This service helped for Retrieving entities from questions and find correct intents.  
2. **Translator Text API:** Used for translating Turkish question to English to retrieve intents and entities via Luis.ai
2. **Custom Vision API:** Used for recognizing car model and car brand in real life with photos

<img src="images/dogusvdf/LuisFlow.png" alt="Dogus Teknoloji VDF Fleet LUIS & Translator Text API Integration"> 

### Translator Text API

To use translator in or bot service we'll use Microsoft Translator Text API. Microsoft Translator APIs can be seamlessly integrated into your applications, websites, tools, or other solutions to provide multi-language user experiences. Leveraging industry standards, it can be used on any hardware platform and with any operating system to perform language translation and other language-related operations such as text language detection or text to speech. [Click Here](https://www.microsoft.com/en-us/translator) for more information about the Microsoft Translator API

<img src="images/dogusvdf/CustomTranslationSystems.png" width="300" alt="Microsoft Translator with BotFramework"> 

#### Getting Started to use Microsoft Translator API
To access the Microsoft Translator Text API you will need to sign up for Microsoft Azure. Follow these steps.
1. Sign up for a Microsoft Azure account at [http://azure.com](http://azure.com)
1. After you have an account go to [http://portal.azure.com](http://portal.azure.com)
1. Select the + **New** option.
1. Select **AI + Cognitive Services** from the list of services.
1. Click **See All** on top right.
1. Select **Translator Text API**.
1. Select the **Create** button.
1. Fill out the rest of the form. 
1. In the **Pricing Tier** section select the pricing tier that fits your needs.
1. Select the **Create** button.
1. You are now subscribed to Microsoft Translator.
1. Go to **All Resources** and select the Microsoft Translator API you subscribed to.
1. Go to the **Keys** option and copy your subscription key to access the service.

Paste this API Key into this "BotTranslator" sample in `MessagesController.cs`

```cs
using System;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
using System.Web.Http;
using System.Web.Http.Description;
using Microsoft.Bot.Connector;
using Newtonsoft.Json;
using System.IO;
using System.Net.Http.Headers;
using System.Xml.Linq;

namespace BotTranslator
{
    [BotAuthentication]
    public class MessagesController : ApiController
    {
        /// <summary>
        /// POST: api/Messages
        /// Receive a message from a user and reply to it
        /// </summary>
        /// 
  
        string ApiKey = "PLACE YOUR MICROSOFT TRANSLATOR API KEY HERE";
        string targetLang = "en";

        public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
        {
            if (activity.Type == ActivityTypes.Message)
            {
                ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));

                var input = activity.Text;

                Task.Run(async () =>
                {
                    var accessToken = await GetAuthenticationToken(ApiKey);
                    var output = await TranslateText(input, targetLang, accessToken);
                    Console.WriteLine(output);

                    Activity reply = activity.CreateReply($"Your text translation to English is => '{output}'");
                    await connector.Conversations.ReplyToActivityAsync(reply);

                }).Wait();
            }
            var response = Request.CreateResponse(HttpStatusCode.OK);
            return response;
        }

        static async Task<string> TranslateText(string inputText, string language, string accessToken)
        {
            string url = "http://api.microsofttranslator.com/v2/Http.svc/Translate";
            string query = $"?text={System.Net.WebUtility.UrlEncode(inputText)}&to={language}&contentType=text/plain";

            using (var client = new HttpClient())
            {
                client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
                var response = await client.GetAsync(url + query);
                var result = await response.Content.ReadAsStringAsync();

                if (!response.IsSuccessStatusCode)
                    return "Hata: " + result;

                var translatedText = XElement.Parse(result).Value;
                return translatedText;
            }
        }

        static async Task<string> GetAuthenticationToken(string key)
        {
            string endpoint = "https://api.cognitive.microsoft.com/sts/v1.0/issueToken";

            using (var client = new HttpClient())
            {
                client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);
                var response = await client.PostAsync(endpoint, null);
                var token = await response.Content.ReadAsStringAsync();
                return token;
            }
        }
       
        private Activity HandleSystemMessage(Activity message)
        {
            if (message.Type == ActivityTypes.DeleteUserData)
            {
                // Implement user deletion here
                // If we handle user deletion, return a real message
            }
            else if (message.Type == ActivityTypes.ConversationUpdate)
            {
                // Handle conversation state changes, like members being added and removed
                // Use Activity.MembersAdded and Activity.MembersRemoved and Activity.Action for info
                // Not available in all channels
            }
            else if (message.Type == ActivityTypes.ContactRelationUpdate)
            {
                // Handle add/remove from contact lists
                // Activity.From + Activity.Action represent what happened
            }
            else if (message.Type == ActivityTypes.Typing)
            {
                // Handle knowing tha the user is typing
            }
            else if (message.Type == ActivityTypes.Ping)
            {
            }

            return null;
        }
    }
}
```

### Language Understanding ###

Conversational intelligence feature of a bot is important for users to have a natural dialog, In this project to add conversational intelligence to the app, team used [Language Understanding Intelligent Service (LUIS)](https://www.luis.ai) from Cognitive Services.

One of the key problems in human-computer interactions is the ability of the computer to understand what a person wants. Language Understanding Intelligent Service (LUIS) enables developers to build smart applications that can understand human language and react accordingly to user requests. LUIS uses the power of machine learning to solve the difficult problem of extracting meaning from natural language input, so that your application doesn't have to. Any client application that converses with users, like a dialog system or a chat bot, can pass user input to a LUIS app and receive results that provide natural language understanding.

<img src="images/dogusvdf/LuisFlow.png" alt="Dogus Teknoloji VDF Fleet LUIS & Translator Text API Integration"> 

A LUIS app is a place for a developer to define a custom language model. The output of a LUIS app is a web service with an HTTP endpoint that you reference from your client application to add natural language understanding to it. A LUIS app takes a user utterance and extracts intents and entities that correspond to activities in the client application’s logic. Your client application can then take appropriate action based on the user intentions that LUIS recognizes.

Here are the steps to define our application

1. We've created a LUIS application on LUIS portal

<img src="images/dogusvdf/luis.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

2. We've defined entities of a rental car like below, importanat part is `Entity Type`, we've defined:
    -  `CarBrand` are hierarchical entities of `CarModel`,
    - `EnginePower`, `Year`, `EngineOil` are hierarchical entities of `CarDetail`
    - `Currency` as Simple entity type.
    - `Number` for `MileAge` and `Term` composites entity type.

<img src="images/dogusvdf/luisEntities.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

3. We've created some intents which are relavant to needs of Dogus Teknoloji, such as showing rental car options and filtering due to requests. In this application we've created 4 Intents like below,
    - `Greeting` : to welcome users
    - `Help` : to help users with their queries
    - `None` : this will be triggered when question can not be defined.
    - `SearchCar` : to search rental car options due to need.

<img src="images/dogusvdf/luisIntents.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

4. We've trained our intent with sample questions .

<img src="images/dogusvdf/luisSearchCarTokens.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

5. Then we've defined all entities in these utterances, you can change the view from dropdown list as selecting `Entities` , `Tokens` or `Composites` .

<img src="images/dogusvdf/luisSearchCar.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

6. Here is the result of training, showing labeled entities.

<img src="images/dogusvdf/luisSearchCarEntities.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

7. To define similar words, we've added list of words into `Features `.

<img src="images/dogusvdf/luisFeatures.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

8. After training words we've tested our application under `"Train & Test"` section

<img src="images/dogusvdf/luisTest.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

9. Publish will help you to understand how your logic works, especially it's great to check API if it's working properly or not. For last step it provides an endpoint to test your queries and retrieve a json response.

<img src="images/dogusvdf/luisPublish.png" alt="Dogus Teknoloji VDF Fleet LUIS Integration">

After searching `"Show me audi A3 TDI 2.0 models"` query through endpoint, result will look like below
```json
{
  "query": "Show me audi A3 TDI 2.0 models",
  "topScoringIntent": {
    "intent": "SearchCar",
    "score": 0.999685347
  },
  "intents": [
    {
      "intent": "SearchCar",
      "score": 0.999685347
    },
    {
      "intent": "Help",
      "score": 0.009338045
    },
    {
      "intent": "None",
      "score": 0.00170092
    },
    {
      "intent": "Greetings",
      "score": 0.00012407644
    }
  ],
  "entities": [
    {
      "entity": "2.0",
      "type": "builtin.number",
      "startIndex": 17,
      "endIndex": 19,
      "resolution": {
        "value": "2"
      }
    },
    {
      "entity": "a3",
      "type": "CarBrand::CarModel",
      "startIndex": 10,
      "endIndex": 11,
      "score": 0.9999996
    },
    {
      "entity": "audi",
      "type": "CarBrand",
      "startIndex": 5,
      "endIndex": 8,
      "score": 0.00173027965
    },
    {
      "entity": "2 . 0",
      "type": "CarDetails::EnginePower",
      "startIndex": 17,
      "endIndex": 19,
      "score": 0.9862478
    },
    {
      "entity": "tdi",
      "type": "CarDetails::EngineOil",
      "startIndex": 13,
      "endIndex": 15,
      "score": 0.9944527
    }
  ]
}
```

#### Custom Vision API
Custom Vision API was announced at Build 2017 conference, and it helps easily customize your own state-of-the-art computer vision models that fit perfectly with your unique use case. Just bring a few examples of labeled images and let Custom Vision do the hard work for training your business logic.

We've decided to use this service in bot framework application. When you upload a photo of a car, Custom Vision API recognizes which brand and which model it's. Then you can get an offer regarding that sepesific car.

<img src="images/dogusvdf/customvision_training.png" alt="Custom Vision API Training"> 

Here's the code snippet for Custom Vision API integration in chat-bot.

Web.config
```cs
...
<configuration>
  <appSettings>
    <!-- update these with your BotId, Microsoft App Id and your Microsoft App Password-->
    <add key="BotId" value="InteractiveAssistant" />
    <add key="CustomVisionUrl" value="https://southcentralus.api.cognitive.microsoft.com/customvision/v1.0/Prediction/YOUR CUSTOM VISION API KEY/url" />
    <add key="CustomVisionImageUrl" value="https://southcentralus.api.cognitive.microsoft.com/customvision/v1.0/Prediction/YOUR CUSTOM VISION API KEY/image" />
    <add key="CustomVisionPredictionKey" value="YOUR CUSTOM VISION PREDICTION KEY" />
    <add key="CustomVisionPredictionRatio" value="0.70M" />
    <add key="CaptiveApiUrl" value="https://southcentralus.api.cognitive.microsoft.com/customvision/v1.0/Prediction/YOUR CUSTOM VISION API KEY/image?iterationId=YOUR CUSTOM VISION API ITERATION ID" />
  </appSettings>
...
```

CustomVisionDialog.cs
```cs
namespace InteractiveAssistant.Dialogs
{
    using Assistant.Business;
    using Assistant.Business.Constants;
    using Microsoft.Bot.Builder.Dialogs;
    using Microsoft.Bot.Connector;
    using System;
    using System.IO;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Threading.Tasks;


    [Serializable]
    public class CustomVisionDialog : DialogBase, IDialog<CreateOfferEntity>
    {
        public async Task StartAsync(IDialogContext context)
        {
            context.Wait(this.PredictImageAsync);
        }

        public async Task PredictImageAsync(IDialogContext context, IAwaitable<IMessageActivity> result)
        {
            var activity = await result;
            var attachment = activity.Attachments?.FirstOrDefault();
            if(attachment == null)
            {
                throw new ArgumentNullException(nameof(attachment));
            }
            // get image stream 
            Stream imageStream;
            using (var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl)))
            {
                var token = await (connectorClient.Credentials as MicrosoftAppCredentials).GetTokenAsync();
                using (HttpClient client = new HttpClient())
                {
                    var uri = new Uri(attachment.ContentUrl);
                    try
                    {

                        if ((uri.Host.EndsWith("skype.com") || uri.Host.Contains("facebook")) && uri.Scheme == "https")
                        {
                            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
                            client.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/octet-stream"));
                        }

                        imageStream = await client.GetStreamAsync(attachment.ContentUrl);
                    }
                    catch (Exception exception)
                    {
                        throw new ArgumentException(exception.ToString());
                    }
                }
            }
            if (imageStream == null)
            {
                throw new ArgumentNullException(nameof(imageStream));
            }

            CustomVision predictions = await CustomVisionProvider.GetImagePredictionsFromImage(imageStream);
            var results = predictions?.Predictions?.Where(a => a.Probability >= 0.70M).Select(a => a.Tag);
            _entity.BrandList = results.Where(a => a.StartsWith(AssistantLUISEntities.BRAND)).Select(a => a.Replace(AssistantLUISEntities.BRAND, string.Empty).Replace(":", string.Empty).Trim()).ToList();
            _entity.ModelList = results.Where(a => a.StartsWith(AssistantLUISEntities.MODEL)).Select(a => a.Replace(AssistantLUISEntities.MODEL, string.Empty).Replace(":", string.Empty).Trim()).ToList();
            await context.PostAsync(string.Format(AssistantTextConstants.TEXT_026, string.Join(",", _entity.BrandList), string.Join(",", _entity.ModelList)));
            context.Done(_entity);
        }
    }
}
```

CustomVisionProvider.cs
```cs
using Newtonsoft.Json;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Net.Http;
using System.Threading.Tasks;

namespace Assistant.Business
{
    public class CustomVisionProvider
    {
        public async static Task<CustomVision> GetImagePredictionsFromURL(CustomVisionURLRequest cvRequest)
        {
            string customVisionUrl = ConfigurationManager.AppSettings["CustomVisionUrl"];
            string customVisionPredictionKey = ConfigurationManager.AppSettings["CustomVisionPredictionKey"];

            using (HttpClient client = new HttpClient())
            {
                client.DefaultRequestHeaders.Clear();
                client.DefaultRequestHeaders.TryAddWithoutValidation("Content-Type", "application/json");
                client.DefaultRequestHeaders.TryAddWithoutValidation("Prediction-Key", customVisionPredictionKey);
                string request = JsonConvert.SerializeObject(cvRequest);

                var result = await client.PostAsync(customVisionUrl,  new StringContent(request));
                var cvResult = await result.Content.ReadAsStringAsync();

                return JsonConvert.DeserializeObject<CustomVision>(cvResult);
            }
        }

        public async static Task<CustomVision> GetImagePredictionsFromImage(Stream imageStream)
        {
            string customVisionUrl = ConfigurationManager.AppSettings["CustomVisionImageUrl"];
            string customVisionPredictionKey = ConfigurationManager.AppSettings["CustomVisionPredictionKey"];

            using (HttpClient client = new HttpClient())
            {
                client.DefaultRequestHeaders.Clear();
                client.DefaultRequestHeaders.TryAddWithoutValidation("Content-Type", "application/octet-stream");
                client.DefaultRequestHeaders.TryAddWithoutValidation("Prediction-Key", customVisionPredictionKey);

                var result = await client.PostAsync(customVisionUrl,  new StreamContent(imageStream));
                var cvResult = await result.Content.ReadAsStringAsync();

                return JsonConvert.DeserializeObject<CustomVision>(cvResult);
            }
        }
    }
}
```

Custom Vision API result in a chat-bot: When you upload a photo of a car, Custom Vision API recognizes which brand and model it's. Then you can get an offer regarding that sepesific car.

<img src="images/dogusvdf/customvision.PNG" width="600" alt="Custom Vision API"> 



## Technology Integration
### Azure Web App
A Bot Framework application provides an web api endpoint. To have a secure connection endpoint requires HTTPS connection where team used Azure Web Apps to provide it.

Deploy your bot to the cloud by following the instructions found in [Deploy a bot to the cloud](https://docs.microsoft.com/en-us/bot-framework/deploy-bot-overview).
Return to the [Bot Framework Portal](https://dev.botframework.com/) and [update your bot's registration data](https://docs.microsoft.com/en-us/bot-framework/portal-register-bot#maintain) to specify the **HTTPS** endpoint for the bot.

To publish a new web app team used below steps to publish their secure endpoint for Chat Bots. 
1. First **right click** on project in Solution Explorer.
2. **Click** Publish.
3. Then **Create New** then Click **Publish**.

<img src="images/dogusvdf/createAppService.png" alt="Dogus Teknoloji VDF Fleet Create and Publish App Service">

4. **Log-in** with your Azure account in pop-up.
5. **Fill** the information for your endpoint and **select** your App Service Plan.
6. Click **Create** .

<img src="images/dogusvdf/createAppService1.png" alt="Dogus Teknoloji VDF Fleet Create and Publish App Service">

7. It'll deploy automatically and run the application on Azure Web App host.
8. For testing on your emulator don't forget to add "**/api/messages**" end of your url like "**http://yourhostname.azurewebsites.net/api/messages**" to test your bot on [Bot Framework Channel Emulator](http://emulator.botframework.com)

<img src="images/dogusvdf/createAppService2.png" alt="Dogus Teknoloji VDF Fleet Create and Publish App Service">

### Azure Application Insight
To enable analytics for your Bot Application you can use Application insight and for more information [Bot analytics](https://docs.microsoft.com/en-us/bot-framework/portal-analytics-overview) defined here.

Analytics is an extension of Application Insights. Application Insights provides service-level and instrumentation data like traffic, latency, and integrations. Analytics provides conversation-level reporting on user, message, and channel data.

<img src="images/dogusvdf/azureAppInsight.png" alt="Dogus Teknoloji VDF Fleet Application Insight usage">

At the same time you can view your bot analytics at [Bot Framework Dev Center](https://dev.botframework.com) such as retention, users per channel and messages per channel.

<img src="images/dogusvdf/botanalytics.png" alt="Dogus Teknoloji VDF Fleet Bot Analytics">

### Azure Cosmos DB
Azure Cosmos DB is a NoSQL document database service designed from the ground up to natively support JSON and JavaScript directly inside the database engine. In this project team used MongoDB in CosmosDB to collect translation analytics, such as original Text and translated text and date time.

<img src="images/dogusvdf/cosmos_db.png" alt="Dogus Teknoloji VDF Fleet CosmosDB usage">

```
using MongoDB.Bson;
using MongoDB.Driver;
using MongoDB.Driver.Builders;
using System.Collections.Generic;
using System.Configuration;
using System.Linq;

namespace SocialWords.Data
{
    public abstract class BaseDataClass
    {
        protected MongoCollection<T> GetCollection<T>()
        {
            var connectionString = ConnectionString();
            var dbName = Database();
            var client = new MongoClient(connectionString);
            var server = client.GetServer();
            var database = server.GetDatabase(dbName);
            var collection = database.GetCollection<T>(typeof(T).Name);

            return collection;
        }
        internal string ConnectionString()
        {
            AppSettingsReader reader = new AppSettingsReader();
            string server = reader.GetValue("MONGO.SERVER", typeof(string)).ToString();
            string port = reader.GetValue("MONGO.PORT", typeof(string)).ToString();
            string db = reader.GetValue("MONGO.DB", typeof(string)).ToString();
            string user = reader.GetValue("MONGO.USER", typeof(string)).ToString();
            string pass = reader.GetValue("MONGO.PASS", typeof(string)).ToString();

            string connString = string.Format("mongodb://{0}:{1}@{2}:{3}/{4}?ssl=true", user, pass, server, port, db);
            return connString;
        }
        internal string Database()
        {
            AppSettingsReader reader = new AppSettingsReader();
            string db = reader.GetValue("MONGO.DB", typeof(string)).ToString();
            return db;
        }
        protected T Insert<T>(T obj)
        {
            var collection = GetCollection<T>();
            var result = collection.Insert(obj);
            if(result.DocumentsAffected > 0)
                return obj;
            return default(T);
        }
        protected T Get<T>(string id)
        {
            ObjectId objId = new ObjectId();
            bool parseResult = ObjectId.TryParse(id, out objId);
            if (parseResult == false)
                return default(T);
            var collection = GetCollection<T>();
            var query = Query.EQ("_id", objId);
            var result = collection.Find(query);
            if (result.Any())
                return result.FirstOrDefault();
            return default(T);
        }
        protected List<T> GetAll<T>()
        {
            var collection = GetCollection<T>();
            return collection.FindAll().ToList();
        }
        protected bool RemoveAll<T>()
        {
            var collection = GetCollection<T>();
            return collection.RemoveAll().UpdatedExisting;
        }
        protected MongoCursor<T> Get<T>(string key, string value)
        {
            var collection = GetCollection<T>();
            var query = Query.EQ(key, value);
            var result = collection.Find(query);
            if (result.Any())
                return result;
            return default(MongoCursor<T>);
        }
        protected bool Remove<T>(string id)
        {
            var objId = ObjectId.Parse(id);
            var collection = GetCollection<T>();
            var query = Query.EQ("_id", objId);
            var result = collection.Remove(query);

            return result.UpdatedExisting;
        }
        protected bool Update<T>(T obj, string id)
        {
            var objId = ObjectId.Parse(id);
            var collection = GetCollection<T>();
            var query = Query.EQ("_id", objId);
            var result = collection.Find(query);
            if (result == null)
                return false;
            T willBeUpdated = result.FirstOrDefault<T>();
            willBeUpdated = obj;

            WriteConcernResult updateResult = collection.Save(willBeUpdated);
            return updateResult.UpdatedExisting;
        }

    }
}
```

<img src="images/dogusvdf/photo4.jpg" alt="Dogus Teknoloji VDF Fleet CosmosDB usage">

### Bot Framework Portal & Microsoft Canvas
After developing the project, last step will be publishing the bot. To publish your chat bot, we'll use [Bot Framework Development Center](https://dev.botframework.com), create a new bot via [My Bots](https://dev.botframework.com/bots) section. Fill the form to publish your bot. 

1. Fill the form with Icon Image, DisplayName, Bot Handle and Long description of your app.

<img src="images/dogusvdf/registerbot1.png" alt="Dogus Teknoloji VDF Fleet Register Bot">

2. Fill with your Bot Framework Messaging Endpoint you published on Azure.

<img src="images/dogusvdf/registerbot2.png" alt="Dogus Teknoloji VDF Fleet Register Bot">

3. To generate `Microsoft App ID` and `Password` click and generate one.

<img src="images/dogusvdf/registerbot4.png" width="700" alt="Dogus Teknoloji VDF Fleet Register Bot">

4. On dashboard, field will be filled with App ID. 

<img src="images/dogusvdf/registerbot5.png" width="700" alt="Dogus Teknoloji VDF Fleet Register Bot">

5. For enabling Analytics of the application, team integrated Application Insight keys to app details.

<img src="images/dogusvdf/registerbot6.png" alt="Dogus Teknoloji VDF Fleet Register Bot">


After we're done with creating application on Portal, last step will be updating the applicaiton details in Bot Application in Visual Studio.

```xml
  <appSettings>    
    <add key="BotId" value="YOUR BOT ID" />
    <add key="MicrosoftAppId" value="YOUR MICROSOFT APP ID" />
    <add key="MicrosoftAppPassword" value="YOUR MICROSOFT APP PASSWORD" />
  </appSettings>
```

### **Test on Emulator**
After publishing your web application on your host, for testing on your emulator don't forget to add **"/api/messages"** end of your url like **"http://yourhostname.azurewebsites.net/api/messages"** to test your bot on Bot Framework Channel Emulator

<img src="images/dogusvdf/Testbot1.png" alt="Dogus Teknoloji VDF Fleet Test Bot">

### **Test on Portal**
After creating the application on Portal and and updating application webconfig with details, we've published the the app on Azure, then we're able to run sample on Bot Framework Portal you can click `Test` to open a chat-bot windows to test your app. 

<img src="images/dogusvdf/Testbot2.png" alt="Dogus Teknoloji VDF Fleet Test Bot">

### **Test on Skype**
Then publishing a bot in a new channel is easy as clicking "add channel". Then documentation will help to publish bot. 
<img src="images/dogusvdf/Testbot3.png" alt="Dogus Teknoloji VDF Fleet Test Bot">

<img src="images/dogusvdf/Testbot4.png" alt="Dogus Teknoloji VDF Fleet Test Bot">


### VDF Chat-bot Demo
Dogus Teknoloji successfuly published VDF chat-bot application on Facebook Messenger, Skype and embedded Web-Chat internally.

1. Bot has capabilies of starting a conversation, when you say "I want to rent car" or any realted centences in Turkish. Then step by step bot is using Multi Dialog form to get all necessary information such as `'Brand'`, `'Model'`, `'Mile Age'`, `'Term'`, `'Currency'`, `'Tire Type'` and `'Ticket type for Toll Gates'`. At the end of the conversation it calculates and bring the best offer to users.

<img src="images/dogusvdf/fbmessengerBot.PNG" alt="Dogus Teknoloji VDF Fleet Skype Canvas integration">

2. When you give some of entities in a sentence, chat-bot is completing all must have information. Such as below When you say "I want Audi A3 with 10K km for 24 months" in Turkish it extracts `'Brand'`, `'Model'`, `'Mile Age'`, `'Term'` entities then chat bot is asking for `'Currency'`, `'Tire Type'` and `'Ticket type for Toll Gates'`.

<img src="images/dogusvdf/fbmessengerBot1.PNG" alt="Dogus Teknoloji VDF Fleet Skype Canvas integration"> 

3. When you say `"I love you"`, `"I miss you"` bot replies with funny answers in Turkish. Also when you say `"Thank you"` and `"Please can you help me"` in Turkish Bot replies with related answers. These triggered via LUIS.

<img src="images/dogusvdf/fbmessengerCustomDialog.PNG" alt="Dogus Teknoloji VDF Fleet Skype Canvas integration">

After these integrations, Cognitive Services and LUIS brings intelligence to Bot and users have seamless experience in their native language.

<img src="images/dogusvdf/photo3.JPG" alt="Dogus Teknoloji VDF Fleet Team">


> "In this implementation we're excited to use LUIS.ai for improving intelligence of the bot also we've used recently announced technolgies like Azure CosmosDB and Custom Vision Services. Using these technologies helped us to gain our Cognitive and AI skills for future projects." - Ünal Karakuş, Team Leader

## Conclusion ##
After implementing this project successfully, Dogus Teknoloji gained new capabilities  in company.

- Measurable impact/benefits
  - With this VDF Fleet representatives save "60 seconds" per transaction, team can prepare the offer in 30 seconds instead of 1:30 minute.
  - VDF reached new end users via social messaging platforms.

- General lessons:
  - [LUIS ](https://www.luis.ai/) And [Translator Text API](https://azure.microsoft.com/en-us/services/cognitive-services/translator-text-api/) are nice combination to have local language support for "Natural Language Processing" (NLP) services for any application.
  - Canvas channels are great tools to provide chatbots to different platforms, this gives flexibility for how to implement your solution into different channels.
  - New user experience of "Connect to channels" helps developers to focus on their business logic and how bot works, rest of the canvas integration is done easily on this platform.
  - Cognitive Services are great way to bring intelligence to bots.
  - LUIS is a great tool to benefit AI capabilities.

- Opportunities going forward:
  - Integrating Xamarin with Speech API will be next step and team will be working on mixing native features of Mobile application and Bot Framework to have a digital assistant.
  - Team will be planning a Personal Assistant for whole company to help their business.
  - Team will work on Custom Vision API to find innovative and fun ways to run their solutions.
  - Team will focus on using CosmosDB more efficiently.

## Additional resources ##
- [Microsoft Bot Framework](https://dev.botframework.com)
- [LUIS - Language Understanding Intelligent Service](https://www.luis.ai/)
- [Translator Text API](https://azure.microsoft.com/en-us/services/cognitive-services/translator-text-api/)
- [Custom Vision API](https://customvision.ai/)
- [Azure Web Apps](https://azure.microsoft.com/en-us/services/app-service/web/)
- [Azure CosmosDB](https://azure.microsoft.com/en-us/services/cosmos-db/)
- [Azure Application Insight](https://azure.microsoft.com/en-us/services/application-insights/)

