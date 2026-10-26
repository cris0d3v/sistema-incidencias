# 06. Security

## Authentication

- Login with email and password. A short-lived access JWT is returned (15 minutes).
- Session refresh with a refresh token in an `HttpOnly`, `Secure`, and `SameSite=Strict` cookie (starting in V2 if the MVP only uses the access token).
- Password hashing with argon2 (or bcrypt as a fallback).
- Login attempt limit per IP and per email (for example, 5 attempts per 15 minutes).
- Generic error messages on login: it is not revealed whether the email exists.

## Authorization

- Verified on the backend for every endpoint through NestJS guards (`JwtAuthGuard` and `RolesGuard`).
- The interface hides buttons that don't apply, but that is only for convenience: the API is the one that decides.
- Visibility rules per resource (who can see an incident) are checked in the service, not just by role.

## Input validation

- All inputs go through DTOs with `class-validator` and a global `ValidationPipe` with `whitelist: true`.
- Undeclared fields are rejected.
- Maximum lengths: title 200 characters, description 5,000, comment 2,000.

## Auditing

- Every status, priority, or assignment change is recorded in `history` with the actor and date.
- The `history` table has no modification permissions for the application.
- Failed login attempts are saved in logs, without passwords.

## Attachments (V2)

- Types allowed by whitelist: PDF, PNG, JPG, TXT. The actual file type is validated, not just the extension.
- Example maximum size: 10 MB per file.
- Files are saved with a generated name, outside the public folder. Downloads go through the API, which verifies permissions.

## Secrets and configuration

- No secrets in the repository. Keys go in environment variables.
- `.env` is in `.gitignore`. `.env.example` has fake values.
- GitHub: enable _secret scanning_ and _push protection_.
- If a secret is published by accident, it is rotated immediately. Deleting the commit is not enough.

## HTTP headers

- Use `helmet` in NestJS.
- CORS restricted to the web application origin.
- HTTPS mandatory in production.
