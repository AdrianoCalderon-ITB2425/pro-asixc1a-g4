
---
# pro-asixc1a-g4
Github del projecte transversal

# 📘 Servei 1: Elasticsearch, Kibana i Auditbeat (versió 8.17.4)

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


# 📘 Servei 2: Nfs


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


