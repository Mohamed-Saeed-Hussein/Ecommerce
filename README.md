# Ecommerce

**A Laravel storefront with a separate administration workspace.**

Product browsing, order management, customer profiles, and back-office tools in one web application.

`PHP 8.2+` · `Laravel 12` · `Blade` · `React / Inertia` · `Vite`

[Preview](#preview) · [Local setup](#local-setup) · [Explore the code](#explore-the-code)

This repository is a fork of [MohamedSayedAbdelrazek/Ecommerce](https://github.com/MohamedSayedAbdelrazek/Ecommerce). The upstream project and its contributors retain their attribution.

---

## Preview

![Administration dashboard with revenue, stock, and recent-order summaries](assets/dashboard_admin.PNG)

<details>
<summary>View the customer storefront and more project images</summary>

![Customer storefront with product cards](assets/HomePage_user.jpg)

[Customer orders](assets/MyOrdersPage_user.jpg) · [Product administration](assets/show_product_admin.PNG) · [Database schema](assets/schema.jpg)

</details>

*Images are the screenshots already included in this repository.*

## Project at a glance

| Area | What is implemented |
| :--- | :--- |
| Customer experience | Product browsing, profile management, order history, and a contact form |
| Administration | Product, category, user, order, and contact-message management |
| Account system | Laravel Fortify with authentication and account-settings routes |
| Frontend | Blade storefront views alongside a React/Inertia starter-kit frontend |
| Data layer | Eloquent models and migrations for products, orders, reviews, payments, and shipping |

The presence of payment-related models does not establish a working external payment-gateway integration.

## Local setup

The application lives inside **`Ecommerce/`**, one level below the repository root. Use a fresh local development database.

Requirements: PHP 8.2+, Composer, a compatible database/PDO driver, and Node.js matching the locked Vite requirement (`^20.19.0 || >=22.12.0`).

```bash
git clone https://github.com/Mohamed-Saeed-Hussein/Ecommerce.git
cd Ecommerce/Ecommerce
composer install
cp .env.example .env
php artisan key:generate
npm ci
```

The supplied environment example selects SQLite. For that configuration, create its file:

```bash
php -r "file_exists('database/database.sqlite') || touch('database/database.sqlite');"
php artisan migrate
php artisan storage:link
npm run build
php artisan serve
```

Open [localhost:8000](http://localhost:8000). Register an account to access the customer pages. Admin routes require the appropriate role; the existing [DatabaseSeeder](Ecommerce/database/seeders/DatabaseSeeder.php) creates a test user, not a documented admin account.

For MySQL, set the `DB_*` values in `.env` before running migrations. For frontend development, run `npm run dev` in a second terminal instead of using only a one-off asset build.

## Explore the code

| Location | Start here for |
| :--- | :--- |
| [Routes](Ecommerce/routes/web.php) | Customer/admin entry points and route middleware |
| [Controllers](Ecommerce/app/Http/Controllers) | Application actions |
| [Models](Ecommerce/app/Models) | Data relationships |
| [Migrations](Ecommerce/database/migrations) | Schema definitions |
| [Blade views](Ecommerce/resources/views) | Storefront and server-rendered screens |
| [Frontend source](Ecommerce/resources/js) | React/Inertia application |
| [Tests](Ecommerce/tests) | Existing test suite |

## Development checks

Run from the inner `Ecommerce/` directory:

```bash
composer test
npm run types
npm run build
```

Use the existing test suite together with a manual check of the customer and admin flows when changing application behavior.
