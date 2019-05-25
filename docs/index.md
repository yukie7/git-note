---
title: git-note
---

# git-note
## 目次
1. [GitHubで他人のリポジトリをForkする](#GitHubで他人のリポジトリをForkする)
2. [ブランチ関連コマンド](#ブランチ関連コマンド)
3. [Githubリポジトリを新規作成](#Githubリポジトリを新規作成)
4. [直前にpushしたコミットの取り消し方法](#直前にpushしたコミットの取り消し方法)

## GitHubで他人のリポジトリをForkする

1. GitHubは自分のリポジトリに他の人のリポジトリを複製することが作成可能
2. Forkはブラウザ上で他人のリポジトリのページから行う
  - Fork、Pull requestはGitではなくGitHubの機能であるため

3. 自分のローカルにマージしたい先のURLをupstreamを紐づける
  - upstreamの部分は任意の文字列

```$ git remote add upstream https://github.com/ogyogy/heroku-hanson.git```

4. upstreamの変更履歴をリモートリポジトリから取得

```$ git fetch upstream```

5. ローカルブランチにupstream/masterをマージして4.で取得した変更を反映

```$ git merge upstream/master```

6. ローカルブランチで変更を行った場合git pushでリモートリポジトリに反映

```$ git push```

## ブランチ関連コマンド
### ブランチの確認

```$ git [option] branch```

- [option]は-a（ローカルリポジトリとリモートリポジトリ全てのブランチを表示）または-r（リモートリポジトリ全てのブランチを表示）
- [option]の指定がない場合はローカルリポジトリ全てのブランチを表示

### ブランチの作成と切り替え

1. ブランチの作成
  - BNは作成したいブランチの名前に読み替える

```$ git branch BN```

2. ブランチの切り替え

```$ git checkout BN```

3. 1.と2.一度に実行するには以下のコマンドを入力

```$ git checkout -b BN```

4. 作成したブランチをリモートリポジトリに反映させるためにはpush

```$ git push origin BN```

### リモートブランチから情報を取得しローカルブランチを作成し切り替え

1. リモートリポジトリをcloneしたとき次の状態であるとする

```
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/develop
```

2. この時origin/developブランチの情報を持ったdevelopブランチをローカルに作成して切り替えるには以下のコマンドを入力

```
$ git checkout -b develop /origin/develop
```

## Githubリポジトリを新規作成

1. ブラウザ上でGithubリポジトリを新規作成
2. 作成後、以下のコマンドを入力してローカル環境にリポジトリをclone
  - new-repoは作成したリポジトリ名に読み替える

```
$ mkdir new-repo
$ cd new-repo
$ echo "# new-repo" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin https://github.com/yukie7/new-repo.git
$ git push -u origin master
```

## 直前にpushしたコミットの取り消し方法
### 方法1 pushしたコミットを削除

- コミットをなかったことにして履歴を削除するのでリモートリポジトリを共有しているときは要注意
  - resetの取り消しはできない
  - 削除したコミットで作業している人がいるとき余計な作業が発生する可能性がある
- 履歴をきれいに残すことができる

1. 直前のコミットを削除

```$ git reset --hard HEAD^```

2. 強制的にpushする
  - 履歴を巻き戻すようなpushはエラーになるので-fオプションで強制

```$ git push -f origin master```

### 方法2 変更を打ち消す新しいコミットを作成

- リモートリポジトリを共有しているとき比較的安全
  - 間違えたコミットと新しいコミットの履歴が残る
  - 乱用すると履歴が煩雑になりやすい

1. 直前のコミットを打ち消す新しいコミットを作成

```$ git revert```

2. pushする
  - 新しいコミットなので-fオプションは不要

```$ git push origin master```

## rebase -i でコミットをまとめる
- [rebase -i でコミットをまとめる](https://backlog.com/ja/git-tutorial/stepup/stepup7_5.html)を参照
