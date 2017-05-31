# Yayakaプロトコル

[Yayaka Protocol (en)](https://github.com/Yayaka/Yayaka)の[9b05ded](https://github.com/Yayaka/Yayaka/tree/9b05ded5d80ae87ada892dee13ace3b98b0c24d6)までを訳しています.

Yayakaプロトコルは, 高度に分散化された, Webアプリケーションの為のプロトコルです.  
それぞれのインスタンスは, 分散化されたWebアプリケーションのすべての機能を実装する必要はありません.

Yayakaプロトコルは, [HVDSGM (ja)](https://hakabahitoyo.wordpress.com/2017/05/22/hvdsgm/)の影響を受けています.

現在, Yayakaプロトコルは不完全であり, リリースされていません.


## 特徴

- 軽量な仕様
- レイヤーや再帰的なプロトコルの拡張性
- JSON


## 構想

### Yayakaサービス

Yayakaプロトコルは, いくつかのYayakaサービスを持っています.  
Yayakaサービスは特別ではありません. しかし, それらは通常一つのWebサービスとして一体化しています.  
Yayakaプロトコルは, それらを複数のホストに分散させることが出来ます.  


### 階層化されたサブプロトコル

階層化されたサブプロトコルにより, 2つの異なるホスト間や異なるYayakaサービス間で通信する方法, イベントの種類, コンテンツの種類を作成出来ます.


## 仕様

- [Yayakaプロトコル 仕様書](specification/index.md)


## 実装

Yayakaプロトコルは, まだ実装されていませんが, [Yayaka.net](https://yayaka.net)はYayakaプロトコルを導入する予定です.

## 貢献

Yayaka-jaへの[貢献](CONTRIBUTING.md)は, こちらをご覧ください.

## ライセンス

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="クリエイティブ・コモンズ・ライセンス" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />この 作品 は <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">クリエイティブ・コモンズ 表示 - 継承 4.0 国際 ライセンス</a>の下に提供されています。
