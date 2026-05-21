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



Les tables de routage sont maintenant configurées pour envoyer le trafic par le biais de la connexion d'appairage lorsque le trafic est destiné à l'autre VPC.



<----------------->

# Tâche 3 : activation des journaux de flux VPC pour fournir des informations sur les données circulant sur le réseau

Maintenant que la connexion d'appairage est établie entre les deux VPC, vous allez configurer les journaux de flux VPC pour surveiller le trafic réseau entre ces deux réseaux. Dans cet atelier, vous allez configurer des journaux de flux VPC pour surveiller le trafic sur la base de données d'hébergement du VPC.

Dans le volet de navigation de gauche, choisissez Vos VPC, puis sélectionnez Shared VPC (VPC partagé).
Dans le panneau inférieur, choisissez l'onglet Journaux de flux.
Choisissez Créer un journal de flux.
Sur la page Créer un journal de flux, configurez les paramètres suivants :
Name - optional (Nom – facultatif) : SharedVPCLogs
Intervalle d'agrégation maximal : 1 minute.
Destination : Envoyer dans CloudWatch Logs.
Groupe de journaux de destination : saisissez ShareVPCFlowLogs pour créer un groupe de journaux du même nom.
Rôle IAM : choisissez vpc-flow-logs-Role.
Choisissez Créer un journal de flux.
Une alerte s'affiche en haut pour indiquer que le journal de flux a été créé pour le VPC partagé.
Dans le volet inférieur, choisissez l'onglet Journaux de flux et notez que SharedVPCLogs a été créé.
Sous Nom de destination, choisissez l'hyperlien ShareVPCFlowLogs pour afficher le groupe de journaux CloudWatch qui a été créé.
Remarque : actualisez la page après quelques minutes si vous recevez le message Log group does not exist (Le groupe de journaux n'existe pas).
Gardez cette fenêtre ouverte.



<img width="783" height="321" alt="image" src="https://github.com/user-attachments/assets/c2dfde53-a3c3-4221-9b9b-aa2966a9d7ce" />



<--------------------->



<img width="863" height="333" alt="image" src="https://github.com/user-attachments/assets/df2c0e05-9375-45bf-9c1f-e567119fc53a" />




<---------------------->



<img width="820" height="322" alt="image" src="https://github.com/user-attachments/assets/1381172a-8f4c-452f-9b8c-5f8a4a7a209c" />




<--------------------->



# Tâche 4 : test de la connexion d'appairage de VPC
Maintenant que vous avez configuré l'appairage de VPC, vous allez tester sa connexion. Pour ce faire, vous allez configurer l'application Inventory afin d'accéder à la base de données via la connexion d'appairage.
En haut de ce guide, choisissez AWS Details (Détails AWS).
Copiez la valeur d'EC2PublicIP et collez-la dans un nouvel onglet de navigateur web.
L'application Inventory et le message Please configure settings to connect to database (Veuillez configurer les paramètres pour vous connecter à la base de données) devraient maintenant s'afficher. 
Choisissez  Paramètres et configurez les paramètres suivants :
Point de terminaison : collez le point de terminaison de la base de données. Pour trouver ce point de terminaison, choisissez AWS Details (Détails AWS) sur la page des instructions de l'atelier. Ensuite, copiez le point de terminaison.
Base de données : inventory
Nom d'utilisateur : admin
Mot de passe : lab-password
Sélectionnez Enregistrer.



<--------------->


<img width="677" height="338" alt="image" src="https://github.com/user-attachments/assets/e669ebdc-0cc6-479c-9867-1b28162b7121" />




<---------------->



<img width="698" height="383" alt="image" src="https://github.com/user-attachments/assets/9f8772d5-f263-4a9e-935e-b9ae0dc79fba" />



L'application doit maintenant afficher les données de la base de données.
Cette étape confirme que la connexion d'appairage de VPC a été établie, car le VPC partagé ne dispose pas d'une passerelle Internet. Le seul moyen d'accéder à la base de données consiste à utiliser la connexion d'appairage de VPC.

# Tâche 5 : analyse des journaux de flux VPC
Dans le cadre de cette tâche, vous allez analyser les journaux de flux VPC pour comprendre le trafic entre l'application et la base de données des VPC appairés.
Accédez à l'onglet ou à la fenêtre du navigateur qui affiche ShareVPCFlowLogs.
Sélectionnez Log stream eni-**.
Après quelques minutes, le trafic réseau commence à s'afficher.
Notez le schéma du trafic dans les journaux, qui ressemble à ce qui suit :



<----------------->




<img width="558" height="221" alt="image" src="https://github.com/user-attachments/assets/d4bc5a73-3111-45c1-b97b-c93d2f24508d" />



<------------------->



<img width="516" height="294" alt="image" src="https://github.com/user-attachments/assets/239b2283-0cb0-4512-a05f-1d1d94a12598" />



<------------------->



# Conclusion
Félicitations ! Vous avez terminé avec succès les étapes suivantes :
créer une connexion d'appairage de VPC ;  
configurer des tables de routage pour utiliser la connexion d'appairage de VPC ;
activer des journaux de flux VPC pour fournir des informations sur les données circulant sur le réseau ;
créer une connexion d'appairage ;
analyser les journaux de flux VPC.

