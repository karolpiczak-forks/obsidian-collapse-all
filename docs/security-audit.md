# Security Audit Report

**Repository:** karolpiczak-forks/obsidian-collapse-all  
**Date:** 2026-08-16  
**Auditor:** GitHub Copilot Task Agent (security-review specialist)

---

## Summary

**Result: No vulnerabilities found.**

The codebase is clean with a minimal attack surface. No malware, no exploitable vulnerabilities, and no hardcoded secrets were identified.

---

## Scope

| Area | Files Examined |
|---|---|
| Source code | `main.ts`, all files in `src/` |
| Build system | `esbuild.config.mjs` |
| Dependencies | `package.json`, `package-lock.json` |
| Configuration | `manifest.json`, `versions.json` |

---

## Malware Check

**Finding: None.**

The plugin is a minimal Obsidian UI utility that collapses and expands folder tree views. It:

- Makes **no network calls**
- Spawns **no child processes**
- Reads or writes **no user data** outside of Obsidian's own API
- Contains **no obfuscated or dynamic code execution**

---

## Vulnerability Assessment

### Source Code (`main.ts`, `src/`)

**Finding: No vulnerabilities.**

All user interaction goes through Obsidian's sandboxed plugin API (`addCommand`, `addSettingTab`, `getLeavesOfType`). No injection, XSS, SSRF, or access-control issues are present. No untrusted HTML is constructed or injected.

### Build System (`esbuild.config.mjs`)

**Finding: No vulnerabilities.**

Standard esbuild configuration for bundling TypeScript. No remote code fetching, no dynamic execution, and no shell-command construction from user input.

### Dependencies (`package.json`, `package-lock.json`)

**Finding: No vulnerabilities.**

All dependencies are listed under `devDependencies` — nothing is bundled into the runtime plugin output. All Obsidian and CodeMirror packages are explicitly marked `external` in the build config, so end users receive no third-party runtime code.

One prior vulnerability was already remediated:

| CVE | Package | Fixed Version | Remediation |
|---|---|---|---|
| CVE-2022-24785 | `moment` | 2.29.4 | `overrides` in `package.json` enforces the patched version transitively |

### Configuration (`manifest.json`, `versions.json`)

**Finding: No vulnerabilities.**

No sensitive data, hardcoded credentials, or supply-chain risks were found in any configuration file.

---

## Conclusion

This repository presents a low-risk, clean codebase. No further remediation is required.
