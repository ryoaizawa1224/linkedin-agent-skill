---
name: li-human
description: >-
  草稿から機械的な特徴やAIで頻出する定型表現、不可視文字などを除去し、
  5つのローカル指標でチェックする。LinkedIn投稿、コメント、返信、DMを見せる前や、
  「AIっぽさを減らして」「humanizeして」と頼まれたときに使う。
---

# li-human

このフォルダには実際に実行できる2つのPythonツールがある。目視だけで済ませず、必要に応じて実行する。

```bash
python3 humanize.py draft.txt --report
python3 detect.py draft.txt
python3 detect.py before.txt after.txt
```

両方とも `slop.json` を読む。ここには生成文で出やすい定型語、不可視文字、タイポグラフィ置換、構造上のパターンが定義されている。ユーザー自身がよく使う語が誤って除去される場合は、lexicon側を調整する。

## 自動修正するもの

### 1. 不可視文字

zero-width space / joiner、word joiner、soft hyphen、BOM、Unicode tag、non-breaking spaceなどを削除・正規化する。

### 2. タイポグラフィ

em dash → comma、en dash → hyphen、curly quote → straight quote、ellipsis → `...`、bullet → hyphenなどを正規化する。

### 3. 定型表現

`slop.json` に入っている、生成AIで過剰に出やすい語句をより平易な表現へ置き換える。URL内は壊さない。

## 自動で直さず、flagするもの

文の構造自体を変える必要があるものは、regexで無理に修正せず検出だけする。

- 「XではなくY」の定型構文
- rule-of-three型の並列
- 「結果は？」のような1語の修辞疑問
- 絵文字の過剰使用
- hashtag wall
- 「Thoughts?」「Agree?」などの汎用engagement bait
- 文長や箇条書き長の過度な均一性

検出された行は意味を維持して書き直し、再度 `detect.py` を実行する。

## 5つのチェック

| 指標 | 見るもの |
| --- | --- |
| BURSTINESS | 文長のばらつき |
| SPECIFICITY | 数字、固有名詞、具体的なマーカー |
| SLOP DENSITY | 定型語の密度 |
| FINGERPRINT | 不可視文字や特定タイポグラフィの密度 |
| VOICE | 人称、口語性、構造上のパターン |

スコアはローカルなヒューリスティクスであり、GPTZero、Originality、Copyleaks、Winston、Turnitin等の外部APIではない。「絶対にAI判定されない」と保証しない。

## 基本手順

1. `humanize.py draft.txt -o clean.txt --report`
2. structural flagを読み、必要な行をモデル側で書き直す。
3. `detect.py draft.txt clean.txt` でbefore / afterを比較する。
4. PASSにならなければ、最も弱い指標を中心に再修正する。
5. ユーザーにはスコアだけでなく、修正後の文章も必ず示す。
