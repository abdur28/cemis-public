# CEMIS — Hospital Management Desktop App

> A native desktop application for hospital management built with Tauri + React — handling patient records, admissions tracking, and clinical workflows with full English/Russian localization. Actively developed (36 commits, last update 2 days ago).

---

## Screenshots

### Dashboard
![CEMIS Dashboard](cemis.png)
*Admin dashboard with patient statistics, admission charts, and recent patient activity — with English/Russian language toggle*

---

## What This Is

CEMIS (Clinical & Emergency Management Information System) is a **native desktop application** I built with Tauri to digitize hospital operations — patient intake, records management, and clinical workflows. It runs as a lightweight native app on Windows, macOS, and Linux, giving medical staff a dedicated workstation tool instead of a browser tab.

This was built for a real bilingual medical environment (English/Russian) where staff need fast, reliable, offline-capable access to patient data.

## Key Features

### Patient Management
Complete patient lifecycle tracking with dynamic routing (`patient/[patientId]`) — registration, admission, treatment records, and discharge. Each patient has a detailed profile with medical history, contact information, and visit logs.

### Dashboard Analytics
At-a-glance hospital operations view: total patients, active cases, discharged patients, and pending admissions. Charts visualize admission trends over configurable time periods.

### Full i18n (English & Russian)
Every UI element — component labels, form fields, validation messages, status indicators, navigation — is fully translated. The `locales/` directory manages translation files, and the `contexts/` layer handles dynamic language switching without page reloads. Recent work has focused on ensuring 100% translation coverage (last 4 commits are all translation work).

### Native Desktop Experience (Tauri)
Built as a proper desktop application using Tauri (Rust-based), not an Electron wrapper. This gives:
- **Tiny bundle size** (~5-10MB vs Electron's 100MB+)
- **Native OS integration** — system tray, file system access, native menus
- **Offline capability** — works without an internet connection
- **Cross-platform** — single codebase compiles to Windows, macOS, Linux

### Authentication & Role-Based Access
Secure login system with role-based permissions for administrators, doctors, nurses, and reception staff. Sensitive patient data is only visible to authorized roles.

## Tech Stack

| Layer | Technology |
|-------|-----------|
| **Desktop Shell** | Tauri (Rust) |
| **Frontend** | React + TypeScript |
| **Styling** | TailwindCSS |
| **UI Components** | shadcn/ui |
| **State Management** | React Context |
| **i18n** | Custom locales system (EN, RU) |
| **Build Scripts** | Custom build pipeline |

## Architecture

```
cemis-desktop/
├── src-tauri/           # Tauri backend (Rust)
│   ├── src/             # Rust source code
│   └── tauri.conf.json  # Tauri configuration
├── src/                 # React frontend
│   ├── pages/
│   │   ├── auth/              # Login/register
│   │   ├── home/              # Dashboard
│   │   └── patient/[patientId]  # Patient detail
│   ├── components/      # Shared UI components
│   ├── constants/       # App configuration
│   ├── contexts/        # React context providers
│   ├── layouts/         # Page layouts
│   ├── lib/             # Utility functions
│   ├── locales/         # EN/RU translation files
│   └── types/           # TypeScript definitions
├── scripts/             # Build & utility scripts
└── public/              # Static assets & icons
```

There's also a companion **`cemis`** web app (Next.js, 29 commits) that provides browser-based access to the same patient data — useful for remote access when staff aren't at a hospital workstation.

## Technical Decisions

**Why Tauri over Electron?** Hospital IT teams deploy software across dozens of workstations. A 5MB Tauri bundle vs a 100MB+ Electron bundle means faster rollouts, less disk usage, and lower memory consumption on shared hospital computers.

**Why React (not Next.js) for the desktop app?** Tauri works best with a standard React SPA. Next.js's server-side features (SSR, API routes) aren't needed in a desktop context where the app runs locally. The companion web app uses Next.js for SEO and server-side benefits.

**Why custom i18n over i18next?** Full control over translation loading and context switching. The locales system is tightly integrated with the component tree — every component pulls translations from context, ensuring consistent language switching across the entire app without page reloads.

## What I'd Improve

- **Add offline-first data sync** — cache patient data locally with conflict resolution when reconnecting
- **Implement audit logging** — track every data access and modification for compliance
- **Add PDF report generation** — patient records, daily summaries, discharge reports
- **Build appointment scheduling** — calendar-based outpatient visit management

---

> Note: This is a private repository. The code is not publicly available to protect patient data handling.

**Built by [Abdurrahman Idris](https://abdurrahmanidris.com)** — Full Stack Developer
