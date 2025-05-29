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