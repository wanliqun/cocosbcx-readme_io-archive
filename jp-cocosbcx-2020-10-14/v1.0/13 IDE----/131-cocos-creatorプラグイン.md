---
title: "13.1 Cocos Creatorプラグイン"
slug: "131-cocos-creatorプラグイン"
hidden: false
createdAt: "2019-10-03T09:18:45.101Z"
updatedAt: "2019-10-03T09:24:50.727Z"
---
[block:api-header]
{
  "title": "Cocos Creatorについて"
}
[/block]
[Cocos Creator](https://www.cocos.com/en/creator)はCocos2d-xをベースして、スクリプト化・コンポーネント型・データ駆動のコンテンツ作成をメインにしているゲーム開発ツールです。

[Cocos Creator](https://www.cocos.com/en/creator)はオープンソースフレームワークのCocos2d-xを基づき、一体化され（All-in-one）、拡張可能、カスタム可能なワークフローエディターです。それから、Cocos CreatorはCocosシリーズで初めてコンポーネントプログラミングデザインとデータ駆動によるデザインを導入し、Cocos2d-xのワークフローでのシーンエディット、UIデザイン、リソース管理、ゲームデバッグ、レビュー、マルチプラットフォームでのリリースなどのプロセスを簡潔しました。
[block:api-header]
{
  "title": "システム構造"
}
[/block]
このプラグインはCocos-BCXのGitHubでオープンソースされていて、アドレスはCocos-BCX For Cocos Creatorです。[BCX For Cocos Creator](https://github.com/CocosBCX/bcx-sdk-creator)プラインとCocos CreatorでBCXとコネクトするSample　プロジェクトが確認できます。
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/12271c7-image001.png",
        "image001.png",
        294,
        254,
        "#3f2f30"
      ]
    }
  ]
}
[/block]
bcx：BCX For Cocos Creatorのプラグインパッケージです（このフォルダを直接packagesにインストールしてから利用可能になります）

Sample：Sampleプロジェクトで、BCXのコール方に関する情報が入っています。
[block:api-header]
{
  "title": "対応"
}
[/block]
Cocos Creator　2.0+
[block:api-header]
{
  "title": "プラグインのインストール"
}
[/block]
・bcxフォルダをCreator内のpackagesにインストールします
	・インストールが完了したら、Creatorのメニューから図のメニューが見られます
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f7db390-image002.jpg",
        "image002.jpg",
        279,
        110,
        "#798391"
      ]
    }
  ]
}
[/block]
・インストールをクリックし、assetsディレクトリ内でbcxファイルが自動作成されます
・プロジェクトを再起動し、assetsからbcxファイルが確認できます
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fe9be7e-image003.png",
        "image003.png",
        414,
        658,
        "#38383a"
      ]
    }
  ]
}
[/block]
・そして、コードでbcxのインターフェイスがコールできるようになります。
[block:api-header]
{
  "title": "Sampleについて"
}
[/block]
・Macを利用している場合、Cocos Creator 2.0+で直接sample/bcx-creatorを起動し、sampleを実行できます
・Windowsを利用している場合、sample/bcx-creator/packages/bcxを削除してから、ルートディレクトリ内のbcxファイルをsample/bcx-creator/packages/にコピーしてください。そして、Cocos Creator 2.0+で開き、実行します。
[block:api-header]
{
  "title": "対応"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0dacfb6-image005.png",
        "image005.png",
        688,
        97,
        "#f7f7f7"
      ]
    }
  ]
}
[/block]
図で示した通り、BCX For Cocos Creator 0.0.1はBCX JS SDK 1.3.0.2をベースにしています。