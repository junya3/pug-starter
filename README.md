## Pug Starter

### 概要

`pug`, `scss`, `typescript`で開発する機会が増えたので、使いやすいようにテンプレートを作成してみました。

### 使い方

1. `npm i`を実行し、環境をインストールしてください。
1. 開発は`/src`で行い、`/src/public`には静的ファイルを、`/src/include`にはテンプレート等を格納しましょう。
1. `npm run watch`とすると自動的に`/dist`にコンパイルされ、同時に Live Server を立ち上げ、擬似的なホットリロードを実現しています。
1. 必要に応じてファイルを書き換えてください。

### 注意点

- style の開発は`include`内で管理し、`main.scss`はいじらないようにしましょう。

### 開発者向け

`package.json`に殆ど書いてあります。
