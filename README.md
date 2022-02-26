### TD-3---Kubernetes
TD3 Kubernetes Ingénieur de spécialité Télécommunication et Informatique

##
## Exercice 1 - Installation
1. Installer la dernière version de Minikube
 
![Version minikube](https://user-images.githubusercontent.com/97112379/155618716-0742efb8-870c-402e-91dc-5091c699b972.png)

2. Vérifier que minikube est bien installée ( minikube version )
 -   minikube start

![verification du bon fonctionnement](https://user-images.githubusercontent.com/97112379/155618800-16a023b3-ce2f-4612-8210-e4309f96150c.png)

##
## Exercice 2 - Manipulation basique de pods

1. Avec la méthode impérative, créer un pod nginx avec pour nom nginx-pod-imperatif.

  - kubectl run nginx-pod-imperatif --image nginx:latest

  ![cretaion imperatif](https://user-images.githubusercontent.com/97112379/155623155-0725d947-966c-44c5-93d0-3a61c7231938.png)

  

2. Avec la méthode déclarative, créer un pod nginx avec pour nom nginx-pod-declaratif.
  
![nginx_declratifPod](https://user-images.githubusercontent.com/97112379/155627736-00ef3798-487d-45f1-bafd-841effcb72ac.png)

 - kubectl apply -f nginx-pod-declaratif.yml

![pod declaratif](https://user-images.githubusercontent.com/97112379/155624779-f1411ca3-4a82-4918-b956-d36357d3c843.png)

Visualisation des podes créés.
- kubectl get pods

![verification de la creation ](https://user-images.githubusercontent.com/97112379/155624964-4f607f84-e5c9-4fa7-bba9-42cd486a297c.png)


3. Avec la méthode impérative, créer un script shell permettant la création de 10 pods nginx nommé de nginx-1 à nginx-10

 - for i in {1..10}; do kubectl run nginx-pod-imperatif-$i --image nginx:latest ; done
 
  ![creation_10Pods](https://user-images.githubusercontent.com/97112379/155683403-51f2f0cf-a913-4440-a4a2-f16c2525502b.png)

4. Stocker le nom et l’adresse IP de tous les pods dans un fichier nommé all-pods.txt

 - kubectl get pods -o custom-columns=NAME:.metadata.name,IP:.status.podIP > all-pods.txt

  ![Recup_IP](https://user-images.githubusercontent.com/97112379/155684233-4a3ceca7-8474-41db-8b3a-4eebbe23217a.png)

5. Supprimer l’ensemble des pods créés pour cet exercice.

  - kubectl delete --all
  
![suppression_all nodes](https://user-images.githubusercontent.com/97112379/155684681-ab38ff9f-2cdb-4bf3-ab41-de5bf88ba7ac.png)

##  
##  Exercice 3 - Manipulation de replicasets

1. Créer un réplicaset nommé webapp-replicaset-imperatif créer à partir de l’image que
vous avez poussé sur votre repository lors du précédent TP ( si vous n’avez pas fait
l’exercice partir d’une image nginx ) de manière impérative.

![imperatif-declaration](https://user-images.githubusercontent.com/97112379/155709039-7a3c2115-f653-42ad-b9ec-c68900ba7e36.png)

- kubectl create -f webapp-replicaset-imperatif.yml

2. Créer un réplicaset nommé webapp-replicaset-declaratif créé à partir de l’image que vous
avez poussé sur votre repository lors du précédent TP ( si vous n’avez pas fait l’exercice
partir d’une image nginx ) de manière impérative.

- Duplication du  fichier webapp-replicaset-declaratif.yaml et changement du nom par celui de la consigne.

- execution de la commande declarative pour la crétion du replicaset

- cp webapp-replicaset-declaratif.yaml webapp-replicaset-imperatif.yaml

- kubectl apply -f webapp-replicaset-declaratif.yml

Vérifications :

![verif replicatset](https://user-images.githubusercontent.com/97112379/155709937-18821855-ffb9-40af-8074-d50465f91931.png)

3. Scaler le premier replicas à 5 instances de manière impérative.

- kubectl scale replicaset webapp-replicaset-imperatif --replicas 5

![visu 5 replicas](https://user-images.githubusercontent.com/97112379/155711706-12e5dc86-4a4d-4e87-ac39-29e71fc17072.png)

4. Scaler le second replicas à 7 instances de manière déclarative.

![scal_7](https://user-images.githubusercontent.com/97112379/155711084-7deb8bd5-d00b-4756-a9c6-6b305f78e2c2.png)

- kubectl apply -f webapp-replicaset-declaratif.yml

![7 replicas](https://user-images.githubusercontent.com/97112379/155712001-b31dff0d-f534-4bf3-a3b8-ec327578e835.png)


5. Quel mécanisme proposé par Kubernetes devrons-nous utiliser ici pour exposer nos
applications sur le web ?

- Le mécanisme que nous devrons utiliser ici est le service discovery fourni par Kubernetes. Il permet d'exposer le service vers l'extérieur du cluster notement avec NodePort à l'aide du NAT (la plage de ports autorisés est entre 30000 et 32767).

![service NodePort](https://user-images.githubusercontent.com/97112379/155725981-903ba091-dae8-463a-b89b-f60ed7b3ebdd.png)
![service NodePort2](https://user-images.githubusercontent.com/97112379/155725995-4b19b830-c5ac-46de-817f-064095edf866.png)

6. Supprimer les 2 replicasets.

![sup replicatSet](https://user-images.githubusercontent.com/97112379/155713340-92592514-cece-4ca7-a42f-6b31779a2725.png)

![sup replicatSet2](https://user-images.githubusercontent.com/97112379/155713409-30b0e1e5-cade-4c18-9e4f-eaef640765f1.png)

##
## Exercice 4 - Manipulation de déploiements.

1. Créer un deployment nommé nginx-deployment-imperatif créer à partir de l’image
nginx:1.15.0

- kubectl create deployment nginx-deployment-imperatif --image nginx:1.15.0 

![imperatif_deployment](https://user-images.githubusercontent.com/97112379/155729878-7731862c-67d1-4f3a-8ac7-92cae767b707.png)

2. Créer un deployment nommé webapp-deployment-declaratif créer à partir de l’image
nginx:1.15.0

Création d'un manifest webapp-deployment-declaratif.

![deployement_declaratif](https://user-images.githubusercontent.com/97112379/155732471-41fe8dc0-12f0-4c08-a3fb-0051b13722b1.png)


- kubectl apply -f webapp-deployment-declaratif.yaml

![deployement_declaratif](https://user-images.githubusercontent.com/97112379/155732152-6cebbc18-7bcf-4c21-a61d-800df09da6b5.png)


3. Lister les déploiements présents dans votre cluster.

- kubectl get deployments.apps

![list deployements](https://user-images.githubusercontent.com/97112379/155732984-9c2f6e3e-6e8d-41de-b326-7ccd0b522302.png)


4. Upgrader l’image du premier déploiement de manière impérative vers la dernière version
de nginx.

- kubectl set image deployment nginx-deployment-imperatif nginx=nginx:latest

![update image-imperatif](https://user-images.githubusercontent.com/97112379/155733383-221fc228-3455-44b3-91b3-f70727deac6d.png)


5. Upgrader l’image du dernier déploiement de manière déclarative vers la dernière version
de nginx.

modification du manifest webapp-deployment-declaratif avec l'image nginx:latest
- kubectl apply -f webapp-deployment-declaratif.yaml


6. Lister les replica sets présent dans votre cluster.

![liste_des replicas](https://user-images.githubusercontent.com/97112379/155735069-84eead69-b27c-44ed-b4a0-7115214a9e09.png)

7. Qu’en constatez-vous ?
- Je constate qu'il y a quatre replicas, on aurait pu supposer que les replicas anciennement upgradés seraient détruits.
- Les replicas les plus agés sont à 0 sur les paramètres (DESIRED, CURRENT et READY)
- Les autres sont à 1.
On peut donc en conclure que qu'il y a eu une bascule automatique sur du service sur les replicas Upgradés.
Les autres sont disponible en cas de roolback.


10. Faire un rollback impératif à la version antérieure des deux déploiements.

- kubectl rollout undo deployment nginx-deployment-imperatif webapp-deployment-declaratif

![roll_back](https://user-images.githubusercontent.com/97112379/155737380-c0dcbc70-50ca-43bb-a2bf-67135a683f56.png)

11. Supprimer les deux déploiements.

- kubectl delete deployments.apps nginx-deployment-imperatif
- kubectl delete deployments.apps webapp-deployment-declaratif
- kubectl get deployments.apps

![delete_deploy](https://user-images.githubusercontent.com/97112379/155747487-3201b3e7-5706-4ce6-b5b7-063220812236.png)

##
## Exercice 5 - Manipulation de Services

1. Créer un déploiement nginx-deploiement à partir d’une image nginx.

- kubectl create deployment nginx-deployment --image nginx:latest

- kubectl get deployments.apps

![deploy_nginxLatest](https://user-images.githubusercontent.com/97112379/155760276-e8fa598c-c954-4f8d-9a4e-4ee077b2c2da.png)


2. Lier les containers du déploiement nginx-deployment avec un nouveau service de type
  ClusterIp nommer nginx-svc-cluster-ip.
  
 - kubectl expose deployment nginx-deployment --type ClusterIP --port=8080 --target-port=80 --name=nginx-svc-cluster-ip

 
 
 ![service NodePort](https://user-images.githubusercontent.com/97112379/155808574-0960f71d-4fba-40f7-98e5-d696083b5ea8.png)


3. Récupérer l’adresse IP du service et le stocker dans un fichier nommer service-ip.txt

- kubectl get services nginx-svc-cluster-ip -o custom-columns=SERVICE-IP:.spec.clusterIP > service-ip.xt

![Recup_IP](https://user-images.githubusercontent.com/97112379/155808822-0ec7deba-c771-4a01-a991-c325294d5bf6.png)

4. Créer un pods nommé utils à partir d’une image nginx.

- kubectl run utils --image nginx:latest

- kubectl get pods

![Pod-utils](https://user-images.githubusercontent.com/97112379/155802260-34139207-e4af-4a0e-bce4-8cc63721e019.png)


6. Se connecter au pods utils ( kubectl exec -ti <nom-du-pod> – /bin/bash )
 
 - kubectl exec -ti utils /bin/bash
 
 ![encore des soucis](https://user-images.githubusercontent.com/97112379/155810098-d84b8dba-b84a-4716-b6ba-768aa77d4371.png)

 
7. Installer curl
 
 Curl est déjà installé.
  
8. Lancer un curl sur le service nginx-svc-cluster-ip.
 
 ![tjrs des problemes](https://user-images.githubusercontent.com/97112379/155810492-1cef9558-46f6-4ddd-b6b8-2055ffbd0b72.png)
  
 Je fini le TD et reviendrais sur cette problématique car tout semble correct !!!!
 
9. Avec vos mots, expliquez le concept de service dans kubernetes.
 
 - On peut expliquer le concept de service dans kubernetes comme un module au dessus des pods qui permet la communication inter pods ou d'exposer les services portés par les pods vers l'extérieur. Ceci en leurs attribue une adresse IP propre et ou un nom DNS unique, afin de permettre leur accessibilité et aussi équilibrer la charge entre eux.
On a constaté que les pods ont une durée de vie très limité et sont à maintes reprises créés et détruits, ce qui par conséquent altère continuellement leurs adresses IP. Aussi le service confère une stabilité au niveau de l'accessibilité.
  
10. Avec vos mots, expliquez les différences entre un service de type LoadBalancer, ClusterIp
&& NodePort.
 
- ClusterIP : Il expose le Service sur une adresse IP interne du cluster. De ce fait, le service n'est accessible que depuis l'intérieur du cluster.
 
- NodePort : Il expose le service vers l'extérieur du cluster à l'aide du NAT.
 
- LoadBalancer : Il utilise l’équilibreur de charge des fournisseurs de cloud. Ainsi, les services NodePort et ClusterIP sont créés automatiquement et sont acheminés par l'équilibreur de charge externe.

##
## Exercice 6 - Manipulation de Configmaps.

1. Générer un confimaps nommer userdata avec pour valeur AGE=<votre-age>
PRENOM=<votre-prenom> stocker le manifeste généré par kubectl dans un fichier
nommer configmaps.yaml
  
 
 Génération du confimaps avec les infos ci-dessus. 
 
- kubectl create configmap userdata --from-literal=AGE=24 --from-literal=PRENOM=Willy -o yaml --dry-run=client > configmaps.yaml
 
 ![generation du fichier confmap](https://user-images.githubusercontent.com/97112379/155819826-def80fed-c9bf-4518-b397-22b12bbc0014.png)

 
  
2. Créez votre configmaps avec la méthode déclarative.
- kubectl apply -f configmaps.yaml
   configmap/userdata created
 
3. Créer un pod nommé nginx-pod avec une image nginx
 
 ![nginx-pod5-3](https://user-images.githubusercontent.com/97112379/155820370-698b3098-2c9e-47b6-abc0-a4d29bce1e0b.png)

  
4. Stocker la valeur AGE du configmaps userdata dans la variable d’environnement
USER_YEAR du pod nginx-pod
 
 ![variable env5-4](https://user-images.githubusercontent.com/97112379/155820795-46b2f6c4-88cd-4f21-8c87-8592eb5712ed.png)

  
5. Stocker la valeur PRENOM du configmaps userdata dans la variable d’environnement
USER_FIRST_NAME du pod nginx-pod
  
 ![variable env5-5](https://user-images.githubusercontent.com/97112379/155821057-225c7b04-ab82-4683-8c06-8961c3354546.png)
  
6. Créer votre pod avec la méthode déclarative.
 
- kubectl apply -f nginx-pod.yaml
 
 ![creation 5-6](https://user-images.githubusercontent.com/97112379/155821403-666556a8-f354-4a1a-89b5-6c03d7c298f8.png)

  
7. Se connecter au pods en ssh avec la commande suivante ( kubect exec –ti <nom-du-pod>
– /bin/bash )
 
 J'ai des problème avec mon bash !!
 ![Probleme avec mon bash](https://user-images.githubusercontent.com/97112379/155821505-24eccee8-28ee-45ee-a163-6e2e368fbbc5.png)

  
8. Afficher les variables d’environnement (USER_FIRST_NAME & USER_YEAR)

 /# echo "$USER_FIRST_NAME a $USER_YEAR ans"

 Le résultat devrait être : willy a 24 ans
