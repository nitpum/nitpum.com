# nitpum.com

[![Netlify Status](https://api.netlify.com/api/v1/badges/d5083e6d-dd3a-42a6-906b-868ebee7ce86/deploy-status)](https://app.netlify.com/sites/nitpum/deploys)

My personal website

## Features

- Work offline (local font, js, etc.)
- Light/Dark mode
- Javascript not required

## Requirement

- Go 1.51+
- Hugo v0.99.1+
- Node.js (optional for prettier)

## Setup

1. Install prettier-plugin-go-template in same scope as `prettier`

```bash
npm install --global prettier-plugin-go-template
```

Use prettier for js formatter

## Create new post

```bash
hugo new --kind post post/<post-name>
```

## Development

```sh
hugo server
```

Render draft content

```sh
hugo server -D
```

## Build

```
hugo
```
