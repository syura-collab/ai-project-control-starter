# Task Packet / Prompt Policy

- status: canonical policy

この文書は、ChatGPTがCodex / Claude CodeなどのImplementation Agentへ渡すTask Packetを作る方針を定義します。

## 1. Purpose

Task Packetの目的は、Project ControlをImplementation Agentへ丸ごと渡すことではありません。

今回の作業を正しく実行するために必要な情報だけを、明確な作業契約としてまとめることです。

## 2. Include

Task Packetには必要に応じて次を含めます。

- Goal
- Scope
- Non-goals
- Current implementation facts
- Canonical decisions relevant to the task
- Constraints
- Human Gates
- Acceptance criteria
- Verification / test requirements
- Stop conditions
- Expected report format

## 3. Exclude

原則として次は含めません。

- Project Control全文
- 無関係な長期履歴
- 会話ログ全文
- 他domainの不要な判断
- credential / API key / token / password
- 不要な個人情報
- Implementation Agentが`main`から直接確認できる大量の実装情報

## 4. Source Priority

Task Packetを作る際のauthorityは次を基本とします。

1. Humanの現在の明示指示
2. `project-control` のCURRENT / canonical documents
3. committed `main` の実装事実
4. checkpoint / legacy reference

古いhandoffや過去statusがCURRENT / canonicalと矛盾する場合、古い情報を優先しません。

## 5. Scope Discipline

Implementation Agentへ「良い感じに改善」「全部直す」などの無限定な依頼をしません。

何を変えてよいか、何を変えないか、どの状態になれば完了かを可能な限り明示します。

プロジェクト全体の再設計が必要に見えても、Task Packetで許可されていなければ勝手にscopeを拡張させません。

## 6. Verification

「実装した」だけで完了にしません。

必要に応じて次をTask Packetへ含めます。

- targeted tests
- full test suite
- lint / type check
- build
- runtime / GUI確認
- regression確認
- diff / changed-files review

プロジェクトのExit Conditionに対応した検証を要求します。

## 7. Inconsistency Handling

Task Packetの前提と`main`の現物が食い違った場合、Implementation AgentはProject Controlを直接確認せず、変更を止めてinconsistencyを報告します。

ChatGPTがプロジェクト全体の文脈と実装事実を再評価し、必要ならTask Packetを更新します。

## 8. Result Handling

Implementation Agentの返答は完了宣言として鵜呑みにしません。

ChatGPTは少なくとも次を確認します。

- Goalに到達したか
- Scope外変更がないか
- Acceptance criteriaを満たしたか
- Verification結果が十分か
- Project Controlへ反映すべき意味の変化があるか

必要な意味の変化だけをProject Controlへ反映します。
