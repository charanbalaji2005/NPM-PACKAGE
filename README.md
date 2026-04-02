# charan-auth-kit

I have personal felt that all Mern web users are wasting their time on their Authentication pages for hours or days to it to make it easy i have created this NPM_PACKAGE for the Web-Developer.

> Scaffold a complete full-stack JWT auth system in seconds.
> Express backend + React frontend — zero config, works with any Node ≥ 14.

## Usage

```bash
npm install charan7/auth-kit-backend
npx charan-auth-kit my-app
```

That's it. You get:

```
my-app/
├── AUTH-KIT-backend/    ← Express · JWT · bcrypt · role-based access
└── AUTH-KIT-frontend/   ← React · Vite · Axios · protected routes
```

## Run it

```bash
# Backend
cd my-app/AUTH-KIT-backend
npm install
node examples/app.js     # → http://localhost:3000

# Frontend (new terminal)
cd my-app/AUTH-KIT-frontend
npm install
npm run dev              # → http://localhost:5173
```

## API endpoints (auto-registered)

| Method | Path           | Auth required |
|--------|----------------|---------------|
| POST   | /auth/register | ✗             |
| POST   | /auth/login    | ✗             |
| GET    | /auth/me       | ✔ Bearer JWT  |

## Storage adapters

| Value      | Requires         |
|------------|------------------|
| `memory`   | nothing (default)|
| `mongo`    | `npm i mongoose` |
| `postgres` | `npm i pg`       |

```js
setupAuth(app, { storage: 'mongo', mongoUri: process.env.MONGO_URI });
```

## Protect your own routes

```js
const { setupAuth, authMiddleware, roleMiddleware } = require('./index');
setupAuth(app, { jwtSecret: process.env.JWT_SECRET });

app.get('/dashboard', authMiddleware, (req, res) => {
  res.json({ user: req.user });
});

app.delete('/admin', authMiddleware, roleMiddleware.requireRole('admin'), handler);
```

## Node version

Works on Node **14, 16, 18, 20, 22** — no engine restrictions.

## License

MIT © charan
