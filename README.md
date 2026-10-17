<p align="center"><img src="docs/logo.png" alt="SmartPharma logo" width="140"></p>

<h1 align="center">SmartPharma</h1>

<p align="center">
  A desktop pharmacy management application: stock, sales, purchases, customers, suppliers and sales statistics.<br>
  <b>Bachelor's degree final-year project</b> (Licence in Computer Science, 2022/2023).
</p>

<p align="center">
  🇬🇧 English · <a href="README.fr.md">🇫🇷 Français</a>
</p>

---

## About

SmartPharma is a Windows desktop application built to help a pharmacy replace paper records with a single tool. It was designed and developed as my bachelor's degree final-year project (*Projet de Fin d'Études de Licence*) at the Faculty of Mathematics and Computer Science, USTO-MB (Oran, Algeria), specialty *Information Systems*.

The project covers the whole software cycle: needs analysis, UML modelling, database design, implementation and testing.

## Features

- **Authentication** with two roles: *Manager* and *Employee*.
- **Stock management**: add, edit, delete and search products (category, shelf, quantity, purchase and sale price, barcode, expiry date). Products that are out of stock or close to expiry are highlighted.
- **Sales**: cash-register style screen (barcode or product name, quantities, customer, running total), invoice generation and ticket printing.
- **Purchases**: supplier orders that update the stock when validated.
- **Customers and suppliers** records.
- **Sales history** by period, with revenue and profit.
- **Statistics**: sales evolution per day, month and year.
- **User management** (manager only).

## Screenshots

| Login | Manager menu |
|---|---|
| ![Login](docs/screenshots/01-login.png) | ![Manager menu](docs/screenshots/02-manager-menu.png) |

| Sale | Purchase |
|---|---|
| ![Sale](docs/screenshots/04-sale.png) | ![Purchase](docs/screenshots/05-purchase.png) |

| Stock | Sales management |
|---|---|
| ![Stock](docs/screenshots/06-stock.png) | ![Sales management](docs/screenshots/07-sales-management.png) |

More: [employee menu](docs/screenshots/03-employee-menu.png) · [sales statistics](docs/screenshots/08-sales-statistics.png)

> The data visible in the screenshots is test data only.

## Design (UML)

The application was modelled with UML before implementation (diagrams made with StarUML).

| Diagram | Files |
|---|---|
| Use cases | [authentication](docs/uml/use-case-authentication.png) · [employee](docs/uml/use-case-employee.png) · [manager](docs/uml/use-case-manager.png) |
| Sequence diagrams | [authentication](docs/uml/sequence-authentication.png) · [sale](docs/uml/sequence-sale.png) · [user management](docs/uml/sequence-user-management.png) |
| Class diagram | [class-diagram.png](docs/uml/class-diagram.png) |

![Class diagram](docs/uml/class-diagram.png)

The main entities are `Produit`, `Vente`, `Achat`, `Client`, `Fournisseur` and `Utilisateur` (specialised into `Gérant` and `Employé`).

📘 Full details (roles, application flow, data dictionary, relational model): **[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)**

## Tech stack

| Area | Tool |
|---|---|
| IDE / framework | WinDev 25 (PC SOFT) |
| Language | WLangage, SQL |
| Database | HFSQL (embedded) |
| Modelling | UML, StarUML |

## Repository layout

```
SmartPharma/
├── src/        WinDev project: windows (FEN_*.wdw), queries (REQ_*.WDR),
│               report (ETATticket.wde), database analysis (BDD.ana), images
├── docs/       logo, UI screenshots, UML diagrams
├── LICENSE     MIT
└── README.md
```

## Run the project

**Open the source** (requires [WinDev 25](https://windev.com) or compatible):

1. Clone this repository.
2. Open `src/PHARMACIEapp.wdp` in WinDev.
3. The HFSQL data files are intentionally **not** included: the database is recreated from the analysis (`src/BDD.ana`) when the project runs. Create a first user account to log in.

**Pre-built executable**: download `SmartPHARMA.exe` from the [Releases](../../releases) page. It is provided as-is and needs the WinDev runtime libraries.

## Notes

- This repository contains **no real data**: customer, supplier and user files were excluded.
- The thesis is not published in full. A short summary of the project is given above.
- WinDev project files are proprietary text/binary formats, so GitHub does not show syntax highlighting for them.

## Possible improvements

- Support for national health-insurance cards (CHIFAA, CNAS).
- Android and iOS companion application.
- Hashed passwords and automated backups.

## License

Released under the [MIT License](LICENSE).
