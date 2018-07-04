# IOSR2015-real-estate-broker
Projekt na przedmiot IOSR. Aplikacja rozproszona do handlu nieruchomościami umożliająca dodawania posiadłości na sprzedać jak i klientów (kupców) zainteresowanych kupieniem domu/mieszkania.

Uruchomienie aplikacji:

* Należy pobrać i wypakować Apache Karaf: http://karaf.apache.org/index/community/download.html - przetestowane na wersji 2.4.1, na innych mogą być inne komendy, więc polecam tę, ewentualnie inną 2.4.x
* Uruchamiamy karafa poleceniem ```bin/karaf```
* Instalujemy listę dodatków:
```
features:chooseurl camel 2.15.1
features:chooseurl activemq 5.11.0
features:install camel
features:install camel-blueprint
features:install camel-soap
features:install activemq-camel
features:install activemq-broker
```
* Budujemy projekt poleceniem 
```mvn install```
* Podczas budowania zostaną wygenerowane pliki .java dla klienta
* Instalujemy bundle na karaf 
```install -s mvn:pl.edu.agh.iosr/real-estate-broker/1.0-SNAPSHOT```
* Do przetestowania uruchamiamy klienta poleceniem 
```mvn -Pclient```

Kilka przydatnych komend consoli karafa (wciśnięcie tab podpowiada komendy):
* ```help``` - otrzymujemy listę wszystkich komend
* ```display``` - wyświetla logi
* ```list``` - wyswietla zainstalowane bundle
* ```update <numer_bundla>``` - aktualizuje paczkę (gdy zmienimy coś w kodzie i uruchomimy ```mvn install``` polecenie zainstaluje utworzoną w ten sposób nową paczkę)
