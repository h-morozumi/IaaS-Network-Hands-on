# 仮想マシンの作成

## 概要

この演習では、仮想ネットワーク上に仮想マシンを作成し、仮想マシン同士の通信を確認します。

## 作業手順

### Task 1 - 仮想マシンの作成

#### Windows Server 2022 仮想マシンの作成

- 基本
    - リソースグループ：azure-hands-on（お使いのリソースグループ名に置き換えてください）
    - 仮想マシン名：workshop-windows-vm
    - リージョン：Japan East
    - 可用性オプション：インフラストラクチャ冗長は必要ありません
    - セキュリティの種類：Standard
    - イメージ：Windows Server 2022 Datacenter -x64 Gen 2
    - サイズ：Standard_D2s_v5
    - ユーザ名：azureuser
    - パスワード：Azure12345678!（自由にパスワードを置き換えてください）
    - パブリック受信ポート：なし
- ディスク
    - OS ディスクの種類：Standard SSD
    - VMと共に削除：有効
- ネットワーク
    - 仮想ネットワーク：azure-vnet-spoke-1
    - サブネット：azure-subnet-spoke-1
    - パブリック IP：なし
    - VMが削除されたときに NIC を削除する：有効
- 管理
    - 自動シャットダウンを有効にする：有効
    - シャットダウン時刻：19:00:00
    - タイムゾーン：(UTC+09:00) 大阪, 札幌, 東京
    - シャットダウン前の通知：有効
    - 電子メール：自分のメールアドレス


<img src="../images/Ex2/1-01.png" width="800" />
<img src="../images/Ex2/1-02.png" width="800" />
<img src="../images/Ex2/1-03.png" width="800" />
<img src="../images/Ex2/1-04.png" width="800" />
<img src="../images/Ex2/1-05.png" width="800" />
<img src="../images/Ex2/1-06.png" width="800" />
<img src="../images/Ex2/1-07.png" width="800" />
<img src="../images/Ex2/1-09.png" width="800" />
<img src="../images/Ex2/1-08.png" width="800" />
<img src="../images/Ex2/1-10.png" width="800" />
<img src="../images/Ex2/1-11.png" width="800" />
<img src="../images/Ex2/1-13.png" width="800" />
<img src="../images/Ex2/1-14.png" width="800" />
<img src="../images/Ex2/1-15.png" width="800" />
<img src="../images/Ex2/1-16.png" width="800" />
<img src="../images/Ex2/1-17.png" width="800" />
<img src="../images/Ex2/1-18.png" width="800" />
<img src="../images/Ex2/1-19.png" width="800" />
<img src="../images/Ex2/1-20.png" width="800" />
<img src="../images/Ex2/1-21.png" width="800" />
<img src="../images/Ex2/1-22.png" width="800" />


#### Ubuntu 20.04 LTS 仮想マシンの作成

- 基本
    - リソースグループ：azure-hands-on（お使いのリソースグループ名に置き換えてください）
    - 仮想マシン名：workshop-windows-vm
    - リージョン：Japan East
    - 可用性オプション：インフラストラクチャ冗長は必要ありません
    - セキュリティの種類：Standard
    - イメージ：Ubuntu Server 20.04 LTS - x64 Gen 2
    - サイズ：Standard_D2s_v5
    - 認証の種類：パスワード
    - ユーザ名：azureuser
    - パスワード：Azure12345678!（自由にパスワードを置き換えてください）
    - パブリック受信ポート：なし
- ディスク
    - OS ディスクの種類：Standard SSD
    - VMと共に削除：有効
- ネットワーク
    - 仮想ネットワーク：azure-vnet-spoke-2
    - サブネット：azure-subnet-spoke-2
    - パブリック IP：なし
    - VMが削除されたときに NIC を削除する：有効
- 管理
    - 自動シャットダウンを有効にする：有効
    - シャットダウン時刻：19:00:00
    - タイムゾーン：(UTC+09:00) 大阪, 札幌, 東京
    - シャットダウン前の通知：有効
    - 電子メール：自分のメールアドレス

<img src="../images/Ex2/2-02.png" width="800" />
<img src="../images/Ex2/2-03.png" width="800" />
<img src="../images/Ex2/2-04.png" width="800" />
<img src="../images/Ex2/2-05.png" width="800" />
<img src="../images/Ex2/2-06.png" width="800" />
<img src="../images/Ex2/2-07.png" width="800" />
<img src="../images/Ex2/2-09.png" width="800" />
<img src="../images/Ex2/2-11.png" width="800" />
<img src="../images/Ex2/2-12.png" width="800" />
<img src="../images/Ex2/2-13.png" width="800" />
<img src="../images/Ex2/2-14.png" width="800" />
<img src="../images/Ex2/2-15.png" width="800" />
<img src="../images/Ex2/2-16.png" width="800" />
<img src="../images/Ex2/2-17.png" width="800" />
<img src="../images/Ex2/2-18.png" width="800" />
<img src="../images/Ex2/2-19.png" width="800" />


### Task 2 - 仮想マシン同士の通信確認

#### Windows Server 2022 にログインする

- ユーザ名：azureuser
- パスワード：Azure12345678!（作成時に指定したパスワード）

<img src="../images/Ex2/3-00.png" width="800" />
<img src="../images/Ex2/3-01.png" width="800" />
<img src="../images/Ex2/3-02.png" width="800" />
<img src="../images/Ex2/3-03.png" width="800" />

#### Windows Server 2022 Ping 応答を許可する
<img src="../images/Ex2/4-01.png" width="800" />
<img src="../images/Ex2/4-02.png" width="800" />

``` powershell
New-NetFirewallRule `
-Name 'ICMPv4' `
-DisplayName 'ICMPv4' `
-Description 'Allow ICMPv4' `
-Profile Any `
-Direction Inbound `
-Action Allow `
-Protocol ICMPv4 `
-Program Any `
-LocalAddress Any `
-RemoteAddress Any 
```

<img src="../images/Ex2/4-04.png" width="800" />
<img src="../images/Ex2/4-03.png" width="800" />

``` powershell
Get-NetFirewallRule | Where-Object Name -Like 'ICMPv4' 
```
<img src="../images/Ex2/4-05.png" width="800" />

#### 疎通確認

##### Linux の IP アドレスを確認する

<img src="../images/Ex2/4-06.png" width="800" />
<img src="../images/Ex2/4-08.png" width="800" />

#### Ubuntu 20.04 LTS にログインする

<img src="../images/Ex2/5-01.png" width="800" />
<img src="../images/Ex2/5-02.png" width="800" />

#### 疎通確認

##### Windows の IP アドレスを確認する

<img src="../images/Ex2/5-03.png" width="800" />
<img src="../images/Ex2/5-05.png" width="800" />

#### Spoke1 と Spoke2 をピアリングする

- リモート仮想ネットワークの概要
    - ピアリング リンクの名前：spoke1-to-spoke2
    - 仮想ネットワーク：azure-vnet-spoke-2
- ローカル仮想ネットワーク ピアリングの設定
    - ピアリング リンクの名前：spoke2-to-spoke1

<img src="../images/Ex2/6-01.png" width="800" />
<img src="../images/Ex2/6-02.png" width="800" />
<img src="../images/Ex2/6-03.png" width="800" />
<img src="../images/Ex2/6-04.png" width="800" />
<img src="../images/Ex2/6-05.png" width="800" />

#### 疎通確認

##### LinuxからWindowsへのPing
<img src="../images/Ex2/6-07.png" width="800" />

##### WindowsからLinuxへのPing
<img src="../images/Ex2/6-08.png" width="800" />




## まとめ

この演習では、仮想ネットワーク上に仮想マシンを作成し、仮想マシン同士の通信を確認しました。

## 次のステップ

[Exercise 3 - 監視とセキュリティ](./Exercise%203.md)　へ進みます。

## 参考資料

- [Azure での仮想マシン](https://learn.microsoft.com/ja-jp/azure/virtual-machines/overviewm)
- [クイック スタート:Azure portal で Linux 仮想マシンを作成する](https://learn.microsoft.com/ja-jp/azure/virtual-machines/linux/quick-create-portal?tabs=ubuntu)
- [クイック スタート:Azure Portal で Windows 仮想マシンを作成する](https://learn.microsoft.com/ja-jp/azure/virtual-machines/windows/quick-create-portal)
- [Windows Server 2019 : 初期設定 : Ping 応答を許可する : Server World ](https://www.server-world.info/query?os=Windows_Server_2019&p=initial_conf&f=6#google_vignette)