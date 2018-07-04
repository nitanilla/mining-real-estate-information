# Real Estate Agency Django App
## Django based website for Real Estate Agency.
---
The application serves to increase sales and to simplify content-managers job.
It aimed to the customers who wants to buy apartment in new buildings.
It collects feedbacks and callback request through the DB.
Callback requests sends to brokers via [Telegram](https://telegram.org/ "Messenger").
---
Production settings are isolated by structure of settings and keeps only at production server.
For the security purposes it must contain:
* Modifed Secret Key;
* DEBUG = False;
* allowed hosts;
* media and static path;
* DB name, user, password and other;
* Yandex Metrica counter ID;
* Telegram token, chats and admin chats;

__Thank you for visiting!__

Info for contributors:
* Use [this Git branching model](http://nvie.com/posts/a-successful-git-branching-model/ "Why I choosed that").

Author: [Andrew Dybov](mailto:dybov.andrew@gmail.com)
MIT Licence