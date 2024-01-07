---
title: changesets warn received 404 for npm info on pre-release
author: nitpum
date: 2024-01-04T21:31:59+07:00
lastmod: 2024-01-07T19:18:24.615Z
toc: true
tags:
    - changesets
    - npm
    - semantic-version
---

I work on monorepo setting up changesets to a project and found a problem when working with pre-release versions.

## What is changesets

[changesets](https://github.com/changesets/changesets) is a versioning and changelogs for monorepo. By writing impacts and change descriptions in markdown changesets file with commits, Changeset will collect these files to determine which package to bump, versioning, create changelogs, and publish package to registry automatically. The only manual work is writing a change file.

## Pre-release version

Semantic version has pre-release version [specs](https://semver.org/#spec-item-9) for an unstable build. The format is something like this `1.0.0-alpha`, `1.0.0-alpha.1` in my case is `0.1.0-beta.1`

## The problem

Everything seems fine. I setup changesets. Make a first changes. Write a changesets file. Push commit to remote. Pipeline run. Changesets tags and push `0.1.0-beta.1` to private registry. Everything works as expected. Nothing to worry. I work on other work.

Sometime later. I make an another change. Push commit to remote.

Pipeline GREEN. But I notice something in the CI log.

```sh
🦋  info npm info @nitpum/ui
🦋  warn Received 404 for npm info "@nitpum/ui"
🦋  info @nitpum/ui is being published because our local version (0.1.0-beta.1) has not been published on npm
```

Look like changesets can't find my package on the registry and try to publish `0.1.0-beta.1` to the registry again because it think this version never published and this is the first times.

But how it can't find the existing version?

After some investigation, I found that changesets use npm info underlying.

## What is npm info

npm info is a command to get package information e.g. description, dependencies, dist-tags, etc.
The command is same as [npm view](https://docs.npmjs.com/cli/v10/commands/npm-view)

```sh
npm info <package-name>
```

## Changesets Implementation

Changesets [implemented](https://github.com/changesets/changesets/blob/main/packages/cli/src/commands/publish/npm-utils.ts#L99-L116) code like this

```ts {linenos=table, hl_lines=[11], linenostart=99}
let result = await spawn("npm", [
	"info",
	packageJson.name,
	"--registry",
	getCorrectRegistry(packageJson),
	"--json",
]);

// Github package registry returns empty string when calling npm info
// for a non-existent package instead of a E404
if (result.stdout.toString() === "") {
	return {
		error: {
			code: "E404",
		},
	};
}
return jsonParse(result.stdout.toString());
```

Changesets check the stdout if returns empty, assume that it run on Github actions and package not exists.
Normally, npm info never returns empty string on stdout.

But these is a case that can returns empty string.

If your package is published pre-release version and never published stable version yet, Looks like the registry can't get package info because no info from stable version so it returns empty string instead (package info is empty)

{{< notice note >}}
Not sure that all registry has this problem. In my case the registry is [SonarType Nexus](https://www.sonatype.com/products/sonatype-nexus-repository)
{{< /notice >}}

## The solution

Publish a stable version to registry once then `npm info` will return package info with pre-release version info correctly, instead of empty string.
