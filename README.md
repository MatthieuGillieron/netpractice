# 🌐 Guide des Réseaux Informatiques - Les Fondamentaux

> **Guide pédagogique pour étudiants débutants (Bac+1 / DUT-BUT Informatique)**

## 📚 Table des matières

1. [Les Fondamentaux Réseau](#-les-fondamentaux-réseau)
2. [Adresses IP et Formats](#-adresses-ip-et-formats)
3. [Les Paquets Réseau](#-les-paquets-réseau)
4. [Le Routage](#-le-routage)
5. [Les Protocoles TCP vs UDP](#-les-protocoles-tcp-vs-udp)
6. [Les Ports Réseau](#-les-ports-réseau)
7. [Le Modèle OSI](#-le-modèle-osi)
8. [LAN vs WAN](#-lan-vs-wan)
9. [Appareils Réseau](#-appareils-réseau)
10. [Sous-réseautage (Subnetting)](#-sous-réseautage-subnetting)

---

## 🔧 Les Fondamentaux Réseau

Un réseau informatique, c'est comme un **système postal géant** où les ordinateurs s'échangent des informations sous forme de "lettres" appelées **paquets**.

### Concepts clés :
- **Adresse IP** = Adresse postale de votre ordinateur
- **Paquet** = Lettre contenant vos données
- **Routeur** = Bureau de poste qui achemine les lettres
- **Protocole** = Règles d'envoi (recommandé, normal, express...)

---

## 📍 Adresses IP et Formats

### IPv4 (Internet Protocol version 4)
Format : `XXX.XXX.XXX.XXX` (4 nombres de 0 à 255)

**Exemples concrets :**
```
192.168.1.1    → Adresse de votre box internet (gateway)
192.168.1.100  → Votre ordinateur sur le réseau local
8.8.8.8        → Serveur DNS de Google
127.0.0.1      → Votre propre machine (localhost)
```

### IPv6 (Internet Protocol version 6)
Format : `XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX:XXXX` (8 groupes hexadécimaux)

**Exemple :**
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

> **Pourquoi IPv6 ?** IPv4 permet ~4 milliards d'adresses, IPv6 en permet 340 sextillions !

---

## 📦 Les Paquets Réseau

### Qu'est-ce qu'un paquet ?

Imaginez que vous envoyez une **lettre recommandée** :

```
┌─────────────────────────────────────┐
│ ENVELOPPE (En-têtes réseau)         │
│ ├─ Expéditeur: 192.168.1.100       │
│ ├─ Destinataire: 8.8.8.8           │
│ ├─ Type: TCP                       │
│ └─ Port: 80                        │
├─────────────────────────────────────┤
│ CONTENU (Données)                   │
│ "GET / HTTP/1.1"                   │
│ "Host: www.google.com"             │
└─────────────────────────────────────┘
```

### Contenu type d'un paquet :
- **En-tête IP** : Adresses source et destination
- **En-tête Transport** : Ports, numéros de séquence
- **Données** : Le contenu réel (page web, email, fichier...)

---

## 🗺️ Le Routage

### Comment un paquet voyage-t-il ?

**Exemple : Votre PC → Google**

```
[Votre PC] → [Switch local] → [Routeur maison] → [FAI] → [Internet] → [Serveurs Google]
192.168.1.100    192.168.1.1      Orange/SFR     Backbone      8.8.8.8
```

### Étapes détaillées :

1. **Votre PC** crée un paquet pour `8.8.8.8`
2. **Switch local** : "Cette adresse n'est pas dans mon réseau local"
3. **Routeur maison** : "Je connais le chemin vers Internet"
4. **FAI** : "Je route vers le backbone Internet"
5. **Internet** : Plusieurs routeurs se passent le paquet
6. **Google** : "C'est pour moi !" et répond

> **Analogie** : C'est comme envoyer une lettre de Marseille à Tokyo - elle passe par plusieurs centres de tri !

---

## 🚀 Les Protocoles TCP vs UDP

### TCP (Transmission Control Protocol)
**= Courrier recommandé avec accusé de réception**

**Caractéristiques :**
- ✅ **Fiable** : Garantit la livraison
- ✅ **Ordonné** : Les données arrivent dans l'ordre
- ❌ **Plus lent** : Beaucoup de vérifications

**Cas d'usage :**
- Navigation web (HTTP/HTTPS)
- Emails
- Transfert de fichiers

### UDP (User Datagram Protocol)
**= Courrier normal, rapide mais sans garantie**

**Caractéristiques :**
- ✅ **Rapide** : Pas de vérifications
- ❌ **Non fiable** : Peut perdre des données
- ❌ **Non ordonné** : Les données peuvent arriver dans le désordre

**Cas d'usage :**
- Streaming vidéo/audio
- Jeux en ligne
- DNS (résolution de noms)

---

## 🚪 Les Ports Réseau

### Qu'est-ce qu'un port ?

Un port, c'est comme un **numéro d'appartement** dans un immeuble (votre adresse IP).

```
Adresse IP : 192.168.1.100 (l'immeuble)
├─ Port 80  : Serveur web (appartement du concierge web)
├─ Port 22  : SSH (appartement de l'administrateur)
├─ Port 25  : Email (appartement du facteur)
└─ Port 443 : HTTPS (appartement sécurisé du web)
```

### Ports standards à connaître :
- **Port 80** : HTTP (web non sécurisé)
- **Port 443** : HTTPS (web sécurisé)
- **Port 22** : SSH (connexion sécurisée)
- **Port 25** : SMTP (envoi d'emails)
- **Port 53** : DNS (résolution de noms)

---

## 🏗️ Le Modèle OSI

### Les 4 premières couches (essentielles)

```
┌─────────────────────────────────────┐
│ Couche 4 - TRANSPORT               │ ← TCP/UDP, Ports
│ (Fiabilité et ports)               │
├─────────────────────────────────────┤
│ Couche 3 - RÉSEAU                  │ ← IP, Routage
│ (Adressage et routage)             │
├─────────────────────────────────────┤
│ Couche 2 - LIAISON                 │ ← Ethernet, WiFi
│ (Communication locale)             │
├─────────────────────────────────────┤
│ Couche 1 - PHYSIQUE                │ ← Câbles, ondes radio
│ (Support physique)                 │
└─────────────────────────────────────┘
```

### Exemples concrets :

**Couche 1 - Physique :**
- Câbles Ethernet (RJ45)
- Ondes WiFi
- Fibre optique

**Couche 2 - Liaison :**
- Ethernet (adresses MAC)
- WiFi (802.11)
- Communication dans le même réseau local

**Couche 3 - Réseau :**
- IP (IPv4/IPv6)
- Routage entre réseaux différents

**Couche 4 - Transport :**
- TCP (fiable)
- UDP (rapide)
- Gestion des ports

---

## 🏠 LAN vs WAN

### LAN (Local Area Network)
**= Réseau local (votre maison/entreprise)**

**Caractéristiques :**
- Petite zone géographique
- Haute vitesse (1 Gbps+)
- Contrôlé par vous
- Adresses privées (192.168.x.x)

**Exemples :**
- Réseau de votre maison
- Réseau d'une école
- WiFi d'un café

### WAN (Wide Area Network)
**= Réseau étendu (Internet)**

**Caractéristiques :**
- Grande zone géographique
- Vitesse variable
- Contrôlé par les FAI
- Adresses publiques

**Exemples :**
- Internet
- Réseau d'une multinationale
- Connexion entre villes

---

## 🔧 Appareils Réseau

### 🧭 Switch - Le distributeur de courrier
**Analogie :** Comme un **distributeur de courrier dans un immeuble**

**Rôle :**
- Connecte plusieurs appareils dans le même réseau
- Apprend les adresses MAC
- Achemine intelligemment les trames

```
[PC1] ──┐
         ├── [SWITCH] ── [Routeur]
[PC2] ──┘
```

### 🔁 Routeur - Le chef de gare
**Analogie :** Comme un **chef de gare** qui dirige les trains

**Rôle :**
- Connecte différents réseaux
- Prend des décisions de routage
- Maintient une table de routage

```
[Réseau A] ── [ROUTEUR] ── [Réseau B]
192.168.1.0/24           10.0.0.0/24
```

### 🚪 Gateway - La porte de sortie
**Analogie :** Comme une **porte de sortie vers le monde extérieur**

**Rôle :**
- Point de sortie du réseau local
- Souvent intégré au routeur
- Traduit entre réseaux privés/publics

---

## 🔢 Sous-réseautage (Subnetting)

### Qu'est-ce que le subnetting ?

Le subnetting, c'est comme **diviser un grand immeuble en plusieurs appartements** avec des adresses distinctes.

### Masque de sous-réseau (Subnet Mask)

Le masque détermine **quelle partie de l'adresse IP identifie le réseau** et quelle partie identifie l'hôte.

**Exemple :** `192.168.1.0/26`

### Conversion en binaire

```
Adresse IP : 192.168.1.0
En binaire : 11000000.10101000.00000001.00000000

Masque /26 : 255.255.255.192
En binaire : 11111111.11111111.11111111.11000000
             ↑─────────────────────────────↑
             26 bits pour le réseau    6 bits pour les hôtes
```

### Notation CIDR

**CIDR** = Classless Inter-Domain Routing

- `/26` signifie que les **26 premiers bits** identifient le réseau
- Les **6 derniers bits** (32-26=6) identifient les hôtes
- Nombre d'hôtes possibles : 2^6 = 64 adresses

### Calcul de l'incrément

**Incrément = 256 - dernier octet du masque**

Pour `/26` :
- Masque : `255.255.255.192`
- Incrément : `256 - 192 = 64`

### Exemple concret : Réseau `192.168.1.0/26`

**Informations du réseau :**
- **Réseau de base :** `192.168.1.0/26`
- **Masque :** `255.255.255.192`
- **Incrément :** 64
- **Nombre d'hôtes :** 62 (64 - 2 pour réseau et broadcast)

**Sous-réseaux créés :**

```
Sous-réseau 1 : 192.168.1.0/26
├─ Adresse réseau    : 192.168.1.0
├─ Première IP utile : 192.168.1.1
├─ Dernière IP utile : 192.168.1.62
└─ Adresse broadcast : 192.168.1.63

Sous-réseau 2 : 192.168.1.64/26
├─ Adresse réseau    : 192.168.1.64
├─ Première IP utile : 192.168.1.65
├─ Dernière IP utile : 192.168.1.126
└─ Adresse broadcast : 192.168.1.127

Sous-réseau 3 : 192.168.1.128/26
├─ Adresse réseau    : 192.168.1.128
├─ Première IP utile : 192.168.1.129
├─ Dernière IP utile : 192.168.1.190
└─ Adresse broadcast : 192.168.1.191

Sous-réseau 4 : 192.168.1.192/26
├─ Adresse réseau    : 192.168.1.192
├─ Première IP utile : 192.168.1.193
├─ Dernière IP utile : 192.168.1.254
└─ Adresse broadcast : 192.168.1.255
```

### Tableau récapitulatif des masques courants

| CIDR | Masque          | Incrément | Hôtes | Sous-réseaux |
|------|-----------------|-----------|-------|--------------|
| /24  | 255.255.255.0   | 256       | 254   | 1            |
| /25  | 255.255.255.128 | 128       | 126   | 2            |
| /26  | 255.255.255.192 | 64        | 62    | 4            |
| /27  | 255.255.255.224 | 32        | 30    | 8            |
| /28  | 255.255.255.240 | 16        | 14    | 16           |

### Erreurs fréquentes à éviter

❌ **Adresses IP en double**
```
PC1: 192.168.1.10/26
PC2: 192.168.1.10/26  ← CONFLIT !
```

❌ **Mauvaise gateway**
```
PC: 192.168.1.65/26 (sous-réseau 2)
Gateway: 192.168.1.1  ← Gateway du sous-réseau 1 !
```

❌ **Utiliser l'adresse réseau ou broadcast**
```
Réseau: 192.168.1.0/26
PC: 192.168.1.0       ← Adresse réseau (interdite)
PC: 192.168.1.63      ← Adresse broadcast (interdite)
```

✅ **Configuration correcte**
```
Sous-réseau: 192.168.1.64/26
PC1: 192.168.1.65
PC2: 192.168.1.66
Gateway: 192.168.1.65 (ou toute IP valide du sous-réseau)
```

---

## 🎯 Points clés à retenir

1. **Une adresse IP** = adresse postale de votre ordinateur
2. **Un paquet** = lettre contenant vos données
3. **TCP** = courrier recommandé, **UDP** = courrier rapide
4. **Routeur** = chef de gare qui dirige le trafic
5. **Switch** = distributeur local dans un immeuble
6. **Gateway** = porte de sortie vers l'extérieur
7. **Subnetting** = diviser un réseau en sous-réseaux plus petits

