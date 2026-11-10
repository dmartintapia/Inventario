# Backend

Django API scaffold for Render. Production uses PostgreSQL through `DATABASE_URL`; local development can use SQLite by leaving that variable unset while `DJANGO_DEBUG=true`.

## Run locally

1. Create and activate a Python virtual environment.
2. Install dependencies with `pip install -r requirements.txt`.
3. Copy `.env.example` to `.env` and set local values (export them in your shell).
4. Run `python manage.py migrate`.
5. Start Django with `python manage.py runserver`.

The `/api/health` endpoint checks that Django can connect to the configured database.

## Render

The root `render.yaml` defines the Python web service. Create a Render Postgres database in the same region, then set the web service's `DATABASE_URL` to that database's **internal** connection string. Set the exact Vercel domain in `CORS_ALLOWED_ORIGINS` after the frontend is deployed. Render runs migrations during the build and starts the app with Gunicorn.

The repository's root `index.html` remains the frontend entry point. It still uses browser localStorage today; the inventory data API and frontend migration are the next implementation step.
