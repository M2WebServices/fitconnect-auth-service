# 🔐 README – `fitconnect-auth-service`

# FitConnect – Auth Service

Service responsable de la gestion des utilisateurs et de l’authentification.

---

## Responsabilités

- Création de compte (signup)
- Connexion (login)
- Gestion des mots de passe (hash)
- Génération de JWT
- Validation des tokens
- Exposition du type `User` en GraphQL

---

## Stack

- NestJS (TypeScript)
- PostgreSQL (schéma `auth`)
- Redis (sessions / tokens invalidés)
- gRPC (vers les autres services)
- GraphQL (sous-schéma fédéré)

---

## Modèle PostgreSQL (schéma `auth`)

```sql
CREATE SCHEMA IF NOT EXISTS auth;

CREATE TABLE auth.user (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email TEXT NOT NULL UNIQUE,
  pseudo TEXT NOT NULL UNIQUE,
  password_hash TEXT NOT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT NOW()
);
