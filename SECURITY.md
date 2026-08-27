# Security Policy

このスターターは、プロジェクトの長期コンテキストとImplementation Agentの作業コンテキストを分離するための運用テンプレートです。

## 秘密情報をcommitしない

次のような情報をrepositoryへcommitしないでください。

- API key / access token
- password
- session cookie
- private key
- `.env` などの秘密設定
- 実データを含むdatabaseやraw export
- 不要な個人情報や機密情報

秘密情報はGitHub Secrets、環境変数、password managerなど、用途に合った仕組みへ分離してください。

## `project-control` はsecurity boundaryではない

`project-control` ブランチをImplementation Agentから通常分離しているのは、長期文脈の混入、不要な作業範囲の拡張、トークン消費を抑えるためです。

秘密情報を保存してよい場所という意味ではありません。

## 誤って秘密情報をcommitした場合

公開issueへ秘密情報を貼らないでください。

秘密情報を誤ってcommitした場合は、単に削除commitを追加するだけでは不十分です。該当するcredentialを失効・再発行し、必要に応じてGit historyからも除去してください。
