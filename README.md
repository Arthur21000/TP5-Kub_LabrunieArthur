Le TP5 consiste à mettre en place un repository Github avec des pages accessible à la public, qui grâce au workflow va publier un nouveau release à chaque changement.

Il y a pour l'instant 3 releases :
  - 0.1.0 : C'est le TP4
  - 0.2.0 : Il prends en compte le nom donnée par l'utilisateur, et peut être lancé plusieurs fois avec un nom différents
    - Webserver : Un Ingress pour accéder au serveur avec un URL ( Oui il était déjà dispo sous le TP 4 xD)
    - MariaDB : En StatefulSet
    - Un NOTES.txt qui indique comment accéder au serveur quand le helm est installé
  - 0.3.0 :
    - Webserver
      - un InitContainers qui vérifie l'état de la base de données
      - Du InitContainers qui applique les droits aux PVC
      - Un LivenessProbe HTTP qui vérifie l'état des pods
    - MariaDB
      - Un ReadinessProbe qui vérifie que la base de données est bien lancé et prête à recevoir des requêtes.

Pour ajouter un nouveau release, des actions sont présentes dans le workflow et se lance dès que la "version" dans le chart.yaml est modifié, il faut donc :
  - Réaliser ses modifications
  - Changer la version dans le Chart.yaml à une version supérieur
  - Push le projet

Pour le lancer il faudra :
  - Télécharger le repository : helm repo add "nomRepo" https://arthur21000.github.io/TP5-Kub_LabrunieArthur/
  - Pour installer : helm install "nom" "nomRepo/deno-webserver" --version "version"
