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
    ```bash
    $ git --version
    git version 2.26.2.windows.1
    ```

2. Gitの初期設定  
    * ユーザ名
    GitHubアカウントと同じユーザー名を登録
    ```bash
    $ git config --global user.name ユーザ名
    ```
    * メールアドレス
    GitHubアカウントと同じメールアドレスを登録
    ```bash
    $ git config --global user.email メールアドレス
    ```
    
3. リポジトリを作成  
    GitHub上で好きな名前のリポジトリを作成する。  

4. クローン  
    プロジェクトのフォルダを作りたいところ（プロジェクトのフォルダの一個上の階層)で以下を実行。
    ```bash
    git clone https://github.com/tokky1013/(プロジェクト名).git
    ```
    例）
    ```bash
    git clone https://github.com/tokky1013/cmd-maze.git
    ```

5. できたフォルダの中に移動  
    例）
    ```bash
    cd cmd-maze
    ```

6. コミットするファイルの準備  
    アップロードしたいファイル（ここではindex.htmlとする）をクローンしたフォルダ内に入れる。

7. インデックスにファイルを追加  
    以下のコマンドでインデックスにファイルを追加する。  
    インデックスとは、コミット前に変更内容を一時的に保存する領域を指し、インデックスに追加されたファイルのみがコミットの対象となる。
    ```bash
    $ git add index.html
    ```
    `git add .`で全ファイルを指定。

8. 追加したファイルをコミット  
    以下のコマンドを入力すると、インデックスに存在するファイルがローカルリポジトリへ追加される。  
    コミットメッセージは変更内容を伝えるためのメッセージ。
    ```bash
    $ git commit -m "コミットメッセージ"
    ```
    コミットメッセージを含めた変更履歴（ログ）は、`git log`コマンドで確認できる。  
    ```bash
    $ git log
    commit 6a8e257...コミットハッシュ.....642e3 (HEAD -> master)
    Author: ユーザ名 <メールアドレス>
    Date:   Tue May 26 18:45:56 2020 +0900

        [Add] index
    ```

9. ローカルリポジトリの変更内容をリモートリポジトリに反映  
    以下のコマンドでローカルリポジトリの変更内容をリモートリポジトリに反映させる。
    ```bash
    $ git push origin main
    ```

10. コンフリクトした時  
    ```bash
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
複数人/複数デバイスで並行して開発する場合は最初に必ずプルする。  
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

<details><summary>

## Git 基本コマンドまとめ（ChatGPTで生成）
</summary>

### 初期設定（最初に一度だけ）
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
```

---

### リポジトリの作成・取得
- 新しいリポジトリを作成  
```bash
git init
```

- 既存リポジトリをクローン  
```bash
git clone https://github.com/username/repo.git
```

---

### ステージング & コミット
- ファイルをステージング  
```bash
git add ファイル名
```

- すべての変更をステージング  
```bash
git add .
```

- コミット  
```bash
git commit -m "メッセージ"
```

---

### 状態の確認
- 作業ツリーとステージの状態を確認  
```bash
git status
```

- コミット履歴を見る  
```bash
git log
```

- 1行で履歴を見る  
```bash
git log --oneline
```

---

### リモートリポジトリ操作
- リモート追加  
```bash
git remote add origin https://github.com/username/repo.git
```

- リモート確認  
```bash
git remote -v
```

- リモートへ push（初回）  
```bash
git push -u origin main
```

- リモートへ push（2回目以降）  
```bash
git push
```

- リモートから pull  
```bash
git pull
```

---

### ブランチ操作
- ブランチ一覧  
```bash
git branch
```

- 新しいブランチを作成  
```bash
git branch ブランチ名
```

- ブランチを切り替え  
```bash
git checkout ブランチ名
```

- ブランチ作成＆切り替え（まとめて）  
```bash
git checkout -b ブランチ名
```

- ブランチをマージ  
```bash
git merge ブランチ名
```

---

### 変更の取り消し
- ステージから外す  
```bash
git reset HEAD ファイル名
```

- 変更を破棄（最新版に戻す）  
```bash
git checkout -- ファイル名
```

---

### よく使う便利コマンド
- 差分を確認  
```bash
git diff
```

- 最新のコミットに上書き（直前の修正）  
```bash
git commit --amend
```

- 履歴付きでファイルを削除  
```bash
git rm ファイル名
```

- ファイル名を変更  
```bash
git mv 古い名前 新しい名前
```

---

### よく使う流れ（例）
```bash
git add .
git commit -m "作業内容"
git push
```


</details>
