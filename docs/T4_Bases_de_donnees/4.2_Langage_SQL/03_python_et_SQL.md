# Python et SQL / mini-projets

Nous allons créer et interroger une base de données ```sqlite``` avec le module ```sqlite3```  de Python.

### 1. Permiers exemples
#### 1.1 Création d'une table 

```python
import sqlite3

#Connexion
connexion = sqlite3.connect('mynewbase.db')

#Récupération d'un curseur
c = connexion.cursor()

# ---- début des instructions SQL

#Création de la table
c.execute("""
    CREATE TABLE IF NOT EXISTS bulletin(
    Nom TEXT,
    Prénom TEXT,
    Note INT);
    """)

# ---- fin des instructions SQL

#Validation
connexion.commit()


#Déconnexion
connexion.close()

``` 

- Le fichier ```mynewbase.db``` sera créé dans le même répertoire que le fichier source Python. Si fichier existe déjà, il est ouvert et peut être modifié.
- ```IF NOT EXISTS``` assure de ne pas écraser une table existante qui porterait le même nom. Si une telle table existe, elle n'est alors pas modifiée.
- La nouvelle table peut être ouverte avec ```DB Browser``` pour vérifier sa structure et ses données.

#### 1.2 Insertion d'enregistrements dans la table
Les morceaux de code ci-dessous sont à positionner entre les balises ```# ---- début des instructions SQL```  et ```# ---- fin des instructions SQL```.

##### 1.2.1 Insertion d'un enregistrement unique
```python
c.execute('''INSERT INTO bulletin VALUES ('Simpson', 'Bart', 17)''')
``` 

Pensez à vérifier avec  ```DB Browser``` si les modifications sont effectives.

##### 1.2.2 Insertion d'un enregistrement unique avec variable
```python
data = ('Simpson', 'Maggie', 2)
c.execute('''INSERT INTO bulletin VALUES (?,?,?)''', data)
``` 


##### 1.2.3 Insertion de multiples enregistrements
```python
lst_notes = [ ('Simpson', 'Lisa', 19), ('Muntz', 'Nelson', 4), ('Van Houten', 'Milhouse', 12) ]

c.executemany('''INSERT INTO bulletin VALUES (?, ?, ?)''', lst_notes)
``` 
Les différentes valeurs sont stockées au préalable dans une liste de tuples.

#### 1.3 Mini-projet 1
Créer un programme qui demande à l'utilisateur un nom et une note, en boucle. Les résultats sont stockés au fur et à mesure dans une base de données. Si le nom est égal à «Q» ou «q», le programme s'arrête.

#### 1.4 ☠ Exemple d'injection SQL
L'injection SQL est une technique consistant à écrire du code SQL à un endroit qui n'est pas censé en recevoir.

![](data/xkcd.png)

https://xkcd.com/327/

- Créez un fichier contenant le code suivant :
```python
import sqlite3

#Connexion
connexion = sqlite3.connect('mabasecobaye.db')

#Récupération d'un curseur
c = connexion.cursor()

c.execute("""
    CREATE TABLE IF NOT EXISTS notes(
    Nom TEXT,
    Note INT);
    """)


while True :
    nom = input('Nom ? ')
    if nom in ['Q','q'] :
        break
    note = input('Note ? ')
    data = (nom, note)
    p = "INSERT INTO notes VALUES ('" + nom + "','" + note + "')"

    c.executescript(p)


#Validation
connexion.commit()


#Déconnexion
connexion.close()


``` 

- Exécutez ce fichier, rentrez quelques valeurs, quittez, et ouvrez dans ```DB Browser``` la table ```notes``` pour bien vérifier que vos valeurs ont bien été stockées.
- Lancez à nouveau le fichier, en donnant ensuite comme nom la chaîne de caractères suivante : 
```g','3'); DROP TABLE notes;--``` 
- Donnez une note quelconque (par exemple 12), quittez le programme... et allez observer l'état de la base de données. La table  ```notes``` n'existe plus !

**Explication** :  
La requête qui a été formulée est ```INSERT INTO notes VALUES ('g','3'); DROP TABLE notes;--','12')``` 

Dans un premier temps, le couple ```('g','3')``` a été inséré.  
Puis l'ordre a été donné de détruire la table ```notes```.  
Le reste du code (qui n'est pas correct) est ignoré car ```--``` est le symbole du commentaire en SQL (l'équivalent du # de Python).  

**Remarques** :  
Évidemment, ce code a été fait spécifiquement pour être vulnérable à l'injection SQL. Il suffit d'ailleurs de remplacer le ```c.executescript(p)``` par ```c.execute(p)``` pour que le code reste fonctionnel mais refuse l'injection SQL. 
Ceci dit, de nombreux serveurs sont encore attaqués par cette technique, au prix de manipulations bien sûr plus complexes que celles que nous venons de voir (vous pouvez par exemple regarder [ici](http://igm.univ-mlv.fr/~dr/XPOSE2011/injections_SQL/exploit.php)). 

Rappelons enfin que ce genre de pratiques est interdit sur un serveur qui ne vous appartient pas.



### 2. Lecture des enregistrements
```python
import sqlite3

#Connexion
connexion = sqlite3.connect('mynewbase.db')

#Récupération d'un curseur
c = connexion.cursor()

data = ('Simpson', )

c.execute("SELECT Prénom FROM Bulletin WHERE Nom = ?", data)
print(c.fetchall())  


#Déconnexion
connexion.close()
``` 

Ce code renvoie ```[('Homer',), ('Lisa',), ('Maggie',)]```, ou une liste vide s'il n'y a pas de résultat à la requête.

#### 2.1 Mini-projet 2
Reprendre le mini-projet précédent, en rendant possible à l'utilisateur de rentrer des notes ou bien de les consulter.

*Exemple :*

![](data/mp2.gif)


#### 2.3 Mini-projet 3


=== "Énoncé"
    Créer un système d'authenfication par login / mot de passe, dans le but de conserver une phrase secrète.  
    
    Idéalement le mot de passe ne sera pas conservé en clair mais haché (à l'aide du module `hashlib`).
    
    *Exemple :*
    
    ![](data/miniprojet3.gif)
=== "Aide"
    La méthode `fetchall()` est simple à utiliser mais peut poser un problème de performance.
    En effet, cette méthode retourne une liste, cela signifie que tous les résultats sont récupérés de la base de données pour être convertis en n-uplets. 
    S’il y a un nombre important de lignes dans le résultat de la requête, cela signifie que la liste peut être très grande et avoir une empreinte mémoire importante.
    
    Parfois, on désire traiter directement la donnée retournée et il n’est pas nécessaire de la stocker dans une liste. 
    Nous pouvons améliorer notre code en optant pour l’appel à la méthode `fetchone()`. 
    Cette méthode retourne un seul résultat sous la forme d’un n-uplet. 
    Lorsqu’il n’y a plus de résultat à lire, la méthode retourne None. 
    
    Le résultat du programme sera le même sauf que les résultats sont extraits un à un et qu’aucune liste n’est créée.
    !!! warning
        Si vous fermez un curseur avant d’avoir extrait tous les résultats, vous obtiendrez une exception. 
        N’utilisez pas la méthode `fetchone()` pour ne retourner que le premier résultat, elle n’a pas été conçue pour cela. 
        Son rôle est de permettre de retourner tous les résultats d’une requête mais un à un.

    Si vous voulez limiter le nombre de résultats retournés par une requête, utilisez l’instruction SQL `LIMIT` 
=== "Correction"
    ```python
    import sqlite3
    import hashlib
    
    connexion = sqlite3.connect('secretdata.db')
    c = connexion.cursor()
    
    c.execute("""
        CREATE TABLE IF NOT EXISTS secret(
        login TEXT,
        password TEXT,
        secret_texte TEXT);
        """)
    
    connexion.commit()
    
    def menu():
        print('-------------')
        print('1. login     ') 
        print('2. register  ')
        print('3. quit      ')
        print('-------------')
        rep = int(input("choix ?"))
        return rep
    
    def register():
        login_identique = True
        
        while login_identique == True :
            login = input("choississez votre login : ")
            tlogin = (login,)
            c.execute("""
            SELECT COUNT(*) FROM secret WHERE login = ?
            """,tlogin)
            if c.fetchone()[0] > 0 :
                print("login déjà utilisé")
            else :
                login_identique = False
                
        pwd = input("choississez votre mot de passe : ")
        pwd_hash = hashlib.md5(pwd.encode()).hexdigest()
        phrase_secrete = input("tapez la phrase secrète que vous voulez conserver : ")
        data = (login, pwd_hash, phrase_secrete)
        c.execute('''
        INSERT INTO secret VALUES (?,?,?)
        ''', data)
        connexion.commit()
    
    def login():
        login_existant = False
        while login_existant == False :
            login = input("login : ")
            tlogin = (login,)
            c.execute("""
            SELECT COUNT(*) FROM secret WHERE login = ?
            """,tlogin)
            if c.fetchone()[0] == 0 :
                print("login inconnu")
            else :
                login_existant = True
    
    
        pwd = input("mot de passe : ")
        pwd_hash = hashlib.md5(pwd.encode()).hexdigest()
        c.execute("""
        SELECT password, secret_texte FROM secret WHERE login = ?
        """,tlogin)
        result = c.fetchone()
        
        pwd_recorded = result[0]
        if pwd_hash == pwd_recorded :
            print("phrase secrète : ", result[1])
        else :
            print("wrong password")
    
    
    while True :
        r = menu()
        if r == 3 :
            break
        
        if r == 2 :
            register()
            
        if r == 1 :
            login()
    
    connexion.close()
    
    ```
    
    
    
    
    
    
