# How to Open This Project in VS Code

## Quick Start

### Option 1: Open from Command Line (Recommended)

1. **Navigate to the project folder:**
   ```bash
   cd path/to/los1
   ```

2. **Open in VS Code:**
   ```bash
   code .
   ```
   
   If the `code` command doesn't work, you may need to [install it first](#installing-code-command).

### Option 2: Open from VS Code

1. **Launch VS Code**
2. **Click** `File` → `Open Folder...`
3. **Navigate** to the `los1` folder
4. **Click** `Select Folder` (or `Open` on Mac)

## First-Time Setup

After opening the project, follow these steps:

### 1. Install Dependencies

Open a terminal in VS Code (`Terminal` → `New Terminal` or `` Ctrl+` ``) and run:

```bash
npm install
```

This installs all required packages including TypeScript, Solana libraries, and development tools.

### 2. Install Recommended VS Code Extensions

For the best development experience, install these extensions:

#### Essential Extensions:
- **TypeScript and JavaScript Language Features** (built-in, just enable)
- **ESLint** - Identifies code quality issues
- **Prettier** - Code formatter

#### Helpful Extensions:
- **npm Intellisense** - Autocomplete npm modules
- **Path Intellisense** - Autocomplete file paths
- **GitLens** - Enhanced Git features

**To install an extension:**
1. Click the Extensions icon in the sidebar (or press `Ctrl+Shift+X`)
2. Search for the extension name
3. Click `Install`

### 3. Build the Project

```bash
npm run build
```

This compiles TypeScript files from `src/` to JavaScript in `dist/`.

## Working with the Project in VS Code

### Running the Application

#### Development Mode (with auto-restart):
```bash
npm run dev
```
This uses `ts-node` to run TypeScript directly without building.

#### Production Mode:
```bash
npm run build
npm start
```
This builds and runs the compiled JavaScript.

### TypeScript IntelliSense

VS Code provides excellent TypeScript support out of the box:
- **Autocomplete**: Type to see suggestions
- **Go to Definition**: `F12` or `Ctrl+Click` on any symbol
- **Find References**: `Shift+F12`
- **Rename Symbol**: `F2`
- **Show Type**: Hover over any variable/function

### Debugging in VS Code

Create a debug configuration:

1. **Click** the Run icon in the sidebar (or press `Ctrl+Shift+D`)
2. **Click** `create a launch.json file`
3. **Select** `Node.js`
4. **Replace** the contents with:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug CLI",
      "runtimeArgs": ["-r", "ts-node/register"],
      "args": ["${workspaceFolder}/src/index.ts"],
      "cwd": "${workspaceFolder}",
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Built App",
      "program": "${workspaceFolder}/dist/index.js",
      "cwd": "${workspaceFolder}",
      "console": "integratedTerminal",
      "preLaunchTask": "npm: build"
    }
  ]
}
```

5. **Set breakpoints** by clicking to the left of line numbers
6. **Press** `F5` to start debugging

### Useful VS Code Shortcuts

| Action | Windows/Linux | Mac |
|--------|---------------|-----|
| Open terminal | `` Ctrl+` `` | `` Cmd+` `` |
| Command palette | `Ctrl+Shift+P` | `Cmd+Shift+P` |
| Quick file open | `Ctrl+P` | `Cmd+P` |
| Find in files | `Ctrl+Shift+F` | `Cmd+Shift+F` |
| Format document | `Shift+Alt+F` | `Shift+Option+F` |
| Toggle sidebar | `Ctrl+B` | `Cmd+B` |

### Project Structure in VS Code

```
los1/
├── src/                    # TypeScript source files
│   ├── index.ts           # CLI entry point
│   ├── moneyMover.ts      # Main orchestrator
│   ├── walletService.ts   # Blockchain interactions
│   ├── priceService.ts    # Token pricing
│   └── types.ts           # TypeScript types
├── dist/                   # Compiled JavaScript (after build)
├── node_modules/           # Dependencies (after npm install)
├── package.json           # Project configuration
├── tsconfig.json          # TypeScript configuration
├── example.js             # Usage example
└── README.md              # Documentation
```

## Installing `code` Command

If the `code .` command doesn't work:

### Windows:
The command should be available after installing VS Code. If not:
1. Open VS Code
2. Press `Ctrl+Shift+P`
3. Type "shell command"
4. Select `Shell Command: Install 'code' command in PATH`
5. Restart your terminal

### Mac:
1. Open VS Code
2. Press `Cmd+Shift+P`
3. Type "shell command"
4. Select `Shell Command: Install 'code' command in PATH`
5. Restart your terminal

### Linux:
The command is usually available after installation. If not, add VS Code to your PATH or use:
```bash
/path/to/VSCode/bin/code .
```

## Troubleshooting

### "Cannot find module" errors
**Solution:** Run `npm install` to install all dependencies.

### TypeScript errors in VS Code
**Solution:** 
1. Ensure TypeScript is installed: `npm install`
2. Reload VS Code: `Ctrl+Shift+P` → `Developer: Reload Window`

### Terminal not working
**Solution:** 
1. Check your default shell in settings
2. Try `Terminal` → `New Terminal`

### Build fails
**Solution:**
1. Delete `node_modules` and `package-lock.json`
2. Run `npm install` again
3. Run `npm run build`

## Next Steps

1. ✅ Open project in VS Code
2. ✅ Install dependencies (`npm install`)
3. ✅ Build the project (`npm run build`)
4. 📖 Read [WHAT_DOES_THIS_DO.md](./WHAT_DOES_THIS_DO.md) to understand the code
5. 📖 Read [README.md](./README.md) for usage instructions
6. 🚀 Run the application (`npm start` or `npm run dev`)

## Additional Resources

- [VS Code TypeScript Tutorial](https://code.visualstudio.com/docs/typescript/typescript-tutorial)
- [VS Code Node.js Debugging](https://code.visualstudio.com/docs/nodejs/nodejs-debugging)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
