# Styx Studios

We make **Local**, a family of desktop apps for Windows and Linux that keep your files on your
computer and work without an account. Every app is written in Rust, including the interface.

| App | What it is |
|---|---|
| [Local Word](https://github.com/Anon5T4R/local-office) | word processor (`.docx`, `.odt`) |
| [Local Sheets](https://github.com/Anon5T4R/local-sheets) | spreadsheets (`.xlsx`, `.ods`, `.csv`) |
| [Local Slides](https://github.com/Anon5T4R/local-slides) | presentations (`.pptx`) |
| [Local PDF](https://github.com/Anon5T4R/local-pdf) | PDF reader and editor |
| [Local Keys](https://github.com/Anon5T4R/Local-Keys) | password manager, desktop and Android |
| [Local Image](https://github.com/Anon5T4R/Local-Image) | image viewer |
| [Local Photo](https://github.com/Anon5T4R/Local-Photo) | RAW photo editor and library |
| [Local Paint](https://github.com/Anon5T4R/Local-Paint) | raster image editor |
| [Local Vector](https://github.com/Anon5T4R/Local-Vector) | vector graphics editor |
| [Local Player](https://github.com/Anon5T4R/Local-Player) | video and audio player |
| [Local Notebook](https://github.com/Anon5T4R/Local-Obsidian) | Markdown notes over a folder of files, desktop and Android |
| [Local Mind](https://github.com/Anon5T4R/Local-Mind) | mind maps |
| [Local Utils](https://github.com/Anon5T4R/Local-Utils) | small everyday tools |

Each app's README says what it does and where it comes from; its `ROADMAP.md` says honestly what
works, what is weak and what is planned. The repositories move to this organization as each app
reaches 1.0; new apps start here.

## How we make the Local apps

These decisions hold for every app.

- **Local files, no account.** The apps open and save files on your disk. Nothing needs a login or a
  server of ours. The only network use is the update check on GitHub, and AI if you turn it on.
- **Rust only, including the UI.** One toolchain, memory safety by default, and no native libraries
  to install. The interface is [egui](https://github.com/emilk/egui) on wgpu. Cryptography and TLS
  are pure Rust too (RustCrypto): no `ring`, `aws-lc` or OpenSSL in the programs.
- **One repository per app, self-contained.** Each app vendors what it builds with (our forks of
  egui and winit, and the shared crates), so a release depends only on its repository and
  crates.io. Shared code (updater, AI panel, MCP server, icons) has one source and is mirrored into
  every app with a hash check.
- **Forks with selective sync.** Most apps start from an open-source Rust app, credited in its
  README. The fork is ours: the upstream is a source of fixes (crashes, data loss, security, file
  compatibility), reviewed one by one, not of direction.
- **Dependencies are governed.** A dependency is added only after checking its license and source,
  and every app's inventory is kept in one place. No git dependencies, no pre-built binaries.
  `cargo-deny` checks advisories, licenses and bans on every build.
- **Releases are reproducible from a tag.** GitHub Actions builds every release from a tagged commit
  with locked dependencies, on Windows and Linux, and signs every file with
  [minisign](https://jedisct1.github.io/minisign/) (one key for all apps:
  `RWTqN+hTTCFbDCGCA1cEJRLp2FSluxIUiJfqdoAYwkwNNVH5MTYH8qSN`). The in-app updater checks that
  signature.
- **AI is optional and yours.** No model or key ships with the apps. You bring a provider, in the
  cloud or local (llama.cpp, Ollama); the app sends only what you ask it to.
- **Agents can use the apps.** Every app exposes its commands over MCP, so an AI agent can operate it
  the way a person does.
- **Windows and Linux.** That is what we use and test. Android exists where it makes sense (Keys,
  Notebook), with the same file format as the desktop. Other systems may build, but are not
  published.

## Made with AI agents

Most of the code in these apps is written by AI coding agents (Claude Code and OpenCode), working
from written plans and reviewed by the maintainer, who decides what gets built and how. Every change
has to pass the same local checks (format, lints, tests, layer rules, license audit) and the CI on
Windows and Linux before it is released. We say this so you can judge the code with that in mind.
If something is wrong, open an issue in the app's repository.
