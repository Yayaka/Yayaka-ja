# メッセージ

*メッセージ*は, 2つのサービス間でやり取りされるJSONデータです.  
2つのサービスが異なるホストならば, パケットによってやり取りされます.


## メッセージの種類

メッセージの種類には, 要求メッセージと応答メッセージの2種類があります.  
要求メッセージは基本的なメッセージタイプで, 応答メッセージは返信用のメッセージタイプです.


## 階層化されたメッセージのルーティング

各要求メッセージは, ルーティングのために**host**, **protocol**, **service**, **action**キーを持っています.  
それらは, 以下の手順で適切なメッセージハンドラに送られます.

1. コネクションは, 指定された**host**にメッセージを送信します.
2. **host**は, 指定された**protocol**にメッセージをルーティングします.
3. **protocol**は, 指定された**service**にメッセージをルーティングします.
4. **service**は, 指定された**action**をハンドルするためにハンドラにメッセージをルーティングします.

各応答メッセージは, ルーティングのために**host**, **reply_to**キーを持っています.  
それらは, 以下の手順で適切なメッセージ送信元に送信します.

1. コネクションは, 指定された**host**にメッセージを送信します.
2. **host**は, 指定された"ID"を持っているメッセージを送信元にルーティングします.


## 検証

メッセージルーティングの各層はメッセージが自分自身に宛てられているか調べるべきです(SHOULD).  
また, **host**, **protocol**, **service**, **action**のうち，一つ以上が不明な場合，いかなる時もメッセージを無視するかもしれません(MAY).


## タイムアウト

Yayakaプロトコルは, メッセージのタイムアウトについて指定しません.


## JSON形式

### 要求

要求メッセージは次のプロパティを持ちます.

#### プロパティ

- MUST **sender** object  
  オブジェクトは次のプロパティを持ちます.

  - MUST **host** string  
    送信元のホスト

  - SHOULD **protocol** string  
    送信元のプロトコル

  - SHOULD **service** string  
    送信元のサービス

- MUST **id** string  
  送信元のホスト内でユニークなID

- MUST **host** string  
  宛先のホスト

- MUST **protocol** string  
  宛先のプロトコル

- MUST **service** string  
  宛先のサービス

- MUST **action** string  
  メッセージの説明の為のテキスト

- MUST **payload** object  
  メッセージ本体

- SHOULD NOT 上記以外のプロパティ

#### 例

```json
{
  "sender": {
    "host": "host1.example.com",
    "protocol": "example",
    "service": "form"
  },
  "id": "0123456789",
  "host": "host2.example.com",
  "protocol": "example",
  "service": "repository",
  "action": "post example",
  "payload": {
    "text": "example text"
  }
}
```

### 応答

要求メッセージとの大きな違いは，応答メッセージは**reply_to**プロパティを持っていることと, **action**プロパティを持っていないことです.

返信メッセージの**sernder**プロパティにプロパティが含稀ている場合, 応答メッセージは**protocol**と**sercice**プロパティを持つべきです(SHOULD).

#### プロパティ

- MUST **sender** object  
  MUST, MAY, SHOULDオブジェクトは, 次のプロパティを持っています.

  - MUST **host** string  
    送信元のホスト

  - SHOULD **protocol** string  
    送信元のプロトコル

  - SHOULD **service** string  
    送信元のサービス

- MUST **id** string  
  送信元のホスト内でユニークなID

- MUST **reply-to** string  
  メッセージの返信用ID

- MUST **host** string  
  宛先のホスト

- MAY **protocol** string  
  宛先のプロトコル

- MAY **service** string  
  宛先のサービス

- MUST **payload** object  
  メッセージ本体

- SHOULD NOT 上記以外のプロパティ

#### 例

```json
{
  "sender": {
    "host": "host2.example.com",
    "protocol": "example",
    "service": "repository"
  },
  "id": "abcdefghij",
  "reply-to": "0123456789",
  "host": "host1.example.com",
  "protocol": "example",
  "service": "form",
  "payload": {
    "status": "ok"
  }
}
```
