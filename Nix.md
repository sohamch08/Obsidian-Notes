---
tags:

- nix
- nixos
- flakes
- home-manager
- learning
- roadmap date: 2026-05-26
---



---

# Learning Nix: Complete Roadmap & Resources

> A step-by-step learning path for Nix, NixOS, Flakes, and Home Manager — from a non-coding background to "the Nix way."
> 
> **End goals:** be able to (1) configure any application declaratively, and (2) write derivations from scratch.

---

## Table of Contents

- [[#How to think about this before you start]]
- [[#Part 1 — The Phased Roadmap]]
    - [[#Phase 0 — Prerequisites (1–2 weeks)]]
    - [[#Phase 1 — Understand why Nix exists (2–3 days, no installation yet)]]
    - [[#Phase 2 — Install Nix on your existing machine (1 day)]]
    - [[#Phase 3 — The Nix language (1–2 weeks, this is the hard part)]]
    - [[#Phase 4 — Your first flake & dev shells (1 week)]]
    - [[#Phase 5 — Home Manager standalone (1–2 weeks)]]
    - [[#Phase 6 — NixOS in a VM (2–3 weeks)]]
    - [[#Phase 7 — NixOS on real hardware]]
    - [[#Phase 8 — "The Nix way" (ongoing)]]
- [[#Part 2 — Complete Resource Library]]
    - [[#The single most important thing to know upfront]]
    - [[#Tier S — start here, in this order]]
    - [[#Tier A — the deeper layer (Phase 3 onward)]]
    - [[#Tier B — for specific goals]]
    - [[#Tier C — daily-use search/reference tools]]
    - [[#Tier D — videos and channels worth knowing]]
    - [[#Tier E — community and help]]
    - [[#Tier F — advanced, for once you're comfortable]]
- [[#A concrete 6-month plan mapped to resources]]

---

## How to think about this before you start

Nix is actually **four different things bundled into one name**, and confusing them is the #1 reason people get stuck:

1. **Nix the language** — a small, pure, functional language used only to describe builds and configurations
2. **Nix the package manager** — the tool that reads `.nix` files and builds/installs things into `/nix/store`
3. **Nixpkgs** — the giant Git repo containing definitions for ~100,000 packages
4. **NixOS** — a Linux distribution where the entire OS is described in Nix files

You learn them in roughly that order, but you'll touch all four early. **Don't try to install NixOS first** — that's the most common mistake.

You don't need a coding background. You need patience, willingness to read documentation, and a working Linux/macOS machine. The Nix learning curve is famously steep, but it's steep mostly because the _concepts_ are unusual, not because the code is hard.

---

# Part 1 — The Phased Roadmap

## Phase 0 — Prerequisites (1–2 weeks)

Before touching Nix, get comfortable with:

- **Terminal basics**: `cd`, `ls`, `cat`, editing files with `nano`/`vim`, environment variables, what `$PATH` is
- **Git**: clone, commit, push, branches
- **The concept of a "function"**: input → output, no side effects. Spend 30 minutes on this if it's unfamiliar. Watch any "intro to functional programming" video on YouTube — Nix is functional and this is the single biggest mental shift
- **What a package manager does**: how `apt` or `brew` install software, why version conflicts happen

You don't need to "learn to code." You need to be able to read and tweak small snippets without panic.

---

## Phase 1 — Understand why Nix exists (2–3 days, no installation yet)

Before installing anything, watch and read for context. This phase is pure motivation — it'll save you weeks of confusion later because you'll know _what problem_ each feature solves.

- **Watch**: "Nix in 100 seconds" by Fireship (2 min, very superficial but sets the vibe)
- **Watch**: "Nix Flakes are an obviously good idea" by No Boilerplate (~10 min) — sells you on flakes specifically
- **Read**: the "What is Nix?" page on [zero-to-nix.com](https://zero-to-nix.com/) by Determinate Systems
- **Skim**: the introduction chapter of the [NixOS & Flakes Book](https://nixos-and-flakes.thiscute.world/) — you'll come back to this many times

By the end of this phase you should be able to answer: _Why would I want immutable, reproducible builds? What's wrong with `apt install`?_

---

## Phase 2 — Install Nix on your existing machine (1 day)

> [!warning] Do not install NixOS yet. Install just the Nix package manager on top of your current Linux/macOS system. You can always uninstall it cleanly.

- Use the **Determinate Systems installer**:
```bash
curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install
```
- It enables flakes and the new CLI by default (the official installer doesn't, and you'd just have to enable them manually anyway)
- After install, run `nix run nixpkgs#hello` — if it prints "Hello, world!" you're set

Spend a day just _playing_:

```bash
nix run nixpkgs#cowsay -- "hi"
nix shell nixpkgs#python3 nixpkgs#nodejs   # then `exit`
nix search nixpkgs firefox
```

Notice that nothing you installed leaked into your normal system. That's the magic.

---

## Phase 3 — The Nix language (1–2 weeks, this is the hard part)

This is where most people quit. **Go slowly.** The language itself is small — maybe 8 concepts — but they combine in unfamiliar ways.

Learn in this order:

1. **Values**: strings, numbers, lists, paths, booleans
2. **Attribute sets** (`{ a = 1; b = 2; }`) — these are _everywhere_; they're like JSON objects
3. **`let ... in ...`** — local variables
4. **Functions** — `x: x + 1` is a function. `{ a, b }: a + b` is a function taking an attribute set.
5. **`with` and `inherit`** — convenience keywords
6. **`import`** — loading other `.nix` files
7. **Lazy evaluation** — values aren't computed until needed
8. **Derivations** — a special attribute set that describes "how to build something"

**Resources, in order:**

1. [nix.dev → "Nix language basics"](https://nix.dev/tutorials/nix-language) — do every exercise, type them yourself, don't just read
2. **`nix repl`** — open it and play. Type `:?` for help. Try `1 + 1`, `{ a = 1; }.a`, `(x: x * 2) 5`
3. [Nix Pills](https://nixos.org/guides/nix-pills/) (chapters 1–8) — denser, older, but the _clearest_ explanation of how derivations work. Read one pill per day.
4. [Vimjoyer on YouTube](https://www.youtube.com/@vimjoyer) — short, focused videos on specific Nix language features

**Goal at the end:** you can read someone else's `flake.nix` and roughly say what each piece does, even if you couldn't write it from scratch yet.

---

## Phase 4 — Your first flake & dev shells (1 week)

This is where Nix becomes _useful_ to your daily life, even before NixOS.

- Make a folder, run `nix flake init`, look at the generated `flake.nix`
- Modify it to create a **devShell** for your MSc project — e.g., a shell that has exactly the TeX Live distribution, `gh`, `pandoc`, and Python you need
- Commit `flake.nix` and `flake.lock` to your repo
- Now anyone (including future-you on a fresh machine) runs `nix develop` in that folder and gets the exact same toolchain

Then learn **`direnv` + `nix-direnv`**: it auto-loads the dev shell whenever you `cd` into the project folder. This is the killer feature — your project just _has_ its own environment.

> [!tip] This phase alone justifies learning Nix even if you never go further.

---

## Phase 5 — Home Manager standalone (1–2 weeks)

Home Manager lets you declaratively manage your _user-level_ config — packages, dotfiles, shell config, git config, neovim plugins — without touching the OS.

- Install Home Manager as **standalone** (not as a NixOS module — you don't have NixOS yet)
- Follow the [official Home Manager manual's "Standalone installation"](https://nix-community.github.io/home-manager/) with flakes
- Start small: just `home.packages = [ pkgs.htop pkgs.ripgrep ];`
- Then declare `programs.git` with your name/email — your `.gitconfig` is now generated from Nix
- Gradually move more dotfiles in: `programs.zsh`, `programs.neovim`, `programs.tmux`

Run `home-manager switch --flake .` after each change. If something breaks, `home-manager generations` lists every previous state and you can roll back.

By the end you'll have a Git repo that fully describes your user environment.

---

## Phase 6 — NixOS in a VM (2–3 weeks)

Now you're ready to meet NixOS — **but in a virtual machine, not on real hardware**.

- Install VirtualBox or QEMU/virt-manager
- Download a NixOS minimal ISO, install it inside the VM
- Get comfortable with `/etc/nixos/configuration.nix` — the file that describes your whole system
- Learn the workflow: edit `configuration.nix` → `sudo nixos-rebuild switch` → if anything's broken, reboot and pick an older generation from the GRUB menu
- Try breaking it on purpose. Rollback. **This is the safety net that makes NixOS pleasant.**

Then **convert to flakes**: move the VM's config into a flake, with `nixpkgs` and `home-manager` as inputs. This is where the [NixOS & Flakes Book](https://nixos-and-flakes.thiscute.world/) becomes your bible — work through it chapter by chapter, applying each lesson to your VM.

---

## Phase 7 — NixOS on real hardware

Only after the VM feels boring should you install on a real machine — ideally a spare laptop, or dual-boot. Bring your flake-based config from the VM with you; most of it will just work.

---

## Phase 8 — "The Nix way" (ongoing)

These are the things that distinguish a Nix user from a Nix _practitioner_. Pick them up gradually, in any order, as you need them:

- **Overlays** — patching/overriding packages from nixpkgs
- **Writing your own derivations** — packaging software that isn't in nixpkgs
- **Modules** — how `programs.git = { ... }` works under the hood; writing your own
- **`pkgs.callPackage`** and the nixpkgs internal conventions
- **Cross-compilation, binary caches, Cachix**
- **Multi-host configs** — one flake describing your laptop, desktop, and a server
- **deploy-rs / colmena** — deploying NixOS configs to remote machines

---

# Part 2 — Complete Resource Library

## The single most important thing to know upfront

Two skills will get you to "everything is easy":

- **For configuring apps** → mastery of `search.nixos.org`, `home-manager option search`, and reading existing module source code on GitHub
- **For writing derivations** → understanding `stdenv.mkDerivation` and the "trivial builders" (`writeShellScriptBin`, `runCommand`, etc.)

Almost every Nix question reduces to one of those two skills. Most resources below are aimed at building them.

---

## Tier S — start here, in this order

These four cover ~80% of what most people ever need.

1. **nix.dev** → https://nix.dev — the official tutorials. Do "Nix language basics," then "First steps with Nix," then "Packaging existing software with Nix." These three alone are gold. Type every example.
2. **NixOS & Flakes Book** by Ryan Yin → https://nixos-and-flakes.thiscute.world — the single best end-to-end book for the modern flakes-first workflow. Read cover-to-cover when you reach Phase 4–6.
3. **Zero to Nix** by Determinate Systems → https://zero-to-nix.com — polished, friendly intro for the first few hours. Especially good for the "what is even happening here" phase.
4. **Vimjoyer** YouTube channel → https://www.youtube.com/@vimjoyer — short focused videos with code on screen. The "Ultimate NixOS Guide | Flakes | Home-manager" video is the best 30 minutes of NixOS content on YouTube. Use his playlists as a topic index — when you hit a concept, search his channel for a video on it.

---

## Tier A — the deeper layer (Phase 3 onward)

These take you from "I can copy configs" to "I understand what they do."

5. **Nix Pills** → https://nixos.org/guides/nix-pills/ — 20 short chapters. Chapters 1–8 build a derivation from first principles. Dense but unmatched for the "click" moment about how Nix actually works. Read one pill per sitting.
6. **Nix from First Principles: Flake Edition** by Tony Finn → https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/ — a modern, flakes-first crash course that updates the Nix Pills style for 2024+.
7. **Nix lectures** by ayats.org:
    - Part 1: https://ayats.org/blog/nix-tuto-1
    - Part 2 (derivations): https://ayats.org/blog/nix-tuto-2
    - Part 3: https://ayats.org/blog/nix-tuto-3
    - Part 2 is especially excellent.
8. **Awesome Nix** → https://github.com/nix-community/awesome-nix — the master index of literally everything else. Bookmark it.
9. **Official Nix Reference Manual** → https://nix.dev/manual/nix/ — keep open in a tab as a lookup, not as something to read top-to-bottom.
10. **Nixpkgs Manual** → https://nixos.org/manual/nixpkgs/stable/ — the "Standard Environment" and "Languages and Frameworks" chapters are essential for derivations. The Python/Node/Rust sections show you exactly how to package those.

---

## Tier B — for specific goals

### To configure any app (your goal #1)

- **Home Manager Manual** → https://nix-community.github.io/home-manager/ — the install guide + the options list (Appendix A) is your daily reference
- **Home Manager Option Search** → https://home-manager-options.extranix.com/ — searchable UI, much better than reading the appendix
- **Mattia Gheda's tutorial** → https://ghedam.at/24353/tutorial-getting-started-with-home-manager-for-nix — best from-scratch standalone Home Manager walkthrough
- **LibrePhoenix's "Manage Dotfiles the Nix Way"** → https://librephoenix.com/2023-11-02-how-to-manage-your-dotfiles-the-nix-way-with-home-manager — clear, beginner-friendly
- **Alex Pearwin's dotfiles post** → https://alex.pearwin.com/2021/07/managing-dotfiles-with-nix/ — shows the "reverse engineer existing dotfiles into Nix" workflow
- **Davis Haupt's macOS Nix guide** → https://davi.sh/blog/2024/02/nix-home-manager/ — if you're on macOS

> [!tip] The pattern to internalize Every program module looks like `programs.<name> = { enable = true; settings = { ... }; }`. Once you've done this for git, zsh, tmux, and neovim, you can do it for _anything_ by reading the options page.

### To write derivations (your goal #2)

- **nix.dev → "Packaging existing software with Nix"** → https://nix.dev/tutorials/packaging-existing-software.html — _the_ tutorial. Do this twice.
- **Nix Pills 6–8** — "Our First Derivation," "Working Derivation," "Generic Builders." This is where the magic stops being magic.
- **Sam Today's "Creating a super simple derivation"** → https://www.sam.today/blog/creating-a-super-simple-derivation-learning-nix-pt-3 — packages a shell script, perfect first exercise
- **Pavluk's Nix Packaging Quickstart** → https://pavluk.org/blog/2023/05/30/nix_packaging.html — clear, no fluff
- **Lambda-Blob's derivation guide** → https://lambdablob.com/posts/program-declarative-nix-package-derivations/ — good mental model
- **Inria's "Hacking Your First Package"** → https://nix-tutorial.gitlabpages.inria.fr/nix-tutorial/first-package.html — academic-style, very clear
- **Nixpkgs source itself** → https://github.com/NixOS/nixpkgs/tree/master/pkgs — the best "examples library" ever. When you want to package something like X, find a similar package in nixpkgs and read its `default.nix`.

**The progression:**

1. Package a shell script
2. Package a Python script with deps
3. Package something from a GitHub release tarball
4. Package something that has to compile (C/CMake)
5. Package something gnarly with patches

---

## Tier C — daily-use search/reference tools

These are what separate a frustrated Nix user from a productive one. **Bookmark all of them.**

- **search.nixos.org** → https://search.nixos.org — packages + NixOS options. The single most-visited Nix URL on Earth.
- **Home Manager Option Search** → https://home-manager-options.extranix.com/
- **Noogle** → https://noogle.dev — search Nix library functions by name, type, or description. Use this whenever you see `lib.something` and don't know what it does.
- **MyNixOS** → https://mynixos.com — alternative options search with a nicer UI
- **Searchix** → https://searchix.alanpearce.eu — searches NixOS, nix-darwin, and home-manager options together
- **nix-search-tv** → https://github.com/3timeslazy/nix-search-tv — terminal fuzzy finder for packages/options, installable as a Nix package itself
- **nix-options-search (nox)** → https://github.com/madsbv/nix-options-search — TUI fuzzy finder for options across nix-darwin/NixOS/home-manager

---

## Tier D — videos and channels worth knowing

- **Vimjoyer** → https://www.youtube.com/@vimjoyer — your default. The NixOS playlist, the Home Manager video, and the Nix Helper (`nh`) video are must-watches.
- **LibrePhoenix** → https://www.youtube.com/@librephoenix — focuses on dotfiles, ricing, and modular configs
- **Matthias Benaets** → https://www.youtube.com/@MatthiasBenaets — long-form, gentle, thorough NixOS install and config series. Great if Vimjoyer feels too fast.
- **NixCon talks** → search "NixCon 2024" or "NixCon 2023" on YouTube — many of the best resources are conference talks
- **Nix Hour** by infinisil (Silvan Mosberger) → search "Nix Hour" on YouTube — weekly deep-dive, often unscripted live debugging. Watch a few when you're past basics; observing a maintainer think is one of the best ways to absorb idioms.

---

## Tier E — community and help

When you're stuck, in roughly this order of usefulness:

- **NixOS Discourse** → https://discourse.nixos.org — search first; ask if you can't find it. Usually friendly and fast.
- **NixOS Wiki (the new official one)** → https://wiki.nixos.org — not `nixos.wiki`, which is the old unofficial one
- **r/NixOS** on Reddit → https://reddit.com/r/NixOS — good for casual questions and seeing what people are building
- **NixOS Matrix/Discord** — `#users:nixos.org` on Matrix; there's a community Discord too. Real-time help.
- **GitHub issues/PRs of nixpkgs and home-manager** — when something breaks, someone has usually already filed it. Search both repos.

---

## Tier F — advanced, for once you're comfortable

You will not need these for months. Listed so you know they exist.

- **Eelco Dolstra's PhD thesis** → https://edolstra.github.io/pubs/phd-thesis.pdf — Nix's foundational document. Academic but illuminating.
- **NixOS Module System** chapter in the NixOS manual → for writing your own modules with `options` and `config`
- **nixpkgs CONTRIBUTING.md** → if you ever want to upstream a package
- **Flake-parts** → https://flake.parts — when your flake gets unwieldy and you want modularity
- **nix-darwin** → https://github.com/LnL7/nix-darwin — only if you're on macOS, but excellent if so
- **NixOS Anywhere / disko / colmena / deploy-rs** — for installing/deploying NixOS to remote machines declaratively

---

# A concrete 6-month plan mapped to resources

|Month|Focus|Resources|Goal|
|---|---|---|---|
|1|Get installed; basic syntax|Zero to Nix quick start + nix.dev language basics + Vimjoyer first videos|Comfortable with `nix run`, `nix shell`, basic Nix syntax|
|2|Understand derivations|Nix Pills 1–8 + nix.dev "Packaging existing software"; build a dev shell|Derivations make sense|
|3|Manage user environment|Home Manager standalone; migrate zsh/git/tmux/neovim configs|Dotfiles are Nix-managed|
|4|NixOS in a VM with flakes|NixOS & Flakes Book, chapter by chapter|Can read and modify any `configuration.nix`|
|5|Package real things|Package a shell script, a Python tool with deps, a small C program|Derivations are no longer scary|
|6|Go all in|Convert real machine to NixOS, modularize, learn overlays|You've reached "the Nix way"|

---

## Realistic pace and warnings

- Plan for **3–6 months** to be comfortable. Six months is normal, not slow.
- You _will_ hit a wall around Phase 3 where derivations feel impossible. **Push through — it clicks suddenly, not gradually.**
- Don't copy random configs from GitHub before you can read them. You'll cargo-cult bugs you can't debug.
- When something breaks, read the error message _carefully_. Nix errors are infamously long but usually precise.
- Keep your Nix configs in Git from day one.

---

## Related notes

- [[Flakes cheatsheet]]
- [[Home Manager snippets]]
- [[Derivation examples]]
- [[msc-project-tifr]]

%% Add your own notes and links here as you progress %%