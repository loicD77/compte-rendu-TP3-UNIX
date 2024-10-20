# [ LP LPW 2024 ] compte rendu TP3 UNIX :
DARRAS Loïc L3 PRO PROJET WEB ET MOBILE

# Présentation/Introduction du travail (avant la table des matières et les explications)



* Ici ce troisième tp recouvre l'écriture de divers scripts dont :
   * analyse.sh
   * concat.sh
   * test-fichier.sh
   * listedir.sh
   * users.sh
   * check-user.sh
   * create-user.sh
   * note.sh



![pingouin-linux-shell](./img/pingouin-linux-shell.png "pingouin-linux-shell")



## Table des Matières


1. [Secure Shell : SSH](#i-secure-shell--ssh)
   - [1.1 Connexion SSH root et configuration](#11-connexion-ssh-root-et-configuration)
   - [1.2 Authentification par clé / Génération de clés](#12-authentification-par-clé--génération-de-clés)
   - [1.3 Authentification par clé / Connexion serveur](#13-authentification-par-clé--connexion-serveur)
   - [1.4 Authentification par clé depuis la machine hôte](#14-authentification-par-clé-depuis-la-machine-hôte)
   - [1.5 Sécurisation de l'accès SSH](#15-sécurisation-de-laccès-ssh)
2. [Processus](#ii--processus)
    - [2.1 Étude des processus UNIX](#21-exercice--etude-des-processus-unix)
      - [2.1.1 Affichage des processus](#211-affichage-des-processus)
      - [2.1.2 PPID et processus parent](#212-ppid-et-processus-parent)
      - [2.1.3 Commande `pstree`](#213-commande-pstree)
      - [2.1.4 Utilisation de la commande `top` et `htop`](#214-utilisation-de-la-commande-top-et-htop)
3. [Arrêt d'un processus](#iii-arrêt-dun-processus)
4. [Les tubes](#iv-les-tubes)
5. [Journal système rsyslog](#v-journal-système-rsyslog)
   


# Présentation/Introduction du travail (avant la table des matières et les explications)


## I) analyse.sh

Voici mon script:

```bash 
#!/bin/bash

# Afficher le message de bienvenue avec le nombre de paramètres
echo "Bonjour, vous avez rentré $# paramètres."

# Afficher le nom du script
echo "Le nom du script est $(basename $0)"

# Vérifier si au moins 3 paramètres ont été fournis
if [ $# -ge 3 ]; then
  echo "Le 3ème paramètre est $3"
else
  echo "Le 3ème paramètre n'a pas été fourni"
fi

# Afficher la liste des paramètres
echo "Voici la liste des paramètres : $@"
```







* Je l'ai ouvert et créé en utilisant **nano analyse.sh**

* Je l'ai exécuté en utilisant  **sh analyse.sh param1 param2 param3**

```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# sh analyse.sh param1 param2 param3
Bonjour, vous avez rentré 3 paramètres.
Le nom du script est analyse.sh
Le 3ème paramètre est param3
Voici la liste des paramètres : param1 param2 param3
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```

* Cela me confirme bien que j'ai rentré **trois paramètres**.
* Le nom du script est bien **"analyse.sh"**
* Mon troisième paramètre est bien **param3**
* Cela m'affiche correctement la liste des différents paramètres : **param1 param2 param3**

