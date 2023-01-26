---
title: "【Laravel】AccessorでEloquent属性値を変換して処理を共通化する"
emoji: "🌟"
type: "tech"
topics:
  - "laravel"
published: true
published_at: "2022-02-07 03:06"
---

# 概要

`Eloquent Model` から取得したIDをハッシュ化する処理を`Accessor`を利用して行ってみましたので紹介します

> アクセサは、Eloquentの属性値にアクセスしたときに、その値を変換するものです。アクセサを定義するには、モデルにget{Attribute}Attributeメソッドを作成します。

https://laravel.com/docs/8.x/eloquent-mutators#attribute-casting

# `Accessor` の定義

- `{カラムのアッパーキャメルケース}Attribute` の形式でメソッドを命名する
    - 今回は`hash_id`にハッシュ化したIDを格納しますので`HashId`としています

```php:User.php
/**
 * Attributeにhash_id属性を生成するアクセサ
　　* @return string
*/
public function getHashIdAttribute()
 {
   return urlencode(Hash::make($this->id));
 }
```

```php
$user = User::query()->findOrFail(1);

// Accessorで変換されたカラム名にアクセスするとハッシュ化した値を取得できます
dd(user->hash_id);
```

# さいごに
今回は`Accessor`の仕組みについて紹介しました。
いいねしていただけると記事執筆の励みになりますので、参考になったと思った方は是非よろしくお願いします！
