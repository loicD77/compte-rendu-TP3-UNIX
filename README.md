# [ LP LPW 2024 ] compte rendu TP3 UNIX :
DARRAS Loïc L3 PRO PROJET WEB ET MOBILE

# Présentation/Introduction du travail (avant la table des matières et les explications)



* Ici ce troisième tp recouvre l'écriture de divers scripts bash dont :
   * analyse.sh
   * concat.sh
   * test-fichier.sh
   * listedir.sh
   * users.sh
   * check-user.sh
   * create-user.sh
   * note.sh



![pingouin-linux-shell](./img/pingouin-linux-shell.png "pingouin-linux-shell")




# Table des Matières


1. [Liste des scripts](#liste-des-scripts)
   - [1.1 analyse.sh](#i-analysesh)
   - [1.2 Concat.sh](#ii-concatsh)
   - [1.3 Test-fichier.sh](#iii-test-fichiersh)
   - [1.4 Listedir.sh](#iv-listedirsh)
   - [1.5 User.sh](#v-usersh)
   - [1.6 Create-user.sh](#vi-create-usersh)
   - [1.7 Check-user.sh](#vii-check-usersh)
   - [1.8 Note.sh](#viii-notesh)

2. [Exercice : lecture au clavier](#exercice--lecture-au-clavier)
   - [2.1 La commande bash read](#i-la-commande-bash-read)
   - [2.2 La commande file](#ii-la-commande-file)
   - [2.3 La commande more](#iii-la-commande-more)
   - [2.4 Détails sur more](#iv-détails-sur-more)
   - [2.5 Écrire un script](#v-ecrire-un-script)


3. [Conclusion](#conclusion)

# Liste des scripts

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

### Test du script : 

```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./analyse.sh param1 param2 param3
Bonjour, vous avez rentré 3 paramètres.
Le nom du script est analyse.sh
Le 3ème paramètre est param3
Voici la liste des paramètres : param1 param2 param3
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./analyse.sh param1 param2 param3 param4
Bonjour, vous avez rentré 4 paramètres.
Le nom du script est analyse.sh
Le 3ème paramètre est param3
Voici la liste des paramètres : param1 param2 param3 param4
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./analyse.sh param1 param2 param3 param4 param5 paramparam lastparam
Bonjour, vous avez rentré 7 paramètres.
Le nom du script est analyse.sh
Le 3ème paramètre est param3
Voici la liste des paramètres : param1 param2 param3 param4 param5 paramparam lastparam
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```

###  Afficher le nombre de paramètres fournis :

* echo : Affiche du texte à l'écran. (On peut aussi utiliser **printf**)
* $# : Représente le nombre de paramètres (arguments) fournis au script. Si vous exécutez le script avec par exemple ./script.sh arg1 arg2 arg3, alors ceci sera égal à 3.

### Afficher le nom du script :

* **basename $0**: La commande basename prend en entrée un chemin et renvoie le nom de fichier sans le chemin complet. Ici, $0 représente le nom du script en cours d'exécution.

* Si le script s'appelle script.sh, la commande basename $0 affichera juste script.sh.

###  Vérifier si au moins 3 paramètres ont été fournis

* if [ $# -ge 3 ] : Cette condition vérifie si le nombre de paramètres (est supérieur ou égal à 3 (-ge signifie "greater than or equal", c'est-à-dire "supérieur ou égal").
* echo "Le 3ème paramètre est $3" : Si 3 paramètres ou plus ont été fournis, cette ligne affiche le troisième paramètre ($3).
* else : Si moins de 3 paramètres sont fournis, il affiche un message indiquant que le troisième paramètre n'a pas été fourni.

## Afficher la liste des paramètres
* $@ : Représente la liste de tous les paramètres passés au script. Chacun des paramètres est traité comme une chaîne distincte.
* Résultat attendu : Affiche la liste de tous les paramètres fournis. Par exemple, si vous exécutez ./script.sh arg1 arg2 arg3, la sortie sera :

```bash 
Voici la liste des paramètres : arg1 arg2 arg3
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


## II) concat.sh

Voici mon script :

```bash 
GNU nano 6.2                                            concat.sh                                                     #!/bin/bash


[ $# -eq 2 ] || { echo "Il faut 2 paramètres."; exit 1; }
echo "Concaténation : $1$2"
```


### Test du script

```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./concat.sh mot1 mot2
Concaténation : mot1mot2
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./concat.sh mot1 mot2 ff
Il faut 2 paramètres.
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#

```


### Shebang (#!/bin/bash)


* Le shebang est donc une ligne spéciale qui montre au système quel type interpréteur utiliser pour exécuter le script concerné. 
* Dans mon contexte, le script  qui doit être exécuté avec Bash est indiqué, ceci est interpréteur de commandes populaire sur les systèmes UNIX et Linux.




### Vérification du nombre de paramètres ([ $# -eq 2 ] || { echo "Il faut 2 paramètres."; exit 1; })
* **$#** :   C'est une variable particulière qui a le nombre d'arguments passés au script. Par exemple, si j'exécute **./concat.sh arg1 arg2** , alors ici cette variable sera égal à 2.
* **[ $# -eq 2 ]** : Ici ma condition vérifie donc si le nombre d'arguments est **égal à 2**. En effet la syntaxe -eq signifie "égal à".
* **||** : C'est un opérateur logique "OU". Si la condition à gauche ($# -eq 2) est fausse, alors la commande à droite sera exécutée.
* **{ echo "Il faut 2 paramètres."; exit 1; }** : Si le nombre d'arguments n'est pas égal à 2, ce bloc de code sera exécuté :
* **echo "Il faut 2 paramètres."** : Ceci affiche un message d'erreur à l'écran, il dit que le script nécessite 2 paramètres.
* **exit 1** : Quitte le script avec un code de sortie de 1, indiquant une erreur. Par convention, un code de sortie de 0 signifie succès, tandis qu'un code de sortie différent de 0 indique une erreur.


### Affichage de la concaténation (echo "Concaténation : $1$2")


* echo : la sortie standard reflète un message (souvent le terminal).
* "Concaténation : $1$2" : Concatène (groissièrement rassembler dans l'ordre indiqué) les chaînes de caractères
* $1 : Représente le premier argument passé au script.
* $2 : C'est donc ici le deuxième argument passé au script.
* En concaténant $1 et $2 (sans espace), le script affichera la concaténation des deux arguments. Par exemple, si vous exécutez ./concat.sh Hello World, le script affichera Concaténation : HelloWorld.


### Résumé du fonctionnement du script :

* Le script vérifie que j'ai mis 2 arguments. Sinon j'ai  un message d'erreur et un code d'erreur.
* Donc si  mes deux seules arguments sont présents, il concatène les deux chaînes contenues dans ces derniers  et affiche le résultat.



## III) test-fichier.sh

Voici le script de ce dernier : 

```bash 

  GNU nano 6.2                                         test-fichier.sh                                                  #!/bin/bash
[ -e "$1" ] || { echo "$1 n'existe pas."; exit 1; }
[ -f "$1" ] && echo "$1 est un fichier." || [ -d "$1" ] && echo "$1 est un répertoire."
[ -r "$1" ] && echo "Lisible."
[ -w "$1" ] && echo "Modifiable."
[ -x "$1" ] && echo "Exécutable."



```


### Test du script 


```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./test-fichier.sh /etc/passwd
/etc/passwd est un fichier.
/etc/passwd est un répertoire.
Lisible.
Modifiable.
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#


```




 ### Vérification de l'existence du fichier ou du répertoire

 * $1 : Représente le premier argument passé au script, qui devrait être un chemin vers un fichier ou un répertoire.
* [ -e "$1" ] : Cette condition vérifie si l'argument fourni ($1) existe. L'option -e teste l'existence d'un fichier ou d'un répertoire.
* || : Opérateur "OU" logique. Si la condition à gauche est fausse (si le fichier n'existe pas), la commande à droite sera exécutée.
* { echo "$1 n'existe pas."; exit 1; } : Si le fichier ou répertoire n'existe pas, le script affiche un message d'erreur et termine immédiatement avec un code de sortie 1 (indiquant une erreur).

### Vérification si c'est un fichier ou un répertoire

* [ -f "$1" ] : Vérifie si l'argument est un fichier régulier. L'option -f teste si c'est un fichier.
* && : Opérateur "ET" logique. Si la condition à gauche est vraie (si c'est un fichier), alors la commande à droite sera exécutée, qui est echo "$1 est un fichier.".
* || : Si la condition précédente (-f) est fausse (ce n'est pas un fichier), alors la commande après || est exécutée.
* [ -d "$1" ] : Vérifie si l'argument est un répertoire. L'option -d teste si c'est un répertoire.
* && : Si c'est un répertoire, il affiche un message indiquant cela.

### Vérification si le fichier est lisible

* [ -r "$1" ] : Vérifie si l'argument est lisible. L'option -r teste si le fichier ou le répertoire a les permissions de lecture.
* && : Si la condition est vraie, le message "Lisible." est affiché.

### Vérification si le fichier est modifiable

* [ -w "$1" ] : Vérifie si l'argument est modifiable (écriture possible). L'option -w teste les permissions d'écriture.
* && : Si la condition est vraie, le message "Modifiable." est affiché.


### Vérification si le fichier est exécutable

* [ -x "$1" ] : Vérifie si l'argument est exécutable. L'option -x teste si le fichier ou le répertoire a les permissions d'exécution.
* && : Si la condition est vraie, le message "Exécutable." est affiché


## IV) listedir.sh


* Voici le script de ce dernier :

```bash 


  GNU nano 6.2                                           listedir.sh                                                    #!/bin/bash

#!/bin/bash
echo "#### Fichiers dans $1 ####"; find "$1" -maxdepth 1 -type f
echo "#### Répertoires dans $1 ####"; find "$1" -maxdepth 1 -type d
```


Test du script :

```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./listedir.sh /etc
#### Fichiers dans /etc ####
/etc/ca-certificates.conf
/etc/protocols
/etc/netconfig
/etc/sudo.conf
/etc/hostname
/etc/ca-certificates.conf.dpkg-old
/etc/environment
/etc/gai.conf
/etc/.pwd.lock
/etc/xattr.conf
/etc/networks
/etc/issue
/etc/ethertypes
/etc/shadow-
/etc/passwd
/etc/subuid
/etc/passwd-
/etc/sudo_logsrvd.conf
/etc/libaudit.conf
/etc/group-
/etc/lsb-release
/etc/bindresvport.blacklist
/etc/rsyslog.conf
/etc/sudoers
/etc/sysctl.conf
/etc/inputrc
/etc/modules
/etc/deluser.conf
/etc/services
/etc/e2scrub.conf
/etc/timezone
/etc/nftables.conf
/etc/ld.so.conf
/etc/gshadow-
/etc/issue.net
/etc/hosts.deny
/etc/manpath.config
/etc/login.defs
/etc/subgid
/etc/wsl.conf
/etc/host.conf
/etc/machine-id
/etc/magic
/etc/screenrc
/etc/fstab
/etc/logrotate.conf
/etc/nsswitch.conf
/etc/bash_completion
/etc/mime.types
/etc/shadow
/etc/fuse.conf
/etc/hosts.allow
/etc/hosts
/etc/adduser.conf
/etc/debian_version
/etc/crontab
/etc/rpc
/etc/group
/etc/zsh_command_not_found
/etc/bash.bashrc
/etc/ucf.conf
/etc/gshadow
/etc/hdparm.conf
/etc/profile
/etc/pam.conf
/etc/debconf.conf
/etc/mke2fs.conf
/etc/shells
/etc/ld.so.cache
/etc/sensors3.conf
/etc/wgetrc
/etc/nanorc
/etc/locale.gen
/etc/legal
/etc/magic.mime
/etc/locale.alias
#### Répertoires dans /etc ####
/etc
/etc/groff
/etc/update-manager
/etc/apt
/etc/depmod.d
/etc/cron.daily
/etc/binfmt.d
/etc/perl
/etc/ssh
/etc/gss
/etc/bash_completion.d
/etc/ld.so.conf.d
/etc/dbus-1
/etc/kernel
/etc/rc3.d
/etc/iproute2
/etc/pam.d
/etc/systemd
/etc/cron.d
/etc/sysctl.d
/etc/default
/etc/logrotate.d
/etc/console-setup
/etc/X11
/etc/cron.monthly
/etc/security
/etc/logcheck
/etc/init.d
/etc/apparmor.d
/etc/rc5.d
/etc/dpkg
/etc/ldap
/etc/alternatives
/etc/ubuntu-advantage
/etc/rc2.d
/etc/terminfo
/etc/rsyslog.d
/etc/rcS.d
/etc/cloud
/etc/PackageKit
/etc/dhcp
/etc/modules-load.d
/etc/rc6.d
/etc/modprobe.d
/etc/sensors.d
/etc/xdg
/etc/tmpfiles.d
/etc/udev
/etc/newt
/etc/glvnd
/etc/apport
/etc/dconf
/etc/ufw
/etc/sysstat
/etc/networkd-dispatcher
/etc/update-motd.d
/etc/apparmor
/etc/profile.d
/etc/rc0.d
/etc/environment.d
/etc/postgresql-common
/etc/sudoers.d
/etc/gtk-3.0
/etc/cron.hourly
/etc/cron.weekly
/etc/selinux
/etc/rc4.d
/etc/netplan
/etc/fonts
/etc/python3
/etc/polkit-1
/etc/opt
/etc/vim
/etc/postgresql
/etc/python3.10
/etc/ca-certificates
/etc/pm
/etc/skel
/etc/ssl
/etc/landscape
/etc/rc1.d
/etc/byobu
/etc/libnl-3
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#


```


### Afficher les fichiers dans le répertoire donné

* **echo "#### Fichiers dans $1 ####"** : Cette commande affiche une ligne de texte qui indique que la liste des fichiers dans le répertoire sera affichée. $1 représente le premier argument passé au script, qui est censé être le chemin d'un répertoire.


* Exemple : Si nous exécutons ./script.sh /chemin/vers/repertoire, cette ligne affichera


```bash 
 Fichiers dans /chemin/vers/repertoire ####:
```

* **find "$1" -maxdepth 1 -type f :**

  * **find :** Une commande qui permet de rechercher des fichiers et répertoires dans un chemin donné.
  * **"$1" :** C'est le répertoire dans lequel find va effectuer la recherche. Ici, il s'agit de l'argument passé en premier au script (c'est-à-dire le chemin fourni par l'utilisateur).
  * **-maxdepth 1 :** Cette option indique que find ne doit explorer que le répertoire courant, sans descendre dans les sous-répertoires. Si vous supprimiez cette option, find listerait aussi les fichiers des sous-répertoires.
  * **-type f :** Cette option spécifie que l'on veut uniquement les fichiers (et non les répertoires). Cela permet de filtrer les résultats pour ne montrer que les fichiers dans le répertoire.
  
  
  * Exemple de sortie : Si le répertoire /chemin/vers/repertoire contient des fichiers comme fichier1.txt et fichier2.doc, la sortie sera :

```bash 
#### Fichiers dans /chemin/vers/repertoire ####
/chemin/vers/repertoire/fichier1.txt
/chemin/vers/repertoire/fichier2.doc
```

### Afficher les répertoires dans le répertoire donné

* echo "#### Répertoires dans $1 ####" : Cette ligne affiche un message indiquant que la liste des répertoires sera affichée.

* Exemple : Si vous exécutez ./script.sh /chemin/vers/repertoire, cette ligne affichera :

```bash 
#### Répertoires dans /chemin/vers/repertoire ####
```

### find "$1" -maxdepth 1 -type d :

* -maxdepth 1 : Comme dans la commande précédente, cette option indique que find ne doit pas explorer les sous-répertoires, mais se limiter au répertoire spécifié.
* -type d : Cette option spécifie que l'on veut uniquement les répertoires (et non les fichiers).
Exemple de sortie : Si le répertoire /chemin/vers/repertoire contient deux sous-répertoires sous-repertoire1 et sous-repertoire2, la sortie sera :

```bash 
#### Répertoires dans /chemin/vers/repertoire ####
/chemin/vers/repertoire
/chemin/vers/repertoire/sous-repertoire1
/chemin/vers/repertoire/sous-repertoire2
```

## V) user.sh 

Utiliser for user in $(cat /etc/passwd) n'est pas idéal car cela ne respecte pas la structure des lignes du fichier, ce qui peut entraîner des erreurs. La méthode avec while et read est plus appropriée pour traiter des fichiers ligne par ligne tout en conservant les relations entre les champs.

* Voici le script de user.sh avec **cut**:  (user2.sh)

  ```bash
  #!/bin/bash

  # Lister les utilisateurs avec un UID supérieur à 100
  for user in $(cut -d: -f1,3 /etc/passwd); do
    username=$(echo $user | cut -d: -f1)
    uid=$(echo $user | cut -d: -f2)
    
    if [ "$uid" -gt 100 ]; then
        echo "$username"
    fi
  done
 

    ```

* Voici le script de user.sh avec **awk**: (user.sh)

```bash 
  GNU nano 6.2                                            users.sh                                                      #!/bin/bash
awk -F: '$3 > 100 {print $1}' /etc/passwd
```


* Test des scripts 
```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./users.sh
nobody
systemd-resolve
messagebus
systemd-timesync
syslog
_apt
uuidd
tcpdump
postgres
sshd
landscape
rootdutp
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./user2.sh
nobody
systemd-resolve
messagebus
systemd-timesync
syslog
_apt
uuidd
tcpdump
postgres
sshd
landscape
rootdutp
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#



```

### Explication avec cut

* Boucle for
 * for user in $(cut -d: -f1,3 /etc/passwd); do
Cette ligne commence une boucle for qui parcourt les utilisateurs extraits du fichier /etc/passwd.
* cut -d: -f1,3 extrait les champs 1 et 3 (nom d'utilisateur et UID) de chaque ligne du fichier /etc/passwd, en utilisant : comme délimiteur.
$(...) exécute la commande et remplace cette partie par sa sortie.
### Explication avec awk

### La commande awk
* awk est un utilitaire puissant utilisé pour la manipulation et l'extraction de données à partir de fichiers texte. Ici, il est utilisé pour traiter le fichier /etc/passwd, qui contient des informations sur les utilisateurs du système.
* -F: : Cette option indique à awk que le fichier /etc/passwd utilise : (deux-points) comme séparateur de champs. Chaque ligne du fichier /etc/passwd contient plusieurs champs séparés par des deux-points.
* $3 : Dans awk, les champs sont numérotés par $n, où n représente le numéro du champ.
* $1 représente le nom d'utilisateur.
* $3 représente l'UID (User ID) de l'utilisateur.
* $3 > 100 : Cette condition vérifie si l'UID de l'utilisateur est supérieur à 100. Sur de nombreux systèmes Linux, les UID inférieurs ou égaux à 100 (parfois 1000) sont réservés aux comptes système (comme root, daemon, etc.), tandis que les UID supérieurs sont utilisés pour les utilisateurs humains.
* {print $1} : Si la condition $3 > 100 est vraie, awk affiche le contenu du champ $1, qui correspond au nom d'utilisateur.


### Fichier /etc/passwd
* Le fichier /etc/passwd est un fichier texte qui contient des informations sur les comptes utilisateurs dans un système Linux. Chaque ligne du fichier correspond à un utilisateur et a cette structure :

```bash 
nom_utilisateur:x:UID:GID:description:home_directory:shell
```

* nom_utilisateur : Le nom d'utilisateur (champ $1).
* UID : L'ID utilisateur (champ $3).
* GID : L'ID de groupe.
* description : Description de l'utilisateur (parfois vide).
* home_directory : Le répertoire personnel de l'utilisateur.
* shell : Le shell par défaut de l'utilisateur (par exemple, /bin/bash).


## VI) create-user.sh

* Voici le script de create-user.sh :

```bash 
  #!/bin/bash

# Vérifier si l'utilisateur courant est root
if [ "$USER" != "root" ]; then
    echo "Ce script doit être exécuté en tant que root."
    exit 1
fi

# Demander des informations sur l'utilisateur
read -p "Entrez le login: " LOGIN
read -p "Entrez le nom: " NOM
read -p "Entrez le prénom: " PRENOM
read -p "Entrez l'UID (laisser vide pour utiliser le système): " USER_UID
read -p "Entrez le GID (laisser vide pour utiliser le système): " USER_GID
read -p "Entrez les commentaires: " COMMENTAIRES

# Vérifier si l'utilisateur existe déjà
if id "$LOGIN" &>/dev/null; then
   echo "L'utilisateur '$LOGIN' existe déjà."
    exit 1
fi

# Vérifier si le répertoire personnel existe déjà
HOME_DIR="/home/$LOGIN"
if [ -d "$HOME_DIR" ]; then
    echo "Le répertoire '$HOME_DIR' existe déjà."
    exit 1
fi

# Créer l'utilisateur avec les informations fournies
if [ -z "$USER_UID" ] && [ -z "$USER_GID" ]; then
    useradd -m -d "$HOME_DIR" -c "$NOM $PRENOM,$COMMENTAIRES" "$LOGIN"
else
    useradd -m -d "$HOME_DIR" -c "$NOM $PRENOM,$COMMENTAIRES" -u "${USER_UID:-$(id -u)}" -g "${USER_GID:-$(id -g)}" "$>fi

# Vérifier si la création de l'utilisateur a réussi
if [ $? -eq 0 ]; then
    echo "L'utilisateur '$LOGIN' a été créé avec succès."
else
    echo "Erreur lors de la création de l'utilisateur '$LOGIN'."
    exit 1
fi

# Créer le répertoire personnel (au cas où useradd ne l'a pas créé)
mkdir -p "$HOME_DIR"
chown "$LOGIN":"${USER_GID:-$(id -g)}" "$HOME_DIR"

echo "Le répertoire personnel '$HOME_DIR' a été créé."
```

* Test du tp :

```bash 
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./create-user2.sh
Entrez le login: JeanMarc
Entrez le nom: Marc
Entrez le prénom: Jean
Entrez l'UID (laisser vide pour utiliser le système):
Entrez le GID (laisser vide pour utiliser le système):
Entrez les commentaires: Compte de JM
L'utilisateur 'JeanMarc' a été créé avec succès.
Le répertoire personnel '/home/JeanMarc' a été créé.
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# grep JeanMarc /etc/passwd
JeanMarc:x:1005:1005:Marc Jean,Compte de JM:/home/JeanMarc:/bin/sh
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#

```

### Vérification des privilèges root

* **if [ "$USER" != "root" ]; then** : Vérifie si l'utilisateur courant n'est pas root. Le script doit être exécuté par un utilisateur ayant des privilèges administratifs pour pouvoir créer des utilisateurs.
* **echo** : Affiche un message d'erreur si l'utilisateur n'est pas root.
* **exit 1** : Quitte le script avec un code d'erreur (1) si la condition est vraie.


###  Demande d'informations utilisateur

```bash 
read -p "Entrez le login: " LOGIN
read -p "Entrez le nom: " NOM
read -p "Entrez le prénom: " PRENOM
read -p "Entrez l'UID (laisser vide pour utiliser le système): " USER_UID
read -p "Entrez le GID (laisser vide pour utiliser le système): " USER_GID
read -p "Entrez les commentaires: " COMMENTAIRES
```


* **read -p** : Permet de demander à l'utilisateur de saisir des informations. Les variables (LOGIN, NOM, PRENOM, etc.) contiendront les valeurs saisies.

### Vérification de l'existence de l'utilisateur

* **id "$LOGIN"** : Vérifie si un utilisateur avec le login donné existe déjà. L'opérateur &>/dev/null redirige les messages d'erreur vers /dev/null, évitant ainsi leur affichage.
* **exit 1** : Quitte le script si l'utilisateur existe déjà.

### Vérification de l'existence du répertoire personnel

* **HOME_DIR="/home/$LOGIN"** : Définit le chemin du répertoire personnel de l'utilisateur.
* **if [ -d "$HOME_DIR" ]; then** : Vérifie si le répertoire personnel existe déjà.
* **exit 1 :** Quitte le script si le répertoire existe déjà.

### Création de l'utilisateur


* useradd : Commande utilisée pour créer un nouvel utilisateur.
* -m : Crée le répertoire personnel de l'utilisateur.
* -d "$HOME_DIR" : Spécifie le chemin du répertoire personnel.
* -c "$NOM $PRENOM,$COMMENTAIRES" : Ajoute un commentaire (nom et prénom) pour l'utilisateur.
* -u  : Définit l'UID de l'utilisateur. Si non spécifié, utilise l'UID par défaut.
* -g  : Définit le GID de l'utilisateur. Si non spécifié, utilise le GID par défaut.

### Vérification de la création de l'utilisateur

* $? : Vérifie le code de sortie de la dernière commande (ici, useradd).
* -eq 0 : Si le code de sortie est 0, cela signifie que la commande a réussi.
* echo : Affiche un message de succès ou d'erreur selon le résultat.

### Création du répertoire personnel

* mkdir -p "$HOME_DIR" : Crée le répertoire personnel, même si le script a échoué à le créer avec useradd.
* chown "$LOGIN":"${USER_GID:-$(id -g)}" "$HOME_DIR" : Change le propriétaire du répertoire personnel pour qu'il corresponde à l'utilisateur nouvellement créé.

### Message de confirmation

```bash 
echo "Le répertoire personnel '$HOME_DIR' a été créé."
```

* Affiche un message indiquant que le répertoire personnel a été créé.



## VII) check-user.sh


```bash

#!/bin/bash

# Vérifier le nombre de paramètres
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <login|UID>"
    exit 1
fi

# Vérifier si le paramètre est un UID ou un login
if [[ $1 =~ ^[0-9]+$ ]]; then
    # C'est un UID
    if getent passwd "$1" > /dev/null; then
        # L'utilisateur existe, afficher l'UID
        echo "$1"
    fi
else
    # C'est un login
    if id "$1" &>/dev/null; then
        # L'utilisateur existe, afficher l'UID
        id -u "$1"
    fi
fi



```


* Test du script :

```bash
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# nano check-user.sh
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./check-user.sh JeanMarc
1005
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./check-user.sh 1005
1005
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./check-user.sh JeanMarcc
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./check-user.sh 244
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#

```
### Vérification du nombre de paramètres


* **$#** : C'est une variable spéciale qui représente le nombre de paramètres passés au script.
* **-ne** : Signifie "not equal". Si le nombre d'arguments n'est pas égal à 1, le script affiche un message d'utilisation et se termine avec un code d'erreur (exit 1).


## Vérification du type de paramètre (UID ou login)

* **=~** : C'est un opérateur qui permet de tester une correspondance avec une expression régulière

### Vérification de l'existence d'un utilisateur par UID


* **getent passwd "$1"** : Cela recherche l'utilisateur correspondant à l'UID dans le fichier de mots de passe.
* **> /dev/null** : Cela redirige la sortie vers /dev/null, ce qui signifie que la sortie standard est ignorée. Seule la valeur de retour de la commande est prise en compte.
* **echo "$1"** : Si l'utilisateur existe, il affiche l'UID.


### Vérification de l'existence d'un utilisateur par login

* **id "$1"** : La commande id est utilisée pour obtenir des informations sur l'utilisateur (comme son UID) basé sur le login.
* **&>/dev/null** : Redirige à la fois la sortie standard et les erreurs vers /dev/null, ne laissant que la valeur de retour.
* **id -u "$1"** : Si l'utilisateur existe, cette commande affiche son UID


## VIII) note.sh

```bash
  GNU nano 6.2                                             note.sh                                                      #!/bin/bash
while :; do
  read -p "Note (q pour quitter) : " note
  case $note in
    [16-9]|1[6-9]) echo "Très bien" ;;
    14|15) echo "Bien" ;;
    12|13) echo "Assez bien" ;;
    10|11) echo "Moyen" ;;
    [0-9]) echo "Insuffisant" ;;
    q) break ;;
    *) echo "Entrée invalide" ;;
  esac
done


```

### Test du script


```bash
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./note.sh
Note (q pour quitter) : 14
Bien
Note (q pour quitter) : 12
Assez bien
Note (q pour quitter) : 18
Très bien
Note (q pour quitter) : 4
Insuffisant
Note (q pour quitter) : q
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```


### while :; do

* Boucle infinie while : La boucle while permet de répéter des commandes tant qu'une condition est vraie. Ici, le : est une syntaxe spéciale qui représente une commande toujours vraie, ce qui signifie que la boucle s'exécutera indéfiniment, jusqu'à ce que la condition d'arrêt (le break) soit rencontrée.
* do : Cette ligne introduit le bloc de code à exécuter à chaque itération de la boucle.


### Lecture de la note

* read -p : Cette commande permet de lire une entrée utilisateur.
* -p "Note (q pour quitter) : " : Cela affiche le message Note (q pour quitter) et lit la saisie de l'utilisateur, qui est stockée dans la variable note.
* L'utilisateur peut entrer une note ou appuyer sur q pour quitter.

### Instruction case
* case est utilisé pour comparer la valeur de $note avec différents modèles (ou motifs). Chaque motif est suivi par une action à exécuter si la comparaison est vraie.


### Cas pour les notes "Très bien"
* [16-9] : Cela vérifie si la note est comprise entre 0 et 9.
* 1[6-9] : Cela vérifie si la note est entre 16 et 19.
Si l'une de ces conditions est remplie, le script affiche "Très bien".

### Cas pour les notes "Bien"
* 14|15 : Ce motif capture les notes égales à 14 ou 15.
* Si c'est le cas, le script affiche "Bien".

### Cas pour les notes "Assez bien"
* 12|13 : Cela vérifie si la note est soit 12 soit 13.
* Si c'est le cas, le script affiche "Assez bien".


### Cas pour les notes "Moyen"
* 10|11 : Cela capture les notes égales à 10 ou 11.
* Si c'est le cas, le script affiche "Moyen".

## Cas pour les notes insuffisantes
* [0-9] : Cela vérifie si la note est un nombre à un chiffre compris entre 0 et 9.
* Si c'est le cas, le script affiche "Insuffisant".

## Cas pour quitter la boucle
* q : Si l'utilisateur entre q, la commande break est exécutée, ce qui sort de la boucle while et termine le script.

## Cas pour entrée invalide
* (*) : Ce motif capture tout ce qui ne correspond pas aux autres motifs précédents.
* Si l'utilisateur entre une valeur qui ne correspond à aucune des notes spécifiées (par exemple, une lettre autre que q), le script affiche "Entrée invalide".


## Fin de la boucle

* La boucle while continue jusqu'à ce que l'utilisateur entre q.




#  Exercice : lecture au clavier

### I) La commande bash read 

```bash
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# echo -n "Entrer votre nom: "
read nom
echo "Votre nom est $nom"
Entrer votre nom: Darras
Votre nom est Darras
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```

### II) La commande file 
bas´ees sur l’examen rapide du contenu du fichier)
```bash
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# nano users.sh
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# nano note.sh
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# echo -n "Entrer votre nom: "
read nom
echo "Votre nom est $nom"
Entrer votre nom: Darras
Votre nom est Darras
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# echo "Ceci est un fichier texte pour mon TP3." > exemple2.txt
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# file exemple2.txt
exemple2.txt: ASCII text
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```

### III) La commande more

```bash
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# more exemple2.txt
Ceci est un fichier texte pour mon TP3.
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#
```

### IV) Détails sur more

* Comment quitter more ?
  * Appuyez sur q.
    
   ![q](./img/q.png "q")

* Comment avancer d’une ligne ?
  * Appuyez sur Entrée.

      ![entree](./img/entree.png "entree")

* Comment avancer d’une page ?
  * Appuyez sur la barre d'espace.

  * En effet voici ce que dis la documentation :
  ![space-more](./img/space-more.png "space-more")

* Comment remonter d’une page ?
  * Appuyez sur b.

  ![b](./img/b.png "b")

* Comment chercher une chaîne de caractères ?
   * Tapez **/votre_chaine** et appuyez sur Entrée. Pour passer à l’occurrence suivante, appuyez sur n.
    ![n](./img/n.png "n")

### V) Ecrire un script 

* Le voici 

```bash
#!/bin/bash

# Vérifie si un argument a été fourni
if [ "$#" -ne 1 ]; then
    echo "Usage: $0 chemin/du/répertoire"
    exit 1
fi

# Parcourt chaque fichier dans le répertoire donné
for fichier in "$1"/*; do
    # Vérifie si c'est un fichier régulier et texte
    if [ -f "$fichier" ] && file "$fichier" | grep -q "text"; then
        echo "Voulez-vous visualiser le fichier $(basename "$fichier") ? (o/n)"
        read reponse
        
        if [[ "$reponse" == "o" || "$reponse" == "O" ]]; then
            more "$fichier"  # Utilise more pour l'affichage page par page
        fi
    fi
done

```

* Voici un exemple d'utilisation : 

```bash



root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./visualisation-fichier.sh test_repertoire
Voulez-vous visualiser fichier1.txt ? (o/n) o
Ceci est un fichier texte
Voulez-vous visualiser fichier2.txt ? (o/n) o
Autre contenu texte
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# nano visualisation-fichier.sh
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3# ./visualisation-fichier.sh test_repertoire
Voulez-vous visualiser le fichier fichier1.txt ? (o/n)
o
Ceci est un fichier texte
Voulez-vous visualiser le fichier fichier2.txt ? (o/n)
o
Autre contenu texte
root@LAPTOP-E9LS6Q7M:/mnt/c/WINDOWS/system32/tp3#

```

# Conclusion

* Ce TP m'a permis de mieux comprendre l'utilité et la puissance du shell Bash dans un environnement UNIX. En explorant divers scripts et en les développant, j'ai appris à automatiser certaines tâches courantes, à manipuler des fichiers, à traiter des paramètres d'entrée, et à gérer des boucles et des conditions de manière efficace. Cela m'a également sensibilisé à l'importance de la lisibilité du code et des commentaires, ainsi qu'aux bonnes pratiques de sécurité, comme la gestion des droits d'accès.

* Bien que Bash soit limité pour des projets complexes comparé à des langages comme Python, il reste un outil indispensable pour l'administration système et la gestion des serveurs. La maîtrise de ces concepts est essentielle pour tout professionnel travaillant dans un environnement Unix/Linux, surtout pour l'automatisation de tâches répétitives et la gestion des systèmes distants.

* Finalement, ce TP m'a fourni une base solide en scripting Bash, que je pourrai approfondir et appliquer dans des contextes professionnels à venir.
