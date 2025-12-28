# 🧭 Travelling Salesman

A dynamic visualization of the Travelling Salesman Problem designed to explore evolutionary computation. It implements a custom Genetic Algorithm that iteratively improves route efficiency using fitness evaluation and probabilistic operators. Uses Server-Sent Events to stream real-time generation updates via Nest.js and React.

## 📦 Technologies

- `TypeScript`
- `Nx`
- `NestJS`
- `React`
- `Vite`
- `Server-Sent Events`
- `SCSS`

## 🚀 Features

- **Genetic Optimization**: Solves the Travelling Salesman Problem using evolutionary operators like crossover, mutation, and selection to find optimal routes.
- **Real-time Streaming**: Uses Server-Sent Events for seamless, unidirectional state updates.
- **Interactive Map**: Visualizes cities and calculated paths on a dynamic map interface for easy inspection.
- **Configurable Heuristics**: Dynamic control over population size, mutation rate, elite group size, and generation limits.
- **Data Volume Control**: Option to toggle between streaming full generation data or only the best routes to optimize performance and network usage.
- **Convergence Detection**: Supports automatic stopping conditions based on population convergence or fixed generation counts.
- **Live Progress Tracking**: Monitors and displays the best route distance and current generation statistics in real-time.

## 🧬 How It Works

This project utilizes a Genetic Algorithm to address the Traveling Salesman Problem (TSP). By simulating natural selection, it evolves a set of possible routes over time, gradually improving them to find an efficient solution.

### Core Steps:

1.  **Initialization**: A starting population of random routes is generated.
2.  **Fitness Evaluation**: Each route is evaluated based on its total distance. Shorter paths are considered more "fit".
3.  **Selection (Elitism)**: A defined percentage of the best routes is automatically carried over to the next generation.
4.  **Crossover**: Offspring are created by combining genetic material from two parents. The algorithm employs an **Order Crossover** technique, which takes a sub-path from one parent and fills the remaining cities from the other parent in the order they appear, ensuring valid routes without duplicates.
5.  **Mutation**: To maintain genetic diversity, random swaps of two cities occur within a route based on the configurable `mutationRate`.
6.  **Termination**: The simulation stops when a fixed number of generations is reached or via the **Until Last Alive** mode. In **Until Last Alive** mode, the algorithm automatically halts when **over 50% of the population has converged to the same route distance**.

## 📍 The Process

This is a small educational project for researching genetic algorithms. This experience provided me with hands-on knowledge in client-server architecture, deploying servers using Docker containers, utilizing Server-Sent Events, and working with interactive canvases.

## 🏗️ System Architecture

The system is built as a unified **NestJS** and **React** application managed within an **Nx** monorepo:

- **Backend API** (`NestJS`): Handles the execution of the Genetic Algorithm. It manages the population lifecycle, performs crossover and mutation operations, and evaluates fitness scores on the server.
- **Real-time Stream** (`Server-Sent Events`): A dedicated unidirectional channel that streams generation updates from the server to the client in real-time.
- **Client** (`React`): Consumes the SSE stream and renders the visualization. It provides an interactive interface for configuring algorithm parameters and viewing the optimization process on a dynamic map.
- 
## 📂 Project Structure

This monorepo project is organized into the following key areas:

- `apps/client` - Main React frontend application built with Vite.
  - `src/app/ControlsPanel.tsx` - UI for configuring algorithm parameters.
  - `src/app/Map.tsx` - Component responsible for visualizing cities and the current best path.
  - `src/app/ResultsViewer.tsx` - Displays real-time statistics and generation progress.
  - `src/main.tsx` - Application entry point.

- `apps/server` - Backend NestJS application.
  - `src/app` - API module handling HTTP requests and SSE stream management.
  - `src/main.tsx` - Server entry point and configuration.

- `libs/algorithm` - Core logic implementation of the Genetic Algorithm.
  - `src/lib/algorithm.ts` - Contains the `TSPSolver` class with methods for selection, crossover, and mutation.

- `libs/shared` - Shared TypeScript definitions.
  - `src/lib/types.ts` - Common interfaces for `Point`, `Route`, `Generation`, and configuration parameters used by both client and server.

## 🚦 Running the Project

1. Clone the repository
2. Install dependencies: `npm install`
3. Start the applications:
### Client
```
npx nx serve client
```
### Server
Option A: Development Mode
```
npx nx serve server
```
Option B: Docker Mode 

**Build:**
```
npx nx run server:docker-build
```

**Run:**
```
docker run -p 3000:3000 server
```

4. Open `http://localhost:4200` in your browser
> [!TIP]
> Highly recommend installing the Nx Console extension for VS Code.

## 🎞️ Preview

https://github.com/user-attachments/assets/86893265-4180-4b2a-a4aa-7e5d740d635f
