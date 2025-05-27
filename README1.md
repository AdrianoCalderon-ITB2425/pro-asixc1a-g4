# pro-asixc1a-g4
Github del projecte transversal

# 📘 Documentació d'instal·lació i configuració: Elasticsearch, Kibana i Auditbeat (versió 8.17.4)

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

---

*Documentació en procés - continuarà amb els següents passos de configuració...*
