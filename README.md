# AstraDemo

Reference application demonstrating AstraOps deployment capabilities. A simple full-stack points counter application deployed to AWS EKS.

## What It Is

A three-tier web application that showcases containerized microservices deployment:

- **Frontend:** React SPA served by Nginx (port 80)
- **Backend:** Express.js REST API (port 5000)
- **Database:** MongoDB for data persistence (port 27017)

The application allows users to increment/decrement a global counter value (0-10) with real-time UI updates.

## Technology Stack

- **Frontend:** React 18, Vite, Nginx
- **Backend:** Node.js 18, Express.js, Mongoose
- **Database:** MongoDB
- **Infrastructure:** Docker, AstraOps, AWS EKS, GitHub Actions

## Local Development

Frontend:
```bash
cd front
npm install
npm run dev  # http://localhost:5173
```

Backend:
```bash
cd back
npm install
export MONGO_URI="mongodb://localhost:27017/points_db"
npm start  # http://localhost:5000
```

Database:
```bash
docker run -d -p 27017:27017 mongo:latest
```

## API Endpoints

- `GET /api/points` - Get current counter value
- `POST /api/points/increment` - Increment counter (max 10)
- `POST /api/points/decrement` - Decrement counter (min 0)

## Deployment with AstraOps

The `astraops.yaml` configuration file defines the deployment:

```yaml
applicationName: points-fullstack
services:
  - name: frontend
    image: jorgeflorentino8/astrademo-frontend:latest
    port: 80
  - name: backend
    image: jorgeflorentino8/astrademo-backend:latest
    port: 5000
  - name: database
    image: mongo:latest
    port: 27017
```

Deploy using the CLI:
```bash
astraops-cli deploy --monitoring
```

CI/CD: The repository uses GitHub Actions to build Docker images and deploy automatically on push to `main` branch.

## Project Structure

```
front/          # React + Vite frontend
back/           # Express.js backend
astraops.yaml   # Deployment configuration
.github/        # CI/CD workflows
```

## Documentation

For comprehensive documentation, visit [DeepWiki Documentation](https://deepwiki.com/AstraOpsOrg/AstraDemo).

## License

Apache License 2.0