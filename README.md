
# HBase Client Java API から TableStore を利用するサンプル


HBase Java Client sample using aliyun-tablestore-hbase-client

-----

## 事前準備

* TableStore のコンソール画面からリージョン選択後、Instance 作成
* 作成した Instance の詳細画面から Instance Access URL (Internet) を確認
* IntelliJ IDEA Community Edition インストール


## プログラム作成と実行

### Maven 設定

* IntelliJ IDEA | New Project | Maven | Create from archetype
* org.apache.maven.archetypes:maven-archetype-quickstart を選択
* GroupId: com.example, ArtifactId: hbase-app
* Next | Project name: hbase-app | Finish | Import Change
* (参考) コマンドプロンプトから作成する場合

```
brew install maven
mvn -B archetype:generate -DgroupId=com.example -DartifactId=hbase-app
#  以下のオプションはデフォルト値なので省略可能
#  -DarchetypeGroupId=org.apache.maven.archetypes
#  -DarchetypeArtifactId=maven-archetype-quickstart
cd hbase-app
mkdir src/main/resources
# 作成された hbase-app ディレクトリを IntelliJ IDEA から開く
```

* c.f. https://jp.alibabacloud.com/help/doc-detail/50163.htm
* 上記の `<dependency>` 部分を `pom.xml` の `<dependencies>` 内へコピー
* IDE の誘導に従って `Import Changes` をクリックし dependencies をインポート

### hbase-site.xml の設定

* `src/main/` に `resources` ディレクトリ作成
* c.f. https://github.com/aliyun/aliyun-tablestore-hbase-client/blob/master/src/test/resources/hbase-site.xml
* 上記をコピーして `hbase-site.xml` を `resources` 内に作成
* 空欄となっている `<value></value>` に Setup での設定事項等を適宜記入
  - endpoint: https://tablestoreinst.ap-southeast-1.ots.aliyuncs.com
  - instancename: Setup で作成したインスタンス名
  - accesskeyid, accesskeysecret も記入

### Java ソースの設定

* c.f. https://github.com/aliyun/aliyun-tablestore-hbase-client/blob/master/src/test/java/samples/HelloWorld.java
* import 文と `HelloWorld` class の内容を `App` class 内へコピー
* `TABLE_NAME` を `Hello-Tablestore` から `HelloTablestore` に変更
* `COLUMN_FAMILY_NAME` が空なので `f1` と記入 (注: `hbase-site.xml` の設定と一致)
* App を右クリック、`Run` を選択して実行

```
Create table HelloTablestore
Write one row to the table
Get a one row by row key
  row_1 = col_value
Scan for all rows:
  col_value
Delete the table
```


## 参照

* http://hbase.apache.org/book.html
* https://github.com/aliyun/aliyun-tablestore-hbase-client
