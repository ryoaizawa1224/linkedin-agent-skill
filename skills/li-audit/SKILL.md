---
name: li-audit
description: >-
  過去のLinkedIn投稿を分析し、何が機能したか、なぜ伸びた／伸びなかったか、
  今後何を増やし何をやめるべきかを整理する。投稿分析やanalyticsの監査を頼まれたときに使う。
---

# li-audit

一般論より、そのアカウント自身の過去投稿を優先して判断するSkill。

## 入力

利用できるものを使う。

- LinkedInのContent Analytics export（CSV）
- 各投稿のimpressions、reactions、comments、reposts等のスクリーンショット
- 投稿本文とreaction数だけでも初期分析は可能

`~/.codex/linkedin/log.md` があれば読み、どのhook formulaを使ったかも照合する。

## 見る指標

可能な範囲で以下を計算し、式も示す。

- **Engagement rate** = (reactions + comments + reposts) / impressions
- **Comment ratio** = comments / reactions
- **Reach multiple** = impressions / follower count
- **Save/send rate** = データが取れる場合

単純なimpressionsだけではなく、engagement rateとreach multipleを重視する。

## パターンを探す

上位投稿と下位投稿を並べ、フック、フォーマット、長さ、テーマ、曜日・時間、初動返信などの差を見る。曜日・時間は最後に確認し、他の要因より過大評価しない。

サンプル数が少ない場合は、無理に傾向を断定しない。主張には根拠と確信度を添える。

## 出力

- 最も強い傾向
- やめること
- 増やすこと
- 次週に試す仮説

を整理し、結論を `$li-plan` に渡して次週の計画へ反映する。
