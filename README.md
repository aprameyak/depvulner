# Dependency Vulnerability Aggregator

A small Express app for keeping a list of dependencies across repositories, with their current and latest versions and whether each is marked vulnerable. It is for developers who want one place to track outdated or flagged packages by hand.

## Features

- Record a dependency with its repository, current version, and latest version
- Mark a dependency as vulnerable or not
- Returns a count of dependencies marked vulnerable
- Saves entries to a local `data.json` file

## Getting started

Requires Node.js.

```bash
npm install
npm start
```

The server runs on http://localhost:3023. Add a dependency and list them:

```bash
curl -X POST http://localhost:3023/api/deps \
  -H "Content-Type: application/json" \
  -d '{"repo":"my-app","dep":"lodash","current":"4.17.15","latest":"4.17.21","vulnerable":true}'

curl http://localhost:3023/api/deps
```

## How it works

- `server.js` is an Express server with `POST /api/deps` and `GET /api/deps`. The GET response includes the 100 most recent entries and the number marked vulnerable.
- Vulnerability status comes from what you submit. The app does not scan lockfiles or query any advisory database.
- Entries are stored in `data.json` in the project folder, which is created on first run and ignored by git.
- `index.html` is served at the root URL but is still a generic placeholder form that is not connected to this API. `utils.js` contains helpers that `server.js` does not use yet.

## Status

Prototype. Manual data entry only; the web page is not wired up, and there is no validation or authentication.

## License

MIT, see [LICENSE](LICENSE).
