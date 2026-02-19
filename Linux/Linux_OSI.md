# 🐧 Maîtriser Linux : Le Guide Réseau (Modèle OSI)

Bienvenue dans le terminal ! Ici, pas de souris, tout se joue au clavier. ⌨️ Pour dépanner une machine Linux, on suit l'ordre logique des couches OSI.

---

## 🛠️ Diagnostic par Couche (Le Cheat Sheet)



### 🟦 Couche 1 & 2 : Physique et Liaison
*Le courant passe-t-il ? Ma carte est-elle reconnue ?*

| Objectif | Commande | Explication |
| :--- | :--- | :--- |
| **Interfaces** | `ip link show` | Liste toutes les cartes réseau (eth0, wlan0...). |
| **État du lien** | `ethtool eth0` | Vérifie si le câble est détecté (Speed, Duplex). |
| **Voisinage** | `ip neigh` | Affiche la table ARP (les adresses MAC autour de toi). |

---

### 🟩 Couche 3 : Réseau (IP & Routage)
*Suis-je visible sur le réseau et puis-je sortir ?*

| Objectif | Commande | Explication |
| :--- | :--- | :--- |
| **Adresse IP** | `ip addr` | Affiche ton adresse IP actuelle. |
| **Passerelle** | `ip route` | Vérifie la "default gateway" (ta sortie internet). |
| **Test simple** | `ping -c 4 8.8.8.8` | Teste la connectivité vers Google. |
| **Tracé** | `mtr google.com` | Un mix entre ping et traceroute (génial pour le débug). |

---

### 🟧 Couche 4 : Transport (Ports & Sockets)
*Le service est-il à l'écoute sur le bon port ?*

| Objectif | Commande | Explication |
| :--- | :--- | :--- |
| **Ports ouverts** | `ss -tulpn` | Liste les ports TCP/UDP en écoute et les processus. |
| **Scanner port** | `nc -zv <ip> 80` | Vérifie si le port 80 est ouvert sur une cible. |

---

### 🟪 Couches Supérieures (Application)
*Le service répond-il réellement ?*

* **DNS :** `dig google.com` ou `nslookup google.com` (Vérifie la résolution de noms).
* **Web :** `curl -I https://github.com` (Affiche les en-têtes HTTP).
* **Logs :** `journalctl -u ssh` (Voir les erreurs du service SSH).

---

## 💡 Astuce de survie Linux
Si une commande ne fonctionne pas, ajoute souvent `sudo` devant (ex: `sudo ethtool eth1`) pour l'exécuter avec les droits d'administrateur.

> **Note :** La plupart de ces commandes font partie du paquet `iproute2`. Si `ifconfig` ne marche pas, c'est normal, il est obsolète. Utilise `ip` !

---

[⬅️ Retour à l'accueil](./README.md) | [💻 Section Windows](./Windows.md)
