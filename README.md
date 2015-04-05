# Vagrant Remote

http://blog.masuidrive.jp/2015/04/06/vagrant-remote/ ‎


検索していくと、[本家のIssuesでもvagrantをリモート実行する議論](https://github.com/mitchellh/vagrant/issues/401)が行われていました。そこで紹介されているプラグインを試してましたが用途とは合いませんでしたし、バージョンアップの多いvagrantで使い続けられるか心配でした。

でもよく考えれば用途さえ限定すれば、リモート実行は難しい事じゃなのではないかと思い自分でvagrant-remoteコマンドを実装してみました。

https://github.com/masuidrive/vagrant-remote

まだ未完成のコマンドですが、とりあえず公開する事にしました。自分でもまだ使っていないので自己責任でお願いします。

Vagrantfileと同じディレクトリに下記の様な`.vagrant-node`ファイルを置き、リモート実行するホストを指定します。あと同時にテンポラリディレクトリを指定します。

<pre># .vagrant-remote
export REMOTE_NODE="user1@10.0.1.9"  # ユーザ名は省略できます
export REMOTE_PATH="/Users/masuidrive/tmp" # 指定しなくてもOK
</pre>

リモート実行するノードはLinuxかOSXでvagrantをインストールしておいてください。OSXでのみテストしているので、Linuxで動かなかったらPull Requestをお待ちしてますw

これで、`vagrant-remote up`をすると、リモートノードにsshしてNFSでローカルフォルダをマウントしてvagrant upを実行します。

`vagrant-remote ssh`でsshはできますが、今のところポートフォワーディングは行いません。そのうちやるかも。

<img src="http://blog.masuidrive.jp/wp-content/uploads/2015/04/vagrant-remote-up.png" alt="vagrant-remote-up" class="alignnone size-full wp-image-1542" />
