# Operating Model

- status: canonical operating model

この文書は、Human / ChatGPT / Implementation Agent の役割、ブランチ、コンテキスト境界の正本です。

## 1. Core Model

このプロジェクトでは、長期的な意味・判断・現在地と、実装作業を分離します。

- `project-control`: Human + ChatGPT がプロジェクト全体を復元・維持するための persistent brain
- `main`: 実装source、stable technical docs、tests、Implementation Agentの通常作業場

`project-control` はfeature branchではなく、`main`へmergeしません。

## 2. Human

Humanは次を所有します。

- Goal
- 重要なtrade-off
- Human Gate
- 不可逆・破壊的・外部影響・金銭・productionなどのプロジェクト固有判断

AIへ委任してよい範囲はProject Charterで定義します。

## 3. ChatGPT

ChatGPTはプロジェクト全体の調整役です。

主な責務:

- `project-control`からプロジェクトの意味・判断・現在地を復元する
- 必要に応じてcommitted `main`の実装事実を確認する
- 次に進めるべき作業を判断する
- Implementation AgentへTask Packetを作成する
- Agentの結果をレビューする
- 必要なProject Control更新を行う

ChatGPTはProject Control全文を毎回読むのではなく、`INDEX.md`を入口に必要な正本だけを選択します。

## 4. Implementation Agents

Codex / Claude CodeなどのImplementation Agentは、通常`main`だけを扱います。

Project Controlを直接読みません。

Agentへ渡すのは、ChatGPTが必要情報だけをまとめたTask Packetです。

AgentはTask Packetに明示されたscope内で、調査・実装・test・reviewを行います。

Task Packetと`main`上の実装事実が食い違う場合は、Project Controlを読みに行ったり前提を勝手に変更したりせず、inconsistencyとして報告します。

## 5. Task Packet

Task PacketはProject Controlのコピーではありません。

今回の作業に必要な情報だけを含めます。

推奨要素:

- Goal
- Scope
- Non-goals
- Canonical facts
- Constraints
- Human Gates
- Acceptance criteria
- Verification requirements
- Stop conditions

長期履歴、無関係なdomain、会話ログ、秘密情報は含めません。

## 6. Project Control Update

Project Controlは日記ではありません。

次のような意味の変化があったときだけ更新します。

- プロジェクト全体の状態
- Active Scope
- Restart Point
- canonical decision
- authority / boundary
- unresolved question

古いCURRENTを追記保存せず、現在状態へ置き換えます。過去状態は原則Git historyへ任せます。

## 7. Security Boundary

このarchitectureはsecurity mechanismではありません。

Project Controlにも次を保存しません。

- API key / token / password
- session / cookie
- private key
- 不要な個人情報
- runtime databaseやraw export

必要な秘密情報はGitHub Secrets、環境変数、password managerなどの適切な仕組みへ分離します。

## 8. Principle

Project Controlを維持すること自体をプロジェクトの目的にしません。

必要な意味・判断・現在地だけを残し、実際のGoal達成を優先します。
