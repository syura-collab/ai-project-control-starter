# Project Control Index

- status: canonical entrypoint
- reader / writer: ChatGPT

Project ControlはChatGPTの外部長期記憶です。このファイルを唯一の起動入口とします。

## 0. Startup

新しいChatGPTチャットでは次の順に読みます。

1. `INDEX.md`
2. `CURRENT.md`
3. このINDEXが対象テーマの正本として指定するcanonical document
4. 必要な場合だけcheckpoint / legacy reference
5. 実装判断が必要ならcommitted `main`

Codex / Claude CodeなどのImplementation Agentへ、このブランチやProject Control文書を直接渡しません。詳細は`OPERATING_MODEL.md`を参照してください。

## 1. Core

| 文書 | 役割 |
|---|---|
| `CURRENT.md` | 現在地・Active Scope・再開地点 |
| `OPERATING_MODEL.md` | ChatGPT persistent brain、Implementation Agent境界、ブランチ運用の正本 |
| `project_charter.md` | プロジェクト目的・成功状態・Human Authority・長期制約 |
| `prompt_policy.md` | ChatGPTがImplementation Agent向けTask Packetを作る方針 |
| `chatgpt_entrypoint.md` | INDEXへの互換入口。現在地を重複保持しない |

## 2. Domain Canonical Map

プロジェクト固有の正本をここへ追加します。

例:

- `<DOMAIN_A>`
  - canonical: `<path/to/canonical.md>`
  - checkpoint: `<path/to/checkpoint.md>` 必要時のみ
- `<DOMAIN_B>`
  - canonical: `<path/to/canonical.md>`

同一テーマに複数文書がある場合、INDEXが現在の優先順位を決めます。

## 3. Classification

### CURRENT / canonical

現在の判断に直接使います。通常再開時に読む対象です。

### decision / strategy / policy

長く使うプロジェクト判断です。INDEXが現行として指定している間は有効です。

### checkpoint / handoff / implementation status

特定時点の事実確認用です。通常再開時には自動で全件読みません。

### legacy

Git historyまたはlegacy referenceとして残しますが、現在判断へ自動適用しません。

## 4. Discovery and History

- INDEX: 正本・読む順番・authorityを決める
- GitHub search: INDEXにない過去情報や固有語を探索する
- Git history: 過去状態・退役文書を復元する

検索結果で古い`status`、`active scope`、`handoff`などを見つけても、CURRENTやINDEXより優先しません。

## 5. File Creation Rule

新しいProject Control文書を作る前に、INDEXと既存文書を確認します。

過去版を保持するためだけに`*_current_YYYYMMDD.md`やhandoffを増殖させません。現在地は`CURRENT.md`へ置き換え、過去状態は原則Git historyへ任せます。
