# nitpum.com

[![Netlify Status](https://api.netlify.com/api/v1/badges/d5083e6d-dd3a-42a6-906b-868ebee7ce86/deploy-status)](https://app.netlify.com/sites/nitpum/deploys)

My personal website

## Features

- No external dependencies (font, css, js, etc.)
- Light/Dark mode
- Javascript not required

## Requirement

- Hugo v0.152.2+
- Go 1.24+ (optional)
- Node.js (optional for prettier)

## Setup

1. Install prettier-plugin-go-template in same scope as `prettier`

```sh
npm install --global prettier-plugin-go-template
```

Use prettier for js formatter

## Create new post

```sh
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

```sh
hugo
```
