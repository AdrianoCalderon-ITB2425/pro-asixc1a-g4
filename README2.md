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


# Documentació del procés de creació i desplegament de la base de dades `gestio_personal`

## 🗃️ 1. Creació de la base de dades local

Vaig crear la base de dades localment utilitzant PostgreSQL al meu ordinador. La vaig anomenar `gestio_personal` i hi vaig afegir diverses taules per gestionar la informació dels empleats, com ara dades personals, contractes, absències i departaments.

![image](https://github.com/user-attachments/assets/7be283fe-2bf7-4031-86d4-1d2187990ed1)

---

## 🔒 2. Còpia de seguretat (backup)

Per prevenir qualsevol pèrdua de dades, vaig generar una còpia de seguretat completa de l'estructura i el contingut de la base de dades. Aquest backup es va desar en un fitxer `.sql`, que conté totes les instruccions necessàries per recrear la base.

![image](https://github.com/user-attachments/assets/7991c879-24c4-41a6-ac9c-8f62b95bb7eb)

---

## 🔁 3. Transferència del backup al servidor remot

Amb la base de dades preparada, vaig utilitzar l'eina `scp` (secure copy) per pujar el fitxer `.sql` al servidor remot. Aquesta eina permet enviar fitxers de manera segura a través d'una connexió SSH.

![image](https://github.com/user-attachments/assets/afd9f994-1224-4f50-96e7-d84d1d97435e)

---

## ⚙️ 4. Restauració de la base de dades al servidor

Un cop el fitxer estava al servidor, em vaig connectar a PostgreSQL i vaig executar el fitxer `.sql` per restaurar la base de dades `gestio_personal`. Això va incloure la creació de les taules i la inserció de totes les dades.


---

## ✅ 5. Verificació del funcionament

Per assegurar-me que tot funcionava correctament, vaig accedir a la base de dades al servidor i vaig comprovar que les taules estaven presents i que les dades s'havien importat correctament.

![image](https://github.com/user-attachments/assets/ad16fcc6-6f01-4112-87a8-08cdf0c77ce8)
![image](https://github.com/user-attachments/assets/1cef5163-ebc3-40b8-b4d2-c76fbe9d674b)
![image](https://github.com/user-attachments/assets/15981f21-8782-4385-a0c4-169ff833cd16)

---

## 🧱 6. Creació d’un usuari restringit

Un aspecte important del projecte ha estat afegir un usuari amb permisos restringits. Aquest usuari té accés limitat i no pot consultar taules sensibles com `emplat` i `absencia`, millorant així la seguretat i el control de l’accés a la informació.

![image](https://github.com/user-attachments/assets/06afad46-2e69-424d-900f-9e0f911616be)

---

## 🧑‍💻 7. Configuració de l'arxiu `index.php`

Finalment, vaig treballar en la interfície web mitjançant `index.php`. Vaig aplicar una mica d’estil i estructura per facilitar-ne l’ús. Tot i que inicialment es volia afegir funcionalitats com cercar i afegir usuaris, finalment només es va implementar l’opció d’exportar les dades a PDF per conservar-les fàcilment.

![image](https://github.com/user-attachments/assets/25c74adf-4dcb-48b8-9e69-099f43cb1507)

---

## 📈 8. Resultat final

L’estructura de la base de dades compleix amb els requisits de l’activitat. És accessible des del servidor i permet el control d’accés mitjançant l’usuari restringit.

![image](https://github.com/user-attachments/assets/66c0716e-4187-4382-9ab0-30954ed73a54)
