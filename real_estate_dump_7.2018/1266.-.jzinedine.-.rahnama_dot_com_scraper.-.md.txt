# rahnama.com scraper 

A Simple Web Automation Script based on Capybara-Slenium/Nokogiri, telegram-bot-ruby,Thor and google_url_shortener.
---


### How to run:
  ```
  bundle install
  ```
#### Command list
  ```
  thor list
  thor rahnama:generate_dic          # Generaet Dictionary based on Ads words
  thor rahnama:help [COMMAND]        # Describe available commands or one specific command
  thor rahnama:scrap_ads             # Scrap the Rahnama.com Real Estate Ads based on provided links.txt
  thor rahnama:send                  # Send ads to Telegram Channel
  thor rahnama:send_daily_digest     # Send ads to Telegram Channel
  thor rahnama:update_elasticsearch  # Update Elasticsearch data
  ```

### Output
Output will be saved in a sqlite database and sent to this telegram channel: **https://telegram.me/hamshahri_ads**  

I've setup an ElasticSearch and [Kibana](http://adventures.gusto.ir/app/kibana#/discover?_g=(refreshInterval:(display:Off,pause:!f,value:0),time:(from:now-30d,mode:quick,to:now))&_a=(columns:!(ad_text,category,counts,pdate,id,_score),index:ads,interval:h,query:(query_string:(analyze_wildcard:!t,query:'*')),sort:!(id,asc))) to make it easier to search and visualize the data as it grows.


### TODOS:
* Save the logo and the filename of bmp file in ads and associate them with advertisers
* ~~Tokenize ads to extract important and mostly used keywords~~
* ~~Make the process scheduled and automatic using `whenever` gem~~
