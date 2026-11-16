# Vue Lottery

A Ukrainian-language educational web application for managing lottery participants and selecting winners. The app combines a participant directory, authenticated user management, and a simple random winner draw in a responsive Vue interface.

## Features

- Browse participants in a searchable, paginated table.
- View participant details and edit or delete participant records.
- Select up to three distinct winners from the currently loaded participants.
- Sign in to access protected participant pages; unauthenticated visitors are redirected to the login page.
- Keep the session across page reloads using persisted client-side state.
- Switch between light and dark themes; the selected theme is saved in browser storage.
- Validate login and participant forms with VeeValidate and Zod.
- Use responsive layouts, reusable UI components, and lazy-loaded routes.

## Tech stack

- **Vue 3** with the Composition API and **TypeScript**
- **Vite** for development and production builds
- **Vue Router** for navigation and route guards
- **Pinia** with persisted state for application state
- **PrimeVue**, **Tailwind CSS**, and **SCSS** for the interface
- **VeeValidate** and **Zod** for form validation
- **ESLint** and **Steiger** for code and Feature-Sliced Design checks

## Demo account and API

The login screen provides a demo account:

| Username | Password |
| --- | --- |
| `emilys` | `emilyspass` |

The application expects a REST API compatible with the endpoints used by [DummyJSON](https://dummyjson.com), including authentication and user operations. DummyJSON is a convenient demo API; its create, update, and delete operations are simulated and are not permanent data changes.

Configure the API base URL in a local environment file before starting the app:

```dotenv
VITE_API_URL=https://dummyjson.com
```

Save this as `client-websystems/.env.local`. Vite reads `VITE_` variables when it starts or builds the app. Do not put secrets in `VITE_` variables: they are bundled into client-side code.

## Getting started

### Prerequisites

- Node.js **20.19+**, **22.13+**, or **24+**
- npm (the project includes `package-lock.json`)

### Install and run

From the repository root:

```sh
cd client-websystems
npm ci
```

Create `client-websystems/.env.local` with the API URL shown above, then start the development server:

```sh
npm run dev
```

Open the local URL printed by Vite, sign in with the demo account, and visit **Users** to browse the participant list.

## Available scripts

Run these commands from `client-websystems/`:

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Vite development server. |
| `npm run build` | Type-check the application with `vue-tsc` and create a production build in `dist/`. |
| `npm run preview` | Serve the production build locally for verification. |
| `npm run lint` | Run ESLint with automatic fixes (`--fix`). |
| `npm run lint:fsd` | Check the source tree's Feature-Sliced Design conventions with Steiger. |

There is currently no test script defined in `package.json`.

## Application routes

| Route | Access | Description |
| --- | --- | --- |
| `/` | Public | Home page and application overview. |
| `/about` | Public | Author information. |
| `/login` | Public | Sign-in form. Authenticated users are redirected to `/users`. |
| `/users` | Authenticated | Searchable and paginated participant list, with winner selection and participant actions. |
| `/users/:id` | Authenticated | Participant details. |
| `/users/:id/edit` | Authenticated | Edit participant information. |
| Other paths | Public | Not-found page. |

## Project structure

The Vue application and its npm configuration live in `client-websystems/`.

```text
client-websystems/
├── public/                 # Static public assets
├── src/
│   ├── app/                # App bootstrap, router, plugins, and global styles
│   ├── entities/           # User and session models, stores, and API services
│   ├── pages/              # Home, about, login, users, and detail/edit pages
│   ├── shared/             # Shared API client, UI components, and utilities
│   └── widgets/            # Shared page-level UI such as the header and winners list
├── package.json
└── vite.config.ts
```

The code is organized around Feature-Sliced Design concepts: application setup and navigation live in `src/app`, domain state and API services in `src/entities`, route-level screens in `src/pages`, and reusable interface elements in `src/shared` and `src/widgets`.

## Production build and deployment

Build the application from `client-websystems/`:

```sh
npm run build
npm run preview
```

Deploy the generated `client-websystems/dist/` directory to a static hosting provider. Configure the host to serve `index.html` as the fallback for application routes, since the app uses Vue Router history mode. Set `VITE_API_URL` in the hosting provider's build environment; Vite embeds it at build time.

## Notes

- Participant data and authentication are provided by the configured API; this repository does not include a backend.
- Winner selections are held in client-side application state and are not persisted by the API.
- The interface is primarily in Ukrainian, although some navigation and controls are labeled in English.
