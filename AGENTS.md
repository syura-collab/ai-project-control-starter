# Implementation Agent Boundary

`project-control` ブランチは、Human + ChatGPT がプロジェクト全体の目的・判断・現在地を保持するための **ChatGPT persistent brain** です。

Codex / Claude Code などのImplementation Agentは、通常作業でこのブランチを直接扱いません。

通常は禁止する操作:

- `project-control` ブランチの fetch / checkout / switch
- Project Control文書の read / search / crawl / index / summarize
- Project Controlの modify / commit / push
- Project Control全文をコンテキストとして要求すること

Implementation Agentは、ChatGPTがProject Controlとcommitted `main`から作成した **Task Packet** と、`main`上の実装事実だけを使って作業します。

Task Packetの前提と`main`の実装挙動が食い違う場合は、Project Controlを確認しに行かず、behavioral inconsistencyとして変更せず報告します。

Project Controlの更新・整理はChatGPTが行います。

この分離はcredential等を守るsecurity boundaryの代替ではありません。目的は、プロジェクト全体の解釈を複数Agentが重複して行うこと、作業範囲が不用意に広がること、不要なトークン消費、`main`の不要な変更を防ぐことです。
