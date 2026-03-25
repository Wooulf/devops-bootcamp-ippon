# DevOps Bootcamp : Infrastructure GitOps Multi-Environnement

Ce projet est une démonstration complète de mes compétences en DevOps à travers une infrastructure Kubernetes versionnée, observable et sécurisée, construite dans une logique GitOps.

[From craftsmanship to industrialization: Multi-environment GitOps with Argo CD and Kustomize on MicroK8s](https://dev.to/woulf/from-craftsmanship-to-industrialization-multi-environment-gitops-with-argo-cd-and-kustomize-on-205)

## 🎯 Objectifs

- Mettre en place une infrastructure Kubernetes avec trois environnements isolés : `dev`, `staging`, `prod`.
- Automatiser les déploiements via GitOps (CI/CD + ArgoCD ou équivalent).
- Ajouter de la supervision (Prometheus, Grafana), de la sécurité (Cert-manager), et de l'IaC (Terraform, Ansible).
- Structurer un projet reproductible et exploitable dans un contexte pro.

## 🛠️ Stack technique

- Kubernetes (MicroK8s)
- Kustomize (overlays par environnement)
- GitHub Actions (CI)
- Prometheus / Grafana (Monitoring)
- Cert-Manager (HTTPS auto)
- Terraform, Ansible (Infra-as-Code)
- Docker (Packaging applicatif)
- GitOps (git = source de vérité)

## 🗂️ Arborescence

```bash
.
├── environments/
│   ├── dev/         # Déploiement dédié au développement
│   ├── staging/     # Environnement de préproduction
│   └── prod/        # Production simulée
├── base/            # Composants K8s communs à tous les environnements
├── README.md
```

💡 Ce projet fait suite à une première mise en place GitOps sur mon portfolio perso (voir [infra-k8s-terraform](https://github.com/Wooulf/infra-k8s-terraform)).


Chaque environnement utilise un overlay Kustomize spécifique, dérivé des manifestes génériques stockés dans `base/`. Cela respecte les bonnes pratiques GitOps : séparation des responsabilités, versioning, et portabilité.

## 🔄 CI/CD

Les pipelines GitHub Actions sont utilisés pour la phase CI (build des images, tests, push vers un registre).  
Le déploiement, quant à lui, est déclenché automatiquement par ArgoCD, qui observe l’état du dépôt Git et synchronise le cluster en conséquence.  
Cela respecte la philosophie GitOps : Git devient la source de vérité, et tout changement validé est automatiquement appliqué dans l’environnement cible.

## 📌 Pourquoi cette structure ?

- **Isolation** : chaque env est indépendant, ce qui permet des tests et déploiements ciblés.
- **Réutilisabilité** : les configs de `base/` sont DRY (Don't Repeat Yourself) et modulables.
- **Lisibilité** : logique claire, alignée avec les standards Kustomize et GitOps.

## Utilisation de **Argo CD Image Updater**

Pour les déploiements, j'utilise donc ce repo surveillé par Argo CD afin de décider quelle version d'image va tourner sur chaque environnement (dans la continuité de la logique GitOps)...  
Afin de ne pas avoir besoin de réaliser un commit manuellement à chaque mise à jour de mon application, sur mon repo d'infra (étant donné qu'ils sont séparés), il y a un outil `Argo CD Image Updater` qui permet de faire automatiquement des commits ou PR à valider, avec la nouveau tag de version d'une image.
Néanmoins, je pourrais être amené à faire beaucoup de déploiements notamment sur la branche dev, et il n'est pas très utile d'avoir des commits qui viendraient polluer à propos de ceci.  
Afin de résoudre ce problème, je viens donc utiliser un tag dev-latest, et j'utilise `Argo CD Image Updater` pour vérifier le changement de **digest** vers lequel pointe le tag dev-latest, afin de mettre à jour le déploiement.  
Ainsi, je me retrouve avec un léger compromis de vérité trouvable sur mon registry DockerHub, mais qui est très facile à accéder, et qui me permet de garder un historique de commits propres. 

## 📬 Contact / Suivi

Je documente l’évolution de ce projet sur [woulf.fr/blog](https://woulf.fr/blog).  
N'hésitez pas à me contacter si vous avez des retours ou des questions techniques.

✉️ corentinboucardpro@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/corentinboucard)
