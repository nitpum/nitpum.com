---
title: Use nanoid in WeChat Mini Program
author: nitpum
date: 2023-11-02T03:25:06.322Z
lastmod: 2023-11-02T03:28:05.540Z
toc: false
tags:
  - wechat
  - mini-program
  - nanoid
  - javascript
---

Developing WeChat mini program

Want to use [nanoid](https://github.com/ai/nanoid) to generate unique id or something like that

npm i nanoid

"node:crypto" is not defined, "crypto" is not defined

Surpise! nanoid is relying on [Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)

WeChat don't have Web Crypto API

What to do now?

Peek the [source code](https://github.com/ai/nanoid/blob/88af1ee0d6610efc308d265018c1cd89f52bb76b/index.browser.js#L50C1-L51C70)

```js {linenos=table, hl_lines=[2], linenostart=50}
export let nanoid = (size = 21) =>
	crypto.getRandomValues(new Uint8Array(size)).reduce(/* ... */);
// ...
```

Oh, it just need only `crpyto.getRandomValues`. Don't require entire crypto API

Fortunately, WeChat mini program has built-in [wx.getRandomValues](https://developers.weixin.qq.com/miniprogram/en/dev/api/device/crypto/wx.getRandomValues.html)!

Let's try to port this

First, change `cryto.getRandomValues()` to `wx.getRandomValues`

```js
export let nanoid = (size = 21) =>
	wx.getRandomValues({
		length: size,
		succes: res => new Uint8Array(res.randomValues
	})
	.reduce(/* ... */)
```

`wx.getRandomValues` it not immediately return value, instead it is a callback style so can't just simple call `.reduce`

Need to move reduce into the success callback function

Don't like that way

Make it promise!

```js
export let nanoid = async (size = 21) => {
	const randomValues = await new Promise((resolve) => {
		wx.getRandomValues({
			length: size,
			success: res => resolve(new Uint8Array(res.randomValues))
		}
	})

	return randomValues.reduce(/* ... */)
};
```

It work!

Copy and paste it some where in the project

npm remove nanoid. No need it in node_modules any more

Here the final code
{{< notice note >}}
I'm not security expert. Use this at your own risk
{{< /notice >}}

```js
export default async function nanoid(size = 21) {
	const randomValues = await new Promise((resolve) => {
		wx.getRandomValues({
			length: size,
			success: (res) => resolve(new Uint8Array(res.randomValues)),
		});
	});

	return randomValues.reduce((id, byte) => {
		byte &= 63;
		if (byte < 36) {
			id += byte.toString(36);
		} else if (byte < 62) {
			id += (byte - 26).toString(36).toUpperCase();
		} else if (byte > 62) {
			id += "-";
		} else {
			id += "_";
		}
		return id;
	}, "");
}
```

Usage

```js
const id = await nanoid();
```
