# rails-graphql

📕📕📕 Ruby on RailsでGraphQLを使うためのサンプルプロジェクト！  

## 実行方法

```shell
docker compose up --build -d
```

## クエリの実行

`http://localhost:3000/graphiql`にアクセスして、以下のクエリを実行してください。  

```graphql
# 全てのアイテムを取得
query {
  items {
    id
    name
  }
}

# 指定したIDのアイテムを取得
query {
  item(id: 1) {
    id
    name
    description
    price
  }
}

# アイテムを作成
mutation {
  createItem(input: {
    name: "New Item ⭐️⭐️⭐️"
    description: "Hello, GraphQL!!!"
    price: 1000
  }) {
    item {
      id
      name
      description
      price
    }
    errors
  }
}
```

