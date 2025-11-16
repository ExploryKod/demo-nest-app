# QuizApp - Application de Quiz Interactive

Application full-stack de quiz développée avec **NestJS** (backend) et **Angular** (frontend). 

Le projet nous a permis d'apprendre l'**Injection de Dépendances**, l'**Inversion de Contrôle**, le pattern **Ports & Adapters**, et le **CQRS**.

## 📌 Note Importante

**Ce projet est composé de deux parties distinctes :**

- **`quizzam` (API Backend)** : Développée **de A à Z** par notre groupe, cette API NestJS implémente tous les patterns architecturaux et fonctionnalités décrits dans ce document.
  - 📦 **Dépôt source** : [https://github.com/ExploryKod/quizzam](https://github.com/ExploryKod/quizzam) (historique Git complet)

- **`quizzy-front` (Application Frontend)** : Application Angular existante qui nous a servi de **support**. Nous l'avons adaptée pour s'intégrer avec notre API, notamment en ajoutant le support de l'authentification JWT et en adaptant les services pour communiquer avec notre backend.
  - 📦 **Dépôt source original** : [https://github.com/fhemery/quizzy-front](https://github.com/fhemery/quizzy-front) (avant nos modifications)
  - 🔧 **Dépôt modifié par notre groupe** : [https://github.com/ExploryKod/quizzy-front](https://github.com/ExploryKod/quizzy-front) (avec ajout d'un chat et nos adaptations)

**L'essentiel du travail de développement et d'architecture présenté ici concerne donc l'API `quizzam`.**

## 🎓 Ce Que Nous Avons Appris

Ce projet nous a permis, en tant que groupe, de développer et maîtriser les compétences suivantes :

### Architecture Logicielle
- ✅ **Pattern Ports & Adapters** : Séparation entre logique métier et infrastructure
- ✅ **CQRS (Command Query Responsibility Segregation)** : Séparation des opérations de lecture et d'écriture
- ✅ **Inversion de Contrôle (IoC)** : Gestion des dépendances par le framework
- ✅ **Injection de Dépendances (DI)** : Injection automatique des dépendances via NestJS
- ✅ **Architecture Modulaire** : Organisation en modules fonctionnels indépendants

### Technologies et Frameworks
- ✅ **NestJS** : Framework backend progressif avec support TypeScript natif
- ✅ **Angular** : Framework frontend avec architecture composants
- ✅ **TypeScript** : Typage statique pour une meilleure maintenabilité
- ✅ **Socket.io** : Communication temps réel via WebSockets

### Gestion des Bases de Données
- ✅ **Abstraction Multi-DB** : Support de MongoDB, Firebase et In-Memory
- ✅ **MongoDB** : Base de données NoSQL avec Mongoose
- ✅ **Firebase** : Backend-as-a-Service pour données et authentification
- ✅ **Pattern Repository** : Abstraction de l'accès aux données

### Authentification et Sécurité
- ✅ **JWT (JSON Web Tokens)** : Authentification basée sur tokens
- ✅ **Firebase Authentication** : Service d'authentification géré
- ✅ **Bcrypt** : Hachage sécurisé des mots de passe
- ✅ **Middleware d'authentification** : Protection des routes API

### Tests et Qualité
- ✅ **Tests End-to-End (E2E)** : Tests complets de l'API avec Supertest
- ✅ **Tests Unitaires** : Tests isolés des composants et services
- ✅ **Mocks et Stubs** : Simulation des dépendances pour les tests
- ✅ **Helpers de Test** : Utilitaires réutilisables pour les tests

### DevOps et Outils
- ✅ **Configuration d'Environnement** : Gestion des variables d'environnement
- ✅ **Docker** : Containerisation de MongoDB
- ✅ **Monorepo** : Gestion de plusieurs projets dans un seul dépôt
- ✅ **Git** : Gestion de version et collaboration en équipe

### Bonnes Pratiques
- ✅ **Séparation des Responsabilités** : Code modulaire et maintenable
- ✅ **Documentation** : README complet et guides détaillés
- ✅ **Sécurité** : Protection des informations sensibles (.gitignore)
- ✅ **Code Propre** : Respect des conventions et patterns établis

## 📋 Structure du Projet

Ce projet est un monorepo contenant deux applications principales :

```
quizapp/
├── quizzam/          # API Backend NestJS (développée de A à Z)
└── quizzy-front/     # Application Frontend Angular (support existant adapté)
```

### Détails des Applications

**`quizzam/` - API Backend**
- ✅ Développée entièrement par notre groupe
- ✅ Implémentation complète des patterns architecturaux (Ports & Adapters, CQRS, IoC, DI)
- ✅ Support multi-base de données (MongoDB, Firebase, In-Memory)
- ✅ Système d'authentification flexible (JWT, Firebase)
- ✅ Tests E2E et unitaires complets
- ✅ Documentation détaillée

**`quizzy-front/` - Application Frontend**
- 📝 Application Angular existante utilisée comme support
- 🔗 **Source originale** : [https://github.com/fhemery/quizzy-front](https://github.com/fhemery/quizzy-front)
- 🔧 **Dépôt modifié** : [https://github.com/ExploryKod/quizzy-front](https://github.com/ExploryKod/quizzy-front) (avec ajout d'un chat et nos modifications)
- ✨ **Adaptations effectuées par notre groupe** :
  - Intégration de l'authentification JWT
  - Adaptation des services pour communiquer avec l'API `quizzam`
  - Configuration de l'environnement pour pointer vers notre backend
  - Modification du service d'authentification pour supporter JWT et Firebase
  - Ajout d'un système de chat en temps réel

## 🎯 Contexte Technologique

### Backend (NestJS)

Le backend est construit avec **NestJS**, un framework Node.js progressif qui exploite :

- **Architecture Modulaire** : L'application est organisée en modules fonctionnels (Quiz, User, Auth, Chat, etc.)
- **Injection de Dépendances (DI)** : Le conteneur DI intégré de NestJS gère toutes les dépendances
- **Inversion de Contrôle (IoC)** : Les dépendances sont injectées plutôt que créées directement, permettant un couplage faible
- **Pattern Ports & Adapters** : Séparation claire entre la logique métier (ports) et l'infrastructure (adapters)

### Patterns Architecturaux Clés

#### 1. **Abstraction de Base de Données avec Ports & Adapters**

L'application supporte plusieurs backends de base de données (MongoDB, Firebase, In-Memory) via une interface unifiée :

```typescript
// Port (Interface)
export interface IQuizRepository {
  findAllFromUser(userId: string): Promise<getUserQuizDTO>;
  findById(id: string): Promise<Quiz | null>;
  create(quiz: CreateQuizDTO): Promise<string>;
  // ... autres méthodes
}

// Adapters (Implémentations)
- MongoQuizRepository      // Implémentation MongoDB
- FirebaseQuizRepository   // Implémentation Firebase
- InMemoryQuizRepository   // Implémentation In-Memory (tests)
```

**Fonctionnement du Changement de Base de Données :**

La base de données est sélectionnée à l'exécution via la variable d'environnement `DATABASE_NAME` :

```typescript
// Dans quiz.module.ts
function database(database: string) {
  switch (database) {
    case "MONGODB":
      return MongoQuizRepository;
    case "FIREBASE":
      return FirebaseQuizRepository;
    case "IN-MEMORY":
      return InMemoryQuizRepository;
  }
}

@Module({
  providers: [
    {
      provide: I_QUIZ_REPOSITORY,
      useClass: database(variables.database), // Sélection dynamique
    },
  ],
})
```

Ce pattern est appliqué à travers tous les modules :
- **Module Quiz** : `IQuizRepository` avec adapters MongoDB/Firebase/In-Memory
- **Module User** : `IUserRepository` avec adapters MongoDB/Firebase/In-Memory
- **Module Ping** : `IPingRepository` avec adapters MongoDB/Firebase/In-Memory

**Avantages de cette approche :**
- ✅ **Testabilité** : Facile de mocker les repositories pour les tests
- ✅ **Flexibilité** : Changer de base de données sans modifier la logique métier
- ✅ **Maintenabilité** : Séparation claire des responsabilités
- ✅ **Évolutivité** : Ajouter de nouveaux adapters sans modifier le code existant

#### 2. **CQRS (Command Query Responsibility Segregation)**

L'application utilise CQRS pour séparer les opérations de lecture et d'écriture :

**Commandes** (Opérations d'écriture) :
- `CreateQuizCommand`
- `UpdateQuizCommand`
- `AddQuestionCommand`
- `UpdateQuestionCommand`
- `DeleteQuizByIdQuery` (agit comme commande)

**Requêtes** (Opérations de lecture) :
- `GetUserQuizzes`
- `GetQuizByIdQuery`
- `GetQuizByExecutionIdQuery`
- `GetUserByIdQuery`

Chaque commande/requête est injectée avec le repository approprié :

```typescript
{
  provide: CreateQuizCommand,
  inject: [I_QUIZ_REPOSITORY],
  useFactory: (repository) => {
    return new CreateQuizCommand(repository);
  },
}
```

**Bénéfices du CQRS :**
- Séparation claire des responsabilités
- Optimisation indépendante des lectures et écritures
- Scalabilité améliorée
- Code plus maintenable

#### 3. **Abstraction de l'Authentification**

Similaire au changement de base de données, l'authentification peut être basculée entre JWT et Firebase :

```typescript
// Dans auth.module.ts
function getAuthRepository() {
  const authType = process.env.AUTH_TYPE || 'JWT';
  
  switch (authType.toUpperCase()) {
    case 'FIREBASE':
      return FirebaseAuthRepository;
    case 'JWT':
    default:
      return JwtAuthRepository;
  }
}
```

## 🧪 Tests

### Tests End-to-End (E2E)

Des tests end-to-end complets sont situés dans `quizzam/e2e/` :

- **Tests API Quiz** (`e2e/src/server/quiz.spec.ts`) : Teste tous les endpoints de quiz
- **Tests API User** (`e2e/src/server/user.spec.ts`) : Teste les endpoints de gestion d'utilisateurs
- **Tests Ping** (`e2e/src/server/ping.spec.ts`) : Teste l'endpoint de vérification de santé

**Helpers de Test :**
- `AuthHelper` : Crée des utilisateurs de test et gère l'authentification
- `QuizHelper` : Crée des quiz de test et gère les données de quiz

**Exécution des Tests E2E :**

```bash
cd quizzam
pnpm test:e2e
# ou
nx e2e quizzam
```

### Tests Unitaires

Les tests unitaires sont co-localisés avec les fichiers sources (`.spec.ts`) :

- `quiz.controller.spec.ts`
- `chat.gateway.spec.ts`
- `app.component.spec.ts` (frontend)

**Exécution des Tests Unitaires :**

```bash
# Backend
cd quizzam
pnpm test

# Frontend
cd quizzy-front
pnpm test
```

## 📦 Installation

### Prérequis

- **Node.js** (v18 ou supérieur)
- **pnpm** (v9.9.0+)
- **MongoDB** (si utilisation de MongoDB)
- **Compte Firebase** (si utilisation de Firebase)

### Installation Backend (`quizzam`)

1. **Naviguer vers le répertoire backend :**
   ```bash
   cd quizzam
   ```

2. **Installer les dépendances :**
   ```bash
   pnpm install
   ```

3. **Configurer les variables d'environnement :**
   ```bash
   cp .env.example .env
   ```

4. **Éditer le fichier `.env` :**
   ```env
   # Configuration Base de Données
   DATABASE_URL=mongodb://localhost:27017/quizapp
   DATABASE_NAME=MONGODB  # Options: MONGODB, FIREBASE, IN-MEMORY

   # Configuration Serveur
   PORT=3000
   GLOBAL_PREFIX=api

   # Configuration Authentification
   AUTH_TYPE=JWT  # Options: JWT, FIREBASE
   JWT_SECRET=votre-cle-secrete-changez-en-production

   # Firebase (uniquement si utilisation de Firebase)
   # FIREBASE_KEY_PATH=src/assets/quizzam-firebase-key.json
   ```

5. **Démarrer MongoDB** (si utilisation de MongoDB) :
   ```bash
   # Utilisant Docker
   docker run -d -p 27017:27017 --name mongodb mongo:latest

   # Ou utilisant le service système
   sudo systemctl start mongod
   ```

6. **Démarrer le backend :**
   ```bash
   pnpm start
   # ou
   nx serve quizzam
   ```

   L'API sera disponible à `http://localhost:3000/api`

### Installation Frontend (`quizzy-front`)

1. **Naviguer vers le répertoire frontend :**
   ```bash
   cd quizzy-front
   ```

2. **Installer les dépendances :**
   ```bash
   pnpm install
   ```

3. **Configurer l'environnement** (si nécessaire) :
   ```bash
   # Éditer src/environments/environment.development.ts
   export const environment = {
     baseUrl: 'http://localhost:3000',
     apiUrl: 'http://localhost:3000/api',
     authType: 'JWT', // ou 'FIREBASE'
   };
   ```

4. **Démarrer le frontend :**
   ```bash
   pnpm start
   # ou
   nx serve quizzy-front
   ```

   L'application sera disponible à `http://localhost:4200`

## 🔐 Configuration et Test de l'Authentification

### Types d'Authentification

L'application supporte deux méthodes d'authentification :

1. **Authentification JWT** (Par défaut)
   - Basée sur email/mot de passe
   - Tokens stockés dans localStorage
   - Aucune dépendance externe

2. **Authentification Firebase**
   - Utilise le SDK Firebase Auth
   - Nécessite la configuration d'un projet Firebase

### Test de l'Authentification JWT

#### Option 1 : Utilisation du Script de Test

```bash
cd quizzam
./test-auth.sh
```

Ce script va :
1. Enregistrer un utilisateur de test (ou se connecter s'il existe)
2. Obtenir un token JWT
3. Tester l'accès à un endpoint protégé

#### Option 2 : Test Manuel avec cURL

**1. Enregistrer un nouvel utilisateur :**
```bash
curl -X POST http://localhost:3000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "testpassword123",
    "username": "TestUser"
  }'
```

**Réponse Attendue :**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "email": "test@example.com",
    "uid": "user_1234567890_abc123",
    "username": "TestUser"
  }
}
```

**2. Se connecter avec un utilisateur existant :**
```bash
curl -X POST http://localhost:3000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "testpassword123"
  }'
```

**3. Accéder à un endpoint protégé :**
```bash
curl -X GET http://localhost:3000/api/users/me \
  -H "Authorization: Bearer VOTRE_TOKEN_ICI"
```

**4. Obtenir les quiz de l'utilisateur :**
```bash
curl -X GET http://localhost:3000/api/quiz \
  -H "Authorization: Bearer VOTRE_TOKEN_ICI"
```

#### Option 3 : Test via Frontend

1. **Démarrer le backend et le frontend :**
   ```bash
   # Terminal 1 - Backend
   cd quizzam && pnpm start

   # Terminal 2 - Frontend
   cd quizzy-front && pnpm start
   ```

2. **Ouvrir le navigateur :** `http://localhost:4200`

3. **S'enregistrer/Se connecter :**
   - Cliquer sur "Register" ou "Login"
   - Utiliser les identifiants :
     - Email : `test@example.com`
     - Mot de passe : `testpassword123`
     - Nom d'utilisateur : `TestUser`

4. **Vérifier l'authentification :**
   - Ouvrir DevTools → Application → Local Storage
   - Chercher les clés `jwt_token` et `jwt_user`

### Identifiants de Test

Après avoir exécuté le script de test ou enregistré manuellement :

- **Email :** `test@example.com`
- **Mot de passe :** `testpassword123`
- **Nom d'utilisateur :** `TestUser`

## 🗄️ Configuration de la Base de Données

### Configuration MongoDB

1. **Installer MongoDB :**
   ```bash
   # Utilisant Docker (recommandé)
   docker run -d -p 27017:27017 --name mongodb mongo:latest
   ```

2. **Configurer `.env` :**
   ```env
   DATABASE_URL=mongodb://localhost:27017/quizapp
   DATABASE_NAME=MONGODB
   ```

3. **Vérifier la connexion :**
   ```bash
   curl http://localhost:3000/api/ping
   ```

### Configuration Firebase

1. **Créer un projet Firebase** sur [Firebase Console](https://console.firebase.google.com/)

2. **Télécharger la clé du compte de service :**
   - Aller dans Paramètres du Projet → Comptes de Service
   - Générer une nouvelle clé privée
   - Sauvegarder comme `quizzam-firebase-key.json` dans `quizzam/src/assets/`

3. **Configurer `.env` :**
   ```env
   DATABASE_NAME=FIREBASE
   FIREBASE_KEY_PATH=src/assets/quizzam-firebase-key.json
   # OU
   GOOGLE_APPLICATION_CREDENTIALS=/chemin/vers/firebase-key.json
   ```

### Configuration In-Memory (Tests)

Pour tester sans base de données :

```env
DATABASE_NAME=IN-MEMORY
```

**Note :** Les données sont perdues au redémarrage du serveur.

## 🚀 Exécution de l'Application

### Mode Développement

**Backend :**
```bash
cd quizzam
pnpm start
# API : http://localhost:3000/api
```

**Frontend :**
```bash
cd quizzy-front
pnpm start
# App : http://localhost:4200
```

### Build de Production

**Backend :**
```bash
cd quizzam
pnpm build
# Sortie : dist/
```

**Frontend :**
```bash
cd quizzy-front
pnpm build
# Sortie : dist/quizzy-front/
```

## 📚 Documentation de l'API

### Endpoints Principaux

- `GET /api/ping` - Vérification de santé
- `POST /api/auth/register` - Enregistrer un nouvel utilisateur
- `POST /api/auth/login` - Connecter un utilisateur
- `GET /api/users/me` - Obtenir l'utilisateur actuel (protégé)
- `GET /api/quiz` - Obtenir les quiz de l'utilisateur (protégé)
- `POST /api/quiz` - Créer un nouveau quiz (protégé)
- `GET /api/quiz/:id` - Obtenir un quiz par ID (protégé)
- `PATCH /api/quiz/:id` - Mettre à jour un quiz (protégé)
- `DELETE /api/quiz/:id` - Supprimer un quiz (protégé)

### Endpoints WebSocket

- `ws://localhost:3000` - Passerelle de chat
- `ws://localhost:3000` - Passerelle d'exécution de quiz

## 🏛️ Points Forts de l'Architecture

### Structure des Modules

```
quizzam/src/
├── auth/              # Module d'authentification (JWT/Firebase)
├── quiz/              # Gestion des quiz (CQRS)
│   ├── commands/      # Opérations d'écriture
│   ├── queries/       # Opérations de lecture
│   ├── adapters/      # Implémentations de base de données
│   └── ports/         # Interfaces de repository
├── users/             # Gestion des utilisateurs
├── chat/              # Chat WebSocket
└── core/              # Module core (configuration DI)
```

### Flux d'Injection de Dépendances

```
Controller → Command/Query → Interface Repository → Implémentation Repository
     ↓              ↓                  ↓                      ↓
  Couche HTTP   Logique Métier    Port (Contrat)    Adapter (Implémentation)
```

### Avantages de cette Architecture

1. **Testabilité** : Facile de mocker les repositories pour les tests
2. **Flexibilité** : Changer de base de données sans modifier la logique métier
3. **Maintenabilité** : Séparation claire des responsabilités
4. **Évolutivité** : Ajouter de nouveaux adapters sans modifier le code existant
5. **Sécurité de Type** : Les interfaces TypeScript garantissent le respect des contrats

## 🔧 Variables d'Environnement

### Backend (`quizzam/.env`)

| Variable | Description | Défaut | Options |
|----------|-------------|--------|---------|
| `DATABASE_URL` | Chaîne de connexion à la base de données | - | URI MongoDB ou config Firebase |
| `DATABASE_NAME` | Type de base de données | `FIREBASE` | `MONGODB`, `FIREBASE`, `IN-MEMORY` |
| `PORT` | Port du serveur | `3000` | Tout port disponible |
| `GLOBAL_PREFIX` | Préfixe de l'API | `api` | - |
| `AUTH_TYPE` | Méthode d'authentification | `JWT` | `JWT`, `FIREBASE` |
| `JWT_SECRET` | Secret de signature JWT | - | Chaîne aléatoire forte |
| `FIREBASE_KEY_PATH` | Chemin des credentials Firebase | - | Chemin vers fichier JSON |

### Frontend (`quizzy-front/src/environments/`)

| Variable | Description | Défaut |
|----------|-------------|--------|
| `baseUrl` | URL de base du backend | `http://localhost:3000` |
| `apiUrl` | URL de l'API backend | `http://localhost:3000/api` |
| `authType` | Type d'authentification | `JWT` |

## 🛠️ Développement

### Ajouter un Nouvel Adapter de Base de Données

1. **Créer la classe adapter :**
   ```typescript
   // adapters/nouvelle-db/nouvelle-db-repository.ts
   export class NouvelleDbRepository implements IQuizRepository {
     // Implémenter toutes les méthodes de l'interface
   }
   ```

2. **Mettre à jour le module :**
   ```typescript
   function database(database: string) {
     switch (database) {
       case "NOUVELLE_DB":
         return NouvelleDbRepository;
       // ... cas existants
     }
   }
   ```

3. **Mettre à jour l'environnement :**
   ```env
   DATABASE_NAME=NOUVELLE_DB
   ```

### Exécution des Tests

```bash
# Tous les tests
pnpm test

# Tests E2E uniquement
pnpm test:e2e

# Tests unitaires uniquement
pnpm test:unit

# Couverture de code
pnpm test:cov
```

## 📝 Licence

MIT

## 📖 Documentation Additionnelle

- [Guide de Test](./TESTING.md) - Instructions détaillées de test
- [Guide de Sécurité](./SECURITY.md) - Bonnes pratiques de sécurité
---

**Développé avec ❤️ en utilisant NestJS et Angular**
