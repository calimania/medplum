---
sidebar_position: 1000
---

# Setting Up Medplum on DigitalOcean

This guide will walk you through the process of setting up Medplum on DigitalOcean.

You can either run the Medplum API in a droplet following the Ubuntu instructions or run it as an app.

The configuration will be passed as `MEDPLUM_` environment variables.

## Prerequisites

### Step 1: Create a PostgreSQL Database

- Log in to your DigitalOcean account.
- Navigate to the Databases section.
- Click on "Create Database Cluster".
- Select PostgreSQL as the database engine.
- Configure your database settings (e.g., region, cluster name).
- Note down the database connection details (host, port, database name, username, password).

### Step 2: Create a Redis Database

- Navigate to the Databases section.
- Click on "Create Database Cluster".
- Select Redis as the database engine.
- Configure your database settings (e.g., region, cluster name).
- Note down the Redis connection details (host, port, password).

### Step 3: Set Up Medplum

- Option 1: Running Medplum API in a Droplet
- Create a new Droplet with Ubuntu.
- SSH into your Droplet.
- Install Node.js and npm:
- Clone the Medplum repository:
- Install dependencies:
- Set up environment variables:
- Run the Medplum API:

### Option 2: Running Medplum as an App

Navigate to the Apps section in DigitalOcean.

Click on "Create App".

Select your repository and branch. Or use the official repo medplum/medplum.

Configure the build and run commands:

**Build Command:**

```
npm install -g @microsoft/api-extractor @microsoft/api-documenter @testing-library/jest-dom rimraf turbo
npx turbo run build --filter=@medplum/server
```

**Run Command:**

```
node packages/server/dist/index.js env
```

**Medplum Configuration**

Set up environment variables in the DigitalOcean interface:

**Database connection**

Indicate that the app and the database are related to enable connections.

[How to add my DigitalOcean App as a trusted resource for my Managed Database](https://docs.digitalocean.com/products/app-platform/how-to/manage-databases/)

```
NODE_ENV=development
MEDPLUM_PORT=8103
MEDPLUM_BASE_URL=https://medplum.yourdomain.com/
MEDPLUM_ISSUER=https://medplum.yourdomain.com/
MEDPLUM_JWKS_URL=https://medplum.yourdomain.com/.well-known/jwks.json
MEDPLUM_AUTHORIZE_URL=https://medplum.yourdomain.com/oauth2/authorize
MEDPLUM_TOKEN_URL=https://medplum.yourdomain.com/oauth2/token
MEDPLUM_USER_INFO_URL=https://medplum.yourdomain.com/oauth2/userinfo
MEDPLUM_APP_BASE_URL=https://ehr.yourdomain.com/
MEDPLUM_STORAGE_BASE_URL=https://your-storage-url
MEDPLUM_MAX_JSON_SIZE=1mb
MEDPLUM_MAX_BATCH_SIZE=50mb
MEDPLUM_BCRYPT_HASH_SALT=10
MEDPLUM_SHUTDOWN_TIMEOUT_MILLISECONDS=30000
MEDPLUM_ACCURATE_COUNT_THRESHOLD=1000000
MEDPLUM_EMAIL_PROVIDER=smtp
MEDPLUM_SUPPORT_EMAIL=support@yourdomain.com
MEDPLUM_DATABASE_HOST=your-database-host
MEDPLUM_DATABASE_PORT=25060
MEDPLUM_DATABASE_DBNAME=your-database-name
MEDPLUM_DATABASE_USERNAME=your-database-username
MEDPLUM_DATABASE_PASSWORD=your-database-password
MEDPLUM_DATABASE_SSL_CA="-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----"
MEDPLUM_DATABASE_SSL_REJECT_UNAUTHORIZED=true
MEDPLUM_DATABASE_SSL_REQUIRE=true
MEDPLUM_DATABASE_QUERY_TIMEOUT=60000
MEDPLUM_DATABASE_RUN_MIGRATIONS=true
MEDPLUM_DATABASE_MAX_CONNECTIONS=10
MEDPLUM_REDIS_HOST=your-redis-host
MEDPLUM_REDIS_PORT=6379
MEDPLUM_REDIS_PASSWORD=your-redis-password
MEDPLUM_REDIS_DB=0
MEDPLUM_REDIS_TLS={}
MEDPLUM_SMTP_HOST=your-smtp-host
MEDPLUM_SMTP_PORT=587
MEDPLUM_SMTP_USERNAME=your-smtp-username
MEDPLUM_SMTP_PASSWORD=your-smtp-password
MEDPLUM_GOOGLE_CLIENT_ID=your-google-client-id
MEDPLUM_GOOGLE_CLIENT_SECRET=your-google-client-secret
MEDPLUM_RECAPTCHA_SITE_KEY=your-recaptcha-site-key
MEDPLUM_RECAPTCHA_SECRET_KEY=your-recaptcha-secret-key
MEDPLUM_LOG_LEVEL=info
MEDPLUM_LOG_REQUESTS=true
MEDPLUM_LOG_AUDIT_EVENTS=true
MEDPLUM_SAVE_AUDIT_EVENTS=true
MEDPLUM_REGISTER_ENABLED=true
MEDPLUM_INTROSPECTION_ENABLED=true
MEDPLUM_KEEP_ALIVE_TIMEOUT=60000
MEDPLUM_VM_CONTEXT_BOTS_ENABLED=true
MEDPLUM_HEARTBEAT_MILLISECONDS=30000
MEDPLUM_HEARTBEAT_ENABLED=true
MEDPLUM_MAX_SEARCH_OFFSET=1000
MEDPLUM_DEFAULT_RATE_LIMIT=100
MEDPLUM_DEFAULT_AUTH_RATE_LIMIT=100
MEDPLUM_MAX_BOT_LOG_LENGTH_FOR_RESOURCE=1000
MEDPLUM_MAX_BOT_LOG_LENGTH_FOR_LOGS=1000
MEDPLUM_CHAINED_SEARCH_WITH_REFERENCE_TABLES=true
```

## Conclusion

By following these steps, you should be able to set up and run Medplum on
DigitalOcean successfully. Make sure to replace the placeholder values with your
actual configuration details. If you encounter any issues, refer to the Medplum
documentation or seek help from the community.