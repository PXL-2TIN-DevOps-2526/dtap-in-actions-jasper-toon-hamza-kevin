# PRODUCTIONSERVER

## I Aanpassing rechten voor gebruik van Docker zonder sudo

We hebben de gebruiker toegevoegd aan de `docker` groep met het commando `sudo usermod -aG docker $USER`, aangezien het gebruik van `sudo` niet hoort volgens de security principes. Hieronder zie je een screenshot waarin het commando wordt uitgevoerd, met de output van `groups`en `docker ps` die beiden succesvol worden uitgevoerd zonder `sudo`.

[sudo usermod voor docker](./screenshots/usermod-docker.png)

## II Bewijs werkende app

### Instancegegevens productieserver

[Instancegegevens productieserver](./screenshots/prodserver.png)

### Bewijs werkende app op productieserver

[Bewijs werkende app op productieserver](./screenshots/workingsite.png)
