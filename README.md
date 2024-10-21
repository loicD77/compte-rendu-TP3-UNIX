# [ LP LPW 2024 ] compte rendu TP3 UNIX :
DARRAS Loïc L3 PRO PROJET WEB ET MOBILE

# Présentation/Introduction du travail (avant la table des matières et les explications)



* Ici ce troisième tp recouvre l'écriture de divers scripts dont :
   * analyse.sh
   * concat.sh
   * test-fichier.sh
   * listedir.sh
   * user.sh
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
   - [2.4 Read file et more](#iv-read-file-et-more)
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

## V) user.sh : 

* Voici ld script de user.sh:

```bash 
  GNU nano 6.2                                            users.sh                                                      #!/bin/bash
awk -F: '$3 > 100 {print $1}' /etc/passwd
```


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
  GNU nano 6.2                                         create-user.sh                                                   #!/bin/bash
[ "$(id -u)" -eq 0 ] || { echo "Vous devez être root."; exit 1; }
read -p "Login : " login
id "$login" &>/dev/null && { echo "$login existe."; exit 1; }
useradd "$login" && echo "Utilisateur $login créé."

```


### Vérification que l'utilisateur exécutant le script est root
* **(id -u) :** Cette commande récupère l'ID utilisateur (UID) de l'utilisateur courant. L'UID de root est toujours 0.
**[ "$(id -u)" -eq 0 ] :** Cette condition vérifie si l'UID est égal à 0, ce qui signifie que l'utilisateur est root.
* **|| :** Opérateur "OU" logique. Si la condition à gauche est fausse (c'est-à-dire que l'utilisateur n'est pas root), alors la commande à droite sera exécutée.
* **{ echo "Vous devez être root."; exit 1; } :** Si l'utilisateur n'est pas root, le script affiche un message d'erreur ("Vous devez être root.") et termine immédiatement avec un code de sortie 1 (indiquant une erreur).


### Lecture d'un nom d'utilisateur (login)

* **read -p "Login : " :** Cette commande lit une entrée de l'utilisateur via le terminal et l'affecte à la variable login.
* **-p :** Cette option permet d'afficher un message d'invite ("Login : ") avant de lire l'entrée.
* **login :** La variable dans laquelle l'entrée sera stockée. L'utilisateur doit entrer un nom d'utilisateur (login) qui sera utilisé plus tard dans le script.

### Vérification si l'utilisateur existe déjà
* id "$login" : Cette commande vérifie si un utilisateur avec le login fourni existe déjà sur le système. La commande id retourne des informations sur l'utilisateur si celui-ci existe.
* &>/dev/null : Cette partie redirige la sortie et les erreurs de la commande vers /dev/null, c'est-à-dire qu'elle les supprime pour ne pas les afficher à l'écran.
* && : Opérateur "ET" logique. Si la commande id "$login" réussit (c'est-à-dire que l'utilisateur existe), alors la commande à droite sera exécutée.
{ echo "$login existe."; exit 1; } : Si l'utilisateur existe déjà, le script affiche un message d'erreur et s'arrête immédiatement avec un code de sortie 1.
Exemple de sortie :

```bash
john existe.
```

### Création du nouvel utilisateur
* useradd "$login" : Cette commande crée un nouvel utilisateur avec le nom d'utilisateur spécifié dans la variable login.
* Si la création de l'utilisateur réussit, la commande retourne un succès.
* && : Opérateur "ET" logique. Si la commande useradd réussit (l'utilisateur est bien créé), la commande à droite est exécutée.
* echo "Utilisateur $login créé." : Cette commande affiche un message indiquant que l'utilisateur a été créé avec succès.


### Exemple de sortie :

* Si l'utilisateur entre john et que l'utilisateur john n'existait pas encore, après l'exécution de useradd, le script affichera :


```bash
Utilisateur john créé.
```


## VII) check-user.sh


```bash
  GNU nano 6.2                                          check-user.sh                                                   #!/bin/bash
id "$1" &>/dev/null && echo "L'utilisateur $1 existe." || echo "L'utilisateur $1 n'existe pas."


```

### Vérification que l'utilisateur est root

* (id -u) : Cette commande retourne l'ID utilisateur (UID) de l'utilisateur qui exécute le script. Si l'utilisateur est root, l'UID sera 0.
* [ "$(id -u)" -eq 0 ] : Cette condition vérifie si l'UID est égal à 0, ce qui signifie que l'utilisateur est root.
* || : Opérateur "OU" logique. Si la condition à gauche échoue (si l'utilisateur n'est pas root), alors la commande à droite sera exécutée.
{ echo "Vous devez être root."; exit 1; } : Si l'utilisateur n'est pas root, le script affiche un message d'erreur ("Vous devez être root.") et se termine avec un code de sortie 1 (indiquant une erreur).


### Lecture du nom d'utilisateur (login)

* read -p "Login : " : Cette commande lit une entrée depuis le terminal, ici le nom d'utilisateur (login) que l'utilisateur souhaite créer.
* -p : Cette option permet d'afficher un message d'invite ("Login : ") avant de lire l'entrée.
* login : La variable dans laquelle la valeur entrée par l'utilisateur sera stockée.


### Vérification si l'utilisateur existe déjà
* id "$login" : Cette commande vérifie si un utilisateur avec le nom d'utilisateur (login) fourni existe déjà. Si l'utilisateur existe, elle retourne des informations sur cet utilisateur.
* &>/dev/null : Cette partie redirige la sortie standard et les erreurs vers /dev/null, ce qui signifie que la sortie ne sera pas affichée.
* && : Opérateur "ET" logique. Si la commande id "$login" réussit (c'est-à-dire que l'utilisateur existe), la commande à droite sera exécutée.
{ echo "$login existe."; exit 1; } : Si l'utilisateur existe déjà, le script affiche un message d'erreur disant que cet utilisateur existe déjà et s'arrête avec un code de sortie 1.

#### Création de l'utilisateur
* useradd "$login" : Cette commande crée un nouvel utilisateur avec le login spécifié. Si la commande réussit, elle retourne un succès.
* && : Opérateur "ET" logique. Si la commande useradd réussit (c'est-à-dire que l'utilisateur a été créé), la commande à droite sera exécutée.
* echo "Utilisateur $login créé." : Si l'utilisateur a bien été créé, le script affiche un message confirmant la création.

Exemple de sortie :

Si l'utilisateur jane n'existait pas avant, le script affichera après la création réussie :



```bash
Utilisateur jane créé.
```



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

### IV) Read file et more

* Comment quitter more ?
  * Il suffit d'appuyer sur q.

* Comment avancer d’une ligne ?
  * Il faut appuyer sur Entrée.

* Comment avancer d’une page ?
  * Il faut utiliser la barre d'espace.

* Comment remonter d’une page ?
  * Il faut appuyer sur b.



Comment chercher une chaîne de caractères ?
Tapez **/votre_chaine** et appuyez sur Entrée. Pour passer à l’occurrence suivante, appuyez sur n.

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

```bash

Voici un exemple d'utilisation : 

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

* Ce TP m'a donc permis de mieux comprendre l'utilité et la puissance du shell Bash dans un environnement de type UNIX. En explorant divers scripts et en les développant, j'ai appris à automatiser certaines tâches courantes, comme manipuler des fichiers, traiter des paramètres d'entrée, et gérer des boucles et des conditions de manière efficace. Cela m'a également sensibilisé à l'importance de la lisibilité du code et des commentaires, ainsi qu'aux bonnes pratiques de sécurité, comme la gestion des droits d'accès.

* Bien que Bash soit limité pour des projets complexes comparé à des langages comme Python, il reste un outil indispensable pour l'administration système et la gestion des serveurs. La maîtrise de ces concepts est essentielle pour tout professionnel travaillant dans un environnement Unix/Linux, surtout pour l'automatisation de tâches répétitives et la gestion des systèmes distants.

* Finalement, ce TP m'a fourni une base solide en scripting Bash, que je pourrai approfondir et appliquer dans des contextes professionnels à venir.
