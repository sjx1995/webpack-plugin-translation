# webpack-plugin-translation

[简体中文](./README.md) | English

💡 Same translation function, but unplugin: [sjx1995/unplugin-i18n-translation](https://github.com/sjx1995/unplugin-i18n-translation)

## Introduction

A Webpack plugin for automatically translating internationalization files.

Translates the local language files of i18n package(i.e. [vue-18n](https://kazupon.github.io/vue-i18n/)) and generates translation files for other languages.

> Online translation is provided by [Tencent Machine Translation](https://cloud.tencent.com/document/api/551/15619).

## Required

Before using, please ensure that you have already installed and configured i18n package(i.e. [vue-18n](https://kazupon.github.io/vue-i18n/)), and that you have a default language localization file as the source file for translation.

In addition, you will also need to apply for an API key from [Tencent Cloud API Key](https://console.cloud.tencent.com/capi).

## Install

```bash
# npm
npm install @sunly95/webpack-plugin-translation --save-dev

# yarn
yarn add @sunly95/webpack-plugin-translation --dev
```

## Usage

### webpack

Configure the plugin in `webpack.config.js`, for detailed configuration parameters see [Configuration](#Configuration).

```js
// webpack.config.js

// import plugin
const AutoTranslation = require("@sunly95/webpack-plugin-translation");

module.exports = {
  plugins: [
    // register plugin
    new AutoTranslation({
      id: secretId, // tencent cloud API secret ID
      key: secretKey,  // tencent cloud API secret key
      originLang: "en",  // origin language
      targetLangs: [
        { lang: "zh", filename: "zh-CN" },
      ], // list of target languages
      originFilePath: "./src/locales/en.json", // origin translation file
      targetDirPath: "./src/locales"  // target translation files directory
    })
  ]
}
```

### vue-cli

Configure the plugin in `vue.config.js`, for detailed configuration parameters see [Configuration](#Configuration).

```js
// vue.config.js

// import plugin
const AutoTranslation = require("@sunly95/webpack-plugin-translation");

module.exports = {
  // register plugin
  config.plugin("AutoTranslation").use(
    new AutoTranslation({
      id: secretId, // tencent cloud API secret ID
      key: secretKey,  // tencent cloud API secret key
      originLang: "en",  // origin language
      targetLangs: [
        { lang: "zh", filename: "zh-CN" },
      ], // list of target languages
      originFilePath: "./src/locales/en.json", // origin translation file
      targetDirPath: "./src/locales"  // target translation files directory
    })
  );
}
```

After configuration, before build process, the file specified by `originFilePath` will be automatically read as the original text for translation. Based on the provided `targetLangs`, translations will be generated automatically, and the translated files will be stored in the directory specified by `targetDirPath`.

## Configuration

| Parameter      | Type                                 | Required | Description                                                                                                                                                                                                                                                                       |
| -------------- | ------------------------------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id             | string                               | ✅        | Tencent Cloud API Key ID                                                                                                                                                                                                                                                          |
| key            | string                               | ✅        | Tencent Cloud API Key                                                                                                                                                                                                                                                             |
| originLang     | string                               | ✅        | Original file language for translation, [see the Source field for valid values](https://cloud.tencent.com/document/api/551/15619)                                                                                                                                                 |
| targetLangs    | { lang: string, filename: string }[] | ✅        | List of target languages for translation. The `lang` field indicates the target language, [see the Target field for valid values](https://cloud.tencent.com/document/api/551/15619), and the `filename` field indicates the filename of the generated i18n file after translation |
| originFilePath | string                               | ✅        | Absolute path of the original translation file                                                                                                                                                                                                                                    |
| targetDirPath  | string                               | ✅        | Directory for storing the translated target files                                                                                                                                                                                                                                 |
| spaceWidth     | number?                              |          | Indentation space count for the generated JSON file after translation, default is 2                                                                                                                                                                                               |

## Changelog

[CHANGELOG](./CHANGELOG.md)
