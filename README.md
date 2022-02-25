### TD-3---Kubernetes
TD3 Kubernetes Ingénieur de spécialité Télécommunication et Informatique

## Exercice 1 - Installation
1. Installer la dernière version de Minikube
 
![Version minikube](https://user-images.githubusercontent.com/97112379/155618716-0742efb8-870c-402e-91dc-5091c699b972.png)

2. Vérifier que minikube est bien installée ( minikube version )

![verification du bon fonctionnement](https://user-images.githubusercontent.com/97112379/155618800-16a023b3-ce2f-4612-8210-e4309f96150c.png)

## Exercice 2 - Manipulation basique de pods

1. Avec la méthode impérative, créer un pod nginx avec pour nom nginx-pod-imperatif.

  kubectl run nginx-pod-imperatif --image nginx:latest

  ![cretaion imperatif](https://user-images.githubusercontent.com/97112379/155623155-0725d947-966c-44c5-93d0-3a61c7231938.png)

  

2. Avec la méthode déclarative, créer un pod nginx avec pour nom nginx-pod-declaratif.
  
![nginx_declratifPod](https://user-images.githubusercontent.com/97112379/155627736-00ef3798-487d-45f1-bafd-841effcb72ac.png)

    
![pod declaratif](https://user-images.githubusercontent.com/97112379/155624779-f1411ca3-4a82-4918-b956-d36357d3c843.png)

Visualisation des podes créés.
kubectl get pods

![verification de la creation ](https://user-images.githubusercontent.com/97112379/155624964-4f607f84-e5c9-4fa7-bba9-42cd486a297c.png)


3. Avec la méthode impérative, créer un script shell permettant la création de 10 pods nginx
   nommé de nginx-1 à nginx-10
  for i in 10 ; do kubectl run -&i nginx-pod-imperatif –image nginx:latest done
  for i in 10 ; do kubectl run nginx-pod-imperatif-$i --image nginx:latest; done
  
4. Stocker le nom et l’adresse IP de tous les pods dans un fichier nommé all-pods.txt

kubectl get pods -o custom-columns=NAME:.metadata.name,IP:.status.podIP > all-pods.txt
kubectl get pods -A -o jsonpath='{range .items[*]}{@.status.podIP}{" "}{@.metadata.name}{"\n"}{end}' > all-pods.txt
kubectl get pods -l app=validate -n {namespace_name} -o custom-columns=ip:.status.podIP
cat all-pods.txt
  
  
5. Supprimer l’ensemble des pods créés pour cet exercice.
  kubectl delete --all
  
##  Exercice 3 - Manipulation de replicasets

1. Créer un réplicaset nommé webapp-replicaset-imperatif créer à partir de l’image que
vous avez poussé sur votre repository lors du précédent TP ( si vous n’avez pas fait
l’exercice partir d’une image nginx ) de manière impérative.

2. Créer un réplicaset nommé webapp-replicaset-declaratif créé à partir de l’image que vous
avez poussé sur votre repository lors du précédent TP ( si vous n’avez pas fait l’exercice
partir d’une image nginx ) de manière impérative.

3. Scaler le premier replicas à 5 instances de manière impérative.

5. Scaler le second replicas à 7 instances de manière déclarative.


7. Quel mécanisme proposé par Kubernetes devrons-nous utiliser ici pour exposer nos
applications sur le web ?

6. Supprimer les 2 replicasets.

## Exercice 4 - Manipulation de déploiements.

1. Créer un deployment nommé nginx-deployment-imperatif créer à partir de l’image
nginx:1.15.0

2. Créer un deployment nommé webapp-deployment-declaratif créer à partir de l’image
nginx:1.15.0

3. Lister les déploiements présents dans votre cluster.


4. Upgrader l’image du premier déploiement de manière impérative vers la dernière version
de nginx.

5. Upgrader l’image du dernier déploiement de manière déclarative vers la dernière version
de nginx.

6. Lister les replica sets présent dans votre cluster.


8. Qu’en constatez-vous ?


10. Faire un rollback impératif à la version antérieure des deux déploiements.


12. Supprimer les deux déploiements.

##Exercice 5 - Manipulation de Services

1. Créer un déploiement nginx-deploiement à partir d’une image nginx.


2. Lier les containers du déploiement nginx-deployment avec un nouveau service de type
  ClusterIp nommer nginx-svc-cluster-ip.
3. Récupérer l’adresse IP du service et le stocker dans un fichier nommer service-ip.txt


4. Créer un pods nommé utils à partir d’une image nginx.

6. Se connecter au pods utils ( kubectl exec -ti <nom-du-pod> – /bin/bash )
  
7. Installer curl
  
8. Lancer un curl sur le service nginx-svc-cluster-ip.
  
9. Avec vos mots, expliquez le concept de service dans kubernetes.
  
10. Avec vos mots, expliquez les différences entre un service de type LoadBalancer, ClusterIp
&& NodePort.
  
## Exercice 6 - Manipulation de Configmaps.

1. Générer un confimaps nommer userdata avec pour valeur AGE=<votre-age>
PRENOM=<votre-prenom> stocker le manifeste généré par kubectl dans un fichier
nommer configmaps.yaml
  
2. Créez votre configmaps avec la méthode déclarative.
  
3. Créer un pod nommé nginx-pod avec une image nginx
  
4. Stocker la valeur AGE du configmaps userdata dans la variable d’environnement
USER_YEAR du pod nginx-pod
  
5. Stocker la valeur PRENOM du configmaps userdata dans la variable d’environnement
USER_FIRST_NAME du pod nginx-pod
  
6. Créer votre pod avec la méthode déclarative.
  
7. Se connecter au pods en ssh avec la commande suivante ( kubect exec –ti <nom-du-pod>
– /bin/bash )
  
8. Afficher les variables d’environnement (USER_FIRST_NAME & USER_YEAR
