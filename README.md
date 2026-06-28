# altstore-source

AltStore ClassicとSideStore向けの公開配布Repo。

アプリのソースコードは置かない。
公開用のアプリ定義、画像、IPA Releaseだけを管理する。

## Source URL

SideStoreとAltStore Classicには次のURLを登録する。

`https://altstore.xnunux.com/source.json`

## ディレクトリ構成

```text
catalog.json              # Source全体とアプリ一覧
apps/
└── <appID>/
    ├── app.json          # アプリの固定メタデータ
    └── icon.png          # 公開用アイコン
```

GitHub Releaseのタグは`<appID>-v<version>`形式にする。
各ReleaseにはIPA、`release-metadata.json`、`SHA256SUMS`を添付する。

## NarouReader

NarouReaderのIPAはprivate RepoのGitHub Actionsでビルドする。
Actionはad-hoc署名とentitlementを検証し、このRepoにDraft Releaseを作成する。
すべてのアセットを添付できた場合だけReleaseを公開する。

公開済みReleaseのアセットは同じタグのまま差し替えない。
更新時は新しいバージョンのReleaseを作成する。

## 開発支援（NarouReader）

NarouReader は無償で配布しており、機能制限や課金要素はありません。

もしこのアプリを気に入っていただけたら、開発者にコーヒーの一杯でもいただけると嬉しいです。
もちろん任意です。支援していただかなくても、アプリの機能や表示は一切変わりません。

- Buy Me a Coffee で支援する: https://buymeacoffee.com/nunu1733

このリンクは外部サイト（Buy Me a Coffee）へ移動します。
リンク先のページで「nunu1733」が NarouReader の開発者として支援先になっていることを確認できます。

## アプリの追加

新しい`appID`を決め、`apps/<appID>/app.json`と公開用アイコンを追加する。
`catalog.json`にも同じ`appID`とmanifestのパスを追加する。

アプリ側のRelease Workflowは、Releaseメタデータへ同じ`appID`を出力する。
Source Workerは`appID`ごとにReleaseを集約し、一つのSource JSONへ複数アプリを掲載する。
