# pronunciation-trainer

英語の発音練習アプリ。**https://yuckeyym.github.io/pronunciation-trainer/**

Claude（`/pronunciation` スキル）が作った練習セットの JSON を貼り付けると、
ブラウザの音声認識で「**意図した語として聞き取られたか**」を判定する。

発音の良し悪しを音響的に採点しているのではなく、**通じたかどうか**を見ている。
Obsidian の `English/Pronunciation/_苦手ログ.md` に
「tempo が temple と誤認される」という記録が並んでいたことが出発点。

## 判定

| 結果 | 条件 |
|---|---|
| ◎ | 認識の第1候補が狙いの語と一致 |
| △ | 第2〜5候補に狙いの語がある／別の語に聞こえた |
| ✗ | `confused` に登録した「誤認されやすい語」になった |

✗ のときは、どの語に化けたかと直し方を出す。

## 貼り付ける JSON

```json
{
  "focus": "vowel-er",
  "items": [{
    "word": "batter",
    "ipa": "/ˈbætər/",
    "types": ["vowel-er", "r-l"],
    "confused": ["battle", "bottle"],
    "tip": "語末の -er は舌先をどこにも触れさせない。触れた瞬間に L になる。",
    "sentence": "The batter hit a foul tip."
  }]
}
```

`word` 以外は省略可。配列だけ（`[{...}]`）でも、` ```json ` で囲まれたままでも読み込める。

## 結果の保存

「Obsidianに追記」で `Journal` Vault の
`English/Pronunciation/Sessions/発音練習 YYYY-MM-DD.md` に直接書き込む（Mac・iPhone 共通）。
`/weekly` の発音の週次分析が、このファイルを読んで「練習して改善したか」を見る。

## 動作条件

- **音声認識にはネット接続が必要。** Safari（iOS 14.5+ / macOS）と Chrome で動く
- 静かな場所のほうが安定する
- 音声認識に非対応のブラウザでは、お手本の読み上げだけ使える

## 更新するとき

1. `index.html` を編集
2. `APP_VERSION` と `APP_DATE`、`CHANGELOG` の先頭を更新
3. `git commit && git push origin main` → GitHub Pages が自動で公開（反映まで1〜2分）

## 関連

日本語の発声練習（リップロール・巻き舌・Kの子音）は別アプリ:
[voice-training](https://github.com/YuckeyYM/voice-training)
