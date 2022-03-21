# Jupyterlab

Helm chart pour le déploiement des jupyterlab dans l'environnement data-process-jupyter

# Detect Secrets

[Detect Secrets](https://github.com/Yelp/detect-secrets) permet d'éviter de commit des secrets dans les répos.

Il y a 3 commandes à executer pour utiliser l'outil : 

1. `detect-secrets scan --all-files  . > .secrets.baseline`

Cette commande est à executer côté client pour scanner les répo et générer un fichier de baseline.

2. `detect-secrets audit .secrets.baseline`

Egalement côté client executer cette commande pour check les mots de passes potentiels. 

**Attention** : Il faut nécéssairement répondre aux questions : 

> Is this a secret that should be committed to this repository? (y)es, (n)o, (s)kip, (b)ack, (q)uit:

afin de pouvoir passer à l'étape suivante, marquez tous les mots de passe trouvé en définissant si ils peuvent être commit ou non, cela aura une importance dans le passage cd la ci/cd.

3. `git ls-files -z | xargs -0 detect-secrets-hook --baseline .secrets.baseline`

Cette commande est executé côté gitlab, elle récupère le fichier `.secrets.baseline` et recheck de répo courant, si il y a des nouveaux mots de passe non marqués ou qu'ils n'ont pas été autorisés à être commits, la ci/cd renverra une erreur.

