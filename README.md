# Absolute Beginner's Guide to npm

Welcome to the world of Node.js and npm! If you are new to backend development or working with JavaScript outside the browser, package managers might sound intimidating. Don't worry—npm is simply an **app store for your code**.

---

## 1. What is npm?

- **npm** stands for **Node Package Manager**.
- It comes automatically bundled when you install Node.js.
- Think of it as a tool that lets you download and use helpful tools, libraries, and utilities written by other developers so you don't have to reinvent the wheel.

---

## 2. Setting Up & Checking Your Version

Before using npm, verify that it is properly installed on your computer.

### The Commands

```bash
node -v
npm -v
```

### 🎯 Mini-Exercise 0: The Health Check
1. Open your terminal (macOS/Linux) or Command Prompt / PowerShell / Git Bash (Windows).
2. Type `node -v` and hit **Enter**.
3. Type `npm -v` and hit **Enter**.
4. **Expected Result**: You should see version numbers printed (for example: `v20.x.x` and `10.x.x`). If you see an error like `command not found`, download and install Node.js from [nodejs.org](https://nodejs.org/).

---

## 3. Initializing a Project (`npm init`)

Every Node project begins with a blueprint file named `package.json`. This file keeps track of your project's name, version, and the packages you install.

### The Commands

- `npm init`: Launches an interactive questionnaire to configure your project.
- `npm init -y`: Skips all questions and accepts sensible defaults immediately (the `-y` stands for "yes").

### 🎯 Mini-Exercise 1: Create Your First Project
1. In your terminal, make a new folder and move into it:
   ```bash
   mkdir my-first-node-project
   cd my-first-node-project
   ```
2. Initialize the project with default settings:
   ```bash
   npm init -y
   ```
3. Look inside your folder (or type `ls` on macOS/Linux, `dir` on Windows).
4. **Expected Result**: You should see a file named `package.json`. If you open it in VS Code or Notepad, you will see JSON formatted data describing your project!

---

## 4. Installing Packages (`npm install`)

When you want to add an external library to your project, you use the install command.

### The Commands

- `npm install <package-name>` (or the shortcut `npm i <package-name>`)

### What happens when you run this?
- npm creates a folder called `node_modules` (where the actual code lives).
- npm creates a `package-lock.json` file (a fingerprint lock ensuring everyone gets the exact same code versions).
- npm records the package inside your `package.json` under `"dependencies"`.

### 🎯 Mini-Exercise 2: Say Hello with `cowsay`
1. Inside your `my-first-node-project` folder, run:
   ```bash
   npm install cowsay
   ```
2. Create a file called `index.js` in the same folder.
3. Add the following JavaScript code to `index.js`:
   ```javascript
   const cowsay = require("cowsay");

   console.log(
     cowsay.say({
       text: "I am using npm!",
       e: "oO",
       T: "U ",
     })
   );
   ```
4. Run your code in the terminal:
   ```bash
   node index.js
   ```
5. **Expected Result**: A friendly ASCII cow speaking your message should appear right in your terminal!

---

## 5. Development Dependencies (`--save-dev` or `-D`)

Some tools are only needed while you are actively writing code (like code formatters, test runners, or auto-restarting tools), but they aren't needed when your app runs in production.

### The Commands

- `npm install --save-dev <package-name>`
- Shortcut: `npm i -D <package-name>`

### 🎯 Mini-Exercise 3: Add a Dev Dependency
1. Install `nodemon` (a tool that automatically restarts Node apps when files change) as a development tool:
   ```bash
   npm i -D nodemon
   ```
2. Open your `package.json` file.
3. **Expected Result**: Notice that `nodemon` is placed under `"devDependencies"`, while `cowsay` remains under `"dependencies"`.

---

## 6. Running Scripts (`npm test`, `npm start`, `npm run`)

The `"scripts"` section in `package.json` lets you define custom shortcuts for terminal commands.

### The Commands

- `npm start`: Runs the script named `"start"`.
- `npm test`: Runs the script named `"test"`.
- `npm run <custom-name>`: Runs any custom script name you define.

### 🎯 Mini-Exercise 4: Create a Shortcut Script
1. Open `package.json` in your text editor.
2. Locate the `"scripts"` object and add `"start"` and `"cow"` lines:
   ```json
   "scripts": {
     "start": "node index.js",
     "cow": "node index.js"
   }
   ```
3. Save the file.
4. Run your built-in script:
   ```bash
   npm start
   ```
5. Run your custom script:
   ```bash
   npm run cow
   ```
6. **Expected Result**: Both commands run `node index.js` and show your cow!

---

## 7. Inspecting, Updating & Removing Packages

As projects grow, you will want to manage installed packages.

### Commands

| Command | What it does |
| :--- | :--- |
| `npm list --depth=0` | Lists top-level packages installed in your project |
| `npm outdated` | Checks if newer versions of your packages exist |
| `npm update` | Updates packages to the latest permitted version |
| `npm uninstall <package>` | Removes a package from `node_modules` and `package.json` |

### 🎯 Mini-Exercise 5: List and Remove a Package
1. Check what packages are installed:
   ```bash
   npm list --depth=0
   ```
2. Now, let's remove `cowsay`:
   ```bash
   npm uninstall cowsay
   ```
3. Check `package.json` again. Notice that `cowsay` is completely gone from the `"dependencies"` section!

---

## 8. Running Packages Without Installing (`npx`)

What if you just want to run a package once without downloading it into your project permanently? That is what `npx` (Node Package Execute) is for!

### 🎯 Mini-Exercise 6: Instant CLI Fun
1. Run this directly in your terminal:
   ```bash
   npx cowsay "No local installation needed!"
   ```
2. **Expected Result**: npm downloads the package temporarily, runs the command, prints the cow, and cleans up after itself.

---

## 9. Rebuilding an Existing Project (`npm install`)

If you download code from GitHub, the `node_modules` folder is almost never included (because it is huge). How do you get the dependencies back?

### 🎯 Mini-Exercise 7: The Reinstall Test
1. Delete your `node_modules` folder manually or run:
   - Mac/Linux: `rm -rf node_modules`
   - Windows (PowerShell): `Remove-Item -Recurse -Force node_modules`
2. Now, restore all dependencies defined in `package.json`:
   ```bash
   npm install
   ```
3. **Expected Result**: npm reads `package.json` and `package-lock.json` and restores the entire `node_modules` directory in seconds.

---

## 10. Summary Cheat Sheet

| Task | Command | Shortcut |
| :--- | :--- | :--- |
| Check versions | `node -v` / `npm -v` | |
| Initialize project | `npm init` | `npm init -y` |
| Install production package | `npm install <pkg>` | `npm i <pkg>` |
| Install dev package | `npm install --save-dev <pkg>` | `npm i -D <pkg>` |
| Restore all project packages | `npm install` | `npm i` |
| Remove package | `npm uninstall <pkg>` | `npm un <pkg>` |
| Run predefined scripts | `npm start` / `npm test` | |
| Run custom script | `npm run <script-name>` | |
| Execute one-time tool | `npx <pkg>` | |
| Check for updates | `npm outdated` | |
