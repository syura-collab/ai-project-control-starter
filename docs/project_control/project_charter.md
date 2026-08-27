# Project Charter

- status: canonical long-term charter

## Project Purpose

**Project:** `<PROJECT_NAME>`

**目的:**

<このプロジェクトは何を実現するために存在するか。>

**成功状態:**

<現実にどうなれば、このプロジェクトは成功と言えるか。>

## System / Product Boundary

<プロジェクトが責任を持つ範囲と、意図的に持たない範囲を書く。>

## Operating Principles

明示された制約とHuman Gateは守ります。ただし、プロジェクトを進める代わりに追加の承認層、基盤、将来向け抽象化を作って仕事を終えません。

過剰停止、過剰確認、過剰長文化、過剰先送りを避けます。合理的に進められる範囲は進め、人間判断が本当に必要な事項だけをまとめて確認します。

プロジェクトの成功条件まで進めます。「実現可能」「実装済み」「準備完了」を、検証済み・稼働済み・Goal達成と同一視しません。

Scopeは明示されたExit Conditionを満たしたときだけ閉じます。

AIの観察、分析、問題提起、代替案提示は制限しません。Human Gateが制限するのは、無断の意思決定・採用・外部実行です。

Project Controlの維持自体を本線にしません。長期記憶として必要な意味・判断だけを残します。

Project Controlは、Humanが手作業でMarkdownを保守するための仕組みではありません。Humanは記録すべき事実・判断・訂正・方針を指示・承認し、通常の文書更新はChatGPTが担当します。

## Human Authority

人間だけが決めること:

- <明示的な人間承認が必要な判断。>
- <不可逆、破壊的、外部影響、金銭、productionなどのプロジェクト固有境界。>

それ以外は、別のプロジェクトルールで禁止されていない限り、現在scope内で進めてよいものとします。

## Roles

### Human

- Goal、重要なtrade-off、Human Gateを所有する
- プロジェクト固有の不可逆・外部影響判断を行う
- Project Controlへ反映すべき事実・判断・訂正・方針を指示・承認する
- 通常はProject Control文書を直接編集しない

### ChatGPT

- プロジェクト全体理解、設計判断、次作業判断を担当する
- `project-control`とcommitted `main`から現在地を復元する
- Project Controlの通常のWriterとして、正本関係と現在地を保ちながら更新する
- Humanの指示・訂正・承認と確認済み事実をProject Controlへ反映する
- Implementation AgentへTask Packetを作成する

### Implementation Agents

- Task Packetに明示されたscope内で、`main`上の調査・実装・test・reviewを行う
- Project Controlを直接読まない・変更しない
- taskをプロジェクト全体の再設計へ拡張しない
- Task Packetと実装事実が食い違う場合は、勝手に前提を変更せず報告する

役割・ブランチ・コンテキスト境界の正本は`OPERATING_MODEL.md`とします。

## Project-Specific Constraints

- <プロジェクトの進め方へ長期的に影響する制約だけを書く。>

## Project-Specific Safety / Human Gates

- <外部write、production、金融、個人情報、破壊的操作などがある場合のみ具体化する。>
