# rails-graphql

📕📕📕 Ruby on RailsでGraphQLを使うためのサンプルプロジェクト！  

## 実行方法

```shell
docker compose up --build -d
docker compose run --rm app bundle exec rails db:migrate
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

# アイテムを更新
mutation {
  updateItem(input: {
    id: 1
    name: "Updated 🎉🎉🎉"
    price: 12345
  }) {
    item {
      id
      name
      price
    }
    errors
  }
}

# アイテムを削除
mutation {
  deleteItem(input: {
    id: 1
  }) {
    item {
      id
    }
    errors
  }
}
```

## おおさわメモ (手順)

### 1. Railsのプロジェクトを作成

```shell
burails new . --api
```

その後、生成されたDockerファイル書き換える。  
※ 当プロジェクトのDockerfileを参照。  
※ 開発用に動かすため。  

### 2. 必要なGemをインストール

```Gemfile
gem 'graphql'
gem "propshaft", "~> 1.1" # APIモードでは必須
```

```shell
bundle install
bundle exec rails generate graphql:install
```

### 3. GraphiQLをインストール

```shell
group :development, :test do
  gem 'graphiql-rails'
end
```

`./config/routes.rb`に以下の行を追加。  

```ruby
  if Rails.env.development?
    mount GraphiQL::Rails::Engine, at: "/graphiql", graphql_path: "/graphql"
  end
```
