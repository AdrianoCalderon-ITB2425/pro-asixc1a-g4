
---
# pro-asixc1a-g4
Github del projecte transversal

# 📘 Servei 1: Elasticsearch, Kibana i Auditbeat (versió 8.17.4)

### 🖥️ Entorn del sistema

- **Sistema operatiu:** Ubuntu Server
- **Usuari dedicat:** `elastic` amb permisos d'administrador
- **Serveis instal·lats:** Elasticsearch, Kibana i Auditbeat
- **Versió dels serveis:** 8.17.4

---

### 0. 📋 Prerequisits

```bash
sudo apt update && sudo apt upgrade -y
```

### 🌟 Pas 1: Creació d'usuari i preparació inicial

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


### 📦 Pas 2: Descàrrega i descompressió dels components

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

### 🌐 Pas 3: Configuració

1. Configuració d'elasticsearch.yml
 
   ![Captura de pantalla de 2025-05-27 11-32-11](https://github.com/user-attachments/assets/49728a22-038b-440d-ba0a-9a9becde6517)




2. Configuració del kibana.yml

    ![image](https://github.com/user-attachments/assets/3fd493f7-36f6-4b14-9c63-64e0a68ec404)
   ![image](https://github.com/user-attachments/assets/5ff4307d-20bb-4855-b5c4-54156da5fbdd)



3. Configuració auditbeat.yml

   ![image](https://github.com/user-attachments/assets/540f4d95-b93e-40b1-8198-d9b3cee6e798)
   ![image](https://github.com/user-attachments/assets/bf99f7d2-678e-46e8-81ce-4b3126c7e962)
   ![image](https://github.com/user-attachments/assets/8911f159-5360-4e99-a539-4095721aea29)


### 📥 Pas 4: Executem elastic per obtenir les claus de Kibana

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

### ✅ Pas 5: Accedir a la web de kibana

![Captura de pantalla de 2025-05-23 12-55-50](https://github.com/user-attachments/assets/3b6cea78-2640-4c7a-852d-bc298587ca31)

---


# 📘 Servei 2: Nfs


### 📦 **1. Instalación de Paquetes**
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install nfs-kernel-server -y
```

### 📂 **2. Preparación del Directorio Compartido**
```bash
sudo mkdir -p /mnt/nfs
sudo chown nobody:nogroup /mnt/nfs
sudo chmod 777 /mnt/nfs  # Ajustar permisos según necesidades
```

### ⚙️ **3. Configuración de Exportaciones NFS**
Editar el archivo `/etc/exports`:
```bash
sudo nano /etc/exports
```
![image](https://github.com/user-attachments/assets/1b5e99f8-3766-4f05-950f-1e64f3fd8dda)



### 🔄 **4. Aplicar Configuración**
```bash
sudo exportfs -arv
sudo systemctl restart nfs-kernel-server
sudo systemctl enable nfs-kernel-server
```

### ✔️ **5. Verificación del Servidor**
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

---

# 📘 Serveis 3 i 4: DNS i Nginx

### 🔧 Instal·lació de DNS
```bash
# Actualitzar repositoris
sudo apt update

# Instal·lar BIND9 i utilitats
sudo apt install bind9 bind9utils bind9-doc

# Verificar instal·lació
systemctl status bind9
```
![image](https://github.com/user-attachments/assets/9226571e-0e84-450a-923f-2b5af94450fb)

### 📁 Estructura d'Arxius DNS
```
/etc/bind/
├── named.conf           # Configuració principal
├── named.conf.local     # Zones locals
├── named.conf.options   # Opcions globals
└── zones/               # Arxius de zona
    ├── db.example.com
    └── db.192.168.1
```

---

### 🌐 Instal·lació de Nginx

```bash
# Actualitzar repositoris
sudo apt update

# Instal·lar Nginx
sudo apt install nginx

# Iniciar i habilitar servei
sudo systemctl start nginx
sudo systemctl enable nginx

# Verificar estat
sudo systemctl status nginx
```
![image](https://github.com/user-attachments/assets/55b1214c-afbb-4fb4-abd6-cc166712e219)

### 📁 Estructura d'Arxius Nginx
```
/etc/nginx/
├── nginx.conf              # Configuració principal
├── sites-available/        # Llocs disponibles
├── sites-enabled/          # Llocs habilitats
├── conf.d/                 # Configuracions addicionals
└── /var/www/html/          # Directori web per defecte
```

---

## ⚙️ Configuració DNS


### � Configuració de Zones (`/etc/bind/named.conf.local`)
![image](https://github.com/user-attachments/assets/3de75146-b972-483f-9868-41a374356108)


### 📝 Arxiu de Zona Directa (`/etc/bind/db.projecteg4.es`)
![image](https://github.com/user-attachments/assets/e4c025f3-be6a-46c3-a858-121bbc3a0bc2)


---

## 🔨 Configuració Nginx

### � Lloc Web Principal (`/etc/nginx/sites-available/g4_proyecto`)
![image](https://github.com/user-attachments/assets/fd36da55-9483-4bf9-9d3b-972d23b45d20)
![image](https://github.com/user-attachments/assets/4e36ea73-98a6-45df-a4dd-226bb87cfdde)




---

## 🔗 Integració DNS + Nginx

### 1️⃣ Configurar Registres DNS
![image](https://github.com/user-attachments/assets/28bee0ea-8462-4041-adee-4f83ddac530f)


## Resultat Final
![image](https://github.com/user-attachments/assets/e7573316-1e4f-4245-abf2-79b47a465b29)


