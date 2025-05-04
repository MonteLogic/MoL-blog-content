---
title: 'Proposal: Markdown CLI CMS'
date: '2024-11-19'
---

Ideally we would use **Frontmatter** for the metadata. So it'll be Markdown CLI. We would use contentlayer for schema validation. But then we would query all of this as one project. Then the CLI, check out one branch of it and then this Branch would be by default which you can just open it.

## Own Server

I would like for it to be on a admin's own server as to not have to deal with people's payments, setups, etc. This data will be still be be backed up. A good CLI for this would GitHub CLI. So the CMS user would not have to go through the set up process as well as have way less security issues.

## Headless WordPress Maybe:

I'm starting to think headless WordPress is the way to go for this.

Ideally we could go on the page, and click edit page in WordPress if we have the auth privileges.

But don't have it use a PHP backbone as PHP is very slow and bulky. So something similar to headless WordPress which you can host on your own server with good security.

Headless WordPress would be an attractive option due to the fact that it's easy to self host WordPress.

## The Bare Basics:

An AWS bucket which would just store data in a certain schema and have routine backups.

## CLI Functionality

Ideally you could just run a CLI command and the .mdx file is scaffolded the title and all the stuff should be optional so you can get straight into your stream of consciousness.
