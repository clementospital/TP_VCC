# TP2

## Etape 1

1. Le rôle d'un réseau privé dans une infrastructure cloud est d'isoler des ressources du reste d'internet afin de les sécuriser et de ne les rendre accessible qu'en interne (les machines autorisées sur ce réseau privé dans le cloud). C'est le routeur externe qui permet uniquement de faire le lien avec l'exterieur. Il sera donc possible de lui indiquer des règles de filtrage et de routage pour préciser qui de l'exterieur peut communiquer avec le réseau privé (en entrée comme en sortie).

2. Un fournisseur cloud propose autant de ressources différentes pour répondre spécifiquement à tout type de service. En effet, un service de calculs d'optimisation ne demandera pas les mêmes types de ressources qu'un service de temps réel ou bien un service de stockage.

3. Voici les étapes d'acheminement du paquet :
   - arrivée par vpn-ext jusqu'au routeur.
   - routage du paquet vers net-discovery via la passerelle (donc subnet-discovery).
   - Si la VM appartient au groupe de sécurité, filtrage du paquet en fonction des règles du groupe.
   - Arrivée ou rejet du paquet à la VM.

## Etape 2

1. Les étapes à réaliser sont les suivantes :
   - Créer la VM et sa clé ssh.
   - Récupérer la clé SSH sur la machine hote.
   - Lier une IP flottante à la VM (afin de pouvoir accéder à la VM via une IP publique).
   - Changer les permissions sur la clef ssh au niveau de la machine hote (chmod 600) afin que seul le propriétaire de la clef puisse l'utiliser (mesure de sécurité ssh).
   - Se placer dans le dossier contenant la clef ssh et se connecter à la VM via le protocole ssh en indiquant la clef à utiliser.
    
  2. Voici les différents rôles :
     - Adresse IP Privée : Celle connue du routeur pour la connexion indiquant avec quelle VM du réseau privé il faut communiquer
     - Adresse Flottante : Celle fournie publiquement permettant de discuter avec le routeur et faisant le lien entre le routeur et l'adresse privée de la VM par une très probable table de routage.
     - Groupe de sécurité : Par-feu de la VM servant de règles de filtrage des paquets pouvant entrer et sortir de la VM.
    
  3. Pour plusieurs raisons :
     - Raison de disponibilité des adresses publiques (il n'y en a pas une infinité comparativement à des adresses privées sur des sous réseaux).
     - Raison d'utilisation (toutes les VM n'ont pas pour vocation d'être accessible au public, certaines servent juste de briques de services communiquante et le service final n'est exposé publiquement que sur une VM).
     - Raison de sécurité (les adresses privées sont totalement isolées d'internet sur openStack).
     - Raison de fléxibilité (possibilité d'attacher et de détacher les IP flottante des VM).

## Etape 3

1. Une VM a besoin de sécurity group surtout si elle possède une adresse publique. Autrement elle pourrait se faire submerger de requêtes non nécessaire / en lien avec le service qu'elle expose.
2. Voici le chemin de la requete :
   - La requète sort du PC host vers l'IP publique en dest
   - Le routeur externe du réseau lit l'IP publique et route le paquet vers l'IP privée qu'il connait dans son sous réseau subnet-discovery
   - Le paquet est acheminé à la VM
   - Le sécurity group regarde ses règles de filtrage et voit que le paquet est bien en protocole TCP sur le port 5000
   - Le sécurity group laisse entrer le paquet
   - La requète arrive sur le port 5000 et est traitée par l'application hello-api écoutant sur ce port.

## Etape 4

1. La snapshot d'une image officielle n'est qu'une copie à l'instant T de l'image officielle. L'image officielle sert de base pour déployer de nouveaux services sur des snapshots de cette dernière.
2. Cela permet d'ajuster de façon dynamique les ressources aux besoins d'un service en fonction de l'évolution de ce service.
3. Plusieurs contextes peuvent répondre à cela :
   - Déploiement d'une snapshot à partir d'une image qui fait face à un incident --> on recrée une snapshot de l'image (sorte de backup d'une version stable)
   - Déploiement rapide d'un environnement pré-configuré (par exemple une image avec un environnement générique pouvant servir à déployer plusieurs environnements différents mais partageant la même base)

