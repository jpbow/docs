---
id: installation
title: Installation
sidebar_label: Installation
---

To start working with Bit follow the steps bellow

- Sign for a Bit Account[]
- Install Bit CLI
- Login to Bit Account
- Setup Bit Workspace

## Sign for a Bit Account

In order to start using Bit a Bit account is required. The Bit account let you create components' collections and join existing collections.
To sign up for a free Bit account go to [bit.dev](https://bit.dev).

You can sign with an email or using your github credentials.

---

## Install Bit CLI

You can install Bit CLI as a binary executable (recommended) or using [NPM / Yarn](#npm-or-yarn).

| [MacOS](#macos) | [Windows](#windows) | [Linux](#linux) |
| :-------: |:-------:| :-------:|


### MacOS

```sh
$ curl -Lo bit https://github.com/teambit/bit/releases/download/v14.2.1/bit-bin-macos
$ chmod +x bit
```

You can copy the bit executable to a directory in your path, or any directory that will be added to your path:

```sh
$ sudo cp bit /usr/local/bin/ 
$ rm bit
```

---

### Windows

- Download the Windows `.exe` file from [here](https://github.com/teambit/bit/releases/download/v14.2.1/bit-bin-win.exe)
- Rename it to `bit.exe` and add it to your `PATH`:
- Add file location to windows path:

```sh
set PATH=%PATH%;C:\bit\
```

---

### Linux

You can use package installer as per your distribution or download the executable directly. 

__**Using Package Installers**__

<!--DOCUSAURUS_CODE_TABS-->
<!--Debian-->

```sh
$ sudo sh -c "echo 'deb [trusted=true] https://bitsrc.jfrog.io/bitsrc/bit-deb all stable' >> /etc/apt/sources.list"
$ sudo apt-get update && sudo apt-get install bit
```

<!--Ubuntu-->

```sh
$ sudo apt-get update && sudo apt-get install ca-certificates
$ sudo sh -c "echo 'deb [trusted=true] https://bitsrc.jfrog.io/bitsrc/bit-deb all stable' >> /etc/apt/sources.list"
$ sudo apt-get update && sudo apt-get install bit
```

<!--CentOS / Fedora / RHEL-->

```sh
$ sudo curl --silent --location https://static.bit.dev/rpm/bit.repo | sudo tee /etc/yum.repos.d/bit.repo
$ sudo yum install bit
```

<!--END_DOCUSAURUS_CODE_TABS-->

__**Download executable**__

```sh
$ curl -Lo bit https://github.com/teambit/bit/releases/download/v14.2.1/bit-bin-linux
$ chmod +x bit
```

You can copy the bit executable to a directory in your path, or any directory that will be added to your path:

```bash
sudo cp bit /usr/local/bin/ && rm bit
```

---

### NPM or Yarn

> Requires node 8.12 and above.

```bash
npm install bit-bin --global
    or
yarn global add bit-bin  
```

---

## Verify Install

Once installed, verify the installation by running the following command:

```bash
bit --version
```

## Login to your Bit Account

Once bit is installed on your machine, you can log into your account. Run the command: 

```bash
bit login
```

You will be taken to the browser to log into the account. If you are already logged in, a success message will be displayed.

Bit is now ready to use with your credentials.

Alternatively, you can [set up Bit authentication using SSH](/guides/authentication). 

You can now start installing and sharing components using Bit. 

## Initialize Bit Workspace

You need to initialize your project's  as a [bit workspace](docs/concepts#developer-setup), in order to start tracking components. 

In the root folder of your project run: 

```bash
bit init
```

### Reset Bit Workspace

If an error caused data corruption you can add the `--reset` flag to `bit init` to re-initialize the workspace.

```bash
bit init --reset
```
