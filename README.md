# JK Question Maker

Bilingual (Bangla + English) Next.js foundation for a public quiz platform.

## Included
- Responsive home and PIN-entry interface
- Dashboard and quiz route placeholders
- Supabase client configuration
- PostgreSQL schema for profiles, groups, group membership, quizzes, image URLs, questions, submissions and ranking index
- Starter RLS policies and Vercel environment template

## Setup
1. Install Node.js 20+ and run `npm install`.
2. Create a Supabase project. In SQL Editor, run `database/schema.sql`.
3. Copy `.env.example` to `.env.local`; add your Supabase project URL and anon key.
4. Run `npm run dev` and open http://localhost:3000.
5. Push this folder to GitHub, import it in Vercel, and add the same environment variables.

## Required production hardening before public launch
This starter does not yet implement authenticated CRUD, secure server-side grading, live Realtime subscriptions, invitation flows, storage upload UI, PDF/CSV export, or full admin moderation. These require Supabase project credentials and server/Edge Function implementation. Never put the Supabase service-role key in browser code. Keep correct answers private until the attempt is submitted; enforce one attempt/idempotency and server-side time limits. Configure Storage bucket policies and test RLS with separate creator, member, anonymous and admin accounts.

## Storage
Create a `question-images` bucket in Supabase Storage. Restrict upload to authenticated users and validate MIME type/size (recommended max 5 MB); public read can be enabled for published quiz images if desired.

## Admin bootstrap
After signup, assign `profiles.role='admin'` to the trusted owner UUID from the Supabase SQL editor. Do not allow users to self-assign admin roles.
