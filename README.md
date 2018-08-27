vagrant + virtual box on windows

vagrantとvirtual boxを使用したlinux環境構築手順です。


vagrantを使用するメリット


  isoファイルのダウンロード、OSインストールの手間を省くことができます。
　コマンドも標準化され、ハイパーバイザーの種類による依存を軽減できます。


vagrantを使用するデメリット


  ネットインストールが前提なので排他環境では使用できません。

〇環境


HostOS:windows7 64bit　※おそらく8,10も同様の手順で問題ないと思います。


GuestOS:centos7

〇tool


vagrant,virtual box,power shell,teraterm


〇インストール手順


1 vagrantのインストール


https://www.vagrantup.com/downloads.html

2 virtual boxのインストール


https://www.virtualbox.org/wiki/Downloads

インストール後にネットワークアダプタのアドレスを確認する。
※後述するVargrantfileの設定で必要になります。

3 teratermのインストール


https://ja.osdn.net/projects/ttssh2

4 pc再起動

以下　power shellで作業


5-1 power shellを起動してバージョンを確認する


※バーションが3.0以上であること


>$PSVersionTable


5-2 vagrant作業ディレクトリの作成とディレクトリ移動


>mkdir C:\Vagrant\centos7


>cd C:\Vagrant\centos7

5-3 centos7のVagrantfileを追加


>vagrant init centos/7


参考：https://app.vagrantup.com/centos/boxes/7


5-3 vagrantプラグインをインストール


>vagrant plugin install vagrant-disksize


Installing the 'vagrant-disksize' plugin. This can take a few minutes...


Fetching: vagrant-disksize-0.1.2.gem (100%)


5-4 Vagrantfileの編集


>notepad .\Vagrantfile


以下のgithubの通りに編集


https://github.com/gisaburo/vagrant/blob/master/centos7


※「centos.vm.network "private_network", ip: "192.168.56.13"」のIPアドレスはvirtual boxインストール時に確認したIPアドレスと同じネットワークとなるように適宜書き換えてください。


5-5 OS起動


>vagrant up centos


==> centos: flag to force provisioning. Provisioners marked to run always will still run.


5-6 ssh情報確認


>vagrant ssh-config centos


IdentityFile C:/Vagrant/centos7/.vagrant/machines/centos/virtualbox/private_key


※IdentityFileのパスを取得しておく


以下、teratermで作業


6-1 Gestosにlogonする


・teratermを起動してホストに「centos.vm.network "private_network", ip: "192.168.56.13"」で設定したIPアドレスを設定してOKをクリック


ユーザ名：vagrant


パスフレーズ：vagrant


「RSA/DSA/ECDSA/ED25519鍵を使う」にチェックして、秘密鍵に「vagrant ssh-config centos」コマンドで取得したIdentityFileのパスを入れてログインする。
※何回かはじかれるかもしれません。
