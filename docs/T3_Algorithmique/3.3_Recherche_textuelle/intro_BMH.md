# Vers Boyer-Moore-Horspool

L'idée est d'améliorer le code précédent (celui on parcourt le motif à l'envers) en **sautant** directement au prochain endroit potentiellement valide. 

Pour cela on regarde le caractère ```X```  du texte sur lequel on s'est arrêté (car ```X``` n'était pas égal au caractère de rang équivalent dans le motif):

- si ```X``` n'est pas dans le motif, il est inutile de se déplacer "de 1" : on retomberait tout de suite sur ```X```, c'est du temps perdu. On se décale donc juste assez pour dépasser ```X```, donc de la longueur du motif cherché.
- si ```X``` est dans le motif (sauf à la dernière place du motif !), on va regarder la place de la dernière occurence de ```X``` dans le motif et de déplacer de ce nombre, afin de faire coïncider le ```X``` du motif et le ```X``` du texte.

???+ tip "Illustration de l'algorithme"
    ![image](data/gif_BM.gif){: .center width=40%}



On dispose de la fonction ```dico_lettres``` :
```python linenums='1'
def dico_lettres(mot):
    d = {}
    for i in range(len(mot)-1):
        d[mot[i]] = i
    return d
```

*Exemple d'utilisation de la fonction ```BMH``` :*

```python
>>> BMH("une magnifique maison bleue", "maison")
[15]
>>> BMH("une magnifique maison bleue", "nsi")
[]
>>> BMH("une magnifique maison bleue", "ma")
[4, 15]
```




??? note "Code à trous :star: :star: :star: :star:"
    ```python linenums='1'
    def dico_lettres(mot):
        d = {}
        for i in range(len(mot)-1):
            d[mot[i]] = i
        return d

    def BMH(texte, motif):


    ```


??? note "Code à trous :star: :star: :star: :octicons-star-24: " 
    ```python linenums='1'
    def dico_lettres(mot):
        d = {}
        for i in range(len(mot)-1):
            d[mot[i]] = i
        return d

    def BMH(texte, motif):
        dico = ...
        indices = ...
        i = ...
        while ...:
            k = ...
            while ...: 
                ...
            if ...: 
                ...
                ...
            else:
                if ...: 
                    ...
                else:
                    ... 

        return ...

    ```

??? note "Code à trous :star: :star: :octicons-star-24: :octicons-star-24:"
    ```python linenums='1'
    def dico_lettres(mot):
        d = {}
        for i in range(len(mot)-1):
            d[mot[i]] = i
        return d

    def BMH(texte, motif):
        dico = ...
        indices = ...
        i = ...
        while i <= ... :
            k = ...
            while ... and ...: 
                ...
            if k == ...: 
                ...
                ... 
            else:
                if ... in dico: 
                    ...
                else:
                    ... 

        return ...

    ```



??? note "Code à trous :star: :octicons-star-24: :octicons-star-24: :octicons-star-24:"
    ```python linenums='1'
    def dico_lettres(mot):
        d = {}
        for i in range(len(mot)-1):
            d[mot[i]] = i
        return d

    def BMH(texte, motif):
        dico = dico_lettres(motif)
        indices = []
        i = 0
        while i <= ... - ...:
            k = ...
            while k >= 0 and texte[...] == motif[...]: 
                k = ...
            if k == ...: 
                indices.append(...)
                i = ...
            else:
                if ... in dico: 
                    i += ... - ... - 1 
                else:
                    i += ...

        return ...

    ```
        



