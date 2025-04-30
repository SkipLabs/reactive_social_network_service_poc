# Reactive Social Network Service (Proof of Concept)

This repository demonstrates a minimal reactive programming system using [Skip](https://www.skiplabs.io/) and TypeScript to simulate a basic social network use case. The goal is to keep things simple, inspectable, and educational.

> “The simpler, the merrier.”

## 🧠 What It Does

We build a tiny reactive service to track "active friends" in social groups. It:
- Defines users and groups as reactive data.
- Tracks active users and friend connections.
- Uses Skip to auto-update data dependencies.
- Exposes a small REST API using Express.

### Example: 
We show how Alice’s list of active friends updates live as data changes, no manual refresh needed.

---

## 📁 Project Structure

```bash
src/
├── activefriends.mts   # Mappers & resources to track active friends
├── data.mts            # Initial user and group data
├── index.ts            # Express server exposing API
├── skipservice.mts     # Skip service and reactive graph
└── types.mts           # Type definitions and Skip interfaces
```

## 🚀 Getting Started
### 1. Clone the Repo
```bash
git clone https://github.com/SkipLabs/reactive_social_network_service_poc
cd reactive_social_network_service
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Build the Project
```bash
npm run build
```

### 4. Start the Service
```bash
npm run start
```
You should see:

```bash
Skip control service listening on port 8081
Skip streaming service listening on port 8080
Groups REST wrapper listening at port 8082
```

## 🔍 Try It Out
### 1. Listen to Alice’s Active Friends
In a new terminal:

```bash
curl -LN http://localhost:8082/active_friends/1
```

### 2. Update Alice's Friends (e.g., Add Eve)
In a third terminal:
```bash
curl http://localhost:8081/v1/inputs/users \
  -X PATCH \
  --json '[[1, [
    {
      "name": "Alice",
      "active": true,
      "friends": [0, 2, 3]
    }
  ]]]'
```
You’ll see reactive updates in the second terminal!

⚙️ NPM Scripts

`npm run build`: Compile TypeScript files into dist/
`npm run start`: Launch the Express and Skip services
`npm run clean`: Remove dist/ and node_modules

🧩 Tech Stack
 - TypeScript
 - Node.js
 - Skip – for reactive data flows
 - Express – lightweight REST API server
