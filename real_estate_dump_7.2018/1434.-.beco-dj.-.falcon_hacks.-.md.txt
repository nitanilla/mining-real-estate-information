# Falcon Hacks
Participating companies:<br />
<ul>
  <li><a href='https://www.ajar.com.kw/en'>Ajar Online</a>
    <br />
    Ajar Online is a cloud service designed for the real estate market, offering quick online rent payment and a free property management platform. <br />
The service allows tenants to pay their rent online, at anytime and anywhere via SMS and email in less than 60 seconds. Simplifying the rent collection process for landlords and providing efficient property management tools to save time, reduce cost and take the right decisions.
  </li>
  <li><a href='https://www.bayzat.com/'>Bayzat</a><br />
  Bayzat is a technology company that provides insurance and HR solutions. We are creating great customer experiences in different verticals with the assistance of cutting-edge technology. Our insurance platform helps individuals and groups compare, buy and use health insurance; while our HR platform provides elegant and efficient ways to handle daily workflows of employees, HR administrators and finance managers. Our current technical challenges include completely automating our cloud infrastructure (infrastructure-as-code) and utilizing AI and machine learning for more accurate document recognition.
  </li>
  <li><a href='https://myki.co/'>myki</a> <br />
    Myki is a Cyber Security company that is defining the future of digital identity; a future where proprietary data remains in the hands of the user and not the service provider. 
Cloud storage of passwords, keys and certificates is convenient but constitutes a big security issue. Hackers shouldn't be able to compromise a publicly accessible server and as a result gain access to users credentials. 
This is why with Myki we keep your data completely off the cloud. We strive to continuously provide the security of being Offline and the convenience of being cloud-connected. 
  </li>
  <li><a href='https://www.propertyfinder.ae/'>PropertyFinder</a> <br />
    Bringing ease and transparency to the market, connecting consumers to their perfect property
  </li>
  <li><a href='https://wrappup.co/'>wrappup</a><br />    
Wrappup was founded on the idea of squeezing the most important information out of your meetings. Wrappup use artificial intelligence to process speech and create playable summaries of your discussions.
  </li>
  
 </ul>
 
 # Challenges
 ## Ajar Online
 See us for details
 
 ## Bayzat
 1. Optical recognition of passports, visas and receipts and automatic extraction of meaningful data
 2. Building an interactive audio/text natural language interface (chatbot) on top of our health insurance search engine which is publicly available at https://www.bayzat.com/health-insurance/family/
 
 ## myki
  https://gitlab.com/owl-challenges/session-sharing [Individual Challenge]
  
 ## PropertyFinder
 Find any innovative way to provide useful information to the consumer using the provided APIs. (eg: mixing the information about restaurant, cinema from GMAP and our property API to help consumer find an appropriate place to live)
 
 Property API: http://propertyfinder-hackathon-2018.sg-1.paas.massivegrid.net/
 Documentation: https://docs.google.com/document/d/1i1ZCP_QOmRCsLYkNAwHbZ6F3VhiIX-bxLI6fLgynO7w/edit?usp=sharing
 
 ## wrappup (Voicera) 
 The following is a list of functionalities we would like you to build in order of priority in python. [Individual]
 <ul>
  <li>
    Take any podcast from youtube, run it through a publicly available speech to text
engine. Please set up an elastic search client and store the transcript on the
elastic search index. You may choose to set it up on your local machine for
testing purposes
  </li>
  <li>
    Based on the keywords, identify the top 20 relevant keywords that categorizes
that transcript. It should account for factors such as uniqueness of word,
frequency and relevance in the transcript
  </li>
  <li>
    Use these keywords and relevance of other words in the vicinity to create
clusters of moments from the transcript that can be called the important
highlights of the discussion with their corresponding timestamps (start & stop
time)
  </li>
  <li>
    The audio should also have the ability to be searched from the data stored in the
elastic search index. If you can make the search understand intent of the query,
for eg “Tell me something about marketing in this conversation”, in essence
looking for moments in the audio where marketing was said, it helps you get a
higher score for the hack challenge.
  </li>
 </ul>
  
  # Submissions
  Submissions will be taken from github 21st April at 1pm. Please make sure to let us know where to find your project before then.
  This is <a href='https://github.com/hackathon-in-a-box/example-hackathon-submission' >an example</a> of what a submission should look like (credit to the guys that created it)
