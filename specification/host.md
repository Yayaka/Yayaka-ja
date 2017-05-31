# ホスト

## ホスト情報

*ホスト情報* は, ホストの詳細な指定が行われているJSONデータです.

### [WIP] エンドポイント

"/.well-known/yayaka"のパスで提供される可能性があります.

### JSON形式

パケットは, 次のプロパティを持つオブジェクトです.


- MUST **yayaka-version** semver  
  Yayakaプロトコルのバージョン

- MUST **host-version** semver  
  ホストの仕様のバージョン

- MUST **connection-protocols** array  
  次のプロパティを持つオブジェクトの配列  
  異なるバージョンの同じ通信プロトコルは許可されます.

  - MUST **name** string  
    通信プロトコル名

  - MUST **version** semver  
    コネクションプロトコルのバージョン

  - MAY **parameters** object  
    コネクションプロトコルの引数

- MUST **message-protocols** array  
  次のプロパティを持つオブジェクトの配列  
  異なるバージョンの同じメッセージプロトコルは許可されます.

  - MUST **name** string  
    通信プロトコル名

  - MUST **version** semver  
    メッセージプロトコルのバージョン

  - MUST **services** array  
    ホスト内で提供されているサービスの配列

  - SHOULD **parameters** object  
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
