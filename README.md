# Git & GitHub Memo

<details><summary>

## 最初にコミット・プッシュする時
</summary>

GitHubのリモートリポジトリにファイルをアップロードする方法  
リモートリポジトリ：GitHub上のリポジトリ  
ローカルリポジトリ：自分のパソコン上のリポジトリ  
1. Gitのインストール
    Windowsの場合[公式ページ](https://gitforwindows.org/)からインストール。  
    Macの場合は最初からインストールされている。  
    コマンドプロンプト/ターミナルから`git --version`でGitのバージョン情報が表示されることを確認。
    ```
    $ git --version
    $ git version 2.26.2.windows.1
    ```

2. Gitの初期設定
   * ユーザ名
   GitHubアカウントと同じユーザー名を登録
   ```
   $ git config --global user.name ユーザ名
   ```
   * メールアドレス
   GitHubアカウントと同じメールアドレスを登録
   ```
   $ git config --global user.email メールアドレス
   ```
    
3. リポジトリを作成
   GitHub上で好きな名前のリポジトリを作成  

4. クローン
   プロジェクトのフォルダを作りたいところ（プロジェクトのフォルダの一個上の階層)で以下を実行。
   ```
   git clone https://github.com/tokky1013/(プロジェクト名).git
   ```
   例）
   ```
   git clone https://github.com/tokky1013/cmd-maze.git
   ```

5. できたフォルダの中に移動
   例）
   ```
   cd cmd-maze
   ```

6. コミットするファイルの準備
   アップロードしたいファイル（ここではindex.htmlとする）をクローンしたフォルダ内に入れる。

7. インデックスにファイルを追加
   以下のコマンドでインデックスにファイルを追加する
   インデックスとは、コミット前に変更内容を一時的に保存する領域を指し、インデックスに追加されたファイルのみがコミットの対象となる。
   ```
   $ git add index.html
   ```
   `git add .`で全ファイルを指定。

8. 追加したファイルをコミット
   以下のコマンドを入力すると、インデックスに存在するファイルがローカルリポジトリへ追加される。コミットメッセージは変更内容を伝えるためのメッセージ。
   ```
   $ git commit -m "コミットメッセージ"
   ```
   コミットメッセージを含めた変更履歴（ログ）は、`git log`コマンドで確認
   ```
   $ git log
   commit 6a8e257...コミットハッシュ.....642e3 (HEAD -> master)
   Author: ユーザ名 <メールアドレス>
   Date:   Tue May 26 18:45:56 2020 +0900

        [Add] index
    ```

9.  ローカルリポジトリの変更内容をリモートリポジトリに反映  
    以下のコマンドでローカルリポジトリの変更内容をリモートリポジトリに反映させる。
    ```
    $ git push origin main
    ```

10. コンフリクトした時
    ```sh
    # ２つのブランチ間でコンフリクトしているファイル fileA.txt と fileB.txt があるとする

    # fileA.txt を現在チェックアウトしているブランチ側の対応に合わせる場合
    $ git checkout --ours fileA.txt
    $ git add fileA.txt    # add を忘れずに
    
    # fileB.txt をマージさせたブランチ側に合わせる場合
    $ git checkout --theirs fileB.txt
    $ git add fileB.txt
    
    $ git commit
    ```

#### 開発の流れ（ローカル）
複数人/複数デバイスで並行して開発する場合は最初に必ずプルする
`git pull origin main`  
↓  
（ブランチを作る場合）  
`git switch -c ブランチ名`  
↓  
ファイルを追加・編集  
↓  
`git add .`  
あるフォルダ内のファイルのみを追加する場合は  
`git add フォルダ名/.`  
↓  
`git commit -m "コミットメッセージ"`  
↓  
`git push origin main`  
（ブランチを作った場合はmainをブランチ名に変更）  
</details>
