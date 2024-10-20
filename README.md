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


Voici la liste des paramètres : arg1 arg2 arg3







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



## test-fichier.sh

Voici le script de ce dernier : 

```bash 

  GNU nano 6.2                                         test-fichier.sh                                                  #!/bin/bash
[ -e "$1" ] || { echo "$1 n'existe pas."; exit 1; }
[ -f "$1" ] && echo "$1 est un fichier." || [ -d "$1" ] && echo "$1 est un répertoire."
[ -r "$1" ] && echo "Lisible."
[ -w "$1" ] && echo "Modifiable."
[ -x "$1" ] && echo "Exécutable."



```
