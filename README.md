# NetPractice - Guide Complet de Configuration Réseau

> [!IMPORTANT]
> Ce guide s'inspire de différentes sources \
> dont une vidéo particulièrement claire : https://youtu.be/HQUw0CfQWAM

## 🎯 Objectif du Projet

NetPractice est un exercice pratique de configuration réseau où vous devez :
- Configurer des adresses IP et masques de sous-réseau
- Établir la connectivité entre différents appareils
- Comprendre le routage et les tables de routage
- Résoudre des problèmes de communication réseau

## 📚 Table des Matières

- [Concepts Fondamentaux](#-concepts-fondamentaux)
- [Adressage IP](#-adressage-ip)
- [Masques de Sous-réseau](#-masques-de-sous-réseau)
- [Équipements Réseau](#️-équipements-réseau)
- [Tables de Routage](#-tables-de-routage)
- [Méthodologie](#️-méthodologie)
- [Outils de Référence](#-outils-de-référence)
- [Exemples Pratiques](#-exemples-pratiques)

## 🔧 Concepts Fondamentaux

### Définitions Essentielles

**LAN (Local Area Network)**
- Réseau local où plusieurs appareils communiquent dans une zone limitée
- Exemple : réseau domestique, réseau d'entreprise

**IP (Internet Protocol)**
- Adresse unique identifiant un appareil sur le réseau
- Format IPv4 : `XXX.XXX.XXX.XXX` (4 octets de 0 à 255)
- Permet aux appareils de communiquer entre eux

**Subnet (Sous-réseau)**
- Division logique d'un réseau plus large
- Défini par une adresse réseau + masque de sous-réseau
- Détermine quels appareils peuvent communiquer directement

## 🌐 Adressage IP

### Format IPv4
```
192.168.1.10/24
├─ Adresse IP : 192.168.1.10
└─ Masque CIDR : /24 (255.255.255.0)
```

### Plages d'Adresses Privées
| Plage | Notation CIDR | Usage |
|-------|---------------|-------|
| `10.0.0.0 - 10.255.255.255` | `10.0.0.0/8` | Grandes entreprises |
| `172.16.0.0 - 172.31.255.255` | `172.16.0.0/12` | Réseaux moyens |
| `192.168.0.0 - 192.168.255.255` | `192.168.0.0/16` | Réseaux domestiques |

### Adresses Réservées
Dans chaque sous-réseau :
- **Adresse réseau** : Première IP (ex: `192.168.1.0`)
- **Adresse broadcast** : Dernière IP (ex: `192.168.1.255`)
- **Plage utilisable** : Entre les deux (ex: `192.168.1.1` à `192.168.1.254`)

## 🎭 Masques de Sous-réseau

### Tableau de Référence CIDR

| CIDR | Masque Décimal | Hôtes Utilisables | Incrément | Usage Typique |
|------|----------------|-------------------|-----------|---------------|
| /30 | 255.255.255.252 | 2 | 4 | Liaison point-à-point |
| /29 | 255.255.255.248 | 6 | 8 | Très petit réseau |
| /28 | 255.255.255.240 | 14 | 16 | Petit bureau |
| /27 | 255.255.255.224 | 30 | 32 | Bureau moyen |
| /26 | 255.255.255.192 | 62 | 64 | Grand bureau |
| /25 | 255.255.255.128 | 126 | 128 | Division en 2 |
| /24 | 255.255.255.0 | 254 | 256 | Réseau standard |

### Calcul Rapide des Sous-réseaux
1. **Incrément = 256 - dernier octet du masque**
2. **Sous-réseaux = multiples de l'incrément**

**Exemple avec /26 (255.255.255.192) :**
- Incrément : 256 - 192 = 64
- Sous-réseaux : 0, 64, 128, 192
- Plages : 0-63, 64-127, 128-191, 192-255

## 🖥️ Équipements Réseau

### Switch
- **Fonction** : Connecte plusieurs appareils dans un même réseau
- **Rôle** : Distribue les données entre les appareils du LAN
- **Caractéristique** : Fonctionne au niveau 2 (liaison de données)

### Router (Routeur)
- **Fonction** : Connecte différents réseaux entre eux
- **Rôle** : Achemine les données entre réseaux distincts
- **Caractéristique** : Peut avoir plusieurs interfaces avec des IP différentes

### Gateway (Passerelle)
- **Fonction** : Point d'entrée/sortie d'un réseau
- **Rôle** : Souvent le même appareil que le routeur
- **Usage** : Route par défaut pour sortir du réseau local

## 📋 Tables de Routage

### Structure
```
Destination     | Masque          | Next Hop (Passerelle)
0.0.0.0         | 0.0.0.0         | 192.168.1.1
192.168.2.0     | 255.255.255.0   | 10.0.0.1
```

### Éléments Clés
- **Destination** : Réseau cible (ou `default`/`0.0.0.0/0` pour route par défaut)
- **Next Hop** : Adresse IP du prochain routeur vers la destination
- **Interface** : Port de sortie du routeur

## 🛠️ Méthodologie

### Stratégie "Clean Slate"
1. **Effacer tout** : Supprimez toutes les configurations modifiables
2. **Vue propre** : Commencez avec un environnement clair
3. **Travailler à rebours** : Utilisez les valeurs données comme références
4. **Un objectif à la fois** : Traitez chaque goal séparément
5. **Vérifications fréquentes** : Testez après chaque modification

### Étapes de Configuration
1. **Analyser la topologie** : Identifier tous les équipements et connexions
2. **Planifier l'adressage** : Choisir les plages IP et masques appropriés
3. **Configurer les interfaces** : Assigner les adresses IP
4. **Définir les routes** : Configurer les tables de routage
5. **Tester la connectivité** : Vérifier que tous les goals sont atteints

## 📊 Outils de Référence

### Règles de Validation
- **Même réseau** : Même masque de sous-réseau obligatoire
- **Communication inter-réseaux** : Routeur nécessaire
- **Pas de conflit** : Chaque IP unique dans son réseau
- **Plages valides** : Respecter les adresses utilisables

### Masques Binaires Valides
```
255 = 11111111    224 = 11100000
254 = 11111110    192 = 11000000  
252 = 11111100    128 = 10000000
248 = 11111000    0   = 00000000
240 = 11110000
```
**Règle** : Après un bit à 0, tous les suivants doivent être à 0

## 💡 Exemples Pratiques

### Configuration Basique
```
PC-A : 192.168.1.10/24
PC-B : 192.168.1.20/24
→ Communication directe possible (même réseau)
```

### Configuration avec Routeur
```
Réseau A : 192.168.1.0/24
Réseau B : 192.168.2.0/24
Routeur : 192.168.1.1 (interface A) + 192.168.2.1 (interface B)
→ Communication via routeur
```

### Table de Routage Type
```
PC dans 192.168.1.0/24 :
Destination : default
Next Hop : 192.168.1.1 (routeur)
```

## 🚨 Erreurs Courantes

### À Éviter
- ❌ Masques différents dans le même réseau
- ❌ Utilisation d'adresses réseau/broadcast
- ❌ Conflits d'adresses IP
- ❌ Routes manquantes ou incorrectes
- ❌ Next hop dans un réseau différent

### Bonnes Pratiques
- ✅ Vérifier la cohérence des masques
- ✅ Tester chaque modification

## 🎯 Conseils de Réussite

### Approche Méthodique
1. **Comprendre avant configurer** : Analysez toute la topologie
2. **Simplicité** : Utilisez des adresses logiques et séquentielles
3. **Cohérence** : Respectez les conventions d'adressage
4. **Patience** : Testez chaque étape avant de continuer

### Outils Mentaux
- **Tableau CIDR** : Mémorisez les masques courants
- **Calcul d'incrément** : 256 - dernier octet du masque
- **Règle du même réseau** : Même masque = communication directe possible
- **Route par défaut** : 0.0.0.0/0 ou "default"

---

## 🎮 Solutions des Niveaux

### Niveau 1 - Configuration Basique
**Objectif :** Configurer deux réseaux simples
```json
{
  "A1": {"ip": "104.99.23.11"},
  "D1": {"ip": "211.191.115.76"}
}
```
**Explication :** Deux réseaux séparés avec masques /24 et /16. Assigner des IPs dans les plages valides.

### Niveau 2 - Masques Variables
**Objectif :** Configurer des masques de sous-réseau
```json
{
  "A1": {"ip": "192.168.57.221"},
  "B1": {"mask": "255.255.255.224"},
  "C1": {"ip": "192.168.57.254"},
  "D1": {"ip": "192.168.57.253"}
}
```
**Explication :** Utilisation de /27 pour créer des sous-réseaux plus petits.

### Niveau 3 - Switch
**Objectif :** Configuration avec switch
```json
{
  "A1": {"mask": "255.255.255.128"},
  "B1": {"ip": "104.198.187.124", "mask": "255.255.255.128"},
  "C1": {"ip": "104.198.187.123"}
}
```
**Explication :** Trois appareils connectés via switch avec masque /25.

### Niveau 4 - Routeur Simple
**Objectif :** Premier routeur
```json
{
  "A1": {"mask": "255.255.255.240"},
  "B1": {"ip": "67.52.110.133", "mask": "255.255.255.240"},
  "R1": {"ip": "67.52.110.134", "mask": "255.255.255.240"}
}
```
**Explication :** Configuration d'un routeur avec masque /28.

### Niveau 5 - Tables de Routage
**Objectif :** Première table de routage
```json
{
  "routes": {
    "Ar1": {"route": "default", "gate": "80.103.79.126"},
    "Br1": {"gate": "163.243.53.254"}
  },
  "ifs": {
    "A1": {"ip": "80.103.79.125", "mask": "255.255.255.128"},
    "B1": {"ip": "163.243.53.253", "mask": "255.255.192.0"}
  }
}
```
**Explication :** Introduction des routes par défaut.

### Niveau 6 - Internet
**Objectif :** Connexion Internet
```json
{
  "routes": {
    "Ar1": {"route": "0.0.0.0/0", "gate": "29.65.6.226"},
    "Ir1": {"route": "29.65.6.128/25"}
  },
  "ifs": {
    "A1": {"mask": "255.255.255.128"},
    "R1": {"ip": "29.65.6.226"}
  }
}
```
**Explication :** Routage vers Internet avec routes spécifiques.

### Niveau 7 - Topologie Complexe
**Objectif :** Plusieurs routeurs
```json
{
  "routes": {
    "Ar1": {"route": "0.0.0.0/0", "gate": "100.198.14.1"},
    "Cr1": {"route": "0.0.0.0/0", "gate": "100.198.14.18"}
  },
  "ifs": {
    "A1": {"ip": "100.198.14.2", "mask": "255.255.255.240"},
    "C1": {"ip": "100.198.14.17", "mask": "255.255.255.240"}
  }
}
```
**Explication :** Réseau avec deux routeurs interconnectés.

### Niveau 8 - Routage Avancé
**Objectif :** Routes spécifiques
```json
{
  "routes": {
    "R1r2": {"route": "141.195.172.0/27", "gate": "141.195.172.61"}
  },
  "ifs": {
    "C1": {"ip": "141.195.172.18", "mask": "255.255.255.252"},
    "R21": {"ip": "141.195.172.61", "mask": "255.255.255.252"}
  }
}
```
**Explication :** Utilisation de /30 pour liaisons point-à-point.

### Niveau 9 - Réseau Complexe
**Objectif :** Multiples sous-réseaux
```json
{
  "routes": {
    "R1r1": {"route": "9.0.0.252/30", "gate": "41.243.18.253"},
    "R1r2": {"route": "63.239.64.0/18", "gate": "41.243.18.253"}
  },
  "ifs": {
    "A1": {"ip": "121.198.129.2", "mask": "255.255.255.128"},
    "D1": {"ip": "63.239.100.38", "mask": "/18"}
  }
}
```
**Explication :** Gestion de plusieurs réseaux avec routage complexe.

### Niveau 10 - Défi Final
**Objectif :** Configuration complète
```json
{
  "routes": {
    "R1r1": {"route": "150.152.40.192/30"},
    "Ir1": {"route": "150.152.40.0/24"}
  },
  "ifs": {
    "H21": {"ip": "150.152.40.3", "mask": "255.255.255.128"},
    "H31": {"ip": "150.152.40.194", "mask": "255.255.255.252"}
  }
}
```
**Explication :** Synthèse de tous les concepts appris.

## 📖 Ressources Complémentaires

- [Vidéo explicative recommandée](https://youtu.be/HQUw0CfQWAM)
- [Calculateur de sous-réseaux en ligne](https://www.subnet-calculator.com/)
- [RFC 791 - Internet Protocol](https://tools.ietf.org/html/rfc791)

---

> [!TIP]
> **Conseil final** : NetPractice est un exercice de logique réseau. Maîtrisez les bases (IP, masques, routage) et appliquez une méthode systématique. La pratique régulière est la clé du succès !

> [!NOTE]
> Si ce guide vous a été utile \
> n'hésitez pas à laisser une ⭐️ pour soutenir le projet !