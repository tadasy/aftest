# iframeを用いたクロスドメイントラッキング

## 概要

ショッピングサイトなどで、ショップサイトと購入完了ページが別ドメインだったときに、コンバージョンを計測できる仕組みを検証した

## 流れ

* `site-a` の `lp.html` から `site-b` の `thankyou.html` に遷移する
* `site-a` の `lp.html` では現在日時をcookieに焼いている
* `site-b` の `thankyou.html` では `site-a` の `iframe_cv.html` をiframeで読み込んでいる
* `site-b` の `thankyou.html` では [postMessage](https://developer.mozilla.org/ja/docs/Web/API/Window/postMessage) を使って `site-a` の `iframe_cv.html` に コンバージョン情報を送信する
* iframe内の `iframe_cv.html` では `lp.html` で焼いた現在時刻と、postMessageで取得したコンバージョン情報を表示する

## 動かし方

`site-a` を立ち上げる
```
$ cd site-a
$ php -S localhost:8080
```

`site-b` を立ち上げる
```
$ cd site-b
$ php -S localhost:8081
```

lp.htmlにアクセス

```
http://localhost:8080/lp.html
```
