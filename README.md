# git-note
// 自分のローカルにマージしたい先のURLをupstreamを紐づける（名前はなんでもい良い）
git remote add upstream https://github.com/ogyogy/heroku-hanson.git

// upstreamの変更履歴をとってくる
git fetch upstream

// 自分のブランチにupstream/masterをマージする
git merge upstream/master

// git pushで反映
git push

[]
// 他の人のリポジトリをfork
自分の中に新たなリポジトリが作成可能

// 自分のローカルに適当なデレク鳥を生成
mkdir line-bot-weather

// cd
cd line-bot...

// git clone 自分のリポジトリ

git checkout -b develop

git branch

git push origin develop



echo "# git-note" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/yukie7/git-note.git
git push -u origin master
