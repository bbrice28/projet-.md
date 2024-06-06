# projet-.md

  # Installer john the ripper sur MacOS

  ## 1-Installer homebrew dans le terminal qui est un gestionnaire de paquet macOS

Commande: /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh) "

- /bin/bash -c :  permet de lancer un nouveau processus dans le shell bash
-  $(curl -fsSL : permet d’utiliser « curl » pour télécharger un fichier, et les options « -fssl » qui permettent de suivre les redirections, utiliser le mode silencieux, et afficher les barres de progression.
- https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh) : l’adresse du fichier à télécharger (ici john the ripper).

  <img width="987" alt="Capture d’écran 2024-05-28 à 14 07 19" src="https://github.com/bbrice28/projet-.md/assets/169658100/cb506380-1f0a-4ea8-81a7-40237724b26b">






## 2- Installer avec la commande brew john the ripper

Commande: brew install John

<img width="419" alt="Capture d’écran 2024-05-28 à 14 08 01" src="https://github.com/bbrice28/projet-.md/assets/169658100/2d1eebd1-72fe-4395-85bf-f201ec6feb15">

- brew : la commande qui permet d’interagir avec homebrew
- Install: la sous commande de brew pour installer le package
- John : le package à installer







## 3- Vérifier l’installation de john the ripper

Commande: john 

- john: le nom de l’executable 

 
 
 # UTILISATION DE JOHN SUR MACOS

## 1- ÉTAPES PRÉALABLES:
Pour pouvoir effectuer l’attaque du hachage par dictionnaire, il faut nous faut, dans ce cas, les fichiers Seclists. Nous y utiliserons le fichier rockyou.txt.

Commande: sudo snap install seclists 

## 2- CRACKING DES HASHAGES DE BASE

Il y a plusieurs façons d'utiliser John l'Éventreur pour craquer des hachages simples, nous allons
en parcourir quelques-uns, avant de passer à en craquer nous-mêmes.

L’objectif est de décrypter le Hash suivant : 1A732667F3917C0F4AA98BB13011B9090C6F8065

Lancer John the Ripper sans spécifier le format john --wordlist=/snap/seclists/current/
Passwords/rockyou.txt hashes.txt

Voir les résultats john --show hashes.txt

## 3- PROBLÈMES SURVENUS LORS DE LA MANIPULATION:

Nous avons rencontré un premier message d’erreur, qui est le suivant:

<img width="839" alt="Capture d’écran 2024-05-30 à 14 23 00" src="https://github.com/bbrice28/projet-.md/assets/169658100/e0aec887-ddac-49ef-80c5-2542a50d6da9">

Ce qui, après recherches, signifie qu’il faut spécifier le format du hachage.

Il a donc fallu ajouter l’outil « hashid » qui permet en effectuant la commande suivante de récupérer les différentes méthodes de hashing possiblement utilisées: pip3 install hashid

Nous avons donc pu récupérer la liste suivante de formats:

<img width="534" alt="Capture d’écran 2024-05-30 à 15 08 28" src="https://github.com/bbrice28/projet-.md/assets/169658100/c9828451-6a2e-405a-b400-cdb1a38d3e6d">

Suite à ces résultats, nous avons donc pu retaper notre commande en spécifiant le format, mais avons reçu un nouveau message d’erreur: 

<img width="292" alt="Capture d’écran 2024-05-30 à 15 11 48" src="https://github.com/bbrice28/projet-.md/assets/169658100/d8beef1a-3608-412b-9c89-8536e25bf631">


Après des recherches approfondies sur le site de john the ripper, ainsi que sur des blogs. Aucune solution n’a été trouvée. Mais une piste probable est que le Mac autorise l’installation de John the Ripper dans son terminal, sans autoriser les dépendances nécessaires à sa bonne exécution.

En conclusion, par soucis d’efficacité, nous n’utiliserons pas John the Ripper sous macOS.


# Récupération d'un mot de passe windows server

## 1- Récupération des fichiers de mot de passe hachés:

Dans un premier temps il faut rassembler nos ressources, à savoir, les mots de passes hachés.
Pour les systèmes windows, ils se trouvent dans les fichiers SAM et SYSTEMES.

Nous allons donc taper les commandes suivantes:

- copy C:\Windows\System32\config\SAM E:\
- copy C:\Windows\System32\config\SYSTEM E:\

## 2- Erreurs et points de blocage

Le message d’erreur suivant apparait:  le processus ne peut pas acceder au fichier car il est en cours d’utilisation.
Il nous informe donc que Sam et System sont en cours d’utilisation et qu’ils ne peuvent pas être copiés.

Pour contourner le problème nous avons donc tenté d’utiliser l’outil de sauvegarde « shadow copy ».
Ce dernier consiste à récupérer les sauvegardes automatiques de windows.

Mais même avec les droits utilisateurs, le même message d’erreur s’est affiché.

Après recherches, aucune solution n’a permis d’avoir une autre sortie que ce message d’erreur. 

En conclusion, dans un soucis d’efficacité, je ne vais pas utiliser John the Ripper dans le but de récupérer les mots de passe d’un serveur Windows.


