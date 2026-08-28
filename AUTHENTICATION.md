# Authentication Architecture

This portfolio uses Supabase Auth for email/password authentication. The frontend is hosted as a static site and communicates directly with Supabase Auth over HTTPS.

## Components

- `index.html` — authentication UI and client-side authentication logic.
- Supabase Auth — account creation, credential verification, session management, and password-reset emails.
- Browser session — Supabase's client maintains the authenticated session; the application does not store passwords.

## Request flow

### Sign up

1. The user enters their name, email, password, and confirmation password.
2. `supabase.auth.signUp()` sends the credentials over HTTPS to Supabase Auth.
3. Supabase creates the authentication account and handles password storage securely.
4. If email confirmation is required, the user receives a confirmation email.
5. After authentication, Supabase provides a session to the client.

### Login

1. The user enters email and password.
2. `supabase.auth.signInWithPassword()` sends the credentials over HTTPS to Supabase Auth.
3. Supabase verifies the credentials.
4. A valid authenticated session is returned to the browser.
5. The application displays the user's account area.

### Session handling

The application calls `supabase.auth.getSession()` when it loads and subscribes to `supabase.auth.onAuthStateChange()` so the UI reflects login/logout state changes.

### Logout

`supabase.auth.signOut()` ends the Supabase authentication session. The UI then returns to the logged-out state.

### Password reset

The user enters their email and the application calls `supabase.auth.resetPasswordForEmail()`. Supabase sends the reset email; the website never receives or stores the user's password.

## Credentials and keys

The Supabase Project URL and publishable key are used by the browser to identify the Supabase project. The publishable key is not a password or service credential.

**Never put a Supabase service-role key, secret key, database password, or other privileged credential in this repository or frontend code.**

## Security model

Authentication is delegated to Supabase Auth rather than implemented with custom password storage. If application data is added to Supabase tables later, Row Level Security (RLS) should be enabled and policies should restrict users to only the records they are authorized to access.

## Important deployment setting

For production password-reset links and email confirmation links, configure the deployed GitHub Pages URL in Supabase Authentication URL Configuration / Redirect URLs. The exact URL depends on the repository's GitHub Pages configuration.
