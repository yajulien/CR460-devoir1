# Devoir 1
## Énoncé

À partir de GitHub, vous copierez le [repository](https://github.com/matbilodeau/CR460-devoir1)
et y appliquerez les modifications nécessaires afin de déployer l'infrastructure
demandée sur GCP via Terraform.  
Vous fournirez 3 captures d'écran: output terraform + site web avec IP + dashboard instances GCP.
Vous sauvegarderez vos modifications (commit) et publierez le code sur votre propre version du repo.
Votre code devra être accessible de manière privée, ajoutez Riad (RiadMan) et Moi seulement.


### L'infrastructure à déployer

Via Terraform :

#### Instances
* une instance nommée "canard"
de type "f1-micro"
debian-10
dans le sous-réseau "prod-dmz"
avec un serveur apache2 à jour
  * _le serveur doit être accessible publiquement_

* une instance nommée "mouton"*
de type "f1-micro"
CoreOs 2514.1.0
cible "interne"
dans le sous-réseau "prod-interne"
  * _cette instance doit être accessible publiquement par ssh_
  * cette instance doit pouvoir recevoir du  trafic TCP sur les ports "1521", "3368", seulement en provenance du sous-réseau "prod-traitement"

* trois instances "cheval"
de type "f1-micro"
CoreOs 2514.1.0
cible "traitement"
dans le sous-réseau "prod-traitement"
  * ces instances doivent pouvoir s'éteindre automatiquement jusqu'à un minimum d'une instance
  **ET**
  * ces instances doivent pouvoir se mettre en fonction automatiquement jusqu'à un maximum de six instances
  **SELON**
  * une évaluation de la charge du CPU à +/- 77% aux 3 minutes      

* une instance nommée "fermier"
de type "f1-micro"
Ubuntu 16.04
cible "fermier"
dans le réseau par défaut de votre projet

#### Réseau
* Le réseau principal nommé "devoir1"
* un sous-réseau "prod-interne" "172.16.5.0/24"
* un sous-réseau "prod-dmz" "192.168.42.0/24"
* un sous-réseau "prod-traitement" "10.0.46.0/24"

* Une règle de pare-feu pour autoriser le trafic web sur les instances ciblées "public-web"
* Une règle de pare-feu pour autoriser le trafic  vers les instances ciblées "traitement" sur les ports TCP "1521", "3368" , seulement à partir des instances sur le sous-réseau "prod-interne"
* Une règle de pare-feu pour autoriser la connexion ssh de l'internet vers les instances ciblées "interne"

#### Compte de service
Un compte de service nommé "mapaq" sera créé avec un rôle de lecture sur les ressources du projet.
une clé d'accès sera générée et sauvegardée localement dans un fichier nommé "mapaq_svc_act.json"


### Remise
La remise du devoir se fera en 2 parties soit une sur moodle et l'autre sur GitHub.  
*Aucune autre forme ou format ne seront acceptés.*

#### Moodle
Sur Moodle, vous remettrez un fichier *PDF* nommé "matricule-Nom_Prénom-devoir1.PDF"
Le fichier contiendra:

* un lien vers votre repository Github (Collaborateurs ?)
* les captures d'écran demandées.

#### GitHub
Les fichiers Terraform doivent être séparés en modules selon les ressources.
Vous devez utiliser:
* des variables pour identifier le projet et la zone de traitement
* un fichier data data pour calculer le réseau par défaut et le projet par défaut, ce dernier via une variable
* un output pour obtenir directement l'adresse ip du serveur web.

# Vous pouvez détruire votre infrastructure une fois les captures d'écran obtenues
