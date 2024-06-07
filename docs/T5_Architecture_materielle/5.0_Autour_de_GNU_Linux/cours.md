# Autour de GNU/Linux
{{initexo(0)}}

## 1. Systèmes d'exploitations :
### 1.1. Définition et historique 



!!! Quote "D'après la définition de Wikipedia "
    « En informatique, un [système d'exploitation](https://fr.wikipedia.org/wiki/Système_d%27exploitation) (souvent appelé OS — de l'anglais Operating System) est un ensemble de programmes qui dirige l'utilisation des ressources d'un ordinateur par des logiciels applicatifs.
    
    Il reçoit des demandes d'utilisation des ressources de l'ordinateur — ressources de stockage des mémoires (par exemple des accès à la mémoire vive, aux disques durs), ressources de calcul du processeur central, ressources de communication vers des périphériques [...] ou via le réseau — de la part des logiciels applicatifs. Le système d'exploitation gère les demandes ainsi que les ressources nécessaires évitant les interférences entre les logiciels. »


!!! abstract "Historique"
    Les années 1960 ont constitué un tournant pour les système d'exploitation. Dans le cadre du projet MAC au *MIT* (Massachusset Institute of Technology), le système d'exploitation **CTTS** (Compatible Time Sharing System)est publié en 1961. C'est l'un des tout premiers système d'exploitation **à temps partagé**, permettant à plusieurs utilisateurs d'utiliser **un ordinateur en même temps**. Cette apparente simultanéité dans l'exécution des programmes a permis de se diriger vers l'informatique moderne.
    
    Le *MIT* s'associa aux laboratoires *BELL* et à *General Electric* pour créer **Multics** qui était un système innovant, héritant de **CTTS**, et était l'un des premier système d'exploitation avec système de fichier hiérarchique, temps partagé, multitâche préemptif (c'est- à-dire la capacité d'arrêter ou d'exécuter une tâche planifiée en cours), multiutilisateur, avec une prise en compte de la sécurité. La première version sortit en 1965.

    En 1969, les laboratoires BELL sortirent du projet et deux de leurs plus brillants informaticiens, [Ken THOMPSON](https://fr.wikipedia.org/wiki/Ken_Thompson) et [Dennis RITCHIE](https://fr.wikipedia.org/wiki/Dennis_Ritchie) qui avaient travaillé sur le projet *Multics* en conçurent une version simplifiée (ils considéraient *Multics* inutilement complexe) qu'ils nommèrent initialement UNICS (UNiplexed Information and Computing Service) puis **UNIX**. L'informatique moderne était née !

    Au fil des années, des surcouches de plus en plus complexes sont ajoutées aux systèmes d'exploitations afin de gérer par exemple les entrées claviers, puis souris, et une interface graphique est ajoutée, simplifiant la tâche pour l'utilisateur.

Chaque ordinateur doit donc disposer d'un OS afin de pouvoir faire fonctionner les différents logiciels en parallèle. Historiquement, chaque fabriquant d'ordinateur a développé en partie son OS. On pourra, de manière non-exhaustive, citer :

- *OS/360* par *IBM*, en 1968 ;
- *DOS* par *Microsoft* en 1981 ;
- *Mac OS* par *Apple* en 1984 ;
- *Windows 3.X* par *Microsoft* en 1990 ; 
- **GNU/Linux** par la communauté en 1991 ; 
- *Android* par *Google* en 2007 ;
- *iOS* par *Apple* en 2007.




### 1.2 GNU/Linux

En 1985, [Richard Stallman](https://fr.wikipedia.org/wiki/Richard_Stallman) quitte le MIT pour écrire un système d'exploitation compatible Unix : [GNU](https://fr.wikipedia.org/wiki/GNU) (**G**nu is **N**ot **U**nix). Opposé au principe du logiciel « propriétaire », il publie le manifeste GNU, où il expose ses  idées de [logiciel libre](https://fr.wikipedia.org/wiki/Logiciel_libre), permettant à chacun de s'approprier, de modifier et de diffuser le code source d'un logiciel.


!!! abstract "{{ exercice() }}"
    Se rendre sur [Wikipédia](https://fr.wikipedia.org/wiki/Logiciel_libre) et expliquer pourquoi il ne faut pas confondre les termes suivants: 
    
    - logiciel libre (free software, libre software ou libreware) ;
    - gratuiciels (freewares) ;
    - open source.

En 1991, [Linus Torvalds](https://fr.wikipedia.org/wiki/Linus_Torvalds), étudiant norvégien de 21 ans, indisposé par la faible disponibilité de serveur UNIX de l'université d'Helsinki décide d'écrire un mini OS dérivé d'Unix pour son PC. Il écrit un [noyau](https://fr.wikipedia.org/wiki/Noyau_de_système_d%27exploitation) auquel il adapte de nombreux composants disponibles du [projet GNU](https://fr.wikipedia.org/wiki/Projet_GNU). Réputé pour sa stabilité (mais aussi pour sa complexité d'installation), le [noyau Linux](https://fr.wikipedia.org/wiki/Noyau_Linux) est adopté par une grande communauté de bidouilleurs ([hacker](https://fr.wikipedia.org/wiki/Hacker_(sous-culture))) sur l'internet, qui étendent régulièrement ses possibilités. Sans publicité, soutenu par la communauté du libre et de l'[open-source](https://fr.wikipedia.org/wiki/Open_source), [Linux](https://fr.wikipedia.org/wiki/Linux) se répand doucement et devient rapidement une alternative crédible à *Windows*, à tel point que 90 % des serveurs du cloud sont des serveurs *Linux*. Linus Torvalds continue à diriger le développement de *Linux*, et est considéré comme le « dictateur bienveillant à vie » (Benevolent Dictator for Life) de celui-ci.

Si, à l'origine, *Linux* a été développé pour les ordinateurs compatibles PC, il n'a jamais équipé qu'une très faible part des ordinateurs personnels. Mais le *noyau Linux*, accompagné ou non des *logiciels GNU*, est également utilisé par d'autres types de systèmes informatiques, notamment les serveurs, téléphones portables, systèmes embarqués ou encore superordinateurs. Le système d'exploitation pour téléphones portables *Android* qui utilise le noyau *Linux* (mais pas *GNU*) équipe aujourd'hui 85 % des tablettes tactiles et smartphones.

## 2. Premiers pas
Selon les modalités à votre disposition.

=== "En ligne"
    - Le site [https://www.pythonanywhere.com](https://www.pythonanywhere.com){:target="_blank"} permet de créer un compte gratuit pour programmer en *python* ou pour disposer d'un [terminal](https://fr.wikipedia.org/wiki/Terminal_(informatique)) sous *Linux*.

=== "Avec WSL"
    - **Installation sur WSL**
        - **Windows Subsystem for Linux (WSL)** est une couche de compatibilité permettant d'exécuter des exécutables binaires *Linux* de manière native sur les dernières versions de Windows (à partir de windows 10). La version WSL 2,sortie en mai 2019, introduit la présence d'un véritable noyau *Linux*.
     
        - Pour installer la distribution Ubuntu, lancer l'invite de commande windows, puis :
        ``` bash title=""
        wsl -install -d Ubuntu
        ```
    - **Utilisation de WSL**
        - Une fois installé, vous avez accès à la distribution depuis l'invite de commande windows par l'intermédiaire de la commande `wsl`.
        - Vous accédez alors à un terminal *Linux* tout ce qui est des plus classique
        - Le prompt est de la forme `nom_utilisateur@nom_machine : chemin_dossier_courant $`.
        - Normalement, votre répertoire courant est symbolisé par `~` , ce qui est un raccourci pour symboliser le répertoire personnel de l'utilisateur.

=== "Sur Raspberry Pi" 
    - **Installation sur Raspberry Pi 4**
        - Il existe des distributions *Linux* spécifiques pour Rasberry 4, mais nous utiliserons **Raspberry Pi OS** (anciennement connu sous le nom de **Raspbian**), qui est une distribution basée sur **Linux Debian** spécialement optimisé pour Rasberry Pi. 
        - Une image est téléchargeable [ici](https://www.raspberrypi.com/software/)
        - Une fois l'image installée sur une carte micro-SD, le mini-ordinateur devrait-être immédiatement fonctionnel.
    !!! example "Exercice"
        Suivez toutes les étapes d'installation de l'OS **Raspebbry Pi OS**, en créant un utilisateur administrateur avec votre nom de famille + première lettre de votre prénom, et un **mot de passe simple**.
    - **Le terminal**
        - Pour obtenir la ligne de commande dans Raspbian, il faut lancer le programme `Terminal`.
        - Le prompt est de la forme `nom_utilisateur@nom_machine : chemin_dossier_courant $` .
        - Normalement, votre répertoire courant est symbolisé par `~` , ce qui est un raccourci pour symboliser le répertoire personnel de l'utilisateur.



## 3. Le Shell Linux
### 3.1. Bash

**Bash** (acronyme de Bourne-Again shell) est un interpréteur en ligne de commande de type script. C’est le shell Unix(l'interpréteur de commande) du projet GNU.


[Le terminal](https://fr.wikipedia.org/wiki/Terminal_(informatique)) fonctionne avec le principe **REPL** : Read Eval Print Loop.

- **Read**: L’utilisateur tape une commande qui est lue par l’interpréteur,
- **Eval**: Cette commande est exécutée et retourne une chaîne de caractères,
- **Print**: La chaîne de caractères est affichée à l’écran,
- **Loop**: On recommence.

Comme tous les interpréteurs en ligne de commande de type script, *Bash* exécute quatre opérations fondamentales:

- Il fournit une liste de commandes permettant d’opérer sur l’ordinateur (lancement de programmes, copie de fichiers, etc.) et il permet de regrouper ces commandes dans un fichier unique appelé [script](https://fr.wikipedia.org/wiki/Langage_de_script) ;

- Il vérifie la ligne de commande lors de son exécution ou lors d’une éventuelle procédure de vérification et renvoie un message d’erreur en cas d’erreur de syntaxe ;

- En cas de validation, chaque ligne de commande est interprétée, c’est-à-dire traduite dans un langage compréhensible par le système d’exploitation qui l’exécute alors.

- Les scripts sont de courts programmes généralement faciles à construire. *Bash* offre un service de gestion de flux, c’est-à-dire qu’il permet que le résultat d’un script (la sortie) soit transmis à un autre script (l’entrée). De cette façon, les scripts peuvent être « chaînés », chacun effectuant une seule tâche bien délimitée.

Les scripts peuvent être exécutés manuellement par l’utilisateur ou automatiquement par le système. Par exemple, dans la distribution GNU/Linux Ubuntu, le répertoire `resume.d` contient un certain nombre de scripts qui s’exécutent automatiquement lors du redémarrage du système, c’est-à-dire après la fin de la mise en veille de celui-ci. Ces scripts servent à relancer les différents programmes interrompus par la mise en veille.

### 3.2. Le système de fichiers
Sur un système *Linux*, **tout est un fichier**, y compris un dossier. Mais pour rester compatible avec l'arborescence classique de windows, nous parlerons donc de :

- **fichier** lorsqu'il s'agit d'une feuille de l'arborescence ; 
- **dossier** lorsqu'on parle d'un noeud ayant des enfants.

Pour naviguer dans l'arborescence, il est nécessaire de connaître deux commandes:

1. la commande `ls` , qui permet de lister tous les enfants du répertoire courant dans l'arborescence et peut utiliser les options suivantes :
    - `ls -a` affiche les fichiers cachés;
    - `ls -R` afiche tous les fichiers dans les sous-répertoires(de manière **récursive**);
    - `ls -l` affichera les détails des fichiers (autorisations,taille,propriétaires,etc...).

 2. la commande `cd` pour Change Directory, qui peut s'utiliser selon les manières suivantes :
    - `cd ~`, ramène au répertoire de l'utilisateur courant;
    - `cd nom_du_repertoire_enfant`, qui déplace le prompt dans le répertoire enfant sélectionné (adressage relatif); 
    - `cd /chemin/absolu/vers/un répertoire`, qui déplace vers le répertoire cible (adressage absolu);
    - `cd ..` qui permet de remonter au répertoire parent.
 
!!! example "{{ exercice() }}"
    Se repérer dans l'arborescence:

    1. Remonter l'arborescence jusqu'à la racine. Donner le chemin absolu de votre répertoire personnel à partir de la racine.
    2. Se déplacer jusqu'au répertoire `/usr/bin` et lister les fichiers présents.
    3. Retourner dans le dossier personnel, puis lister les fichiers présents, en affichant les détails. Quelles sont les informations données ? Quels sont les utilisateurs recensés du système ?

!!! abstract "Les dossiers systèmes Linux"
    Dans un système de type UNIX , on dispose d'une arborescence de fichiers dont la racine est `/` , puis d'un certain nombres de répertoires dont voici les principaux éléments :
    ``` title=""
    /
    ├── bin     ← Commandes de base du système
    ├── dev     ← Fichiers représentant les dispositifs matériels (devices) du système 
    ├── etc     ← Fichiers de configuration du système
    ├── home    ← Répertoire d'accueil (HOME) des utilisateurs
    ├── lib     ← Librairies                                  
    ├── mnt     ← Points de montage (clés usb etc.)           
    ├── proc    ← État du système et de ses processus         
    ├── root    ← Répertoire de l'administrateur système      
    ├── run     ← Variables d'état du système depuis le boot  
    ├── sys     ← Informations sur le noyau et les périphériques 
    ├── usr     ← Logiciels installés avec le système, base de données etc.
    └── var     ← Données fréquemment utilisées et modifiées 
    ```

### 3.3. Les utilisateurs et les droits
En *Linux*, tout fichier, et par extension dossier, appartient à un propriétaire ainsi qu'à un groupe et un utilisateur quelconque ne pourra pas forcément avoir tous les droits sur un fichier qui ne lui appartient pas.

Par exemple, étudions la sortie donnée par la commande ls -l suivante :
```bash
-rw-r--r--    1 raoul         staff    21359 2024-06-07 02:16 cours.md
drwx------@ 887 raoul         staff    28384  6 jui     22:22 Downloads
```

- `-` indique que l'élément trouvé est un fichier alors que `d` indique qu'il s'agit d'un dossier;
- les 9 lettres suivantes indiquent les droits dont disposent les utilisateurs sur ce fichier; 
- le nombre suivant est pour nous sans intérêt (il s'agit d'un compteur de liaison) ;
- `@` indique que l'existence d'[attributs étendus](https://fr.wikipedia.org/wiki/Attributs_étendus)
- le groupe de lettre suivant est le nom de l'**utilisateur** propriétaire du fichier ou dossier ;
- le groupe de lettre suivant est le nom **du groupe** propriétaire du fichier ou dossier ;
- `21359` et `28384` représentent respectivement la taille en octet du fichier et celle du dossier ;
- on trouve ensuite la date et l'heure de la dernière modification ; 
- enfin le nom du fichier ou du dossier.



!!! abstact "Les utilisateurs"
    Pour un fichier, on distinguera **trois types d'utilisateurs** :
    
    - `u` pour user, c'est-à-dire le propriétaire du fichier ;
    - `g` pour group, le groupe auquel appartient le fichier ;
    - `o` pour other, tous les autres utilisateurs.




!!! warning   "Super-Utilisateur"

    ![image](data/sandwich.png){: .center width=30%}
    Par défaut, il existe un **super-utilisateur** nommé `root` qui possède tous les droits sur un os *Linux*. 
    
    Pour modifier des attributs au niveau système, il faut prendre les droits de super-utilisateur, grâce à la commande `sudo` (super-user do). Cette commande demande systématiquement à l'utilisateur faisant partie du groupe des super-utilisateurs (*sudoers*) de confirmer avec son mot de passe (celui choisi à l'installation du système) toute action de modification effectuée au niveau du système.
    
    Par exemple pour une mise à jour sous Ubuntu, on tapera les commandes suivantes : 
    
    - Mise à jour de la base de donnée des paquets systèmes :
    ```bash
    sudo apt update
    ```
    - mise à jour des paquets :
    ```bash
    sudo apt upgrade
    ```
    **Attention ! Avec de grands pouvoirs viennent de grandes responsabilités !**
  
  
!!!abstract  "Les droits"
    Pour un fichier donné, on distinguera 4 permissions :
    
    - `r` : read, droit de lire le fichier ;
    - `w` : write, droit de modifier le fichier ;
    - `x` : execute, droit d'exécution du fichier ; 
    - `-` : aucun droit sur le fichier.
    
!!! example "{{ exercice() }}"
    Quels sont les droits des utilisateurs sur le dossier Téléchargements de mon PC ?
 
!!! abstract "Attribution des permissions"
    Pour donner ou supprimer des permissions sur un fichier `mon_texte.txt` , on utilise la commande `chmod` de la manière suivante :
    
    - Pour donner les droits en lecture et écriture à l'utilisateur:
    ```bash
    chmod u+rw mon_texte.txt
    ```
    - Pour supprimer les droits en modification au groupe :
    ```bash
    chmod g-w mon_texte.txt
    ```
    - Pour supprimer tous les droits aux autres utilisateurs :
    ```bash
    chmod o-rwx mon_texte.txt
    ```
    
    Il est aussi possible d'utiliser la notation octale pour gérer ces droits. Par exemple, la commande suivante :
    ```bash
    chmod 640 mon_texte.txt
    ```
    en sachant que `r = 4`, `w =2`, `x=1` , et que le premier chiffre correspond à l'utilisateur, le second au groupe, et le troisième aux autres. 
    
    Ainsi ici :
    
    - l'utilisateur à les droits de lecture et d'écriture (4+2 = 6) ; 
    - le groupe à le droit de lecture (4) ;
    - les autres n'ont aucun droit (0).
    
    Une commande telle que `chmod 777 mon_texte.txt` done tous les droits de lecture, écriture et exécution à tous les utilisateurs du système.

!!! danger "La suite à venir (en travaux)"

Exercice
1. Copiez un fichier quelconque depuis votre session Windows vers votre session WSL par l'intermédiaire de l'explorateur de fichier de windows.
2. Quels sont les droits sur ce fichier ?
3. Modifiez-les de manière à ce que seul l'utilisateur principal (vous) ait des droits de lecture, écriture et exécution sur ce fichier, et que les autres n'aient qu'un droit de lecture.
3.4. Les principales commandes Shell sous *Linux*
Voici, de manière non-exhaustive, quelques-unes des commandes les plus utiles sous *Linux* :
pwd :donnelecheminabsoludurépertoirecourant.
man (raccourci de manual) : donne le manuel de la commande passée en argument.
cat (raccourcideconcatenate):sonutilisationsimpleestd'aficherlecontenud'unfichierdirectementdansleterminal. Cependant cette commande permet bien d'autres choses :
: crée un nouveau fichier dans le répertoire courant, et le remplit avec les saisies de l'utilisateur (
+ C pour quitter) ;
cat fichier 1 fichier2 > fichier3 :concatènelescontenusdesfichiers1et2dansunnouveaufichier.
cp (raccourci de copy) : copie un fichier dans un dossier :
cp bidule.jpg /home/bob/photo copie le fichier bidule.jpg vers le répertoire /home/bob/photo , si les permissions sont
correctement attribuées.
mv (raccourcidemove):dépalceunfichierversunrépertoirecible,etparextensionpermetderenommerunfichier:
mv bidule.jpg /home/bob/photo déplace le fichier bidule.jpg vers /home/bob/photo ; mv bidule.jpg truc.jpg renomme le fichier bidule.jpg en truc.jpg .
cat > nv_fichier.txt
  ⌃ Ctrl
    


(pour make directory) : crée un nouveau répertoire dont le nom est passé en argument.
rmdir nom_dossier (pourremovedirectory):supprimeunrépertoirevidedontlenomestpasséenargument.
rm (pourremove):supprimeleoulesfichierspassésenarguments.Attentionàcettecommandequipeuttoutcasser!:
rm * :supprimetouslesfichiersdurépertoirecourant
rm -R:supprimedemanièrerécursivetouslesfichiersetsous-dossiersdurépertoirecourant!
Il existe aussi des commandes interdites, à ne jamais utiliser sous peine de mise au ban de la société, lynchage en place
publique, etc...
touch nv_fichier : permet de créer un nouveau fichier vide en lui passant le nom en argument. A préférer à la commande cat .
find : permet de chercher des fichiers et/ou des dossier dans un dossier donné. Par exemple find /home/ -name mon_texte.txt cherche le fichier mon_texte.txt dans le répertoire home et tous ses sous-dossiers.
locate : permet de donner la localisation d'un fichier dans le système de fichier. locate est très rapide, car elle utilise une base de donnée mise à jour régulièrement qui recense tous les fichiers du système. Cependant, la mise à jour de cette base de donnée n'est pas immédiate, donc les modifications récentes ne sont pas prises en compte.
grep : permet de chercher une chaîne de caractère dans un fichier. grep toto bob.txt renverra toutes les lignes du fichier bob.txt contenant la chaîne toto . grep est très eficace, mais ne fonctionne pas correctement sur les fichiers pdf et odt ...
head : renvoie les 10 premières lignes d'un fichier. On peut paramétrer le nombre de lignes obtenues avec l'option -n : head -n 5 bob.txt envoie les 5 premières lignes du fichier bob.txt .
tail : fonctionne de la même manière que head , mais en renvoyant les 10 dernières lignes.
diff :comparedeuxfichierslignesparlignes,etrenvoietoutescellesprésentantunedifférence.Pratique!
               Un petit TP
1. Téléchargez le fichier Arborescence.tar.gz
2. Créez dans votre dossier personnel un dossier TP
3. Copiez le fichier précédent dans ce dossier, puis décompressez le avec la commande
tar -xzf Arborescence.tar.gz
Attention, ce peut-être long...
4. Vous aurez besoin de la commande locate qui n'est pas installée. Exécutez la commande suivante pour installer le paquet nécessaire à son utilisation :
sudo apt install plocate
5. Pour débuter, cherchez le fichier   dans l'arborescence, et lisez-le ! Bon courage, vous aurez probablement à chercher en parallèle sur   des commandes spécifiques avec les options qui vont bien pour parvenir à la fin de ce TP ! (Petit point de détail, si une commande vous semble trop longue, vous pouvez l'interrompre avec le raccourci clavier ++ctrl+C++)
   commencement.txt
StackOverflow
 1. Richard Stallman est un peu le grand gourou de l'informatique, soit adulé, soit détesté... Mais un personnage incontournable (voir ici)
2. que voici un bel acronyme récursif !
3. en réalité, nous devrions toujours parler de système GNU/Linux, car *Linux* n'est que le noyau du système. On trouvera ici un célèbre texte faussement attribué à Richard Stallman sur ce point de détail. Fun fact, ce texte est parfois récité par coeur par certains ardents défenseurs du libre...
4. si vous avez oublié, le jeu terminus
mkdir nv_dossier


