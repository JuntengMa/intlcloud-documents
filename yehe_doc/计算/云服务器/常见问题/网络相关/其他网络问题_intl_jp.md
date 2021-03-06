### CVMにログインした後、ネットワークに接続できません。この問題を解決するにはどうすればよいですか。
CVMにログインした後、インターネットにアクセスできない（ウェブページにアクセスできないなど）場合は、DNS構成を確認する必要があります。以下の手順に従って、CVMがDNSアドレスを自動的に取得するように設定します。
> 下記の操作は、Windows Server 2012を例に説明します。
> 
1. Windows CVM にログインします。
2. OSのインターフェースで<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png"style="margin:0;width:22px;">をクリックし、【コントロールパネル】>【ネットワークとインターネット】>【ネットワークの状態とタスクの表示】>【アダプターの設定の変更】を選択します
3. 【イーサネット】を右クリックして、【プロパティ】を選択し、「イーサネットのプロパティ」ウィンドウを開きます。
4. 「イーサネットのプロパティ」ウィンドウで、【インターネットプロトコルバージョン4（TCP/IPv4）】ウィンドウをダブルクリックして開きます。
5. 以下の図に示すとおり、「インターネットプロトコルバージョン4（TCP/IPv4）」ウィンドウで【IPアドレスを自動的に取得する】と【DNSサーバーのアドレスを自動的に取得する】を選択し、【OK】をクリックします。
![](https://main.qcloudimg.com/raw/8a597efe05adc2f96d4b40b6cd633ca4.png)

### VPCインスタンスは、基本ネットワークのインスタンスと相互接続できますか。

#### できますが、下記の制限があります。
VPC IPアドレス範囲（CIDR）は10.0.0.0/16-10.0.47.0/16（サブセットを含む）でなければなりません。そうでない場合、衝突が発生します。

#### 設定手順：
[VPCコンソール](https://console.cloud.tencent.com/vpc/vpc?rid=1)にログインし、VPCのID/名前をクリックして、VPCの詳細ページに入り、次に[Classiclink]タブをクリックして、**Associate with CVM**で設定を行い、CVMを関連付けます。 

### VPC CVMと相互接続されている基本ネットワーク内のCVMを表示するにはどうすればよいですか。
[VPCコンソール](https://console.cloud.tencent.com/vpc/vpc?rid=1)にログインし、VPCのID/名前をクリックして、VPCの詳細ページに入り、**Classiclink**で該当VPC CVMと相互接続されている基本ネットワーク内のCVMを確認できます。

### CVMのネットワークは、海外ネットワークに切り替えることができますか。
CVMを購入した後は、ネットワークを切り替えることができません。海外ネットワークが必要な場合は、CVMを返品して海外のCVMを購入することをお勧めします。

### プライベートネットワークDNSを設定するには、どうすればいいですか。
[プライベートネットワークDNS](https://intl.cloud.tencent.com/document/product/213/5225)をご参照ください。

### 同じIP範囲内では、VPNはIP範囲のIPアドレスを取得できますが、インターネットにはアクセスできません。この問題を解決するにはどうすればよいですか。

次の設定が正しいかどうかを確認してください。
1. 手動で追加したIPが自動取得したIPと同じIPサブネットにあるかどうか、サブネットマスクが一致しているかどうか、デフォルトゲートウェイを設定したかどうか、デフォルトゲートウェイアドレスが正しいかどうか確認してください。
2. DNSを設定したかどうか、DNSアドレスが正しいかどうか確認してください。
3. 上記の設定がすべて正しい場合は、静的に設定されたIPアドレスに競合があるかどうか確認してください。
  
上記の方法で解決できない場合は、 [チケットを提出](https://console.cloud.tencent.com/workorder/category) してください。

### アカウントAとアカウントB下にあるCVMを同じプライベートネットワークに追加するにはどうすればよいですか。

アカウント間のネットワークはデフォルトでは相互接続できません。アカウント間のネットワークを相互接続するには、[Peering Connection](https://intl.cloud.tencent.com/document/product/553/35190)または[Cloud Connection Network](https://intl.cloud.tencent.com/document/product/1003/31987)サービスを購入することができます。
