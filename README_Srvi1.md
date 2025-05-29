
---
# pro-asixc1a-g4
Github del projecte transversal

# 📘 Servei 1: Streaming

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

# 📘 Servei 1: Base De Dades

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

# 📘 Servei 3: Elasticsearch, Kibana i Auditbeat (versió 8.17.4)

## 🖥️ Entorn del sistema

- **Sistema operatiu:** Ubuntu Server
- **Usuari dedicat:** `elastic` amb permisos d'administrador
- **Serveis instal·lats:** Elasticsearch, Kibana i Auditbeat
- **Versió dels serveis:** 8.17.4

---

## 0. 📋 Prerequisits

```bash
sudo apt update && sudo apt upgrade -y
```

## 🌟 Pas 1: Creació d'usuari i preparació inicial

1. He creat un usuari específic per gestionar els serveis d'Elastic:
   ```bash
   sudo useradd -m -s /bin/bash elastic
   sudo passwd elastic --> (@ITB2025)
   sudo usermod -aG sudo elastic
   ```

2. Creació del directori de treball:
   ```bash
   mkdir ~/elastic
   cd ~/elastic
   sudo chown -R elastic:elastic /home/elastic/elastic/
   ```

3. Configuració del firewall per habilitar els ports necessaris:
   ```bash
   Habilitats al Security Group de AWS
   ```
![image](https://github.com/user-attachments/assets/c3934997-ed86-4b1f-a947-f99ae2b5c234)
![image](https://github.com/user-attachments/assets/b3f8a032-a4d1-453e-b427-277ed6161a14)


## 📦 Pas 2: Descàrrega i descompressió dels components

1. Descàrrega dels paquets Elastic Stack versió 8.17.4:
   ```bash
   wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.17.4-linux-x86_64.tar.gz
   wget https://artifacts.elastic.co/downloads/kibana/kibana-8.17.4-linux-x86_64.tar.gz
   wget https://artifacts.elastic.co/downloads/beats/auditbeat/auditbeat-8.17.4-linux-x86_64.tar.gz
   ```

2. Descompressió dels arxius:
   ```bash
   tar -xzf elasticsearch-8.17.4-linux-x86_64.tar.gz
   tar -xzf kibana-8.17.4-linux-x86_64.tar.gz
   tar -xzf auditbeat-8.17.4-linux-x86_64.tar.gz
   ```
![image](https://github.com/user-attachments/assets/94bf3486-8d7f-40ad-af6e-ec7d793263a5)

---

## 🌐 Pas 3: Configuració

1. Configuració d'elasticsearch.yml
 
   ![Captura de pantalla de 2025-05-27 11-32-11](https://github.com/user-attachments/assets/49728a22-038b-440d-ba0a-9a9becde6517)




2. Configuració del kibana.yml

    ![image](https://github.com/user-attachments/assets/3fd493f7-36f6-4b14-9c63-64e0a68ec404)
   ![image](https://github.com/user-attachments/assets/5ff4307d-20bb-4855-b5c4-54156da5fbdd)



3. Configuració auditbeat.yml

   ![image](https://github.com/user-attachments/assets/540f4d95-b93e-40b1-8198-d9b3cee6e798)
   ![image](https://github.com/user-attachments/assets/bf99f7d2-678e-46e8-81ce-4b3126c7e962)
   ![image](https://github.com/user-attachments/assets/8911f159-5360-4e99-a539-4095721aea29)


## 📥 Pas 4: Executem elastic per obtenir les claus de Kibana

   ```bash
   ./bin/elasticsearch
   ```

1. El primer cop que executem l'eslatic ens donara unes claus com aquestes
   ![image](https://github.com/user-attachments/assets/5fe713d9-426b-40bd-a8b3-b9db7d3df538)

2. Introdium les claus al kibana setup

   ```bash
   ./bin/kibana-setup
   ```
   ![image](https://github.com/user-attachments/assets/92f97ae6-a237-4345-9c5f-3f60cd0f093a)

3. Ho executem tot simultàniament en 3 terminals diferents

   ```bash
   ./bin/elasticshearch
   ./bin/kibana
   sudo ./auditbeat -e
   ```

## ✅ Pas 5: Accedir a la web de kibana

![Captura de pantalla de 2025-05-23 12-55-50](https://github.com/user-attachments/assets/3b6cea78-2640-4c7a-852d-bc298587ca31)

---


# 📘 Servei 4: Nfs


## 📦 **1. Instalación de Paquetes**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nfs-kernel-server -y
```

## 📂 **2. Preparación del Directorio Compartido**
```bash
sudo mkdir -p /mnt/nfs
sudo chown nobody:nogroup /mnt/nfs
sudo chmod 777 /mnt/nfs  # Ajustar permisos según necesidades
```

## ⚙️ **3. Configuración de Exportaciones NFS**
Editar el archivo `/etc/exports`:
```bash
sudo nano /etc/exports
```
![image](https://github.com/user-attachments/assets/0cd1e0d8-81ad-4fb0-a7f8-9a832216c949)


## 🔄 **4. Aplicar Configuración**
```bash
sudo exportfs -arv
sudo systemctl restart nfs-kernel-server
sudo systemctl enable nfs-kernel-server
```

## ✔️ **5. Verificación del Servidor**
```bash
showmount -e localhost
sudo exportfs -v
sudo systemctl status nfs-kernel-server
```
![image](https://github.com/user-attachments/assets/0b30f119-0562-418b-848b-14e3eb62125c)

## 💻 **6. Configuración del Cliente NFS**
### Instalación:
```bash
sudo apt install nfs-common -y
```

### Montaje Temporal:
```bash
sudo mkdir -p /mnt/nfs_client
sudo mount -t nfs 44.207.251.233:/mnt/nfs /mnt/nfs_client 
```

### Montaje Permanente (fstab):
```bash
echo 44.207.251.233:/mnt/nfs  /mnt/nfs_client  nfs  defaults,_netdev  0  0" | sudo tee -a /etc/fstab
sudo mount -a
```


