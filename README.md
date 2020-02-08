# 使い方


## 新しくReactアプリを作成する場合

既にサンプルのhello-worldアプリが作成されているのでこれを削除し、以下のコマンドでcreate-react-appを実行する。

```
docker-compose run --rm node sh -c "create-react-app my-app"
# my-appを自分のアプリ名に変える
```

docker-compose.ymlのenvironmentのREACT_APP_NAMEを自分のアプリ名に変更


```
version: "3"
services:
  node:
    build:
      context: ./app
    environment:
      - NODE_ENV=production
      - REACT_APP_NAME=my-app # ここのmy-appを修正
    volumes:
      - ./app:/usr/src/app
    ports:
      - "3000:3000"
```

## アプリケーションの開発を行う

- 開発サーバーを立ち上げる

```
docker-compose run --rm --service-ports node ash -c "cd \$REACT_APP_NAME; yarn start"
```

- コードを修正する

この状態でホストマシン上で'app/my-app'内を修正すればビルドされます。

- パッケージを追加する

```
docker-compose run --rm  --service-ports node ash -c "cd \$REACT_APP_NAME; yarn add package-name"
```
