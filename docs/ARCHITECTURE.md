# SmartPharma – Architecture and data model

[← Back to README](../README.md)

## 1. Users and roles

| Role | Can do |
|---|---|
| **Employee** | Sell, purchase, manage stock, customers and suppliers, consult sales history and statistics |
| **Manager** | Everything an employee can do, plus **create, edit and delete user accounts** |

Every user must authenticate (username, password, role) before reaching the main menu.

## 2. Application flow

```
Login ──► Main menu ──┬─► Stock            (products, search, expiry / out-of-stock alerts)
                      ├─► Sales            (cash register → invoice → stock decreases)
                      ├─► Purchases        (supplier order → stock increases)
                      ├─► Customers
                      ├─► Suppliers
                      ├─► Sales management (history by period, revenue, profit)
                      ├─► Statistics       (sales per day / month / year)
                      └─► Users            (manager only)
```

Source windows in `src/` follow this structure: `menu_principal.wdw`, `FEN_Vente.wdw`, `FEN_Achat.wdw`, `FEN_Table_produit.wdw`, `FEN_Table_client.wdw`, `FEN_Table_fournisseur.wdw`, `FEN_Gerer_les_ventes.wdw`, `FEN_Statistiques.wdw`, `FEN_User.wdw`, and so on. Reports and statistics are fed by the `REQ_*.WDR` queries.

## 3. Class diagram

![Class diagram](uml/class-diagram.png)

## 4. Data dictionary

| Entity | Attribute | Meaning | Type |
|---|---|---|---|
| **Utilisateur** (User) | IDutilisateur | Identifier | Integer |
| | Nom, Prenom | Last / first name | Text |
| | Mdp | Password | Alphanumeric |
| | Poste | Role (Manager / Employee) | Text |
| | Num, Adresse | Phone, address | Integer, Alphanumeric |
| **Produit** (Product) | IDproduit | Identifier | Integer |
| | Nom, Categorie, Rayon | Name, category (medicine, vitamin…), shelf (A, B…) | Alphanumeric |
| | Quantite | Quantity in stock | Integer |
| | PrixAchat, PrixVente | Purchase price, sale price | Real |
| | Codebarre | Barcode | Integer |
| | Date_exp | Expiry date | Date |
| **Vente** (Sale) | IDvente, IDclient | Identifiers | Integer |
| | Total, Benefice | Total amount, profit | Real |
| | Date, Heure | Date and time of the sale | Date, Time |
| **Achat** (Purchase) | IDachat, IDfournisseur | Identifiers | Integer |
| | Total | Total of the purchase order | Real |
| | Date, Heure | Date and time | Date, Time |
| **Client** (Customer) | IDclient, Nom, Prenom, Adresse, Num | Customer record | Integer, text |
| **Fournisseur** (Supplier) | IDfournisseur, Nom, Prenom, Adresse, Num | Supplier record | Integer, text |

## 5. Relational model

```
Utilisateur (IDutilisateur, Nom, Prenom, Mdp, Poste, Num, Adresse)
Produit     (IDproduit, Nom, Categorie, Rayon, Quantite, PrixAchat, PrixVente, Codebarre, Date_exp)
Vente       (IDvente, #IDclient, Total, Date, Heure, Benefice)
Achat       (IDachat, #IDfournisseur, Total, Date, Heure)
Client      (IDclient, Nom, Prenom, Adresse, Num)
Fournisseur (IDfournisseur, Nom, Prenom, Adresse, Num)

Vendre      (#IDproduit, #IDvente)      -- products sold in a sale
Acheter     (#IDproduit, #IDachat)      -- products bought in a purchase
Enregistrer (#IDutilisateur, #IDvente | #IDclient | #IDfournisseur)
Consulter   (#IDutilisateur, #IDachat)
```

Passage rules from the class diagram: every entity becomes a relation keyed by its identifier; every many-to-many association becomes a relation whose key is the concatenation of the linked identifiers.

## 6. Use cases and sequences

| Use cases | Sequence diagrams |
|---|---|
| [Authentication](uml/use-case-authentication.png) | [Authentication](uml/sequence-authentication.png) |
| [Employee](uml/use-case-employee.png) | [Sale](uml/sequence-sale.png) |
| [Manager](uml/use-case-manager.png) | [User management](uml/sequence-user-management.png) |
