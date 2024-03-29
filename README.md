# backup
ファイルバックアップシステム

## 環境設定(Mac)

go のインストール
```
$ brew install go
```

Path の設定
```
$ mkdir $HOME/go
$ echo 'export GOPATH=$(go env GOPATH)' >> ~/.bash_profile
$ echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> ~/.bash_profile
$ source ~/.bash_profile
```

clone
```
$ mkdir $HOME/go/src
$ cd $HOME/go/src
$ git clone github.com/fumihirokinoshita/backup
```

ライブラリのインストール
```
$ go get github.com/matryer/filedb
```

## 概要

backup
- add: バックアップするフォルダを指定
- list: 指定してるフォルダのリストを確認
- remove: 指定しているフォルダの削除

backupd
```
$ $home/go/src/backupd/cmds/backupd
```
下で同じフォルダ名のディレクトリを作成し, 実行することで自動backup  
バックアップデータはarchive内にzip形式で保存される

### 実行の流れ
```
$ $home/go/src/backup/cmds/backup
$ go build -o backup
$ backup -db=./backupdata add ./フォルダ名
$ backup -db=./backupdata list
$ backup -db=./backupdata remove ./フォルダ名

$ $home/go/src/backupd/cmds/backupd
$ go build -o backupd
$ mkdir フォルダ名
$ ./backupd -db="../backup/backupdata/" -archive="./archive" -interval=検知時間
```