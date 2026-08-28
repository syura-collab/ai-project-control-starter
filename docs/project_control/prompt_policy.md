# Task Packet / Prompt Policy

- status: canonical policy

この文書は、ChatGPTがCodex / Claude CodeなどのImplementation Agentへ渡すTask Packetを作る方針を定義します。

## 1. Purpose

Task Packetの目的は、Project ControlをImplementation Agentへ丸ごと渡すことではありません。

今回の作業を正しく実行するために必要な情報だけを、明確な作業契約としてまとめることです。

Task Packetは項目を埋めるためのtemplateではありません。今回のtaskを正しく安全に完了するための必要十分なcontextだけを渡します。

## 2. Include

Task Packetには必要に応じて次を含めます。

- Goal
- Scope
- Non-goals（必要な場合のみ）
- Current implementation facts
- Canonical decisions relevant to the task
- Constraints
- Human Gates
- Acceptance criteria
- Verification / test requirements
- Stop conditions
- Expected report format

Goal、scope、canonical decision、Human Gate、受入条件など、Implementation Agentが推測してはいけないsemanticは省略しません。

## 3. Exclude

原則として次は含めません。

- Project Control全文
- 無関係な長期履歴
- 会話ログ全文
- 他domainの不要な判断
- credential / API key / token / password
- 不要な個人情報
- Implementation Agentが`main`から低コストで直接確認できる実装情報の重複コピー

迷った場合は「情報を多く渡す」より、「今回の判断に必要か」で採否を決めます。

## 4. Source Priority

Task Packetを作る際のauthorityは次を基本とします。

1. Humanの現在の明示指示
2. `project-control` のCURRENT / canonical documents
3. committed `main` の実装事実
4. checkpoint / legacy reference

古いhandoffや過去statusがCURRENT / canonicalと矛盾する場合、古い情報を優先しません。

## 5. Scope Discipline

Implementation Agentへ「良い感じに改善」「全部直す」などの無限定な依頼をしません。

変更対象と完了状態を、今回のtaskに必要な範囲で明示します。

Non-goals / prohibitionsは網羅的に列挙しません。今回のtaskから合理的に生じうるscope拡張や、過去に問題になった誤推測を防ぐために必要なものだけを書きます。

単に「今回は実施しない」という理由だけで、無関係な将来作業や別工程をTask Packetへ追加しません。

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

## 9. Work Package and Session Boundary

関連する調査、実装、確認、修正、test、commit、push、最終確認は、工程ごとに不要に分割せず、原則として1つの論理作業パッケージとして扱います。

独立したtask、大きなphase変更、Human Gate、前提の不一致、または安全に継続できない状態が生じた場合は分割して構いません。

ChatGPTやImplementation Agentのconversationが変わること自体は、Work Packageを分割する理由にしません。

再開時は過去の会話全文を再投入するのではなく、現在状態と残作業に必要な情報だけを引き継ぎます。
