# Rapport : Déploiement d’Applications avec Helm Charts et ArgoCD

## Introduction
Ce projet consiste à utiliser Helm pour gérer les déploiements sur un cluster Kubernetes et à intégrer ArgoCD pour le déploiement continu. Nous avons créé des Helm Charts pour déployer une application MERN composée de MongoDB, d'un serveur Node.js, et d'un client React. L'outil ArgoCD est utilisé pour automatiser le déploiement continu à partir d'un dépôt Git hébergeant les charts Helm.

## Architecture du Projet
L'architecture du projet est basée sur trois composants principaux, chacun déployé à l'aide de Helm Charts et géré via ArgoCD :
- MongoDB : Base de données NoSQL utilisée par l'application.
- Serveur MERN : API Node.js qui sert de backend pour l'application.
- Client MERN : Interface React consommant les services du serveur
````
        mern-charts/             
        │   ├── mongodb/             
        │   │   ├── Chart.yaml       
        │   │   ├── values.yaml      
        │   │   ├── templates/       
        │   │   │   ├── deployment.yaml  
        │   │   │   ├── service.yaml     
        │   │   │   └── pvc.yaml         
        │   ├── server/              
        │   │   ├── Chart.yaml       
        │   │   ├── values.yaml      
        │   │   ├── templates/       
        │   │   │   ├── deployment.yaml  
        │   │   │   ├── service.yaml     
        │   │   │   └── ingress.yaml     
        │   ├── client/              
        │   │   ├── Chart.yaml       
        │   │   ├── values.yaml      
        │   │   ├── templates/       
        │   │   │   ├── deployment.yaml  
        │   │   │   ├── service.yaml     
        │   │   │   └── ingress.yaml  
````
## Étapes Réalisées
  1.  Télécharger le binaire Helm :
    - lien : https://github.com/helm/helm/releases
    - Vérification de l'installation de Helm avec la commande :
  ````
    helm version
  ````
  2. Création des Helm Charts pour l’application MERN
     
       - Création de trois charts Helm séparés pour MongoDB, le serveur, et le client.
       - Modification des fichiers values.yaml pour configurer chaque composant selon les besoins.
     
  3. Hébergement des Charts Helm dans un Dépôt Git
      ````
       cd ../
       git init
       git add mern-charts/
       git commit-m "Ajout des charts Helm"
       git remote add origin [URL_DU_DEPOT_GIT]
       git branch-M main
       git push-u origin main
      ````

  4. Installation d’ArgoCD et Accès à l’Interface
  ````
    //Créez un namespace dédié pour ArgoCD

       - kubectl create namespace argocd
       - kubectl get namespaces

    // Installation d’ArgoCD

      - kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

    // Vérifiez que les pods d’ArgoCD

      - kubectl get pods -n argocd
    
    
  ````
<div>
 
  <img src="https://github.com/user-attachments/assets/19941bb2-fcc0-4dea-a502-bf892defc729" alt="Capture d'écran de l'application React" width="300" />
</div>
  5. Configuration d’ArgoCD pour le Déploiement via Git
  
  - Modifiez le mot de passe:
    
<div>
  <img src="https://github.com/user-attachments/assets/ed1b63c6-3a63-4a78-81d2-0730fbbf9822" alt="Capture d'écran de l'application React" width="300" />
</div>

  ````
 - CliquezsurSettings(icône en forme d’engrenage) puis sur Repositories.
 - Cliquez sur Connect Repo using HTTPS ou Connect Repo using SSH,selon votre configuration.
 - Si votre dépôt est privé, vous devrez fournir des informations d’authentification (clé SSH ou token d’accès personnel).
  ````
 - Création de l'application mern-app dans ArgoCD, incluant la configuration des paramètres Helm, comme le nom de l’application, le dépôt Git, et le namespace de destination.
   <div>
       <img src="https://github.com/user-attachments/assets/eb555c57-3fe4-4a81-a681-411cd8f3d40e" alt="Capture d'écran de l'application React" width="300" />
   </div>
   
 6. Mise à Jour Continue avec ArgoCD 
      - Modification des charts Helm ou des fichiers de configuration et mise à jour du dépôt Git.
      - ArgoCD détecte les modifications et met à jour l'application automatiquement sans intervention manuelle.
    
7. Accès à l'Application Déployée
   
    - Ouvrir l'Éditeur de texte avec des privilèges administratifs.
    - Accéder au fichier hosts
    - Modifier le fichier hosts : 127.0.0.1    mern-app.local
    
8. Nettoyage des Ressources

  ````
    - kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    - kubectl delete namespace argocd
    - kubectl get namespaces 

  
  ````
### Images du Projet
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 16px; padding: 16px; background-color: #f9f9f9; border: 1px solid #ccc; border-radius: 8px;">
  <img src="https://github.com/user-attachments/assets/a4801b97-25bf-40f4-a5c5-863755b28f81" alt="Capture d'écran de l'application React" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);" />
  <img src="https://github.com/user-attachments/assets/b2010800-4b10-458e-9a72-451f4846d335" alt="Capture d'écran de l'application React" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);" />
  <img src="https://github.com/user-attachments/assets/8af8a693-de4a-436c-b7ad-fb469287ad63" alt="Capture d'écran de l'application React" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);" />
  <img src="https://github.com/user-attachments/assets/0445529a-a209-4746-84ef-7d7cf8b233ed" alt="Capture d'écran de l'application React" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);" />
  <img src="https://github.com/user-attachments/assets/83c5c900-6b2e-469e-9c85-497e82e402d1" alt="Capture d'écran de l'application React" style="width: 100%; border-radius: 8px; box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);" />
</div>


