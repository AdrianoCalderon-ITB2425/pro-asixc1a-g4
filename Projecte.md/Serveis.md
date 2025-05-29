
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

---

# 📘 Serveis 3 i 4: DNS i Nginx

## 📚 Taula de Continguts
1. [Instal·lació de DNS](#-instal·lació-de-dns)
2. [Instal·lació de Nginx](#-instal·lació-de-nginx)  
3. [Configuració DNS](#%EF%B8%8F-configuració-dns)  
4. [Configuració Nginx](#-configuració-nginx)  
5. [Integració DNS + Nginx](#-integració-dns--nginx)

---

## 🔧 Instal·lació de DNS
```bash
# Actualitzar repositoris
sudo apt update

# Instal·lar BIND9 i utilitats
sudo apt install bind9 bind9utils bind9-doc

# Verificar instal·lació
systemctl status bind9
```
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

## 🌐 Instal·lació de Nginx

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

### 🔧 Configuració Principal (`/etc/bind/named.conf.options`)
```bind
options {
    directory "/var/cache/bind";
    
    // Configurar forwarders (DNS públics)
    forwarders {
        8.8.8.8;
        8.8.4.4;
        1.1.1.1;
    };
    
    // Configuracions de seguretat
    allow-recursion { localhost; 192.168.1.0/24; };
    allow-query { localhost; 192.168.1.0/24; };
    
    // IPv6
    listen-on-v6 { any; };
    
    // Deshabilitar transferències de zona
    allow-transfer { none; };
};
```

### � Configuració de Zones (`/etc/bind/named.conf.local`)
```bind
// Zona directa
zone "example.com" {
    type master;
    file "/etc/bind/zones/db.example.com";
};

// Zona inversa
zone "1.168.192.in-addr.arpa" {
    type master;
    file "/etc/bind/zones/db.192.168.1";
};
```

### 📝 Arxiu de Zona Directa (`/etc/bind/zones/db.example.com`)
```bind
$TTL    604800
@       IN      SOA     ns1.example.com. admin.example.com. (
                        2024052701      ; Serial
                        604800          ; Refresh
                        86400           ; Retry
                        2419200         ; Expire
                        604800 )       ; Negative Cache TTL

; Servidors de noms
@       IN      NS      ns1.example.com.

; Registres A
ns1     IN      A       192.168.1.10
www     IN      A       192.168.1.20
web     IN      A       192.168.1.20
mail    IN      A       192.168.1.30

; Registre MX
@       IN      MX      10 mail.example.com.

; Registre CNAME
ftp     IN      CNAME   www.example.com.
```

---

## 🔨 Configuració Nginx

### � Lloc Web Principal (`/etc/nginx/sites-available/default`)
```nginx
server {
    listen 80;
    listen [::]:80;
    server_name example.com www.example.com;
    
    root /var/www/html;
    index index.html index.htm index.nginx-debian.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;
    
    server_tokens off;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
}
```


---

## 🔗 Integració DNS + Nginx

### 1️⃣ Configurar Registres DNS
```bind
www     IN A     192.168.1.20    ; Servidor web principal
app     IN A     192.168.1.20    ; Aplicació web
api     IN A     192.168.1.20    ; API
static  IN A     192.168.1.21    ; Contingut estàtic
```
---
