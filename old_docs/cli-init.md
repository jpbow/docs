---
id: cli-init
title: Init
permalink: docs/cli-init.html
layout: docs
category: CLI Reference
prev: cli-install.html
next: cli-link.html
---

Initializes Bit on a local workspace. This will creates Bit's configuration, and a `.bit` directory, which will contain Bit's objects & models.

## Synopsis

```bash
bit init [-b|--bare] [-s|--shared <group-name>] [-t|--standalone] [--reset] [--reset-hard]
```

## Options

**-b, --bare [name]**

Initializes an empty bit bare Collection.

```bash
bit init --bare
```

**-s, --shared <group-name>**

Adds group write permissions to a Scope properly.

```bash
bit init --shared group-name
```

**-t, --standalone**

Creates the [component store](/docs/initializing-bit.html#component-store) outside the `.git` directory.

```bash
bit init --standalone
```

**--reset**

Resets Bit to its initial state. Use this in case you have any corrupted data.

```bash
bit init --reset
```

**--reset-hard**

Removes Bit completely from a local workspace. Use this in case you want to completely remove Bit from your project.

This will delete `.bitmap`, `bit.json` and `.bit`.

```bash
bit init --reset-hard
```