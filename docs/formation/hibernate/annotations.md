---
layout: default
title: "Annotations - Hibernate"
permalink: /formation/hibernate/annotations/
lang: fr
my_menu: menu-hibernate.html
---

## Les annotations

### Les annotations pour les entités

#### @Column

- A mettre au niveau d'un attribut.

##### Paramètres de l'annotation

- `nullable` de type booléen
- `name` permet de personnaliser le nom de la colonne en base de données.

#### @Entity

- Objectif : indiquer que l'objet est issue de la base de données.
- Provenance de l'annotation : javax.persistence.Entity
- A mettre au niveau de la classe.

#### @Enumerated

- Pour les données de type énumération.
- A mettre au niveau de l'attribut.

##### Paramètres de l'annotation

- Ajouter entre parenthèses `EnumType.STRING`.

##### Pour information

Il est possible d'utiliser un convertisseur (voir page sur les convertisseur).

#### @Table

- Avec le paramètre `name` il est possible alors de changer le nom de la table en base de données.
- A mettre au niveau de la classe.

#### @Transient

- Permet de ne pas ajouter la donnée en base.
- A mettre au niveau d'un attribut.

#### Property access ou field access

- Property access : concerne une méthode
- Field access : concerne un attribut (à privilégier)

### Les autres annotations

#### @Repository

Objectif : indiquer qu'il s'agit d'un repository.
Provenance de l'annotation : org.springframework.stereotype.Repository

#### @PersistenceContext

Objectif : dialoguer avec la base de données.
Exemple d'utilisation : sur une classe de type EntityManager dans le repository (javax.persistence.EntityManager).
Provenance de l'annotation : javax.persistence.PersistenceContext
