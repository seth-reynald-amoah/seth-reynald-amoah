# Seth Reynald Amoah — Portfolio

Personal portfolio website for Seth Reynald Amoah, an IT enthusiast, aspiring software developer, and digital innovation enthusiast.

## Live project

The site is a static frontend with Supabase email/password authentication.

## Technology

- HTML5
- CSS3
- JavaScript (ES modules)
- Supabase Auth
- GitHub Pages

## Authentication

The portfolio includes a working authentication system with:

- Account registration with email and password
- Email confirmation
- Email/password login
- Invalid-credential rejection
- Authenticated account view
- Session detection and state changes
- Logout
- Password-reset email flow

### Architecture

```text
Browser
  │
  ├── Create Account / Login
  │           │
  │           ▼
  │      Supabase Auth
  │           │
  │      credential check
  │           │
  │           ▼
  │     Authenticated session
  │           │
  │           ▼
  │       My Account
  │           │
  │           ▼
  │         Logout
  │
  └── GitHub Pages serves the static frontend
```

Authentication is delegated to Supabase. Passwords are not stored in this repository. The browser uses a Supabase publishable key; privileged service-role/secret keys and database passwords must never be committed to the frontend.

See [`AUTHENTICATION.md`](AUTHENTICATION.md) for the component model, request flow, credential/token handling, session lifecycle, and security boundaries.

## Learning focus

This project demonstrates practical understanding of frontend development, third-party authentication integration, asynchronous JavaScript, session-aware UI state, and basic application security boundaries.
