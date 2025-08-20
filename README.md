# Pug Starter Debug

このプロジェクトは、Pug + SCSS + TypeScript を使ったサブディレクトリ対応テンプレートです。

## フォルダ構成例

```
project-root/
├─ src/
│  ├─ app/          # ページ管理
│  └─ component/    # コンポーネント管理
├─ public/
│  └─ assets/       # 画像、CSS、JS
└─ dist/            # コンパイル後出力
```

## basePath について

- GitHub Pages やサブディレクトリで公開する場合、HTML やリンクのルートを統一するためのパスです。
- 例: `https://username.github.io/pug_starter_debug/`
- すべてのリンクや画像、CSS/JS のパスを `${basePath}/...` で指定します。
- **layout.pug に定義**しておけば、子ページ側で再定義する必要はありません。
- 注意点:
  - basePath の値を変更すると、すべてのリンク・画像・CSS/JS パスが影響を受けます。
  - 子ページで同じ変数名を定義すると、layout の basePath が上書きされます。
  - ページ内アンカー（例: `#section`）には影響しません。

## コンパイル後の出力例

```
dist/
├─ index.html       # トップページ
├─ about/
│  └─ index.html    # 下層ページ
└─ assets/
   ├─ style/main.css
   ├─ js/main.js
   └─ image/sample.png
```

## 使い方

### ページ管理

- `src/app` にページを管理
- `src/component` にコンポーネントを管理
- 開発時には以下を使用：

  ```bash
  npm run watch
  ```

  - pug、scss、typescript を監視し、擬似的にホットリロード
  - 対象を制限したい場合：

    ```bash
    npm run watch:pug
    ```

- 通常の監視でも `dist` にコピーされます
- 画像のみを dist に格納する場合：

  ```bash
  npm run copy:images
  ```

- 単独で live-server を立てる場合：

  ```bash
  npm run serve
  ```

### リンクや画像、CSS/JS の書き方

- CSS/JS は basePath を使って統一：

  ```pug
  link(rel="stylesheet", href=`${basePath}assets/style/main.css`)
  script(type="module", src=`${basePath}assets/js/main.js`)
  ```

- 下層ページリンクや画像も basePath を使用：

  ```pug
  a(href=`${basePath}about/`) Aboutページ
  img(src=`${basePath}assets/image/sample.png`, alt="サンプル")
  ```

- これにより、サブディレクトリ配下での 404 を防ぎ、すべてのリソースを統一的に管理できます。

### ページタイトルの追加

- layout で定義されたタイトルブロックに追加する場合：

  ```pug
  block prepend title
    - const pageTitle = "トップページ";
  ```

- 前に追加したい場合は `prepend`、後ろに追加したい場合は `append` を使用
- HTML 出力例:

  ```html
  <title>FlowSync | トップページ</title>
  ```

## 注意点

- basePath を間違えるとリンク切れや 404 になります。
- 子ページで同名変数を定義すると layout の変数が上書きされます。
- ページ内アンカー（例: `#section`）は basePath の影響を受けません。

## Tips

- layout に basePath を定義しておくと、全ページでリンク管理が簡単になります。
- 子ページでページタイトルを追加する際は `block prepend title` または `block append title` を使い分けましょう。
