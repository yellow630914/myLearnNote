# Git指令

## 前置
​		git config --global user.name "USERNAME"  //創建全域使用者
​		git config --global user.name "USERNAME"  //創建全域電郵
​		git config --list //查看配置

## git指令
​		git init //創建git本地倉庫
​		git status //查看目前倉庫狀態
​		git ls-files //查看git本地倉庫中的檔案目錄
​		git add docsname.xxx //將文件放入暫存區
​		git commit -m '註解' //批准改變至git本地倉庫
​		git commit -am '註解' //批准文件夾內所有文件的改變至git本地倉庫
​		git rm docsname.xxx //直接刪除文件包括git本地倉庫
​		git log //查看倉庫版本紀錄
​		git log --pretty=oneline //查看紀錄精簡至第一行與註解
​		git log --graph --pretty=oneline //同上,圖形化
​		git reflog //查看所有紀錄
​		git clone url //下載指定網址的git倉庫
​		git remote add origin git@github.com:userName/respositoryName.git //綁定至特定github遠端倉庫
​		git push -u origin main //將倉庫推送到遠端的main主幹
​		ssh-keygen -t rsa -C "GitHub帳號email" //創建一個對應github帳號的sshkey
​		git fetch //獲取遠端狀態

## git HEAD指令
​		git reset --hard HEAD^ //退回上個版本
​		git reset --hard HEAD~i //退回上i個版本
​		git reset --hard commitCode //依照commitCode退回版本

## git 分支指令
​		git checkout branchName //切換到指定分支
​		git checkout -b new_branchName //新建並切換分支
​		git branch -d branchName //刪除指定分支
​		git branch //查看所有分支,有*號為現分支
​		git merge branch //合併分支,需先切換到主幹
​		git branch -m|-M oldBranchName newBranchName //分支更名
​		git branch -a //查看本地與遠端分支
​		git push origin branchName //推送本地分支到遠端
​		git push origin :branchName //刪除遠端分支
​		git checkout -b localBranch origin/branchName //拉取遠端分支並在本地創建分支
​		git  pull //由遠端拉取分支

## git 標籤指令
​		git tag tagName //為現在版本上標籤
​		git tag -a tagName -m 'xxx' //上標籤並上描述
​		git tag //查看標籤
​		git tag -d tagName //刪除一個本地標籤
​		git push origin tagName //推送本地標籤至遠端
​		git push origin --tags //推送所有未推送的標籤至遠端
​		git push origin :refs/tags/tagName //刪除一個遠端的標籤