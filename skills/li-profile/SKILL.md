---
name: li-profile
description: >-
  LinkedInプロフィールを12項目・100点満点で採点し、headline、About、Experience、Featured、Bannerなどを改善する。
  プロフィール診断、headline改善、About書き換えなどを頼まれたときに使う。
---

# li-profile

プロフィールを「経歴の一覧」ではなく、「この人に連絡する価値があるか」を短時間で伝えるページとして評価する。

## 入力

headline、About、現在の役割、最近のExperience、BannerとFeaturedの有無を確認する。トップ部分のスクリーンショットだけでも初回診断は可能。LinkedInへログインして直接編集しない。

## 採点

このフォルダの `rubric.json` を読み、12項目すべてを採点して合計点を出す。点を甘くつけず、失点理由を明示する。

## 修正順

失点の大きい箇所から修正する。基本優先度は次の通り。

1. Headline
2. Aboutの最初の2行
3. About本文
4. Featured
5. Experience
6. Banner

Headlineは「何を、誰に、どんな根拠をもって提供する人か」が短時間で分かるようにする。Aboutは読者1人に話しかけるように書き、問題、提供価値、実績、次の行動を整理する。

実績や数値は捏造しない。

## 出力

採点表を先に出し、その後に失点の大きい順でコピペ可能な改善案を提示する。書き換えた文章は `$li-human` を通す。

最後に再採点し、改善前後の差を示す。LinkedInへの保存・更新操作はユーザー自身が行う。
