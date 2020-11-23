## Eksamen i DevOps

##### Hovedfokuset mitt har ikke vært å lage en avansert applikasjon, derfor viser den minimalt, men er samtidig innholdsrik nok til å demonstrere de DevOps-prinsippene jeg har gjort.  

##### Oppgave 1
##### I denne oppgaven har jeg koblet opp GCP sammen med travis for å gjøre det slik at hver gang jeg gjør en endring og pusher til github så lager travis et docker image av applikasjonen og laster det opp i GCP i container registry. 
##### Dette har jeg gjort ved hjelp av docker-multi-stage build som vi lærte i dette emnet. For å få til dette har jeg kryptert google service account nøklene med travis encrypt i shellet for å gi hemmeligheter til travis. Deretter har jeg lagt til openssl outputen jeg har fått og lagt det inn i travis filen. Siden jeg benyttet meg av windows, måtte jeg bruke linux shell for å kryptere nøklene. Kommandoen jeg kjørte var først travis login --pro, for å logge inn på travis. Så lagde jeg meg service account osv i GCP, lastet ned JSON nøklene for service accounten også kjørte: travis encrypt-file google-key.json. Samme kommandoen brukte jeg når jeg krypterte nøkler/token for feks Logz.io og Statuscake. 

##### Oppgave 2 
##### I denne oppgaven her har jeg addet dependencyene som trengs, men ikke fått implementert metrics i koden. Jeg kjørte blant annet: docker run --rm influxdb:1.0 influxd config > influxdb.conf, og docker run --name influxdb -p 8083:8083 -p 8086:8086 -p 25826:25826/udp -v $PWD/influxdb:/var/lib/influxdb -v $PWD/influxdb.conf:/etc/influxdb/influxdb.conf:ro -v $PWD/types.db:/usr/share/collectd/types.db:ro influxdb:1.0. Når det var gjort startet jeg grafana med kommandoen: docker run -d -p 3000:3000 --name grafana grafana/grafana:6.5.0 og gikk inn på linken http://localhost:3000/ . Konfiguerte datasourcen mydb med url http://host.docker.internal:8086.  Noe mer enn det gjorde jeg ikke i denne oppgaven. 
                                                                                                                                                                                                                                                                                                                                                                                                      
##### Oppgave 3 
##### I denne oppgaven har jeg gjort det slik at det blir lest logger til logz.io og i consollen når man kjører applikasjonen. For å gjøre det i henhold til twelve factor app prinsippet så har jeg ikke lagt inn log.io token i logback filen men kryptert det og lagt det til som variabel i infrastruktur repoen min. Så ingen kan bruke tokenet mitt bombadere meg med logger. Kunne forsåvidt gjort det med logz urlen også men siden det ble nevnt i timen at den har vært det samme en god stund nå så lot jeg det være. La inn LOG.info i noen av controllerne mine for å vise at det blir skrevet ut logger. I logback filen refererer jeg til den slik ${LOGZ_TOKEN}. 
