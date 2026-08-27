# Security Policy

このスターターは、プロジェクトの長期コンテキストとImplementation Agentの作業コンテキストを分離するための運用テンプレートです。

## 作業用リポジトリはPrivateで作成する

このスターターから作る作業用リポジトリは **Private** を前提とします。

GitHubの公開範囲はブランチ単位ではなくリポジトリ単位です。リポジトリをPublicにすると、`main`だけでなく、プロジェクトの目的・現在地・重要な判断・再開地点などを保持する **`project-control` ブランチも公開されます。**

アプリ、ライブラリ、Webサイト、ドキュメントなどの成果物をPublicで公開する場合は、**公開用リポジトリを別に作成し、公開してよい成果物だけをそちらへ配置してください。** 作業用リポジトリそのものをPublicへ変更しないことを、このスターターの標準運用とします。

## 秘密情報をcommitしない

Privateリポジトリであっても、次のような情報をrepositoryへcommitしないでください。

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
