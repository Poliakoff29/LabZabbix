# 🖥️ Supervision réseau complète avec Zabbix 7.4

Mise en place d'une infrastructure de supervision réseau complète avec Zabbix 7.4,
couvrant des équipements hétérogènes : serveurs Linux/Windows, pare-feu, routeur,
switch manageable et monitoring de sites web.

## 📌 Auteur
**DANNON ROCK** — Jr Network Engineer & Cybersecurity

## 🗓️ Date
Novembre 2026

---

## 🏗️ Architecture du lab

| Équipement | Rôle | Méthode |
|---|---|---|
| Zabbix Server 7.4 | Serveur de supervision | — |
| Ubuntu Server | Serveur Linux | Agent Zabbix |
| Windows (poste) | Poste utilisateur | Agent Zabbix |
| pfSense | Pare-feu | SNMP v2c |
| MikroTik | Routeur | SNMP v2c |
| Switch Cisco | Commutateur | SNMP v2c |

---

## 1️⃣ Installation de Zabbix Server

Zabbix Server 7.4 installé via l'appliance OVF importée dans VirtualBox.
- Accès GUI : `http://<IP>/zabbix` — Login : `Admin` / `zabbix`
- Accès SSH : `root` / `zabbix`

<img width="1365" height="678" alt="Capture d&#39;écran 2026-11-04 092631" src="https://github.com/user-attachments/assets/920c4b67-8bec-4546-9ff2-a6d7164792ac" />


---

## 2️⃣ Supervision Ubuntu Server (Agent Zabbix)

Installation de `zabbix-agent2` sur Ubuntu Server, configuration du fichier
`/etc/zabbix/zabbix_agent2.conf` avec l'IP du serveur Zabbix, puis ajout
de l'hôte dans la GUI avec le template `Linux by Zabbix agent`.

![02-ubuntu-host-green.png]

---

## 3️⃣ Supervision Windows (Agent Zabbix)

Installation de l'agent Zabbix 2 (.msi) sur le poste Windows, ouverture
du port 10050 dans le pare-feu Windows, puis ajout de l'hôte avec le
template `Windows by Zabbix agent`.

![03-windows-host-green.png]

---

## 4️⃣ Supervision pfSense (SNMP)

Activation du service SNMP dans **Services → SNMP** sur pfSense avec la
community `public`. Ajout de l'hôte dans Zabbix avec une interface SNMP
et le template `Network Generic Device by SNMP`.

<img width="1363" height="644" alt="Capture d&#39;écran 2026-11-04 132229" src="https://github.com/user-attachments/assets/4b0b76aa-20b1-4a06-9fad-d5ebd6f8c9e8" />

---

## 5️⃣ Supervision MikroTik (SNMP)

Activation SNMP via WinBox (**IP → SNMP**) ou CLI RouterOS. Restriction
d'accès à l'IP du serveur Zabbix uniquement. Template utilisé :
`MikroTik Router by SNMP`.

![05-mikrotik-host-green.png]

---

## 6️⃣ Supervision Switch Cisco (SNMP)

Configuration SNMP sur IOS avec `snmp-server community public RO` et
ACL limitant l'accès au serveur Zabbix. Template utilisé :
`Cisco IOS by SNMP`.

![06-cisco-snmp-config.png]

---

## 7️⃣ Gestion des utilisateurs, groupes et rôles

Création de groupes d'utilisateurs avec permissions sur les groupes d'hôtes.
Création d'utilisateurs avec assignation de rôles :

| Rôle | Niveau d'accès |
|---|---|
| Super admin | Accès total |
| Admin | Gestion hôtes et configs |
| User | Lecture seule |

<img width="1354" height="680" alt="Capture d&#39;écran 2026-11-04 123538" src="https://github.com/user-attachments/assets/50f34657-44c0-490c-b4e9-269cddc446a5" />

---

## 8️⃣ Carte réseau (Network Map)

Création d'une map réseau visuelle dans **Monitoring → Maps** avec tous
les équipements, liens et icônes représentatifs. Intégration de la map
dans le dashboard principal.

![08-network-map-complete.png]

---

## 9️⃣ Remplacement de la carte par Google Maps

Configuration du fournisseur de tuiles Google Maps dans
**Administration → Général → Paramètres géographiques** via une clé
API Google Cloud. Les équipements sont géolocalisés sur une vraie carte.

![09-google-maps-config.png]

---

## 🔟 Monitoring disponibilité sites web

Création de scénarios web dans **Configuration → Hôtes → Scénarios web**
pour surveiller la disponibilité et le temps de réponse des sites.

| Site surveillé | URL |
|---|---|
| Google | https://www.google.com |
| GitHub | https://www.github.com |

![10-web-monitoring-results.png]

---

## 📊 Dashboard global

Dashboard centralisé `Supervision Lab` regroupant :
- Statut de tous les hôtes
- Map réseau
- Graphiques CPU/RAM/Trafic
- Liste des alertes actives

![11-dashboard-global.png]

---

## 🔔 Alertes email

Configuration des alertes email via **Administration → Gestionnaire de médias**
avec envoi automatique sur déclenchement d'un trigger de niveau `Warning`
ou supérieur.

![12-alert-action-config.png]

---

## 🛠️ Technologies utilisées

- **Zabbix 7.4**
- **SNMP v2c**
- **Zabbix Agent 2**
- **Ubuntu Server 24.04**
- **Windows 10/11**
- **pfSense**
- **MikroTik RouterOS**
- **Cisco IOS**
- **Google Maps API**

---

## 📁 Structure des captures

| Fichier | Contenu |
|---|---|
| `01-zabbix-dashboard.png` | Dashboard Zabbix après installation |
| `02-ubuntu-host-green.png` | Hôte Ubuntu vert dans Zabbix |
| `03-windows-host-green.png` | Hôte Windows vert dans Zabbix |
| `04-pfsense-snmp-config.png` | SNMP activé sur pfSense |
| `05-mikrotik-host-green.png` | Hôte MikroTik vert dans Zabbix |
| `06-cisco-snmp-config.png` | SNMP configuré sur Cisco |
| `07-user-roles-config.png` | Gestion utilisateurs et rôles |
| `08-network-map-complete.png` | Map réseau complète |
| `09-google-maps-config.png` | Carte Google Maps configurée |
| `10-web-monitoring-results.png` | Résultats monitoring sites web |
| `11-dashboard-global.png` | Dashboard global complet |
| `12-alert-action-config.png` | Configuration des alertes |

---

> 📌 Projet réalisé dans le cadre du Master Réseaux & Télécommunications
> — UATM GASA Formation, Cotonou, Bénin.
