<h1 align="center">
	<a href="https://github.com/WolfSoftware">
		<img src="https://raw.githubusercontent.com/WolfSoftware/branding/master/images/general/banners/64/black-and-white.png" alt="Wolf Software Logo" />
	</a>
	<br>
	Encrypt/Decrypt secrets using KMS
</h1>

<p align="center">
	<a href="https://travis-ci.com/AWSToolbox/kms-vault">
		<img src="https://img.shields.io/travis/com/AWSToolbox/kms-vault/master?style=for-the-badge&logo=travis" alt="Build Status">
	</a>
	<a href="https://github.com/AWSToolbox/kms-vault/releases/latest">
		<img src="https://img.shields.io/github/v/release/AWSToolbox/kms-vault?color=blue&style=for-the-badge&logo=github&logoColor=white&label=Latest%20Release" alt="Release">
	</a>
	<a href="https://github.com/AWSToolbox/kms-vault/releases/latest">
		<img src="https://img.shields.io/github/commits-since/AWSToolbox/kms-vault/latest.svg?color=blue&style=for-the-badge&logo=github&logoColor=white" alt="Commits since release">
	</a>
	<a href="LICENSE.md">
		<img src="https://img.shields.io/badge/license-MIT-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" alt="Software License">
	</a>
	<br>
	<a href=".github/CODE_OF_CONDUCT.md">
		<img src="https://img.shields.io/badge/Code%20of%20Conduct-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
	</a>
	<a href=".github/CONTRIBUTING.md">
		<img src="https://img.shields.io/badge/Contributing-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
	</a>
	<a href=".github/SECURITY.md">
		<img src="https://img.shields.io/badge/Report%20Security%20Concern-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
	</a>
	<a href=".github/SUPPORT.md">
		<img src="https://img.shields.io/badge/Get%20Support-blue?style=for-the-badge&logo=read-the-docs&logoColor=white" />
	</a>
</p>

## Overview

A bash script for managing secrets encrypted / decrypted via AWS KMS. This script is designed for encrypting things like yaml keys or other **small** pieces of data.

## Limitations

There is 4K limit with regards to KMS encryption so do not use it for encrypting large files.

If you need to encrypt large files then use something like gpg or openssl and use this script to protect the **private** key.

> We won't detail how to use gpg or any other tools for file encryption here, most methods will create a public and private key, and you can use this tool to protect that private key.

## Usage

```
Usage: kms-vault.sh [ -hdel ] [ -k key alias ] [ -f input filename ] [ -o output filename ]
  -h    : Print this screen
  -d    : decrypt a given file
  -e    : encrypt a given file
  -f    : The name of the name to encrypt
  -k    : The alias for the key to encrypt with
  -l    : List the available KSM key aliases/names
  -o    : Name of the output file
```

The script has 3 operating modes:

1. [List available KMS keys](#list-keys)
2. [Encrypt a file](#encrypt-file)
3. [Decrypt a file](#decrypt-file)

<a name="list-keys"></a>
## List Keys

```shell
./kms-vault.sh -l

Available Aliases:
1. alias/puppet
```

The alias name is used when encrypting the file contents. Not ALL KSM keys are listed, the script will not use a key which is AWS managed or 
any key which doesnt have a TargetKeyId attribute.

It is also possible that attempts to use certain keys might well be meet with the following error:

```
An error occurred (AccessDeniedException) when calling the Encrypt operation: <truncated output>
```

This is due to IAM restrictions to the key you are attempting to use, this normally happens with AWS managed keys like S3 and RDS which is why the script 
excludes them, but may also occur if you have set the access permissions to your custom key to be to restrictive.

You are required to create your own KMS keys for encryption/decryption purposes. (A tool for creating this will be released shortly and the link placed here).

<a name="encrypt-file"></a>

## Encrypt File

```shell
./kms-vault.sh -e -f <input file> -k <key alias> -o <output file>
```

The output from the script will be a long base64 encoded string, the output can be redirected to a file (an output file option is on the todo list)

<a name="decrypt-file"></a>

## Decrypt File

```shell
./kms-vault.sh -d -f <input file> -o <output file>
```

The output from the script will be the decrypted contains of the file, the output can be redirected to a file (an output file option is on the todo list)

## Contributors

<p>
	<a href="https://github.com/TGWolf">
		<img src="https://img.shields.io/badge/Wolf-black?style=for-the-badge" />
	</a>
</p>

## Show Support

<p>
	<a href="https://ko-fi.com/wolfsoftware">
		<img src="https://img.shields.io/badge/Ko%20Fi-blue?style=for-the-badge&logo=ko-fi&logoColor=white" />
	</a>
</p>
