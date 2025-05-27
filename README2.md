# Configuració de streaming amb NGINX RTMP

Primerament, vam instal·lar els paquets corresponents per fer el streaming d’àudio i vídeo. Un dels elements principals va ser el **nginx RTMP**. En aquest servei vam haver de modificar fitxers com:

/usr/local/nginx/conf/nginx.conf

També va ser necessari instal·lar el paquet de **ffmpeg**.

El mòdul **nginx-rtmp** et permet fer streaming de vídeo i àudio amb **alta qualitat** i **baixa latència**. És ideal per fer servir amb aplicacions com **OBS** o **ffmpeg**.

D’altra banda, existeixen opcions com **Icecast2 amb DarkIce**, que són perfectes per a ràdio online. No obstant això, aquestes no donen suport al vídeo i requeririen instal·lar i configurar més paquets addicionals. Per això vam escollir **nginx-rtmp**, per la seva **configuració senzilla** i la **qualitat alta** tant d’àudio com de vídeo.

## Pujada d’arxius i execució

Després vam haver de pujar els arxius **MP4** —els vídeos utilitzats— mitjançant la comanda scp. Un cop els vídeos es trobaven a les instàncies d’**AWS**, ja podíem iniciar el servei d’àudio i vídeo des de la terminal.

## Implementació via web

Però nosaltres hi vam afegir un pas més, per tal de fer-ho accessible també **via web**, mitjançant un **HTML personalitzat**. Aquest fitxer HTML va ser creat específicament per donar suport al streaming, i permet que la visualització via navegador sigui **estructurada**, **polida** i fàcil d’utilitzar.
