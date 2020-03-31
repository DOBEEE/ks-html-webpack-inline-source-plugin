# Inline Source extension for the HTML Webpack Plugin

[![npm version](https://badge.fury.io/js/ks-html-webpack-inline-source-plugin.svg)](https://badge.fury.io/js/ks-html-webpack-inline-source-plugin)

## 修复点：

原有 html-webpack-inline-source-plugin 在配合 html-webpack-plugin 时，传入的参数 filename 必须为`xxx.html`的文件名形式，如果写成`xxx/xxx.html`如下方代码，则会报错：

```
new HtmlWebpackPlugin({
    template: 'index.html`,
    filename: `${name}/index.html`,
    chunks: [`${name}`],
    inlineSource: '.(js|css)$',
    minify: {
        removeComments: true,
        collapseWhitespace: true,
        removeAttributeQuotes: true,
    },
});
```

报错信息：

```
TypeError: Cannot read property 'source' of undefined
```

对应 issues：https://github.com/DustinJackson/html-webpack-inline-source-plugin/issues/57

Enhances [html-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin)
functionality by adding the `{inlineSource: 'regex string'}` option.

This is an extension plugin for the [webpack](http://webpack.github.io) plugin [html-webpack-plugin](https://github.com/ampedandwired/html-webpack-plugin) (version 4 or higher). It allows you to embed javascript and css source inline.

## Installation

You must be running webpack on node 6 or higher.

Install the plugin with npm:

```shell
$ npm install --save-dev ks-html-webpack-inline-source-plugin
```

## Basic Usage

Require the plugin in your webpack config:

```javascript
var HtmlWebpackInlineSourcePlugin = require("ks-html-webpack-inline-source-plugin");
```

Add the plugin to your webpack config as follows:

```javascript
plugins: [new HtmlWebpackPlugin(), new HtmlWebpackInlineSourcePlugin()];
```

The above configuration will actually do nothing due to the configuration defaults.

When you set `inlineSource` to a regular expression the source code for any javascript or css file names that match will be embedded inline in the resulting html document.

```javascript
plugins: [
  new HtmlWebpackPlugin({
    inlineSource: ".(js|css)$" // embed all javascript and css inline
  }),
  new HtmlWebpackInlineSourcePlugin()
];
```

## Sourcemaps

If any source files contain a sourceMappingURL directive that isn't a data URI, then the sourcemap URL is corrected to be relative to the domain root (unless it already is) instead of to the original source file.

All sourcemap comment styles are supported:

- `//# ...`
- `//@ ...`
- `/*# ...*/`
- `/*@ ...*/`
