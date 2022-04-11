# nitpum.com

[![Netlify Status](https://api.netlify.com/api/v1/badges/d5083e6d-dd3a-42a6-906b-868ebee7ce86/deploy-status)](https://app.netlify.com/sites/nitpum/deploys)

My personal website

## Features

- Work offline
- Light/Dark mode

## Requirement

- Go 1.51+
- Hugo v0.91.2+
- Node.js (optional for prettier)

## Setup

1. Install prettier-plugin-go-template in same scope as `prettier`

```bash
npm install --global prettier-plugin-go-template
```

Use prettier for js formatter

## Development

```sh
hugo serve
```

Render draft content

```sh
hugo serve -D
```

## Build

```
hugo
```
