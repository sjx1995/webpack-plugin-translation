# webpack-plugin-translation

简体中文 | [English](./README_EN.md)

💡 相同的翻译功能，但是unplugin：[sjx1995/unplugin-i18n-translation](https://github.com/sjx1995/unplugin-i18n-translation)

## 介绍

一个自动翻译国际化文件的Webpack插件

将国际化插件(比如[vue-18n](https://kazupon.github.io/vue-i18n/))的本地语言文件翻译并生成其它语言的翻译文件

> 在线翻译由 [腾讯机器翻译](https://cloud.tencent.com/document/api/551/15619) 提供

## 必需

在使用之前请确保已经安装并配置了国际化插件(比如[vue-18n](https://kazupon.github.io/vue-i18n/))，而且已经有一个默认语言的本地化文件作为翻译的源文件

此外，还需要申请一个[腾讯云API密匙](https://console.cloud.tencent.com/capi)

## 安装

```bash
# npm
npm install @sunly95/webpack-plugin-translation --save-dev

# yarn
yarn add @sunly95/webpack-plugin-translation --dev
```

## 使用

### webpack

在`webpack.config.js`中配置插件，传入的配置参数详情见[配置](#配置)

```js
// webpack.config.js

// 引入插件
const AutoTranslation = require("@sunly95/webpack-plugin-translation");

module.exports = {
  plugins: [
    // 注册插件
    new AutoTranslation({
      id: secretId, // 腾讯云API密钥ID
      key: secretKey,  // 腾讯云API密钥Key
      originLang: "zh",  // 源语言
      targetLangs: [
        { lang: "en", filename: "en-US" },
      ], // 要翻译的语言列表
      originFilePath: "./src/locales/zh-CN.json", // 翻译原始文本文件，即vue-i18n的本地化文件
      targetDirPath: "./src/locales"  // 翻译后的文件存放目录
    })
  ]
}
```

### vue-cli

在`vue.config.js`中配置插件，传入的配置参数详情见[配置](#配置)

```js
// vue.config.js

// 引入插件
const AutoTranslation = require("@sunly95/webpack-plugin-translation");

module.exports = {
  // 注册插件
  config.plugin("AutoTranslation").use(
    new AutoTranslation({
      id: secretId, // 腾讯云API密钥ID
      key: secretKey,  // 腾讯云API密钥Key
      originLang: "zh",  // 源语言
      targetLangs: [
        { lang: "en", filename: "en-US" },
      ], // 要翻译的语言列表
      originFilePath: "./src/locales/zh-CN.json", // 翻译原始文本文件，即vue-i18n的本地化文件
      targetDirPath: "./src/locales"  // 翻译后的文件存放目录
    })
  );
}
```

配置完成后，在打包时会自动读取`originFilePath`指定的文件作为翻译的原始文本，根据传入的`targetLangs`自动翻译并生成翻译文件，存放在`targetDirPath`指定的目录下

## 配置

| 参数           | 类型                                 | 是否必需 | 说明                                                                                                                                                                                   |
| -------------- | ------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id             | string                               | ✅        | 腾讯云API密匙ID                                                                                                                                                                        |
| key            | string                               | ✅        | 腾讯云API密匙key                                                                                                                                                                       |
| originLang     | string                               | ✅        | 原始翻译文本语言，[取值见输入参数的Source字段](https://cloud.tencent.com/document/api/551/15619)                                                                                       |
| targetLangs    | { lang: string, filename: string }[] | ✅        | 需要翻译成的目标语言列表，`lang`字段表示要翻译成的语言，[取值见输入参数的Target字段](https://cloud.tencent.com/document/api/551/15619)，`filename`字段表示翻译后生成的i18n文件的文件名 |
| originFilePath | string                               | ✅        | 原始翻译文本的绝对路径                                                                                                                                                                 |
| targetDirPath  | string                               | ✅        | 翻译后生成的目标翻译文件的存储目录                                                                                                                                                     |
| spaceWidth     | number?                              |          | 翻译后后生成的json文件的缩进空格数，默认为2                                                                                                                                            |

## 更新日志

[CHANGELOG](./CHANGELOG.md)
