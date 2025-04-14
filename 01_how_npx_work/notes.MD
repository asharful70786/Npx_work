# How `npx` Works – Step by Step

> `npx` is a powerful CLI tool that comes with `npm`. It allows you to run Node.js packages without installing them globally.

## Step-by-Step Process

### 🥇 Step 1: Check Local Project (current directory)

1. `npx` checks for a `package.json` file in the current project directory.
2. If it exists, it looks for the specified command in:
   - The `name` field of the package.
   - The `bin` field, which tells where the executable file is located.
3. If found, it uses the local executable (from `./node_modules/.bin/`).

✅ If command is found here, `npx` runs it and exits.

---

### 🥈 Step 2: Check `node_modules/.bin/`

If not found in `package.json`, `npx` directly checks:
```bash
./node_modules/.bin/<command-name>
```

✅ If found, it executes that local version.

---

### 🥉 Step 3: Check Global Packages

If not found locally, `npx` searches for globally installed packages.

- It checks the global `node_modules` path.
- You can find the global install location by running:
```bash
npm root -g
```
or
```bash
npm prefix -g
```

✅ If the command is installed globally, `npx` uses it.

---

### 🏅 Step 4: Download from NPM Registry (Remote)

If not found locally or globally:

1. `npx` searches the npm registry for the package.
2. If it finds the package, it downloads and installs it **temporarily** in a cache folder.

✅ Then runs the command from there.

---

### 💾 Step 5: Use NPX Cache

- `npx` keeps downloaded packages in a **cache** directory for reuse.
- Cache path:
```bash
~/.npm/_npx/<hash>/
```
- You can inspect this folder to see the temporary files used by `npx`.

---

## 🔄 Summary Flow

```text
Local package.json  →  ./node_modules/.bin/  →  Global packages  →  NPM Registry →  NPX Cache
```

---

## 🖠 Tips

- To clear the cache:  
  ```bash
  npx clear-npx-cache
  ```

- You can also run commands without installing globally, e.g.:
  ```bash
  npx create-react-app my-app
  ```

---

## 📚 References

- [npm official docs](https://docs.npmjs.com/)
- Try exploring `which npx`, `npx --version`, and `npm config list` for deeper insights.

