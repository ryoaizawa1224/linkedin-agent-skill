# LinkedIn Agent Skill for Codex

LinkedInアカウントの「書く・考える・振り返る」を担当する、Codex向け11個のSkillセットです。MITライセンス、登録不要、APIキー不要、外部サービスへの接続も不要です。

投稿案を21種類のフックから作るSkill、他人の投稿へのコメントを書くSkill、自分の投稿についたコメントへの返信を作るSkill、プロフィールを100点満点で採点して改善するSkill、1週間の投稿・交流計画を作るSkillなどが含まれます。

さらに `$li-human` が、em dashや生成AIで出やすい定型表現、不可視文字などを除去し、5つのローカル指標で文章をチェックします。

**LinkedInへの投稿・コメント・DM送信は自動では行いません。** Skillが文章を作り、最終的な投稿操作はユーザーが行います。

このforkは、Jake Schincariol氏のClaude向けオリジナル版をOpenAI Codex向けに移植したものです。コンテンツ戦略やPythonツールの基本設計は原作者によるもので、Codex向けのパッケージング、呼び出し方法、ファイルパスなどを調整しています。

## インストール

### CodexにGitHubからインストールさせる

Codexにこのリポジトリを渡し、`skills/` 以下のSkillをすべてインストールするよう依頼します。

```text
https://github.com/ryoaizawa1224/linkedin-agent-skill

このリポジトリのLinkedIn Skillsをすべてインストールして、$li-post が使えることを確認して。
```

CodexのSkill installerは、GitHubリポジトリから `$CODEX_HOME/skills`（通常は `~/.codex/skills`）へSkillを直接インストールできます。

### 手動でグローバルインストール

```bash
git clone https://github.com/ryoaizawa1224/linkedin-agent-skill.git
mkdir -p ~/.codex/skills
cp -r linkedin-agent-skill/skills/li-* ~/.codex/skills/
```

### プロジェクト単位でインストール

対象プロジェクトの `.agents/skills/` にSkillフォルダをコピーします。

```bash
mkdir -p .agents/skills
cp -r /path/to/linkedin-agent-skill/skills/li-* .agents/skills/
```

このリポジトリにはCodex Plugin用の `.codex-plugin/plugin.json` も含めます。

## 最初にvoice.mdを作る

`templates/voice.md` を次の場所へコピーします。

```text
~/.codex/linkedin/voice.md
```

テンプレートを自分で埋めてもよいですし、自分の過去投稿を3本Codexに渡して「これを元にvoice.mdを作って」と依頼しても構いません。関連するSkillはこのファイルを参照し、文体や避ける表現、読者像などを合わせます。

`voice.md`、`log.md`、`plan.md` はユーザー個人のローカルファイルとして扱います。個人情報や非公開情報が含まれる場合、このpublicリポジトリへcommitしないでください。

## 11個のSkill

| Skill | 内容 |
| --- | --- |
| `$li-post` | 1つのアイデアからLinkedIn投稿を作成。21種類のフックから3案を選び、本文まで作る。 |
| `$li-comment` | 他人の投稿へのコメント案を作成。投稿内容に応じて9タイプから選ぶ。 |
| `$li-reply` | 自分の投稿についたコメントを分類し、返信案を作成。 |
| `$li-profile` | プロフィールを12項目・100点満点で採点し、改善文を作る。 |
| `$li-plan` | 1週間の投稿内容・投稿時刻・交流対象を計画。`~/.codex/linkedin/plan.md` に保存。 |
| `$li-human` | 文章のAIっぽい定型表現や不可視文字などを除去・検査するローカルツール。 |
| `$li-carousel` | LinkedInのドキュメント投稿／カルーセルの構成とスライド文面を作成。 |
| `$li-repurpose` | 動画、ニュースレター、記事、文字起こしなどから複数投稿を抽出。 |
| `$li-dm` | 接続申請文、最初のDM、フォローアップ文を作成。 |
| `$li-inbox` | LinkedIn受信箱の内容をlead / recruiter / peer / ask / spamに分類し、必要な返信だけ作る。 |
| `$li-audit` | 過去投稿を分析し、何が機能しているか、何をやめるべきかを整理。 |

## Humanizer

`$li-human` には外部依存のない2つのPythonスクリプトが含まれています。すべてローカルで実行されます。

```bash
python3 humanize.py draft.txt --report
python3 detect.py draft.txt
python3 detect.py before.txt after.txt
```

主な処理は次の通りです。

- ゼロ幅スペース、joiner、soft hyphen、BOM、non-breaking spaceなどの不可視・format文字を除去／正規化
- em dash → comma、en dash → hyphen、curly quote → straight quote、ellipsis → `...` などのタイポグラフィ正規化
- [`slop.json`](skills/li-human/slop.json) に登録された生成AIで頻出しやすい定型表現の置換

三段論法的な定型、1語だけの修辞疑問、ハッシュタグの壁、露骨なengagement bait、文長の均一さなどは、自動修正せず「要書き換え」として検出します。

5つの指標は BURSTINESS、SPECIFICITY、SLOP DENSITY、FINGERPRINT、VOICE です。これらはローカルなヒューリスティクスであり、GPTZero等の外部検出APIではありません。また、「AI生成と絶対に検出されない」ことを保証するものでもありません。

## Codexで使う状態ファイル

必要に応じて以下を参照します。

```text
~/.codex/linkedin/voice.md
~/.codex/linkedin/log.md
~/.codex/linkedin/plan.md
```

- `voice.md`: 文体、読者像、使う／使わない表現、公開可能な実績など
- `log.md`: 過去に作成・投稿した内容の履歴。`$li-audit` で利用
- `plan.md`: `$li-plan` が作成する週間運用計画

## LinkedInの自動操作について

このSkillセットはLinkedIn上での投稿、コメント、connection request、DM送信、スクレイピングを自動実行しません。最終的なLinkedIn上の操作はユーザー自身が行います。

また、実績、数値、クライアント、成果、共通の知人などを捏造しません。必要な事実が不足している場合は、ユーザーに確認するか、未確定であることを明示します。

## 主なファイル

```text
.codex-plugin/plugin.json        Codex Plugin manifest
skills/li-post/hooks.json        21種類の投稿フック
skills/li-human/slop.json        定型表現・不可視文字・構造パターン
skills/li-human/humanize.py      文章クリーニング
skills/li-human/detect.py        5指標によるチェック
skills/li-profile/rubric.json    プロフィール100点採点基準
templates/voice.md               文体プロフィールのテンプレート
```

## Credit

Original skill pack: Jake Schincariol — [opusjake.ai](https://opusjake.ai)

Original repository: [Jakeschincariol/linkedin-agent-skill](https://github.com/Jakeschincariol/linkedin-agent-skill)

Codex向け移植・日本語化: Ryo Aizawa

## License

MIT。詳細は [LICENSE](LICENSE) を参照してください。
