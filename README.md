# Assignment 6 Environments (DTAP)
We starten deze opdracht met de configuratie van de 2 servers.

## Configuratie
Voor deze opdracht maak je gebruik van 2 virtuele machines in AWS:
*   **Testserver:** Een nieuwe Ubuntu Server VM in de AWS cloud (t2.micro, public subnet, public ip, vergeet je **security group** niet). Je mag hiervoor de Cloud Essentials learner lab gebruiken.
*   **Productieserver:** Een nieuwe Ubuntu Server VM in de AWS cloud (t2.micro, public subnet, public ip, vergeet je **security group** niet). Je mag hiervoor de Cloud Essentials learner lab gebruiken.

Voeg daarnaast ook de code van de calculator app toe aan deze repository. Je kan als alternatief ook rechtstreeks de repository `https://github.com/PXL-2TIN-DevOps-Resources/calculator-app-finished` clonen in de eerste stap van je pipeline.

### Configuratie testserver & productieserver
De servers zijn nieuwe kale Ubuntu vms die we gebruiken voor de deployment van de applicatie in de test- en productieomgeving. Deze draait voor alle groepen in AWS. Installeer docker op je machines. Je kan hiervoor eventueel [deze installatiegidsen](https://www.digitalocean.com/community/tutorial-collections/how-to-install-and-use-docker) gebruiken.

Belangrijk is dat de `ubuntu` user het docker commando moeten kunnen gebruiken (zonder `sudo`!!). Denk doorheen de opdracht ook goed na over het gebruik van security groups (poort 22 voor `ssh`/`scp`, poort 80 voor de gedeployde app, ...).

## Opgave
In deze repository voorzie je 2 workflows. Elke workflow heeft zijn eigen pipeline:
- de test deployment worfklow: Doorloopt het hele CI process en zorgt voor een artifact en deployed dit naar de testserver
- de production deployment workflow: doorloopt enkel het CD proces en neemt het laatste artifact en deployed deze a.d.h.v. `ssh` op de production server

Details van bovenstaande implementaties kan je hieronder terugvinden.

_Tip: Het is niet toegelaten om het `sudo` commando te gebruiken. Heb je geen rechten in bepaalde folders of commando's? Dan zorg je ervoor dat de gebruiker `ubuntu` de juiste rechten krijgt.

# test deployment workflow
Je krijgt een bestaande pipeline met enkele steps in. Voorzie minimaal volgende extra steps in deze pipeline:
*   Step `Install dependencies`: Configureer en installeer NodeJS en voer `npm install` uit om dependencies te installeren
*   Step `Build artifact`: In deze stage bouw je een docker image van de nodeJS applicatie. (Tip: Zorg eerst voor een werkende Dockerfile en test deze lokaal). De image wordt vanuit de pipeline gebuild.
*   Step `Push artifact`: In deze stage push je de gebouwde image naar dockerhub. Je maakt hier gebruik van een publieke image op het profiel van één van je teamgenoten.
*   Step `deployment`: In deze stage zorg je ervoor dat de docker container opgestart wordt op poort 3000 en blijft draaien na het uitvoeren van de pipeline.
    * _Tip 1: Gebruik de container vanuit dockerhub!_
    * _Tip 2: Denk eraan dat er misschien nog een vorige versie van de applicatie actief is._
    * _Tip 3: Denk aan je security groups._
    
    
* Als je vervolgens naar [http://<vm-ip>:3000](http://<vm-ip>:3000) surft, zal je de calculator app kunnen gebruiken.

![alt_text](https://i.imgur.com/9leib3p.png "image_tooltip") _Heb je aanpassingen gedaan om ubuntu rechten te geven tot bepaalde mappen of commando's, dan documenteer je dit in oplossing.md onder punt (a)._
  
# production deployment workflow


Het doel van deze pipeline is het voorzien van volgende steps:

*   Stage `pull prod`: Zorg ervoor dat je in deze stage op je remote server de laatste versie van je docker container download a.d.h.v. dockerhub.
*   Stage `start prod`: Zorg ervoor dat de container wordt opgestart op je remote server. Na het opstarten moet je de applicatie kunnen gebruiken op poort 80.
    *   _Tip 1: Maak gebruik van Github secrets voor het opslaan van je credentials voor de SSH verbinding_
*   Stage `test prod`: Doe een check om te kijken of de applicatie werkt. Voorlopig kan je dit testen met het `curl` commando om te controleren of je een statuscode 200 krijgt als je het IP adres van de `productieserver` bezoekt.

# Deliverable
Deze repository met:
- 2 workflows met bovenstaande beschreven stages
    - Een niet werkende (=syntax errors in het pipeline script) Jenkinsfile = -30% op het eindresultaat
    - Gebruik van `sudo` in je workflows resulteert in een 0 op deze PE
- Eventueel de code van de calculator app
- Een opgevulde `oplossing.md` file met antwoorden op bovenstaande vragen inclusief screenshots indien nodig.
