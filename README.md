## 4. Sostenibilitat i càlcul de la petjada ecològica del projecte

El nostre CPD, ubicat al soterrani de l’edifici de CaixaBank a l’Avinguda Diagonal, ha estat dissenyat sota criteris estrictes de sostenibilitat, eficiència energètica i respecte pel medi ambient. El seu funcionament, principalment virtualitzat a AWS, permet minimitzar l’impacte ecològic tot mantenint alts nivells de rendiment i seguretat.

### 4.1. Eficiència energètica

**Climatització intel·ligent i optimitzada**: S’utilitza el sistema **Vertiv Liebert DSE**, que incorpora **free-cooling** (refrigeració amb aire exterior), evitant el consum d’aigua i aprofitant l’energia ambiental. Aquest sistema està reforçat amb **climatització perimetral redundant N+1** i **contenció de passadissos freds i calents**, augmentant l’eficiència del flux tèrmic.
**Pressió negativa i disseny passiu**: Es promou la **circulació d’aire passiva** mitjançant disseny tèrmic i pressió negativa, reduint la necessitat de climatització activa.
**Distribució elèctrica optimitzada**: Mitjançant **PDU intel·ligents** i una **xarxa redundant A/B**, es permet un monitoratge i control del consum en temps real. El cablejat elèctric utilitza **conductors THHN/THWN-2 dins tubs EMT galvanitzats**, amb alta resistència i seguretat.

### 4.2. Reducció de l’impacte ambiental

**Virtualització completa a AWS**: L’ús de servidors EC2 elimina la necessitat de gran part del maquinari físic, reduint considerablement el consum elèctric i l'espai necessari.  
**Apagat automàtic de dispositius fora d’horari**: Els equips de xarxa estan configurats per aturar-se automàticament quan no són necessaris, evitant consums innecessaris.
**Cablejat optimitzat**: Es redueix la longitud i quantitat de cablejat emprat, minimitzant materials i pèrdues elèctriques.

### 4.3. Energia renovable

**AWS utilitza energia 100% renovable** (objectiu assolit al 2025). Això implica que tot el processament i l’emmagatzematge al núvol es realitza amb fonts d’energia neta, reduint dràsticament les emissions associades al consum informàtic.

### 4.4. Sistemes eficients de climatització

El sistema **no consumeix aigua**, a diferència d’altres refrigeracions evaporatives o hidròliques, contribuint així a un menor impacte sobre els recursos hídrics.
El **disseny del CPD**, amb terres i sostres tècnics, permet una gestió òptima del flux d’aire i facilita el manteniment sense interrupcions.

### 4.5. Monitoratge i gestió sostenible

**Sensors ambientals** dins dels racks permeten una gestió precisa de temperatura, humitat i vibració, allargant la vida útil dels equips i millorant l’eficiència.
El monitoratge mitjançant **AWS CloudWatch, Elastic Stack (ELK), Zabbix i Grafana** detecta consums anòmals i optimitza l’ús de recursos de manera proactiva.

### 4.6. Càlcul aproximat de la petjada ecològica

#### Consum elèctric estimat (virtualitzat en AWS)

**Instàncies EC2 actives**:  
  Suposant un consum mitjà de 40 W per instància → 6 instàncies x 40 W = 240 W  
  Funcionament mitjà: 20 hores/dia, 6 dies/setmana  
  → 240 W × 20 h/dia × 6 dies/setmana × 52 setmanes = **1.497,6 kWh/any**

**Trànsit de dades (streaming)**:  
  Estimació: 7 TB/mes (vídeo + àudio) → 84 TB/any  
  → 84.000 GB × 5 W/GB = **420.000 Wh = 420 kWh/any**

**Consum total estimat**:  
  **1.497,6 + 420 = 1.917,6 kWh/any**

#### Emissions de CO₂ (amb energia renovable d’AWS)

Factor de conversió mitjà per AWS: **0,0002 kg CO₂/kWh**
**Emissions anuals**: 1.917,6 kWh × 0,0002 = **0,3835 kg CO₂ eq.**  
  → Pràcticament nul, degut a la utilització exclusiva d’energia verda.

### 4.7. Certificacions i bones pràctiques

**Equipament amb certificat ENERGY STAR**, garantint una alta eficiència energètica.
Compliment de les polítiques ambientals d’AWS i alineació amb els **Objectius de Desenvolupament Sostenible (ODS)**, especialment:
  - **ODS 7**: Energia neta i assequible.
  - **ODS 9**: Infraestructura resilient i sostenible.
  - **ODS 12**: Consum i producció responsables.
  - **ODS 13**: Acció climàtica.
  - **ODS 16**: Sistemes resilients i segurs.
