# StarterCraft Monorepo

**StarterCraft Monorepo** is an opinionated monorepo setup that allows you to easily create and manage multiple frontend apps using StarterCraft, run Node.js servers, and develop internal libraries without the need for excessive publishing.

This setup is ideal for scaling projects, sharing code between apps, and maintaining a consistent development workflow.

---

## 📂 Folder Structure

```
startercraft-monorepo/
├── packages/
│   ├── web/             # StarterCraft frontend app
│   ├── backend/         # Node.js server
│   └── @myorg/ui/       # Internal UI library
├── node_modules/
├── package.json
├── pnpm-workspace.yaml  # Defines all workspace packages
├── tsconfig.base.json   # Base TypeScript configuration
└── README.md
```

* **packages/**: Contains all apps, servers, and internal libraries.
* **workspace**: The monorepo uses PNPM/Yarn workspaces to manage dependencies and link packages internally.
* **@myorg/ui**: Example of a fully-featured internal library that can be imported by frontend apps without publishing.

---

## ⚡ Key Features

* **Multiple Frontend Apps**: Each app can use StarterCraft as a base.
* **Node.js Servers**: Run backend services directly in the monorepo.
* **Internal Libraries**: Create reusable libraries (UI components, utilities, etc.) shared across apps.
* **Workspace Linking**: No need to publish internal libraries to NPM; apps can reference them locally via workspaces.

---
## 🚀 Create a New Project

To quickly start a new frontend project using the StarterCraft template, run:
```sh
npx create-startercraft my-awesome-scalable-project
```

Replace my-awesome-scalable-project with your desired project name. This command will create a new project with all configurations, best practices, and StarterCraft defaults included.

Once created, move the new project into the monorepo:
```sh
mv my-awesome-scalable-project packages/my-new-app
```

Install dependencies and link local packages:
```sh
pnpm install
```

Your new StarterCraft app is now fully part of the monorepo and can consume internal libraries like @myorg/ui without publishing.

## ➕ Adding a New App

1. Create a new folder inside `packages/`:

```bash
mkdir packages/my-new-app
```

2. Initialize a new package:

```bash
cd packages/my-new-app
pnpm init
```

3. Add your frontend or Node.js project structure.
4. Add the new app to your workspace (`pnpm-workspace.yaml`):

```yaml
packages:
  - "packages/*"
```

5. Install dependencies and link local packages:

```bash
pnpm install
```

---

## ➕ Adding a New Library

1. Create a new library folder inside `packages/`:

```bash
mkdir packages/@myorg/my-lib
cd packages/@myorg/my-lib
pnpm init
```

2. Add your code (e.g., TypeScript, React components).
3. Add build and dev scripts in `package.json`. For example, using `tsup`:

```json
"scripts": {
  "dev": "tsup src/index.tsx --watch",
  "build": "tsup src/index.tsx --format cjs,esm --dts"
}
```

4. Import this library in your apps using the workspace alias:

```ts
import { MyComponent } from "@myorg/my-lib";
```

5. Run `pnpm install` at the root to link everything automatically.

---

## ⚙️ Workspaces

This monorepo uses **PNPM Workspaces** to manage dependencies:

* Packages inside `packages/` are automatically linked.
* Changes in internal libraries are immediately available in apps without publishing.
* Reduces duplication of dependencies across packages.

---

## 🚀 Getting Started

1. Install dependencies:

```bash
pnpm install
```

2. Run the frontend app:

```bash
pnpm --filter web dev
```

3. Run the backend server:

```bash
pnpm --filter backend dev
```

4. Run all projects concurrently:

```bash
pnpm run dev
```

---

## ✅ Advantages

* Centralized development for multiple apps and libraries
* Easy integration of internal libraries
* No need for frequent publishing of shared code
* Scalable structure suitable for large teams and projects
