# PureForce API

FastAPI service used by the PureForce storefront and admin dashboard.

## Deploy configuration

Set these variables in the backend host before deploying:

- `DATABASE_URL`: persistent PostgreSQL connection string. Do not use the example value.
- `JWT_SECRET`: a private random value of at least 32 characters.
- `ADMIN_EMAILS`: comma-separated email addresses allowed to open the dashboard. Use the same email as the Firebase account.
- `GROQ_API_KEY`: optional; required for the product assistant.
- `GMAIL_USER` and `GMAIL_APP_PASSWORD`: optional; enables order notification email.

Never commit `.env` or real credentials. `ADMIN_EMAILS` is checked by the API, so hiding the dashboard link alone does not grant administrator access.

## Run locally

1. Copy `.env.example` to `.env` and set real local values.
2. Install dependencies with `pip install -r requirements.txt`.
3. Start with `uvicorn main:app --host 0.0.0.0 --port 8000`.
4. Check `GET /health`.

The storefront currently uses `https://pureforcebackend1-8nz9lv60.b4a.run`. Configure the deployed service to use this repository and set its environment variables before testing sign-in and orders.

## Current analytics limits

The admin analytics endpoint reports registered users, orders, recent order history, and product quantities. Website visits, confirmed paid sales, profit, subscriptions, campaign open rates, and real visitor locations are not collected by this API. Orders are requests awaiting payment confirmation; they must not be counted as completed sales.
