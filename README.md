# VPC--Appairage
Atelier guidé : création d'une connexion d'appairage de VPC

Il se peut que vous deviez connecter vos clouds privés virtuels (VPC) pour transférer des données entre eux. Cet atelier explique comment créer une connexion d'appairage de VPC privé entre deux VPC.
À la fin de cet atelier, vous serez en mesure d'effectuer les tâches suivantes :
créer une connexion d'appairage de VPC ;  
configurer des tables de routage pour utiliser la connexion d'appairage de VPC ;
activer des journaux de flux VPC pour fournir des informations sur les données circulant sur le réseau ;
créer une connexion d'appairage ;



<img width="623" height="311" alt="image" src="https://github.com/user-attachments/assets/b7fe8627-aae4-46ca-b01c-b55513ea5e7d" />



# Tâche 1 : création d'une connexion d'appairage de VPC
Votre tâche consiste à créer une connexion d'appairage entre deux VPC.
Une connexion d'appairage de VPC est une connexion réseau entre deux VPC qui permet d'acheminer le trafic entre eux de manière privée. Les instances dans les VPC peuvent communiquer entre elles comme si elles faisaient partie du même réseau. Vous pouvez créer une connexion d'appairage de VPC entre vos propres VPC, avec un VPC situé dans un autre compte AWS ou avec un VPC au sein d'une autre Région AWS.
Dans le cadre de cet atelier, deux VPC sont fournis : Lab VPC (VPC de l'atelier) et Shared VPC (VPC partagé). Le VPC de l'atelier comporte une application Inventory qui s'exécute sur une instance Amazon Elastic Compute Cloud (Amazon EC2) dans un sous-réseau public. Le VPC partagé comporte une instance de base de données qui s'exécute dans un sous-réseau privé.



<img width="576" height="291" alt="image" src="https://github.com/user-attachments/assets/84244bd7-3b0e-442c-9f69-c75862c6d147" />

 

<-------------------->


<img width="460" height="307" alt="image" src="https://github.com/user-attachments/assets/6bd62ff9-df66-4a87-b7ce-70fbbab40812" />



<------------------>



<img width="645" height="309" alt="image" src="https://github.com/user-attachments/assets/306d1fa3-b932-460c-b3cf-4ae3ac83c47c" />




<------------------->


<img width="622" height="285" alt="image" src="https://github.com/user-attachments/assets/ce3f979b-5379-4938-ab5f-6258c3c8b11b" />


<----------------->



<img width="666" height="49" alt="image" src="https://github.com/user-attachments/assets/0911573b-b7c9-442c-ac85-2e626b13d5f7" />



<----------------->

# Tâche 2 : configuration des tables de routage
Vous allez maintenant mettre à jour les tables de routage des deux VPC afin d'envoyer le trafic du VPC de l'atelier vers la connexion d'appairage du VPC partagé.

<---------------->



<img width="568" height="209" alt="image" src="https://github.com/user-attachments/assets/aac54af2-248d-429b-8f23-51f367b6d65e" />



<------------------>

Dans le volet de navigation de gauche, sélectionnez Tables de routage.

Sélectionnez  Lab Public Route Table (Table de routage publique de l'atelier) (pour Lab VPC [VPC de l'atelier]).

Vous allez configurer la table de routage publique associée au VPC de l'atelier. Si l'adresse IP de destination se trouve dans la plage du VPC partagé, la table de routage publique envoie le trafic à la connexion d'appairage.

Dans l'onglet Routes, sélectionnez Modifier les routes, puis configurez les paramètres suivants :

Sélectionnez Ajouter une route.

Destination : 10.5.0.0/16 (le paramètre est le bloc d'adresse CIDR [Classless Inter-Domain Routing] du VPC partagé.)
Cible : choisissez Connexion d'appairage dans la liste déroulante, puis dans la barre de recherche, choisissez Lab-Peer.
Choisissez Enregistrer les modifications.
Vous allez maintenant configurer le flux inverse pour le trafic provenant du VPC partagé à destination du VPC de l'atelier.
Retournez aux tables de routage et sélectionnez  Shared-VPC Route Table (Table de routage du VPC partagé). Si les cases à cocher d'autres tables de routage sont sélectionnées, désélectionnez-les.
Cette table de routage concerne le VPC partagé. Vous allez la configurer pour qu'elle envoie le trafic vers la connexion d'appairage si l'adresse IP de destination se trouve dans la plage du VPC de l'atelier.
Dans l'onglet Routes, sélectionnez Modifier les routes, puis configurez les paramètres suivants :
Sélectionnez Ajouter une route.
Destination : 10.0.0.0/16 (ce paramètre est le bloc d'adresse CIDR du VPC de l'atelier.)
Cible : choisissez Connexion d'appairage dans la liste déroulante, puis dans la barre de recherche, choisissez Lab-Peer.
Choisissez Enregistrer les modifications.
Les tables de routage sont maintenant configurées pour envoyer le trafic par le biais de la connexion d'appairage lorsque le trafic est destiné à l'autre VPC.


<--------------------->



<img width="803" height="206" alt="image" src="https://github.com/user-attachments/assets/2f0ec5b5-bdc6-4f45-8f06-dd2dc8f4929d" />



<------------------->



<img width="650" height="247" alt="image" src="https://github.com/user-attachments/assets/468584d7-89e4-46d6-9cc2-66c3464c6661" />



<-------------------->


Vous allez maintenant configurer le flux inverse pour le trafic provenant du VPC partagé à destination du VPC de l'atelier.



<-------------------->



<img width="737" height="279" alt="image" src="https://github.com/user-attachments/assets/adc959eb-da9b-4e93-8550-ebf307a893f8" />



<-------------------->




<img width="762" height="163" alt="image" src="https://github.com/user-attachments/assets/f25ccd91-eaa8-4c4f-b4e5-559d9bbea410" />




<------------------->




<img width="641" height="243" alt="image" src="https://github.com/user-attachments/assets/9fafb3f1-f898-4c44-b4ea-85545caec3b0" />




<----------------->











