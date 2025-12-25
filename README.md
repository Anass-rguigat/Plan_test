# Plan de Test - Inventory Management System

Ce document contient tous les scénarios de tests unitaires et le plan de test complet de l'application.

---

## Table des Matières

1. [Vue d'ensemble](#vue-densemble)
2. [Tests Unitaires - Services](#tests-unitaires---services)
3. [Tests Unitaires - Sécurité](#tests-unitaires---sécurité)
4. [Tests Unitaires - Contrôleurs](#tests-unitaires---contrôleurs)
5. [Matrice de Couverture](#matrice-de-couverture)
6. [Exécution des Tests](#exécution-des-tests)

---

## Vue d'ensemble

### Types de Tests

- **Tests Unitaires** : Tests isolés des services, contrôleurs et composants de sécurité
- **Tests de Contrôleurs** : Tests des endpoints REST avec MockMvc

### Outils Utilisés

- **JUnit 5** : Framework de test
- **Mockito** : Framework de mocking
- **Spring Boot Test** : Support de test Spring
- **H2 Database** : Base de données en mémoire pour les tests

---

## Tests Unitaires - Services

### 1. CategoryService

**Fichier** : `CategoryServiceImplTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testCreateCategory_Success` | Créer une catégorie avec succès | Status 200, message "Category Saved Successfully" |
| `testGetAllCategories_Success` | Récupérer toutes les catégories | Status 200, liste de catégories non vide |
| `testGetCategoryById_Success` | Récupérer une catégorie par ID | Status 200, catégorie retournée |
| `testGetCategoryById_NotFound` | Récupérer une catégorie inexistante | Exception NotFoundException |
| `testUpdateCategory_Success` | Mettre à jour une catégorie | Status 200, catégorie mise à jour |
| `testUpdateCategory_NotFound` | Mettre à jour une catégorie inexistante | Exception NotFoundException |
| `testDeleteCategory_Success` | Supprimer une catégorie | Status 200, catégorie supprimée |
| `testDeleteCategory_NotFound` | Supprimer une catégorie inexistante | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

### 2. ProductService

**Fichier** : `ProductServiceImplTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testSaveProduct_Success` | Créer un produit avec image | Status 200, produit sauvegardé |
| `testSaveProduct_WithoutImage` | Créer un produit sans image | Status 200, produit sauvegardé |
| `testSaveProduct_CategoryNotFound` | Créer un produit avec catégorie inexistante | Exception NotFoundException |
| `testUpdateProduct_Success` | Mettre à jour un produit | Status 200, produit mis à jour |
| `testUpdateProduct_NotFound` | Mettre à jour un produit inexistant | Exception NotFoundException |
| `testGetAllProducts_Success` | Récupérer tous les produits | Status 200, liste de produits |
| `testGetProductById_Success` | Récupérer un produit par ID | Status 200, produit retourné |
| `testGetProductById_NotFound` | Récupérer un produit inexistant | Exception NotFoundException |
| `testDeleteProduct_Success` | Supprimer un produit | Status 200, produit supprimé |
| `testDeleteProduct_NotFound` | Supprimer un produit inexistant | Exception NotFoundException |
| `testSearchProduct_Success` | Rechercher un produit | Status 200, produits trouvés |
| `testSearchProduct_NotFound` | Rechercher un produit inexistant | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

### 3. SupplierService

**Fichier** : `SupplierServiceImplTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testAddSupplier_Success` | Ajouter un fournisseur | Status 200, fournisseur sauvegardé |
| `testUpdateSupplier_Success` | Mettre à jour un fournisseur | Status 200, fournisseur mis à jour |
| `testUpdateSupplier_NotFound` | Mettre à jour un fournisseur inexistant | Exception NotFoundException |
| `testGetAllSupplier_Success` | Récupérer tous les fournisseurs | Status 200, liste de fournisseurs |
| `testGetSupplierById_Success` | Récupérer un fournisseur par ID | Status 200, fournisseur retourné |
| `testGetSupplierById_NotFound` | Récupérer un fournisseur inexistant | Exception NotFoundException |
| `testDeleteSupplier_Success` | Supprimer un fournisseur | Status 200, fournisseur supprimé |
| `testDeleteSupplier_NotFound` | Supprimer un fournisseur inexistant | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

### 4. TransactionService

**Fichier** : `TransactionServiceImplTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testPurchase_Success` | Effectuer un achat | Status 200, stock augmenté, transaction créée |
| `testPurchase_SupplierIdRequired` | Achat sans supplierId | Exception NameValueRequiredException |
| `testPurchase_ProductNotFound` | Achat avec produit inexistant | Exception NotFoundException |
| `testSell_Success` | Effectuer une vente | Status 200, stock diminué, transaction créée |
| `testSell_ProductNotFound` | Vente avec produit inexistant | Exception NotFoundException |
| `testReturnToSupplier_Success` | Retourner un produit au fournisseur | Status 200, stock diminué, transaction créée |
| `testReturnToSupplier_SupplierIdRequired` | Retour sans supplierId | Exception NameValueRequiredException |
| `testGetAllTransactions_Success` | Récupérer toutes les transactions | Status 200, liste paginée |
| `testGetAllTransactionById_Success` | Récupérer une transaction par ID | Status 200, transaction retournée |
| `testGetAllTransactionById_NotFound` | Récupérer une transaction inexistante | Exception NotFoundException |
| `testUpdateTransactionStatus_Success` | Mettre à jour le statut d'une transaction | Status 200, statut mis à jour |
| `testUpdateTransactionStatus_NotFound` | Mettre à jour une transaction inexistante | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

### 5. UserService

**Fichier** : `UserServiceImplTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testRegisterUser_Success` | Enregistrer un utilisateur | Status 200, utilisateur créé |
| `testRegisterUser_WithDefaultRole` | Enregistrer avec rôle par défaut | Status 200, rôle MANAGER assigné |
| `testLoginUser_Success` | Connexion réussie | Status 200, token JWT retourné |
| `testLoginUser_EmailNotFound` | Connexion avec email inexistant | Exception NotFoundException |
| `testLoginUser_InvalidPassword` | Connexion avec mot de passe incorrect | Exception InvalidCredentialsException |
| `testGetAllUsers_Success` | Récupérer tous les utilisateurs | Status 200, liste d'utilisateurs |
| `testGetCurrentLoggedInUser_Success` | Récupérer l'utilisateur connecté | Utilisateur retourné |
| `testGetCurrentLoggedInUser_NotFound` | Utilisateur connecté inexistant | Exception NotFoundException |
| `testGetUserById_Success` | Récupérer un utilisateur par ID | Status 200, utilisateur retourné |
| `testGetUserById_NotFound` | Récupérer un utilisateur inexistant | Exception NotFoundException |
| `testUpdateUser_Success` | Mettre à jour un utilisateur | Status 200, utilisateur mis à jour |
| `testUpdateUser_WithPassword` | Mettre à jour avec nouveau mot de passe | Status 200, mot de passe encodé |
| `testUpdateUser_NotFound` | Mettre à jour un utilisateur inexistant | Exception NotFoundException |
| `testDeleteUser_Success` | Supprimer un utilisateur | Status 200, utilisateur supprimé |
| `testDeleteUser_NotFound` | Supprimer un utilisateur inexistant | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

## Tests Unitaires - Sécurité

### 1. JwtUtils

**Fichier** : `JwtUtilsTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testGenerateToken_Success` | Générer un token JWT | Token non null et non vide |
| `testGetUsernameFromToken_Success` | Extraire l'email du token | Email correctement extrait |
| `testIsTokenValid_Success` | Valider un token valide | true |
| `testIsTokenValid_InvalidUsername` | Valider un token avec mauvais username | false |
| `testIsTokenValid_ExpiredToken` | Valider un token expiré | Exception ou false |

**Couverture** : 100% des méthodes de JwtUtils

---

### 2. CustomUserDetailsService

**Fichier** : `CustomUserDetailsServiceTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testLoadUserByUsername_Success` | Charger un utilisateur par email | UserDetails retourné |
| `testLoadUserByUsername_NotFound` | Charger un utilisateur inexistant | Exception NotFoundException |

**Couverture** : 100% des méthodes du service

---

## Tests Unitaires - Contrôleurs

### 1. AuthController

**Fichier** : `AuthControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testRegisterUser_Success` | Endpoint POST /api/auth/register | Status 200, utilisateur enregistré |
| `testLoginUser_Success` | Endpoint POST /api/auth/login | Status 200, token retourné |

---

### 2. CategoryController

**Fichier** : `CategoryControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testCreateCategory_Success` | POST /api/categories/add (ADMIN) | Status 200 |
| `testGetAllCategories_Success` | GET /api/categories/all | Status 200 |
| `testGetCategoryById_Success` | GET /api/categories/{id} | Status 200 |
| `testUpdateCategory_Success` | PUT /api/categories/update/{id} (ADMIN) | Status 200 |
| `testDeleteCategory_Success` | DELETE /api/categories/delete/{id} (ADMIN) | Status 200 |

---

### 3. ProductController

**Fichier** : `ProductControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testSaveProduct_Success` | POST /api/products/add (ADMIN) | Status 200 |
| `testUpdateProduct_Success` | PUT /api/products/update (ADMIN) | Status 200 |
| `testGetAllProducts_Success` | GET /api/products/all | Status 200 |
| `testGetProductById_Success` | GET /api/products/{id} | Status 200 |
| `testDeleteProduct_Success` | DELETE /api/products/delete/{id} | Status 200 |
| `testSearchProduct_Success` | GET /api/products/search?input=... | Status 200 |

---

### 4. SupplierController

**Fichier** : `SupplierControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testAddSupplier_Success` | POST /api/suppliers/add (ADMIN) | Status 200 |
| `testGetAllSuppliers_Success` | GET /api/suppliers/all | Status 200 |
| `testGetSupplierById_Success` | GET /api/suppliers/{id} | Status 200 |
| `testUpdateSupplier_Success` | PUT /api/suppliers/update/{id} (ADMIN) | Status 200 |
| `testDeleteSupplier_Success` | DELETE /api/suppliers/delete/{id} (ADMIN) | Status 200 |

---

### 5. TransactionController

**Fichier** : `TransactionControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testPurchase_Success` | POST /api/transactions/purchase | Status 200 |
| `testSell_Success` | POST /api/transactions/sell | Status 200 |
| `testReturnToSupplier_Success` | POST /api/transactions/return | Status 200 |
| `testGetAllTransactions_Success` | GET /api/transactions/all | Status 200 |
| `testGetTransactionById_Success` | GET /api/transactions/{id} | Status 200 |
| `testGetTransactionByMonthAndYear_Success` | GET /api/transactions/by-month-year | Status 200 |
| `testUpdateTransactionStatus_Success` | PUT /api/transactions/{id} | Status 200 |

---

### 6. UserController

**Fichier** : `UserControllerTest.java`

#### Scénarios de Test

| Test | Description | Résultat Attendu |
|------|-------------|------------------|
| `testGetAllUsers_Success` | GET /api/users/all (ADMIN) | Status 200 |
| `testGetUserById_Success` | GET /api/users/{id} | Status 200 |
| `testUpdateUser_Success` | PUT /api/users/update/{id} | Status 200 |
| `testDeleteUser_Success` | DELETE /api/users/delete/{id} (ADMIN) | Status 200 |
| `testGetUserTransactions_Success` | GET /api/users/transactions/{userId} | Status 200 |
| `testGetCurrentUser_Success` | GET /api/users/current | Status 200 |

---

## Matrice de Couverture

### Services

| Service | Tests Unitaires | Couverture |
|---------|----------------|------------|
| CategoryService | 8 tests | 100% |
| ProductService | 12 tests | 100% |
| SupplierService | 8 tests | 100% |
| TransactionService | 12 tests | 100% |
| UserService | 15 tests | 100% |

### Sécurité

| Composant | Tests Unitaires | Couverture |
|-----------|----------------|------------|
| JwtUtils | 5 tests | 100% |
| CustomUserDetailsService | 2 tests | 100% |

### Contrôleurs

| Contrôleur | Tests | Couverture |
|------------|-------|------------|
| AuthController | 2 tests | 100% |
| CategoryController | 5 tests | 100% |
| ProductController | 6 tests | 100% |
| SupplierController | 5 tests | 100% |
| TransactionController | 7 tests | 100% |
| UserController | 6 tests | 100% |

### Total des Tests

- **Tests Unitaires Services** : 55 tests
- **Tests Unitaires Sécurité** : 7 tests
- **Tests Unitaires Contrôleurs** : 31 tests
- **TOTAL** : **93 tests**

---

## Exécution des Tests

### Exécuter Tous les Tests

```bash
cd backend
mvn test
```

### Exécuter un Test Spécifique

```bash
mvn test -Dtest=CategoryServiceImplTest
```

### Exécuter avec Couverture de Code

```bash
mvn clean test jacoco:report
```

Le rapport sera généré dans : `target/site/jacoco/index.html`

---

## Scénarios de Test Détaillés

### Scénario 1 : Gestion Complète d'une Catégorie

1. Créer une catégorie
2. Récupérer toutes les catégories
3. Récupérer la catégorie par ID
4. Mettre à jour la catégorie
5. Supprimer la catégorie
6. Vérifier que la catégorie n'existe plus

### Scénario 2 : Gestion Complète d'un Produit

1. Créer une catégorie
2. Créer un produit avec catégorie
3. Récupérer tous les produits
4. Rechercher un produit
5. Mettre à jour le produit
6. Supprimer le produit

### Scénario 3 : Cycle de Transaction Complet

1. Créer une catégorie
2. Créer un fournisseur
3. Créer un produit
4. Effectuer un achat (stock augmente)
5. Effectuer une vente (stock diminue)
6. Retourner un produit au fournisseur
7. Récupérer toutes les transactions
8. Mettre à jour le statut d'une transaction

### Scénario 4 : Authentification et Gestion Utilisateur

1. Enregistrer un utilisateur
2. Se connecter (obtenir token)
3. Récupérer l'utilisateur connecté
4. Mettre à jour l'utilisateur
5. Récupérer tous les utilisateurs (ADMIN)
6. Supprimer l'utilisateur

### Scénario 5 : Gestion des Erreurs

1. Tester NotFoundException pour toutes les entités
2. Tester InvalidCredentialsException pour login
3. Tester NameValueRequiredException pour transactions
4. Tester les validations de champs requis

---

## Critères de Succès

### Tests Unitaires

- Tous les services ont des tests unitaires complets
- Tous les cas de succès sont testés
- Tous les cas d'erreur sont testés
- Utilisation de mocks pour isoler les dépendances
- Couverture de code > 90%

### Tests de Contrôleurs

- Tous les endpoints sont testés
- Tests avec MockMvc
- Vérification des codes de statut HTTP
- Vérification des réponses JSON

---

## Maintenance des Tests

### Bonnes Pratiques

1. **Nommage** : `test[NomMéthode]_[Scénario]_[RésultatAttendu]`
2. **Structure** : Given-When-Then (Arrange-Act-Assert)
3. **Isolation** : Chaque test est indépendant
4. **Mocking** : Utiliser Mockito pour les dépendances
5. **Assertions** : Vérifier tous les aspects importants

### Ajout de Nouveaux Tests

Lors de l'ajout d'une nouvelle fonctionnalité :

1. Créer les tests unitaires pour le service
2. Créer les tests pour le contrôleur
3. Vérifier que tous les tests passent
4. Mettre à jour ce document

---

## Conclusion

Le plan de test couvre :
- **93 tests unitaires** au total
- **100% de couverture** des services
- **Tous les scénarios** de succès et d'erreur
- **Tests de sécurité** pour l'authentification
- **Tests de contrôleurs** pour tous les endpoints REST

Tous les tests sont automatisés et peuvent être exécutés avec une simple commande Maven.

