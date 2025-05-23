# DevOps Bootcamp : Infrastructure GitOps Multi-Environnement

Ce projet est une démonstration complète de mes compétences en DevOps à travers une infrastructure Kubernetes versionnée, observable et sécurisée, construite dans une logique GitOps.

## 🎯 Objectifs

- Mettre en place une infrastructure Kubernetes avec trois environnements isolés : `dev`, `staging`, `prod`.
- Automatiser les déploiements via GitOps (CI/CD + ArgoCD ou équivalent).
- Ajouter de la supervision (Prometheus, Grafana), de la sécurité (Cert-manager), et de l'IaC (Terraform, Ansible).
- Structurer un projet reproductible et exploitable dans un contexte pro.

## 🛠️ Stack technique

- Kubernetes (MicroK8s)
- Kustomize (overlays par environnement)
- GitHub Actions (CI/CD)
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

## 📬 Contact / Suivi

Je documente l’évolution de ce projet sur [woulf.fr/blog](https://woulf.fr/blog).  
N'hésitez pas à me contacter si vous avez des retours ou des questions techniques.

✉️ corentinboucardpro@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/corentinboucard)
