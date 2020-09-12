# 基本的なLAMP環境でPHPの開発ができるDocker環境

### Dockerによって構築されるLAMPの環境には下記のものがある
* centos
* apache
* mysql
* phpmyadmin
* php


### 使い方
cloneしてきたdocker_compose_lampに移動して下記の手順でdockerを立ち上げる
```
docker-compose build
docker-compose up -d
docker-compose exec web bash
```
これで開発の準備は終わり！次のアドレスにアクセスすると/html/においたphpが確認できる→http://localhost<br>
phpmyadminは次のでアクセス可能→http://localhost:8903/

下記のディレクトリーにsqlファイルを置いておいたらimage起動時にデータの初期化ができる。
./db/mysql_init/