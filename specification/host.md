# ホスト

## ホスト情報

*ホスト情報* は, ホストの詳細な指定が行われているJSONデータです.

### [WIP] エンドポイント

"/.well-known/yayaka"のパスで提供されるかもしれません.

### JSON形式

パケットは, 次のプロパティを持つオブジェクトです.


- 必須 **yayaka-version** semver  
  Yayakaプロトコルのバージョン

- 必須 **host-version** semver  
  ホストの仕様のバージョン

- 必須 **connection-protocols** array
  次のプロパティを持つオブジェクトの配列  
  異なるバージョンの同じ通信プロトコルは許可されます.

  - 必須 **version** semver  
    コネクションプロトコルのバージョン

  - 任意 **parameters** object  
    コネクションプロトコルの引数

- 必須 **message-protocols** array  
  次のプロパティを持つオブジェクトの配列  
  異なるバージョンの同じメッセージプロトコルは許可されます.

  - 必須 **name** string
    通信プロトコル名

  - 必須 **version** semver  
    メッセージプロトコルのバージョン

  - 必須 **services** array  
    ホスト内で提供されているサービスの配列

  - 任意 **parameters** object  
    メッセージプロトコルの引数

### 例

```json
{
  "yayaka-version": "1.0.0",
  "host-version": "1.0.0",
  "connection-protocols": [
    {
      "name": "https-jwt",
      "version": "1.0.0",
      "parameters": {
        "connect-path": "/connect",
        "authenticate-path": "/authenticate"
      }
    },
    {
      "name": "phoenix-channel",
      "version": "1.0.0",
      "parameters": {
        "websocket-path": "/socket/websocket",
        "topic-template": "remotes:{{host}}"
      }
    }
  ],
  "message-protocols": [
    {
      "name": "yayaka",
      "version": "1.0.0",
      "services": ["identity", "repository", "social-graph"],
      "parameters": {
        "presentation-protocols": {
          "github-flavored-markdown": {
            "version": "1.0.0"
          }
        }
      }
    },
    {
      "name": "status",
      "version": "1.0.0",
      "services": ["monitor"]
    }
  ]
}
```
