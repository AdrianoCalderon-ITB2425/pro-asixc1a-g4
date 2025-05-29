# Presentació disseny CPD-grup4

Aquí podem veure en el cablejat vermell el sistema antiincendis per gas, ja que no és recomanable utilitzar aigua ni la retirada total d’oxigen a la sala.  
En groc, podem veure el circuit elèctric que porta energia a tots els punts necessaris, inclòs el generador en cas que hagi de repartir energia.

![image](https://github.com/user-attachments/assets/73e7aa74-6aba-49c0-8b0a-28409daa39df)
![image](https://github.com/user-attachments/assets/3d23021a-ad5b-4a90-88a3-2cbb108c49d3)
![image](https://github.com/user-attachments/assets/7eb3c777-f7e9-4421-b514-d217c5a7c038)
![image](https://github.com/user-attachments/assets/89ebffaa-8abe-4bfb-96ee-1db9349d560f)
![image](https://github.com/user-attachments/assets/b1f242ff-7801-460f-bdc4-a6c8d0fa7535)


### 1. Ubicació física i estructura del CPD
- **Ubicació**: Soterrani, zona protegida amb accés restringit. A l’edifici de CaixaBank, a la planta -4. Av. Diagonal 621-629.

![image](https://github.com/user-attachments/assets/eca685a0-9cc5-4673-a9c4-5611f9da453f)

  
- **Mesures de seguretat física**:
  - Vidres tintats i blindats.
  - Control d’accés biomètric + targetes RFID.

![image](https://github.com/user-attachments/assets/2d67de7e-6dcc-4c62-9f29-f70c3c796e33)
![image](https://github.com/user-attachments/assets/2ce18d24-85c8-4e0b-9dd2-8517e9f58c70)


  - Videovigilància 24/7 amb càmeres IP d’alta resolució.

![image](https://github.com/user-attachments/assets/6cb66907-a973-49d6-b8d6-7e627d47e069)

    
  - Identitat discreta: sense senyalització externa ni finestres visibles.
- **Distribució**:
  - Racks de mida mitjana-gran, ben espaiats.
  - Cablejat per conductes tècnics, etiquetat per color i funció.
  - Fibra òptica predominant + una mica de coure (patch).
  - Accés superior i inferior mitjançant terra i sostre tècnic.
 
    ![image](https://github.com/user-attachments/assets/3dbe7da4-be17-4ce1-a9a7-76ea8fe19058)



### 2. Climatització i eficiència energètica
- **Sistema de refrigeració principal**: Vertiv Liebert DSE (free-cooling + sense ús d’aigua).

![image](https://github.com/user-attachments/assets/12654b27-d98d-44ff-ab02-1a61b0642031)
![image](https://github.com/user-attachments/assets/f3bd904b-f10f-476d-9d09-5fb2065dd512)

  
- **Climatització perimetral redundant N+1**.
- **Temperatura/Humitat controlades**: 20–24 °C / 45–55 % HR.
- **Optimització natural**: Circulació d’aire passiva aprofitant la pressió negativa i el disseny tèrmic.
- **Contenció de passadissos freds/calents**.


### 3. Racks i infraestructura de xarxa
- **Racks**: Vertiv VR Rack 42U – pany electrònic amb obertura manual en emergències.
- **Disseny modular amb organització accessible**.

![image](https://github.com/user-attachments/assets/bb65387e-6dc4-44b2-a939-c0b2f3f968fd)

  
- **Equipament als racks**:
  - Patch panels: Belden Modular Cat6a / LC per a FO.

  ![image](https://github.com/user-attachments/assets/77a373f0-1c8b-4e1a-b1bd-467930cd495a)

     
  - Switches: TP-Link Omada SG6654X amb gestió L3 i 10 Gb SFP+.
 
![image](https://github.com/user-attachments/assets/f04881da-ea67-412c-a0d4-cce5e346a14e)

  
- **Monitoratge ambiental**: Sensors de temperatura, humitat i vibració.


### 4. Infraestructura elèctrica
- **SAI (UPS)**: Eaton 9PX 11kVA (doble conversió, amb bateria d’1 hora d’autonomia).

![image](https://github.com/user-attachments/assets/68c2325a-0694-43f5-a414-e3ab407023f6)

  
- **Generador de suport**: Generac Industrial 150kW gas natural, arrencada automàtica en 10 s.

![image](https://github.com/user-attachments/assets/e47111d5-9ba5-434e-8342-4a68d59e71cf)

  
- **Xarxa elèctrica**: Redundant A/B per a racks + distribució mitjançant PDU intel·ligents.
- **Cablejat elèctric**: THHN/THWN-2 en tubs EMT galvanitzats (diferents calibres segons potència): Són cables de coure amb alta resistència tèrmica i aigua, protegits dins tubs metàl·lics per evitar danys i interferències, assegurant una distribució elèctrica segura i fiable dins del CPD.

  ![image](https://github.com/user-attachments/assets/131ba7a4-96b3-4276-b3c4-2dd22f897448)


### 5. Seguretat física i lògica
- **Física**:
  - Accessos biomètrics i videovigilància IP.
    
![image](https://github.com/user-attachments/assets/8d8c68c7-845e-42cb-aa6d-44096d3d2977)
 
  - Detectors de fum tipus VESDA.

![image](https://github.com/user-attachments/assets/da91a6b9-8c29-42c9-a189-d8f3ad8e3a7b)
    
  - Extinció amb gas Novec 1230 (no danya el maquinari).

![image](https://github.com/user-attachments/assets/241f9b6d-23f7-4406-a8a0-155f14369a21)

  
  - Vies d’evacuació senyalitzades.
- **Lògica**:
  - Autenticació 2FA (Windows i Linux).
  - Firewalls NGFW (a AWS: AWS Network Firewall).
  - Còpies de seguretat automatitzades (AWS Backup + S3 Glacier).
  - Monitoratge: Amazon CloudWatch + Kibana + Zabbix.
  - Configuració RAID (RAID 10 i 5 en bases de dades).
  - VPN IPsec per a accés remot a equips del CPD.
  - Antiincendis: Novec 1230 (FK-5-1-12), sistema de supressió del foc per gas.


### 6. Servidors al núvol – AWS
- **Tot està virtualitzat a AWS, fent servir instàncies EC2 sobre**:
  - Ubuntu Server 22.04 LTS per a servidors Linux.
  - Windows Server 2022 Datacenter per a entorns Windows.
- **Serveis configurats**:
  - **Rol** | **SO** | **Instància EC2 recomanada**
  - Àudio i vídeo (streaming) | Ubuntu Server | m6i.xlarge (4 vCPU, 16 GB)
  - Base de dades (PostgreSQL) | Ubuntu Server | r6g.large (Graviton, RAM optimitzada)
  - Servidor web (Apache/Nginx) | Ubuntu Server | t4g.medium
  - Elasticsearch + Kibana | Ubuntu Server | c7g.xlarge
  - Directori actiu i DNS | Ubuntu Server | t3.medium + AWS Directory Service



### 7. Monitoratge i gestió
- **AWS CloudWatch**: Registres, ús de CPU, RAM, xarxa.
- **Elastic Stack (ELK)**: Centralització d’esdeveniments amb panells.
- **Zabbix**: Monitoratge personalitzat de serveis clau.
- **Grafana + Prometheus (opcional)**: Anàlisi visual.


### 8. Sostenibilitat
- **Energia verda contractada per AWS (100 % renovable per a 2025)**.
- **Ús de contenció tèrmica + equips amb certificat ENERGY STAR**.
- **Apagat automàtic dels equips de xarxa fora de l’horari**.
- **Virtualització per reduir maquinari físic**.
- **Cablejat curt i optimitzat**.
- **El disseny del CPD està orientat a garantir un funcionament sostenible i eficient, minimitzant l’impacte ambiental i optimitzant els recursos energètics i materials**.


#### 8.1. Eficiència energètica
- Es fa ús de la contenció de passadissos freds i calents, que permet separar els fluxos d’aire fred i calent, reduïnt significativament la demanda energètica del sistema de climatització.
- El sistema de refrigeració principal, Vertiv Liebert DSE, utiliza free-cooling (refrigerar amb aire exterior) i no consumeix aigua, la qual cosa augmenta l’eficiència i redueix l’impacte ambiental.
- La distribució elèctrica es realitza mitjançant PDU intel·ligents i xarxes redundants A/B, que permeten un control precís i una optimització del consum energètic.


#### 8.2. Reducció de l’impact ambiental
- La total virtualització a AWS implica una reducció important del maquinari físic necessari localment, disminuint el consum elèctric i l’ús d’espai.
- Els equips de xarxa estan configurats per a un apagat automàtic fora d’horari, evitant consums innecessaris.
- El cablejat és curt i optimitzat, minimitzant l’ús de materials i les pèrdues en la transmissió.

#### 8.3. Energia renovable
- La infraestructura en núvol contractada utilitza energia 100% renovable segons l’objectiu d’AWS per al 2025, contribuint així a la reducció d’emissions i a l’ús responsable dels recursos energètics.

#### 8.4. Sistemes eficients de climatització
- S’aposta per un sistema que evita l’ús d’aigua en la refrigeració, una pràctica més sostenible i menys dependent de recursos hídrics.
- El disseny tèrmic aprofita la circulació passiva d’aire mitjançant la pressió negativa, afavorint la dissipació natural de la calor i reduint la necessitat de climatització activa.

#### 8.5. Monitoratge i gestió sostenible
- El CPD incorpora sensors per a la mesura constant de temperatura, humitat i vibració, assegurant un ambient òptim per a la vida útil dels equips i l’eficiència energètica.
- Es fan servir eines de monitoratge com AWS CloudWatch, Zabbix, Grafana i Elastic Stack que permeten detectar consums innecessaris o anomalies per ajustar els recursos de manera proactiva.
