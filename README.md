openssh-git-auth-mysql
======================

Patch d'openssh permettant d'appeler un script tiers pour l'authentification par clé.

Il s'agit d'une version plus récente d'openssh que celle du dépôt : https://github.com/wuputahllc/openssh-for-git
Le principe est à 100% équivalent.

(Bien sûr, ce patch est fourni sans aucune garantie. Faites attention !)

But
======================

Le but premier était de déporter le stockage des clés publiques (fichier authorized_keys) vers une base de données MySQL.
L'intérêt est double : pouvoir gérer plusieurs millions de clés (comme github) sans aucune perte de performance, 
et en faciliter la gestion (un insert en sql est plus pratique que reconstruire un fichier à chaque modification).


Utilisation
======================

Il suffit d'ajouter la ligne suivante dans le fichier de configuration d'openssh (sshd_config):
''' AuthorizedKeysScript %h/.ssh/authorized_keys_script

Puis de renommer votre script "de lien" comme ci-dessus (ex: /home/git/.ssh/authorized_keys_script).
Valeur de retour du script :
 - 0, Authentification ok
 - 1, Erreur ou mauvaise clé
(Il faut faire ATTENTION, sinon c'est une brêche pour votre sécurité).

Si vous souhaitez écrire votre propre script, veuillez lire la page suivante : https://github.com/wuputahllc/openssh-for-git#writing-the-programscript


Exemples
======================

Vous trouverez, entre autres, un script python permettant de comparer la clé avec le contenu d'une base de données.

