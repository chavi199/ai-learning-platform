# AI learning platform

A full-stack application that generates a lesson from a topic. A signed-in user chooses a category, the server asks OpenAI for the lesson, and the result is stored in MongoDB. An admin manages categories and sub-categories.

The interface supports Hebrew and English.

## Stack

- React 18, TypeScript, Vite, Tailwind CSS
- Node.js, Express, TypeScript
- MongoDB and Mongoose
- JWT authentication, with an admin role
- OpenAI API
- Docker Compose

## Run with Docker

Docker Desktop has to be running.

```bash
cp server/.env.example server/.env
```

Set `JWT_SECRET` and `OPENAI_API_KEY` in `server/.env`. The example file already points `MONGO_URI` at the MongoDB container.

```bash
docker compose up -d --build
docker compose exec -T server npm run seed-categories
docker compose exec -T server npm run create-admin
```

- Frontend: `http://localhost:5173`
- API: `http://localhost:5000`

`create-admin` asks for an email and a password. That account can manage categories.

## Run without Docker

Start MongoDB locally, set `MONGO_URI` to that instance, then:

```bash
cd server
npm install
npm run dev
npm run seed-categories
```

```bash
cd frontend
npm install
npm run dev
```

## Layout

```text
frontend/     React application
server/       Express API, models, and seed scripts
docker-compose.yml
```

The lesson API is under `/api/lessons`. Categories are under `/api/categories`, and sign-in is under `/api/users`.
