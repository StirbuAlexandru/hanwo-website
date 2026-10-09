# HANWO Website

Presentation website for **HANWO** agricultural tractors, distributed in Romania by **Agrorus**, with an **admin dashboard** that lets the client manage products and content on their own, without a developer.

🌐 **Live:** [www.hanwo.ro](https://www.hanwo.ro)

> This is a public showcase copy of a real client project, without credentials, deployment configuration or customer data.

## Features

### Public website
- Home page with a configurable hero image, featured products and promotions
- Product catalog by category and detailed product pages with image galleries
- Testimonials section
- Contact form and product enquiry form, with email notifications
- Floating call / WhatsApp buttons
- Responsive layout for mobile and desktop

### Admin dashboard
- Password-protected login with token-based authentication
- **Products** – add, edit and delete products, with image uploads
- **Promotions** – create and remove promotions shown on the website
- **Hero image** – change the main image on the home page
- **Testimonials** – manage customer testimonials
- **Messages** – read, mark as read and delete enquiries sent through the contact form

## Architecture

```
┌────────────────────────┐
│  React + Vite (SPA)    │  public website + admin dashboard
└───────────┬────────────┘
            │ REST API
┌───────────▼────────────┐
│  Node.js server        │  API, auth, image uploads, static frontend
└───────────┬────────────┘
            │
   ┌────────┴────────┐
   ▼                 ▼
JSON files       Brevo API
(products,       (email notifications
 promotions,      for new messages)
 settings,
 testimonials)
```

Data is stored in **JSON files** on the server instead of a database: the catalog is small, so this keeps hosting simple and cheap while still letting the client edit everything from the dashboard.

## Tech stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 19, Vite, React Router, Tailwind CSS, Font Awesome, React Icons |
| **Backend** | Node.js (native `http` module), dotenv |
| **Storage** | JSON files, local image uploads |
| **Email** | Brevo transactional email API |
| **Hosting** | Render |

## Project structure

```
src/            React frontend (pages, components, styles)
server/         Node.js API server
server/data/    JSON data files
public/         Static assets and product images
```

## Running locally

```bash
npm install
cp .env.example .env    # then fill in the values
npm run server          # API server
npm run dev             # frontend (Vite)
```

Required environment variables (see `.env.example`):

| Variable | Description |
|---|---|
| `ADMIN_PASSWORD` | Password for the admin dashboard |
| `ADMIN_TOKEN` | Secret token issued after admin login |
| `BREVO_API_KEY` | Brevo API key for email notifications (optional) |
| `EMAIL_FROM`, `EMAIL_TO` | Sender and recipient for notification emails |
| `PORT` | Server port |

The server refuses to start if `ADMIN_PASSWORD` or `ADMIN_TOKEN` is missing.

## Author

**Alexandru Știrbu** – Junior Frontend Developer, [WebLift Digital](https://webliftdigital.ro)
