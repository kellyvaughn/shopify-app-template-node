# 🧩Shopify App Template - Node with Typescript

This is a template for building a [Shopify app] using Node and React with Typescript.

## What are the differences from [original](https://github.com/Shopify/shopify-app-template-node)?

- All important js files converted to ts
- Add some packages
  - Eslint
  - Prettier
  - Prisma for easy database management
- Define original types
- Add example app code with billing

**Please feel free to contribute if you find some issues.**

## Quickstart

1. Clone the repo,

```sh
npx degit SaeedYasin/shopify-app-template-node shopify-app-ts && npx degit SaeedYasin/shopify-frontend-template-react shopify-app-ts/web/frontend
```

2. Go to your app's directory and install packages.

```sh
cd shopify-app-ts && pnpm i
```

3. You can delete the `.gitmodules` file.

4. Go to `shopify-app-ts/web/backend` folder and rename `.env.example` to `.env` and fill the values. Do same for `shopify-app-ts/web/frontend` folder.

5. On shopify partner's dashboard, select your app and then go to "App setup". In the "Protected customer data access" section click "request Access" and then fill out all information, give reasons for all fields like name/email/phone/address. If your app doesn't need this info then you can edit this info in `shopify-app-ts\web\middleware\shopData.ts`.

6. Go to your app's directory and then run the app,

```sh
cd shopify-app-ts && pnpm dev
```

- Install and start using the app by opening provided URL in your browser: _https://some-ngrok-subdomain-xxxx.ngrok.io?shop=your-shop-name.myshopify.com&host=YourHostValue_

# Important Links

- Shopify-api v6 changes: _https://github.com/Shopify/shopify-api-js/blob/main/docs/migrating-to-v6.md#changes-to-api-clients_
- Shopify-api v6 getting started _https://github.com/Shopify/shopify-api-js/blob/main/README.md#configurations_
- Shopify-api v6 reference docs _https://github.com/Shopify/shopify-api-js/blob/main/docs/reference/README.md_
- @shopify/admin-graphql-api-utilities details _https://github.com/Shopify/quilt/blob/main/packages/admin-graphql-api-utilities/README.md_
- Typescript docs _https://www.typescriptlang.org/docs/_
- [React typescript docs](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example)
- [Shopify Polaris Documents](https://polaris.shopify.com/)

# Deployment

- _https://www.shopify.com/partners/blog/oauth-recommendations_

- Create a SECOND public app in your Shopify partner account. As App url and allowed redirect urls simply add https://localhost/ for now. It's important to have two apps, one created previously for development and a new one which will be your production app. I would suggest to call them differently, I simply use the same name and add "(development)" in the name of the one I use in development.
- Deploy to any hosting service and configure your env variables on it (from the production app we just created) and get its public URL.
- Go to your newly created app (the production one) in shopify partners dashboard and in your app setup, paste the url from your hosting service in the App url (e.g https://your-app-domain.com/), and in the Allowed redirection URL(s) add the same url with the suffix /auth/callback, /auth/shopify/callback and /api/auth/callback e-g,

```sh
https://your-app-domain.com/auth/callback
https://your-app-domain.com/auth/shopify/callback
https://your-app-domain.com/api/auth/callback
```

- Add your gdpr routes as well i-e https://your-app-domain.com/api/webhooks/customers_data_request, https://your-app-domain.com/api/webhooks/customers_redact, https://your-app-domain.com/api/webhooks/shop_redact.
- Then using https://your-app-domain.com?shop=your-shop-name.myshopify.com you can install the app to test it out.

- We can also follow these steps to deploy app on fly.io or heroku, _https://shopify.dev/apps/deployment/web_
  - Fly.io setting up MySQL _https://fly.io/docs/app-guides/mysql-on-fly_
  - Fly.io autoscalling _https://fly.io/docs/reference/scaling_

Every time you work on your development app, you can just follow the workflow described above, and when you are ready to push your changes to production, you will simply need to commit and push your changes to Github as normal, and your hosting service maybe can pick up these new changes and push to your app and deploy the new changes to your hosted app.

This means, one code base but 2 apps, this is the most common workflow used by App Developers. 🎉

# Credits

Thanks to [tomotomy](https://github.com/tomotomy/shopify-app-template-node-typescript) and [KaiSpencer](https://github.com/KaiSpencer/shopify-app-template-node-ts) and [Michael Gibbons](https://github.com/Michael-Gibbons/OSB) shopify app starter template for many of the ideas and code samples used in this template.

---

# Shopify App Template - Node（Original）

This is a template for building a [Shopify app](https://shopify.dev/apps/getting-started) using Node and React. It contains the basics for building a Shopify app.

Rather than cloning this repo, you can use your preferred package manager and the Shopify CLI with [these steps](#installing-the-template).

## Benefits

Shopify apps are built on a variety of Shopify tools to create a great merchant experience. The [create an app](https://shopify.dev/apps/getting-started/create) tutorial in our developer documentation will guide you through creating a Shopify app using this template.

The Node app template comes with the following out-of-the-box functionality:

- OAuth: Installing the app and granting permissions
- GraphQL Admin API: Querying or mutating Shopify admin data
- REST Admin API: Resource classes to interact with the API
- Shopify-specific tooling:
  - AppBridge
  - Polaris
  - Webhooks

## Tech Stack

This template combines a number of third party open-source tools:

- [Express](https://expressjs.com/) builds the backend.
- [Vite](https://vitejs.dev/) builds the [React](https://reactjs.org/) frontend.
- [React Router](https://reactrouter.com/) is used for routing. We wrap this with file-based routing.
- [React Query](https://react-query.tanstack.com/) queries the Admin API.

The following Shopify tools complement these third-party tools to ease app development:

- [Shopify API library](https://github.com/Shopify/shopify-node-api) adds OAuth to the Express backend. This lets users install the app and grant scope permissions.
- [App Bridge React](https://shopify.dev/apps/tools/app-bridge/getting-started/using-react) adds authentication to API requests in the frontend and renders components outside of the App’s iFrame.
- [Polaris React](https://polaris.shopify.com/) is a powerful design system and component library that helps developers build high quality, consistent experiences for Shopify merchants.
- [Custom hooks](https://github.com/Shopify/shopify-frontend-template-react/tree/main/hooks) make authenticated requests to the Admin API.
- [File-based routing](https://github.com/Shopify/shopify-frontend-template-react/blob/main/Routes.jsx) makes creating new pages easier.

## Getting started

### Requirements

1. You must [download and install Node.js](https://nodejs.org/en/download/) if you don't already have it.
1. You must [create a Shopify partner account](https://partners.shopify.com/signup) if you don’t have one.
1. You must [create a development store](https://help.shopify.com/en/partners/dashboard/development-stores#create-a-development-store) if you don’t have one.

### Installing the template

This template can be installed using your preferred package manager:

Using yarn:

```shell
yarn create @shopify/app
```

Using npm:

```shell
npm init @shopify/app@latest
```

Using pnpm:

```shell
pnpm create @shopify/app@latest
```

This will clone the template and install the required dependencies.

#### Local Development

[The Shopify CLI](https://shopify.dev/apps/tools/cli) connects to an app in your Partners dashboard. It provides environment variables, runs commands in parallel, and updates application URLs for easier development.

You can develop locally using your preferred package manager. Run one of the following commands from the root of your app.

Using yarn:

```shell
yarn dev
```

Using npm:

```shell
npm run dev
```

Using pnpm:

```shell
pnpm run dev
```

Open the URL generated in your console. Once you grant permission to the app, you can start development.

## Deployment

### Application Storage

This template uses [SQLite](https://www.sqlite.org/index.html) to store session data. The database is a file called `database.sqlite` which is automatically created in the root. This use of SQLite works in production if your app runs as a single instance.

The database that works best for you depends on the data your app needs and how it is queried. You can run your database of choice on a server yourself or host it with a SaaS company. Here’s a short list of databases providers that provide a free tier to get started:

| Database   | Type             | Hosters                                                                                                                                                                                                                               |
| ---------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MySQL      | SQL              | [Digital Ocean](https://www.digitalocean.com/try/managed-databases-mysql), [Planet Scale](https://planetscale.com/), [Amazon Aurora](https://aws.amazon.com/rds/aurora/), [Google Cloud SQL](https://cloud.google.com/sql/docs/mysql) |
| PostgreSQL | SQL              | [Digital Ocean](https://www.digitalocean.com/try/managed-databases-postgresql), [Amazon Aurora](https://aws.amazon.com/rds/aurora/), [Google Cloud SQL](https://cloud.google.com/sql/docs/postgres)                                   |
| Redis      | Key-value        | [Digital Ocean](https://www.digitalocean.com/try/managed-databases-redis), [Amazon MemoryDB](https://aws.amazon.com/memorydb/)                                                                                                        |
| MongoDB    | NoSQL / Document | [Digital Ocean](https://www.digitalocean.com/try/managed-databases-mongodb), [MongoDB Atlas](https://www.mongodb.com/atlas/database)                                                                                                  |

To use one of these, you need to change your session storage configuration. To help, here’s a list of [SessionStorage adapter packages](https://github.com/Shopify/shopify-api-js/tree/main/docs/usage/session-storage.md).

### Build

The frontend is a single page app. It requires the `SHOPIFY_API_KEY`, which you can find on the page for your app in your partners dashboard. Paste your app’s key in the command for the package manager of your choice:

Using yarn:

```shell
cd web/frontend/ && SHOPIFY_API_KEY=REPLACE_ME yarn build
```

Using npm:

```shell
cd web/frontend/ && SHOPIFY_API_KEY=REPLACE_ME npm run build
```

Using pnpm:

```shell
cd web/frontend/ && SHOPIFY_API_KEY=REPLACE_ME pnpm run build
```

You do not need to build the backend.

## Hosting

When you're ready to set up your app in production, you can follow [our deployment documentation](https://shopify.dev/apps/deployment/web) to host your app on a cloud provider like [Heroku](https://www.heroku.com/) or [Fly.io](https://fly.io/).

When you reach the step for [setting up environment variables](https://shopify.dev/apps/deployment/web#set-env-vars), you also need to set the variable `NODE_ENV=production`.

## Known issues

### Hot module replacement and Firefox

When running the app with the CLI in development mode on Firefox, you might see your app constantly reloading when you access it.
That happened in previous versions of the CLI, because of the way HMR websocket requests work.

We fixed this issue with v3.4.0 of the CLI, so after updating it, you can make the following changes to your app's `web/frontend/vite.config.js` file:

1. Change the definition `hmrConfig` object to be:

   ```js
   const host = process.env.HOST
     ? process.env.HOST.replace(/https?:\/\//, "")
     : "localhost";

   let hmrConfig;
   if (host === "localhost") {
     hmrConfig = {
       protocol: "ws",
       host: "localhost",
       port: 64999,
       clientPort: 64999,
     };
   } else {
     hmrConfig = {
       protocol: "wss",
       host: host,
       port: process.env.FRONTEND_PORT,
       clientPort: 443,
     };
   }
   ```

1. Change the `server.host` setting in the configs to `"localhost"`:

   ```js
   server: {
     host: "localhost",
     ...
   ```

### I can't get past the ngrok "Visit site" page

When you’re previewing your app or extension, you might see an ngrok interstitial page with a warning:

```text
You are about to visit <id>.ngrok.io: Visit Site
```

If you click the `Visit Site` button, but continue to see this page, then you should run dev using an alternate tunnel URL that you run using tunneling software.
We've validated that [Cloudflare Tunnel](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/run-tunnel/trycloudflare/) works with this template.

To do that, you can [install the `cloudflared` CLI tool](https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/installation/), and run:

```shell
# Note that you can also use a different port
cloudflared tunnel --url http://localhost:3000
```

Out of the logs produced by cloudflare you will notice a https URL where the domain ends with `trycloudflare.com`. This is your tunnel URL. You need to copy this URL as you will need it in the next step.

```shell
2022-11-11T19:57:55Z INF Requesting new quick Tunnel on trycloudflare.com...
2022-11-11T19:57:58Z INF +--------------------------------------------------------------------------------------------+
2022-11-11T19:57:58Z INF |  Your quick Tunnel has been created! Visit it at (it may take some time to be reachable):  |
2022-11-11T19:57:58Z INF |  https://randomly-generated-hostname.trycloudflare.com                                     |
2022-11-11T19:57:58Z INF +--------------------------------------------------------------------------------------------+
```

Below you would replace `randomly-generated-hostname` with what you have copied from the terminal. In a different terminal window, navigate to your app's root and with the URL from above you would call:

```shell
# Using yarn
yarn dev --tunnel-url "https://randomly-generated-hostname.trycloudflare.com:3000"
# or using npm
npm run dev --tunnel-url "https://randomly-generated-hostname.trycloudflare.com:3000"
# or using pnpm
pnpm dev --tunnel-url "https://randomly-generated-hostname.trycloudflare.com:3000"
```

## Developer resources

- [Introduction to Shopify apps](https://shopify.dev/apps/getting-started)
- [App authentication](https://shopify.dev/apps/auth)
- [Shopify CLI](https://shopify.dev/apps/tools/cli)
- [Shopify API Library documentation](https://github.com/Shopify/shopify-api-js#readme)
