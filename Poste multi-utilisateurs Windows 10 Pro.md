---
title: Poste multi-utilisateurs Windows 10 Pro

---

# Rapport technique — Poste multi-utilisateurs Windows 10 Pro

## 1. Introduction

Dans le cadre de ce projet, j'ai configuré une machine virtuelle fonctionnant sous **Windows 10 Pro** afin de mettre en place un environnement multi-utilisateurs.

L'objectif principal est de créer plusieurs comptes avec des niveaux de permissions différents, de protéger les dossiers personnels des utilisateurs et de mettre en place des mesures de sécurité concernant les mots de passe et le verrouillage des sessions.

La machine virtuelle utilisée pour ce projet est nommée :

**VM-WIN10-MULTIUSER**

---

## 2. Architecture de la machine

### Système d'exploitation

* Système : **Windows 10 Pro**
* Type : **Machine virtuelle**
* Nom de la machine : **VM-WIN10-MULTIUSER**
* Utilisation : **Poste multi-utilisateurs**

### Architecture des comptes

| Compte           | Type           | Utilisation                  |
| ---------------- | -------------- | ---------------------------- |
| AdminMaintenance | Administrateur | Maintenance et configuration |
| Utilisateur1     | Standard       | Utilisation quotidienne      |
| Utilisateur2     | Standard       | Utilisation quotidienne      |
| Utilisateur3     | Standard       | Utilisation quotidienne      |

Le compte **AdminMaintenance** est destiné uniquement aux opérations de maintenance et d'administration. Les comptes utilisateurs sont des comptes standards afin de limiter leurs privilèges.
![Capture d'écran 2026-09-15 104421](https://hackmd.io/_uploads/Hyy5HqLYGe.png)

---

## 3. Installation du système d'exploitation

Une machine virtuelle a été créée dans **VMware Workstation** afin d'installer Windows 10 Pro.

Un espace disque de **60 Go** a été attribué à la machine virtuelle.

Après la création de la machine virtuelle, l'installation de Windows 10 Pro a été effectuée à partir d'une image ISO.

Une fois l'installation terminée, le nom du PC a été configuré avec :

```text
VM-WIN10-MULTIUSER
```

### Capture d'écran

![Capture d'écran 2026-09-15 084706](https://hackmd.io/_uploads/B11iZqUFzx.png)

![Capture d'écran 2026-09-15 084626](https://hackmd.io/_uploads/By0uZqUKfx.png)

![Capture d'écran 2026-09-15 094716](https://hackmd.io/_uploads/rym1zq8tfx.png)



---

# 4. Création du compte administrateur

Un compte administrateur dédié à la maintenance a été créé :

```text
AdminMaintenance
```

Ce compte possède les droits administrateur sur la machine.

Il n'est pas destiné à être utilisé pour les tâches quotidiennes. Son utilisation est réservée aux opérations nécessitant des privilèges élevés, comme la modification des paramètres système, la gestion des utilisateurs ou la configuration de la sécurité.

### Objectif

La séparation entre le compte administrateur et les comptes standards permet de limiter les risques liés à une utilisation quotidienne avec des privilèges administrateur.

### Capture d'écran

![Capture d'écran 2026-09-15 094749](https://hackmd.io/_uploads/ByzbGqUFzg.png)
![Capture d'écran 2026-09-15 094759](https://hackmd.io/_uploads/Syt-M5UKfl.png)
![Capture d'écran 2026-09-15 095148](https://hackmd.io/_uploads/SkPfMq8Ffe.png)
![Capture d'écran 2026-09-15 095658](https://hackmd.io/_uploads/H1xQMcLKfg.png)
![Capture d'écran 2026-09-15 095710](https://hackmd.io/_uploads/Skj7z98Fze.png)
![image](https://hackmd.io/_uploads/HJS5zqLYfg.png)


---

# 5. Création des comptes utilisateurs standards

Trois comptes utilisateurs standards distincts ont été créés :

```text
Utilisateur1
Utilisateur2
Utilisateur3
```

Ces comptes ne disposent pas des privilèges administrateur.

Cette configuration permet à chaque utilisateur d'utiliser la machine sans pouvoir modifier librement les paramètres système nécessitant des droits élevés.

### Tableau récapitulatif

| Utilisateur      | Privilèges     |
| ---------------- | -------------- |
| AdminMaintenance | Administrateur |
| Utilisateur1     | Standard       |
| Utilisateur2     | Standard       |
| Utilisateur3     | Standard       |

### Capture d'écran
![Capture d'écran 2026-09-15 114022](https://hackmd.io/_uploads/HJApM5LKGx.png)

![image](https://hackmd.io/_uploads/Bkgaz5IFGx.png)

---

# 6. Protection des dossiers personnels

Windows crée automatiquement un dossier personnel pour chaque utilisateur dans :

```text
C:\Users\
```

Les dossiers sont donc organisés de la manière suivante :

```text
C:\Users\Utilisateur1
C:\Users\Utilisateur2
C:\Users\Utilisateur3
```

Chaque utilisateur dispose de son propre espace personnel.

Les permissions NTFS permettent de limiter l'accès aux fichiers personnels des autres utilisateurs.
![Capture d'écran 2026-09-15 114211](https://hackmd.io/_uploads/rySG75Utfx.png)

![image](https://hackmd.io/_uploads/S16-7qIYfg.png)

---

## 6.1 Création d'un fichier de test

Pour vérifier le fonctionnement des permissions, un fichier de test a été créé dans le dossier personnel de `Utilisateur1`.

Chemin :

```text
C:\Users\Utilisateur1\Documents\FichierUtilisateur1.txt
```

Le fichier contient un texte permettant de vérifier qu'il appartient bien à `Utilisateur1`.

### Capture d'écran

![Capture d'écran 2026-09-15 105920](https://hackmd.io/_uploads/SyC4X9LtMx.png)


---

# 7. Test du cloisonnement entre utilisateurs

Afin de vérifier que les utilisateurs ne peuvent pas accéder aux fichiers personnels des autres, un test a été réalisé.

Après avoir créé le fichier avec `Utilisateur1`, la session a été fermée puis une connexion avec `Utilisateur2` a été effectuée.

`Utilisateur2` a ensuite essayé d'accéder au dossier :

```text
C:\Users\Utilisateur1\Documents
```

L'accès au contenu personnel de l'autre utilisateur a été refusé.

Cela démontre que les permissions du système permettent de protéger les données personnelles entre les différents comptes standards.

### Résultat du test

| Action                                                    | Résultat   |
| --------------------------------------------------------- | ---------- |
| Utilisateur1 accède à ses propres fichiers                | ✅ Autorisé |
| Utilisateur2 tente d'accéder aux fichiers de Utilisateur1 | ❌ Refusé   |
| Utilisateur3 tente d'accéder aux fichiers de Utilisateur1 | ❌ Refusé   |

### Capture d'écran
![Capture d'écran 2026-09-15 114431](https://hackmd.io/_uploads/H1ljQcLtfl.png)



---

# 8. Vérification des permissions NTFS

Les permissions du dossier utilisateur peuvent être consultées depuis les propriétés du dossier.

Pour cela :

**Clic droit sur le dossier → Propriétés → Sécurité**

Les permissions permettent notamment de déterminer quels comptes peuvent accéder au dossier, le modifier ou en consulter le contenu.

Cette configuration contribue au cloisonnement des données entre les différents utilisateurs.

### Capture d'écran
![Capture d'écran 2026-09-15 110752](https://hackmd.io/_uploads/ByIJ498tfl.png)
![Capture d'écran 2026-09-15 110804](https://hackmd.io/_uploads/S1TeEcUKzg.png)

![image](https://hackmd.io/_uploads/rkdqm5IKGg.png)

---

# 9. Politique de mots de passe

Une politique de mots de passe a été mise en place afin d'améliorer la sécurité des comptes utilisateurs.

La stratégie prévoit notamment les paramètres suivants :

| Paramètre                    |          Valeur |
| ---------------------------- | --------------: |
| Longueur minimale            |   10 caractères |
| Complexité                   |         Activée |
| Historique des mots de passe | 5 mots de passe |
| Durée de vie maximale        |        90 jours |
| Durée de vie minimale        |          1 jour |

La complexité des mots de passe permet d'éviter l'utilisation de mots de passe trop simples et facilement devinables.

> **Remarque :** la configuration de cette stratégie nécessite des privilèges administrateur.

### Configuration

La stratégie est accessible avec :

```text
Windows + R
```

puis :

```text
secpol.msc
```

Ensuite :

```text
Stratégies de compte
→ Stratégie de mot de passe
```

### Capture d'écran
![Capture d'écran 2026-09-15 111500](https://hackmd.io/_uploads/HyFS49IFfe.png)

![Capture d'écran 2026-09-15 111952](https://hackmd.io/_uploads/Hy6EEqItzx.png)


---

# 10. Politique de verrouillage automatique

Une politique de verrouillage automatique de la session a été configurée afin de protéger le poste lorsqu'un utilisateur reste inactif.

La session est configurée pour demander une nouvelle authentification après une période d'inactivité de :

**5 minutes**

L'utilisateur doit alors saisir à nouveau son mot de passe pour accéder à sa session.

Cette mesure permet de limiter les risques d'accès non autorisé lorsqu'un utilisateur quitte temporairement son poste.

### Configuration

La configuration est accessible depuis les paramètres de l'écran de veille.

L'option permettant de demander l'ouverture de session lors de la reprise a été activée.

### Capture d'écran
![Capture d'écran 2026-09-15 111236](https://hackmd.io/_uploads/Bk1FN5UKfe.png)
![Capture d'écran 2026-09-15 111325](https://hackmd.io/_uploads/B1utN9IYGx.png)



---

# 11. Test du verrouillage automatique

Un test a été effectué afin de vérifier le fonctionnement du verrouillage automatique.

La session a été laissée inactive pendant la durée configurée.

Après cette période, Windows a verrouillé la session et a demandé une nouvelle authentification.

### Résultat

**Résultat : ✅ Conforme**

Le verrouillage automatique fonctionne correctement.

### Capture d'écran

![image](https://hackmd.io/_uploads/rJ0_DpUFMl.png)



---

# 12. Test des différents comptes

Chaque compte a été testé individuellement afin de vérifier que les utilisateurs peuvent se connecter correctement.

### Tests réalisés

| Test                                               | Résultat      |
| -------------------------------------------------- | ------------- |
| Connexion avec Utilisateur1                        | ✅ Réussie     |
| Connexion avec Utilisateur2                        | ✅ Réussie     |
| Connexion avec Utilisateur3                        | ✅ Réussie     |
| Connexion avec AdminMaintenance                    | ✅ Réussie     |
| Accès de Utilisateur1 à ses fichiers               | ✅ Autorisé    |
| Accès de Utilisateur2 aux fichiers de Utilisateur1 | ❌ Refusé      |
| Accès de Utilisateur3 aux fichiers de Utilisateur1 | ❌ Refusé      |
| Verrouillage automatique                           | ✅ Fonctionnel |
| Politique de mot de passe                          | ✅ Configurée  |

---

# 13. Cloisonnement des permissions

L'organisation finale des comptes est la suivante :

```text
                    WINDOWS 10 PRO
                          │
              ┌───────────┴───────────┐
              │                       │
      AdminMaintenance           Comptes standards
      Administrateur                    │
              │              ┌─────────┼─────────┐
       Maintenance       Utilisateur1 Utilisateur2 Utilisateur3
                         Standard     Standard     Standard
```

Le compte administrateur est séparé des comptes utilisés quotidiennement.

Les comptes standards ne disposent pas des mêmes privilèges que le compte `AdminMaintenance`.

Les dossiers personnels sont également séparés afin de protéger les données de chaque utilisateur.

---

# 14. Résultats

Les objectifs du projet ont été réalisés :

* ✅ Installation de Windows 10 Pro sur une machine virtuelle.
* ✅ Création d'un compte administrateur dédié à la maintenance.
* ✅ Création de trois comptes utilisateurs standards.
* ✅ Mise en place du cloisonnement des dossiers personnels.
* ✅ Vérification des permissions NTFS.
* ✅ Mise en place d'une politique de mots de passe.
* ✅ Mise en place du verrouillage automatique de session.
* ✅ Tests réalisés avec les différents comptes.
* ✅ Vérification de l'accès refusé aux fichiers des autres utilisateurs.

---

# 15. Conclusion

La machine virtuelle **VM-WIN10-MULTIUSER** est maintenant configurée pour un usage multi-utilisateurs.

La séparation entre le compte administrateur et les comptes standards permet de réduire les privilèges accordés aux utilisateurs.

Les permissions NTFS permettent de protéger les dossiers personnels afin que les utilisateurs standards ne puissent pas consulter les données personnelles des autres comptes.

Enfin, la politique de mots de passe et le verrouillage automatique de la session apportent des mesures de sécurité supplémentaires.

Les différents tests réalisés montrent que le cloisonnement entre les utilisateurs fonctionne correctement et que la machine répond aux objectifs du projet.
