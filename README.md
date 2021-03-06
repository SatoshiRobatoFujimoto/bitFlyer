# bitFlyer

株式会社bitFlyer様が提供している、bitFlyer Lightning APIのSDKをGoで実装してみました。

[APIマニュアル](https://lightning.bitflyer.jp/docs)

APIは、PublicとPraivateの2種類あります。

Private APIを利用する場合は、ご自身のAPI KeyとSecretが必要です。

そのため、事前にbitFlyerでアカウントを作成しておく必要があります。



## Go version

Go 1.5

## Installation

```go
go get github.com/pokochi/bitFlyer
```

## Operating instructions

APIのメソッドは、リクエストの頭文字を大文字にしたキャメル表記です。

例：[API キーの権限を取得](https://lightning.bitflyer.jp/docs#api-キーの権限を取得)

リクエストが/v1/me/getpermissionsなので、GetPermissions()を実行します。

* Require
```go
import "github.com/pokochi/bitFlyer"
```

* Public API

```go
//引数なし
b := bitFlyer.PublicApi{}
err, s := b.GetHealth()

//引数あり
b := bitFlyer.PublicApi{}
m := make(map[string]string)
m["product_code"] = "BTC_JPY"

err, s := b.GetBoard(m)
```

* Private API

```go
//引数なし
b := bitFlyer.NewPermissions("Your API KEY", "Your API SECRET")
err, s := b.GetPermissions()

//引数あり
b := bitFlyer.NewTrade("Your API KEY", "Your API SECRET")
m := make(map[string]string)
m["product_code"]     = "BTC_JPY"
m["child_order_type"] = "MARKET"
m["side"]             = "BUY"
m["size"]             = "0.01"
m["minute_to_expire"] = "10"

err, s := b.SendChildOrder(m)
```

## Todo

* [新規の親注文を出す（特殊注文）](https://lightning.bitflyer.jp/docs#新規の親注文を出す特殊注文)の実装。
* テストケース
* エラー処理のリファクタ

## License

MIT
