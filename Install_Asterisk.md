# Tutoriel d'installation d'Asterisk sur Ubuntu 24

## Objectif

Dans ce tutoriel, vous apprendrez à installer **Asterisk** sur un serveur **Ubuntu 24**. Asterisk est un logiciel de **téléphonie IP** permettant de créer des systèmes de communication vocale.

### Prérequis
- **Ubuntu 24 Server** installé (ou toute version d'Ubuntu compatible).
- Accès à un terminal ou à la ligne de commande avec **droits sudo**.

---

## Étapes d'installation

### 1. **Mise à jour du système**

Avant d'installer Asterisk, il est recommandé de mettre à jour votre système pour vous assurer que vous disposez des derniers paquets.

Exécutez les commandes suivantes pour mettre à jour les dépôts et installer les dernières versions des paquets :

```bash
sudo apt-get update
sudo apt-get upgrade -y
```

---

### 2. **Installation des dépendances requises**

Asterisk a besoin de plusieurs paquets et bibliothèques pour fonctionner correctement. Exécutez cette commande pour installer toutes les dépendances nécessaires :

```bash
sudo apt-get install -y bison wget openssl libssl-dev libasound2-dev libc6-dev libxml2-dev libsqlite3-dev libnewt-dev libncurses-dev zlib1g-dev gcc g++ make perl uuid-dev git subversion unixodbc-dev unixodbc autoconf libedit-dev libsrtp2-dev libspandsp-dev bzip2 libcurl4-openssl-dev libopus-dev
```

- Cette commande installe des outils de compilation, des bibliothèques nécessaires pour la gestion des codecs audio et vidéo, ainsi que des dépendances pour la sécurité et la gestion des connexions réseau.

---

### 3. **Téléchargement du code source d'Asterisk**

Maintenant que les dépendances sont installées, il est temps de télécharger le code source d'Asterisk.

1. Allez dans le répertoire `/usr/src`, qui est habituellement utilisé pour télécharger et stocker les sources de logiciels :

    ```bash
    cd /usr/src
    ```

2. Téléchargez la dernière version stable d'Asterisk (remplacez le lien si nécessaire avec la dernière version disponible) :

    ```bash
    sudo wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-22-current.tar.gz
    ```

3. Décompressez l'archive téléchargée :

    ```bash
    sudo tar -xzvf asterisk-22-current.tar.gz
    ```

---

### 4. **Configuration de Asterisk**

Une fois le code source téléchargé et décompressé, vous devez configurer Asterisk pour préparer la compilation.

1. Changez de répertoire pour entrer dans le dossier Asterisk :

    ```bash
    cd asterisk-22-*
    ```

2. Configurez Asterisk en exécutant le script de configuration avec l'option `--with-jansson-bundled` (nécessaire pour Asterisk 22) :

    ```bash
    sudo ./configure --with-jansson-bundled
    ```

Ce processus vérifie votre système pour s'assurer que toutes les dépendances sont disponibles et prépare Asterisk pour la compilation.

---

### 5. **Compilation et installation d'Asterisk**

Une fois la configuration terminée, vous pouvez compiler Asterisk et l'installer.

1. Compilez Asterisk avec la commande suivante :

    ```bash
    sudo make
    ```

2. Installez Asterisk avec la commande suivante :

    ```bash
    sudo make install
    ```

3. Installez les fichiers de configuration par défaut et les exemples :

    ```bash
    sudo make config
    sudo make samples
    ```

Cela installera Asterisk, les fichiers de configuration par défaut et les exemples utiles pour commencer à utiliser le système.

---

### 6. **Démarrer Asterisk**

Asterisk est maintenant installé, et vous pouvez le démarrer en mode **foreground** pour vérifier qu'il fonctionne correctement.

1. Démarrez Asterisk en mode "foreground" avec un niveau de log détaillé :

    ```bash
    sudo asterisk -vvvvvvvvgc
    ```

Cela démarre Asterisk et vous permet de voir les logs directement dans le terminal. Vous devriez voir un message indiquant que Asterisk est en fonctionnement.

---

### 7. **Arrêter Asterisk**

Si vous avez démarré Asterisk en mode foreground et souhaitez l'arrêter, utilisez la commande suivante dans la console Asterisk :

```bash
core stop now
```

---

### 8. **Démarrer Asterisk en arrière-plan**

Si vous voulez démarrer Asterisk en arrière-plan, vous pouvez simplement utiliser :

```bash
sudo asterisk
```

Cela démarre Asterisk comme un service en arrière-plan, vous permettant de libérer votre terminal.

---

### 9. **Se connecter à la console Asterisk**

Si vous avez démarré Asterisk en arrière-plan, vous pouvez vous connecter à la console Asterisk pour l’administrer.

Utilisez la commande suivante pour vous connecter à la console Asterisk :

```bash
sudo asterisk -r
```

Cela vous permettra de voir les logs en temps réel et d’exécuter des commandes dans l'interface de ligne de commande Asterisk.

---

### 10. **Utilisation de systemd (méthode recommandée)**

Pour une gestion plus simple d'Asterisk, il est préférable d'utiliser **systemd**, le gestionnaire de services de Linux. Voici les commandes à utiliser :

1. Pour démarrer Asterisk avec **systemd** :

    ```bash
    sudo systemctl start asterisk
    ```

2. Pour vérifier si Asterisk fonctionne correctement avec **systemd** :

    ```bash
    sudo systemctl status asterisk
    ```

Cela vous permet de gérer Asterisk comme un service standard sur votre serveur.

---

## Conclusion

Vous avez maintenant installé Asterisk sur votre serveur Ubuntu 24 ! Vous pouvez commencer à configurer des extensions, des appels vocaux, et à explorer toutes les fonctionnalités puissantes qu'offre Asterisk. 

Pour aller plus loin, vous pouvez consulter la documentation officielle d'Asterisk pour configurer des scénarios de téléphonie, ajouter des utilisateurs, et interagir avec d'autres systèmes de téléphonie.

---

### Remarques

- Si vous rencontrez des problèmes lors de l'installation, assurez-vous que toutes les dépendances sont installées et que votre système est à jour.
- **Systemd** est la méthode recommandée pour gérer Asterisk, car elle permet de s'assurer qu'Asterisk redémarre automatiquement en cas de redémarrage du serveur.

--- 

Ce tutoriel vous a guidé à travers l'installation complète d'Asterisk sur Ubuntu 24. Vous pouvez maintenant commencer à explorer et configurer votre serveur Asterisk selon vos besoins !
