# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Percy's Pooch Parade is a static website for a dog walking business run by Perseus Reginald (age 10) in Ivanhoe, VIC. It is a client project managed by Digital Sanctum.

- **Stack:** Single-page HTML/CSS/JS (no build step, no framework)
- **Fonts:** Google Fonts (Fredoka, Nunito)
- **Form handling:** Formspree (https://formspree.io/f/xjgaadbn)
- **Repository:** `github.com/preginald/percys-pooch-parade`
- **Production:** https://poochparade.reginald.au
- **VPS:** 159.223.82.75 (Apache), site root `/var/www/poochparade.reginald.au`
- **Auto-deploy:** GitHub Actions on push to `main` (SSH via `appleboy/ssh-action`)

## Project Structure

```
percys-pooch-parade/
├── .github/workflows/deploy.yml   # CI/CD pipeline
├── images/
│   └── percy-and-doggo.webp       # About section photo
├── index.html                      # Entire site (HTML + CSS + JS)
└── CLAUDE.md                       # This file
```

## Sanctum Core Integration

This project is tracked in Sanctum Core (Digital Sanctum's ERP/CRM platform).

- **Project UUID:** `fc0c7f20-5217-41c6-930b-06e525adbf26`
- **Project name:** Percy's Pooch Parade Website
- **CLI tool:** `sanctum` (symlinked from `scripts/dev/sanctum.sh` on Pete's machine)
- **Ticket commands** are run by Pete, not Claude — Claude does not have access to `sanctum` CLI.

### Milestones
- Phase 1: Foundation (repo, CI/CD, DNS, SSL) — completed
- Phase 2: Website Polish (content, form, SEO, dark mode, mobile nav) — completed
- Phase 3: Go Live (testing, launch checklist) — in progress

## Development Doctrines

### 1. Consultative (MANDATORY)
- **No unsolicited code.** Propose a technical solution and wait for approval before writing code.
- **One step at a time.** Do not combine plans and code in one response.

### 2. Surgical Reconnaissance (MANDATORY)
- **Recon before edit.** Use `grep -n` and `sed -n` to scan before proposing changes.
- **Minimal changes.** Target only the lines that need to change — don't rewrite entire files.
- **Always verify.** After any change, run a grep to confirm the change landed correctly.

### 3. Delivery Pattern
1. Create a ticket for the work (if one doesn't exist) — Pete runs `sanctum ticket create`
2. Perform surgical recon, comment ticket with proposed solution — Pete runs `sanctum ticket comment`
3. Implement the proposed solution on a feature branch
4. Verify the change
5. Push the branch for Pete to review, test, and merge
6. Pete resolves the ticket via `sanctum ticket resolve`

## Git Workflow

- **Always work on a feature branch** (`feat/<ticket>-<description>`). Never commit directly to `main`.
- Pete pulls the branch, tests locally, then merges to `main` (locally or via PR).
- Pushes to `main` auto-deploy to production via GitHub Actions.
- Commit messages reference ticket numbers: `#605: update footer link`
- **Never force push to main.**

## Editing Guidelines

Since the entire site is a single `index.html` file:

- **CSS** is in a `<style>` block in the `<head>`
- **HTML** content is in the `<body>`
- **JavaScript** is in a `<script>` block before `</body>`
- **Dark mode** uses CSS variables in `:root`, `[data-theme="dark"]`, and `@media (prefers-color-scheme: dark)`
- **Always-dark sections** (#promise, footer) use hardcoded light colours — do not use CSS variables for text in these sections
- **Font declarations** include system fallback stacks — maintain these when editing

## Key Features

| Feature | Implementation |
|---|---|
| Dark/light mode | CSS variables + `data-theme` attribute + localStorage |
| Active nav | IntersectionObserver on `section[id]` elements |
| Mobile menu | Hamburger toggle with full-screen overlay |
| Walking paw trails | SVG paw prints with `pawStamp` CSS keyframes |
| Contact form | Formspree AJAX submission with loading/success/error states |
| SEO | Meta description, Open Graph tags, canonical URL, SVG favicon |

## Services & Pricing (source of truth)

- **Quick Walk:** 30 minutes, $10 — neighbourhood walk
- **Big Adventure:** 60 minutes, $18 — park & trail walk

These appear in the pricing cards section and the contact form dropdown. Update both if pricing changes.

## Contact Details

- **Phone:** 0420 479 680
- **Service area:** Ivanhoe, VIC
- **Domain:** poochparade.reginald.au
