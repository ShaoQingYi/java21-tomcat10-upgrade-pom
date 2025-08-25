# inheritanceTrustEuc-upgrade-pom

[![Java](https://img.shields.io/badge/Java-21-blue.svg)](https://openjdk.org/projects/jdk/21/)
[![Maven](https://img.shields.io/badge/Maven-3.9.11-brightgreen.svg)](https://maven.apache.org/)

## 概要
本リポジトリは、**Java 8 → 21、Tomcat 9 → 10、5.7.1.SP1.RELEASE → 5.10.0.RELEASE** への  
アップグレードに必要な **Maven POM プロジェクト** です。  
外部ネットワーク環境で依存関係・プラグインを一括ダウンロード（go-offline）し、  
内部環境に持ち込むことを目的としています。

---

## 前提条件
- **Java 21** (例: 21.0.8)  
- **Apache Maven 3.9.11**  
- インターネットアクセス可能な環境

---

## 手順（外部環境）

1. GitHub から本リポジトリを ZIP 形式でダウンロードし、下記のパスに解凍します。
   ```bash
   例：C:\Maven\inheritanceTrustEuc

2. Maven の設定ファイル `settings.xml` の編集

   2.1 **Jaspersoft 依存ライブラリを取得するためのリポジトリ定義** を追加します。
   
   2.2 **ダウンロード先のローカルリポジトリの指定** を追加します。
   
   ※ `settings.xml` ファイルは、Maven をインストールしたディレクトリの `conf` フォルダ内に配置されています。
   ```xml
   <settings>
    ...
      
    <localRepository>C:\Maven\repo</localRepository>
   
    <mirrors>
      <mirror>
        <id>jaspersoft-third-party-https</id>
        <name>Jaspersoft third-party (HTTPS)</name>
        <url>https://jaspersoft.jfrog.io/artifactory/third-party-ce-artifacts/</url>
        <mirrorOf>jaspersoft-third-party</mirrorOf>
      </mirror>
      <mirror>
        <id>jr-ce-releases-https</id>
        <name>Jaspersoft CE releases (HTTPS)</name>
        <url>https://jaspersoft.jfrog.io/artifactory/jr-ce-releases/</url>
        <mirrorOf>jr-ce-releases</mirrorOf>
      </mirror>
      <mirror>
        <id>jr-ce-snapshots-https</id>
        <name>Jaspersoft CE snapshots (HTTPS)</name>
        <url>https://jaspersoft.jfrog.io/artifactory/jr-ce-snapshots/</url>
        <mirrorOf>jr-ce-snapshots</mirrorOf>
      </mirror>
    </mirrors>
    ...
   </settings>

   ```
   上記の例では、後でダウンロードした依存ライブラリは全部 C:\Maven\repo に保存されます。
   パスは任意で変更可能です。
3. コマンドプロンプトを起動し、解凍したプロジェクトフォルダに移動します。
   <img width="806" height="406" alt="image" src="https://github.com/user-attachments/assets/36940f58-ca7c-47dc-ac42-af35463c3427" />
   
   <img width="1103" height="257" alt="image" src="https://github.com/user-attachments/assets/3f05b3fc-0898-40ed-ab01-4a0c8b9d1f3c" />
4. Maven コマンドの実行

   4.1 以下のコマンドを実行します。
   
   ※これにより、必要な依存ライブラリおよびビルド用プラグインがすべてローカルリポジトリにダウンロードされます。

   ```bash
   mvn -U -DresolvePlugins=true dependency:go-offline

   ```
   -U ：
   依存関係のメタデータを強制的に最新化します。

   -DresolvePlugins=true ：
   ビルドに必要な Maven プラグインも合わせてダウンロードします。

   dependency:go-offline ：
   プロジェクトで使用するすべての依存ライブラリとプラグインを取得します。

   <img width="1104" height="320" alt="image" src="https://github.com/user-attachments/assets/00025b12-f995-497f-a4f0-1c6f181d6bfd" />

   4.2 実行中の画面（依存関係やプラグインを順次ダウンロードされます）
   
   <img width="1105" height="610" alt="image" src="https://github.com/user-attachments/assets/bbc81137-76a8-4f90-b794-ecb5571c708d" />

   4.3 実行完了（BUILD SUCCESS）
   
   すべての依存関係が正常に取得されると`BUILD SUCCESS`が表示されます。
   
   <img width="1097" height="586" alt="image" src="https://github.com/user-attachments/assets/35d28f9d-5059-45ff-8e44-f1a4035bb3f3" />

5. ローカルリポジトリの持ち込み

   ローカルリポジトリのフォルダをZIP形式で圧縮し、内部環境に持ち込みます。

   <img width="851" height="249" alt="image" src="https://github.com/user-attachments/assets/946185eb-fc97-49f9-9da9-f82cf23f77aa" />

   <img width="792" height="726" alt="image" src="https://github.com/user-attachments/assets/f8e779ef-97d3-419d-9fd5-37110d704938" />






