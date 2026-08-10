# lino-letter

Lino Well-being「人生のハンドルを取り戻すメールレター」の登録LP。
公開先: https://letter.linowellbeing.com/ （GitHub Pages）

## 構成
- `index.html` … LP本体（1ファイル完結・CSS埋め込み）
- `images/` … ロゴ・プロフィール写真
- `CNAME` … 独自ドメイン letter.linowellbeing.com（ムームーDNSにCNAME設定済み・2026-08-10）

## 登録フォームの仕組み
素のHTML formで my UTAGE の Worker に直接POSTしている。

```
action="https://ml.chiho-m.workers.dev/signup"
hidden: list=lino / scenario=handle / source=lp-letter
```

- 送信すると Worker 側の「確認メールをお送りしました」ページに遷移する
- 確認メールのリンクを押すと登録確定＋ステップ配信（全27通）が開始
- **JavaScript(fetch)方式にはしないこと。** Worker に CORS ヘッダーが無いため、
  別ドメインからの fetch はブラウザにブロックされる（素のform POSTは制限を受けない）
- Worker に独自ドメイン（例 ml.linowellbeing.com）を当てたら `action` を差し替える

## 原稿の出どころ
`Mothership-lab/2026-07_lino_merumaga_lp.txt`（2026年7月にUTAGEで公開していたLPの原稿）
