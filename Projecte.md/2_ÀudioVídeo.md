# pro-asixc1a-g4
Github del projecte transversal

## 🎥 Projecte de Streaming d'Àudio i Vídeo amb NGINX RTMP

Aquest document recull pas a pas tot el procés de creació, configuració i execució d'un sistema de **streaming d'àudio i vídeo** utilitzant **NGINX amb el mòdul RTMP**, així com les eines complementàries per fer-lo accessible des del navegador web.

---

## 📡 1. Configuració de streaming amb NGINX RTMP

Per habilitar la capacitat de transmetre vídeo i àudio per internet, vam utilitzar el servidor web **NGINX** juntament amb el **mòdul RTMP (Real-Time Messaging Protocol)**. Aquesta combinació ens permet fer streaming en temps real amb gran qualitat i baixa latència.

### 🔧 Instal·lació dels paquets

- Instal·lació de NGINX amb suport per RTMP.
- Compilació del mòdul `nginx-rtmp-module` si cal.
- Instal·lació del paquet `ffmpeg` per manipular fluxos de vídeo i àudio.

```bash
sudo apt install ffmpeg
```

### 🧠 Per què NGINX RTMP?

Tot i que hi ha alternatives com Icecast2 + DarkIce, aquestes només permeten emissió d'àudio. En canvi, NGINX RTMP ofereix:

- Suport de vídeo i àudio.
- Configuració senzilla.
- Alta compatibilitat amb OBS i FFmpeg.
- Excel·lent rendiment i estabilitat.

![image](https://github.com/user-attachments/assets/9fc02e5c-6260-4991-8845-4e1d2e93cc2c)

---

## 📤 2. Pujada d'arxius i execució del servei

Un cop configurat el servidor RTMP, vam preparar els fitxers de vídeo (per exemple, .mp4) que volíem emetre.

### 🚀 Transferència via scp

Els arxius es van pujar al servidor remot mitjançant la comanda:

```bash
scp -i Escriptori/DADES/MarcManzorro/PROJECTE_TRANSVERSAL/pro-asicx1A-grup4.pem Escriptori/DADES/MarcManzorro/PROJECTE_TRANSVERSAL/entre_dos_aguas.mp4  ubuntu@54.164.134.61:/home/ubuntu/
```
![image](https://github.com/user-attachments/assets/ce4652c3-f643-4d32-9ad5-bb5f30293eec)

Això permet tenir el contingut disponible al servidor per fer el streaming.

### ▶️ Emissió amb FFmpeg

Per enviar el vídeo al servidor RTMP, vam utilitzar FFmpeg amb una comanda com aquesta:

```bash
ffmpeg -stream_loop -1 -re -i entre_dos_aguas.mp4 -c:v libx264 -preset veryfast -c:a aac -f flv rtmp://54.164.134.61:1935/live/stream
```
O un altre video, dels que tinguem descarrgats en mp4.
Aquest procés envia el flux a l'aplicació live definida a NGINX, amb el nom de stream.


![image](https://github.com/user-attachments/assets/833430f5-5c25-4d2d-9069-b0cb47689c05)

---

## 🌐 3. Implementació via web

Per fer el servei més accessible i millor nvisualment, es va crear un fitxer HTML amb un reproductor que permet als usuaris veure el vídeo directament des del navegador.


### ✅ Avantatges del web:

- Accés directe des de qualsevol navegador.
- No cal cap aplicació externa per visualitzar el vídeo.
- Interfície simple i neta, personalitzable.

![image](https://github.com/user-attachments/assets/bab52df9-03a5-47ff-a17f-da9f0cd808b1)

---

## ✅ Resultat final

Amb aquesta configuració hem obtingut un sistema de streaming funcional i eficient que permet:

- Fer emissió d'àudio i vídeo en temps real.
- Fer arribar el contingut tant via reproductor com via web.
- Mantenir una estructura simple, segura i versàtil.

Aquest sistema és ideal per presentacions, classes en directe, projectes de ràdio/vídeo online, i molt més.