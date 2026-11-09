# TP 11 : Authentification JDBC / JPA

Nom : [Nom et prénom]
Filière : [Filière]

## Le projet

Dans les TP précédents, les utilisateurs étaient écrits dans le code et disparaissaient à chaque arrêt de l'application. Ici ils sont enregistrés dans MySQL, avec leurs rôles. Spring Security va les chercher dans la base au moment de la connexion.

## Outils

- Java 17, Maven, IntelliJ
- Spring Boot 3.5.11 (Web, Security, Data JPA, Thymeleaf)
- MySQL (XAMPP)
- Lombok

## Comment ça marche

- `User` et `Role` : deux entités liées par une relation ManyToMany.
- `UserRepository` et `RoleRepository` : accès à la base.
- `CustomUserDetailsService` : cherche l'utilisateur par son nom et donne ses rôles à Spring Security.
- `SecurityConfig` : règles d'accès et BCrypt pour les mots de passe.
- `DatabaseInitializer` : crée les rôles et les deux comptes au démarrage (seulement s'ils n'existent pas déjà).

## Lancer le projet

1. Démarrer MySQL dans XAMPP.
2. Lancer `SpringSecurityJpaApplication` dans IntelliJ.
3. Ouvrir http://localhost:8080/login

La base `security_db` et les tables sont créées toutes seules.

## Les comptes

| Utilisateur | Mot de passe | Rôles |
|---|---|---|
| admin | 1234 | ADMIN, USER |
| user | 1111 | USER |

## Mes tests

### 1. Connexion avec user

Après la connexion, la page d'accueil affiche le nom et le rôle : ROLE_USER.

<img width="377" height="271" alt="Capture d&#39;écran 2026-11-09 085215" src="https://github.com/user-attachments/assets/81060024-61b0-44e3-a7c1-6183c4a35195" />


### 2. Espace utilisateur avec user

Le compte `user` peut entrer dans l'espace utilisateur.

<img width="340" height="165" alt="Capture d&#39;écran 2026-11-09 085233" src="https://github.com/user-attachments/assets/b55b1b90-f637-4694-a83d-76e57cdec9c7" />


### 3. Espace admin avec user

Quand `user` essaie d'ouvrir `/admin/dashboard`, l'accès est refusé (erreur 403).

<img width="429" height="176" alt="Capture d&#39;écran 2026-11-09 085222" src="https://github.com/user-attachments/assets/797ccb10-0db2-42b5-99f8-d5fc26e1388f" />


### 4. Connexion avec admin

Le compte `admin` peut entrer dans l'espace administrateur.

<img width="334" height="163" alt="Capture d&#39;écran 2026-11-09 085256" src="https://github.com/user-attachments/assets/0d8bc22d-7036-4df7-ad10-e63fceb0a901" />


### 5. Admin dans l'espace utilisateur

Comme `admin` a aussi le rôle USER, il peut aussi ouvrir l'espace utilisateur.

<img width="328" height="162" alt="Capture d&#39;écran 2026-11-09 085305" src="https://github.com/user-attachments/assets/d514eefa-a458-4941-91c6-bcdab4aabe22" />



