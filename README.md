# Firesale

A desktop Markdown editor built with Electron, TypeScript, and Vite. Edit Markdown and preview the rendered output side by side.

Based on the [Electron v3 course](https://frontendmasters.com/courses/electron-v3/) on Frontend Masters.

## Features

- Live Markdown preview with GitHub Flavored Markdown support.
- Open and save local `.md` files using native dialogs.
- Export the preview as HTML.
- Reveal an opened file in the file manager or open it in the default application.

## Getting started

Requires **Node.js 22.12+**, **pnpm 12.3.4**, and Git.

```sh
git clone https://github.com/EricTsai83/firesale.git
cd firesale
pnpm install --frozen-lockfile
pnpm start
```

If pnpm is not available, run `corepack enable` when Corepack is installed, or install it with `npm install --global pnpm@12.3.4`. No environment variables or backend services are required.

## Usage

Type in the left pane to preview Markdown on the right, or choose **Open File** to edit an existing document. Use **Save File** to save changes and **Save HTML** to export the preview.

Open files with **File → Open**, `Cmd+O` on macOS, or `Ctrl+O` on Windows and Linux. After opening a file, **Show File** and **Open in Default Application** provide access through the operating system.

## Development and packaging

| Command | Description |
| --- | --- |
| `pnpm start` | Launch the app in development mode. |
| `pnpm package` | Build and package the app into `out/`. |
| `pnpm make` | Create distribution files in `out/make/`. |

Configured formats are ZIP for macOS, Squirrel.Windows for Windows, and DEB/RPM for Linux. Build on the target platform with its required packaging tools; Linux makers require `dpkg`, `fakeroot`, and `rpmbuild`.

Signing, macOS notarization, and publishers are not configured. The `pnpm publish` script requires publisher configuration before use.

## Project structure

```text
src/main/index.ts     Electron window, menus, file operations, and IPC
src/preload.ts        Bridge between the main process and the UI
src/renderer/        Editor events, Markdown rendering, and styles
src/electron.d.ts    Shared API and Electron/Vite type declarations
index.html           Application layout
forge.config.js      Build and packaging configuration
vite.*.config.mjs    Vite configuration for each process
```

The UI uses Tailwind CSS. Markdown is converted to HTML with unified, remark, and rehype.

## Current limitations

- **New File** and **Revert** are not implemented.
- There is no autosave or unsaved-change prompt. Save before opening another file or closing the window.
- Save-state indicators may remain stale until the next edit. File-manager actions are enabled after opening a file, but not immediately after its first save.
- HTML exports contain the preview markup only, without a full page or styles. Remote images are blocked by the current Content Security Policy.
- DevTools opens automatically, including in packaged builds.
- No automated tests are configured; `pnpm lint` is a placeholder. Verify editing, file operations, and export manually with `pnpm start`.

## License

[MIT](./LICENSE)
