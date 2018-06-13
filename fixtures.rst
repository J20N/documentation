# Fixtures
La base de données `fixtures` est une base commune, généralement utilisée pour les tests fonctionnels.

Si, pour une raison qui est propre à votre test fonctionnel, une entrée à besoin d'être ajoutée, il faudra mettre à jour celle-ci sur la branche `develop`.

Voici les étapes à suivre:

Récupérez la dernière version de `develop`:
```sh
    $ git checkout develop
    $ git pull
```

Depuis un docker, utilisez l'exécuteur de commande:
```sh
    $ sudo mysql
    $ > drop database fixtures
    $ ./cli.sh Database patchAll # Met à jour la base de données
    $ ./cli.sh Fixtures load # Charge la base fixtures
```

Effectuez vos modifications.

```sh
    $ ./cli.sh Fixtures dump
```

Revenez sur votre instance Git
```sh
    $ git status # liste des fichiers modifiés
    $ git add "fichier-schema.sql" "fichier.sql" "..." # Ajoute les fichiers à envoyer
    $ git checkout "fichier_a_ne_pas_envoyer.sql" "..." # Supprime les fichiers non utiles
    $ git status # A ce stade, seuls vos fichiers utiles sont présents
    $ git commit -m"Message propre à votre commit"
    $ git push
    $ git checkout "topic/votrebranche"
    $ git rebase develop # On va récupérer votre modification de la DB fixtures
```

Revenez sur Docker, et relancer les commandes
```sh
    $ sudo mysql
    $ > drop database fixtures
    $ ./cli.sh Database patchAll # Met à jour la base de données
    $ ./cli.sh Fixtures load # Charge la base fixtures
```

Vérifiez, vos modifications sont désormais présentes pour tout le monde.
