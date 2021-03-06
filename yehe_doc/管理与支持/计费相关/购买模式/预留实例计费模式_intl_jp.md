### RI課金モードの説明

リザーブドインスタンス（Reserved Instances、RI）は実際の物理インスタンスではなく、請求の割引はアカウントでのオンデマンドインスタンスの使用に適用され、実質的には従量課金モードに該当します。使用中の従量課金制の物理インスタンスとRIの属性と一致する場合、従量課金制の物理インスタンスには料金の割引が適用されます。従来のリソースインスタンスを元にRIを購入してアクティブ化することも、リソースインスタンスを購入する前にRIを購入することもできます。一定のRIの前払いを行った後、購入した期間内において対応する特定の割引が受けられます。従来のサブスクリプション（年額／月額課金）と従量課金の課金モードに比べ、RIと従量課金制インスタンスを組み合わせた課金モードは柔軟性とコスト面での優位性を有し、ユーザーに最大の割引優待をご提供します。

**サポートされている製品**

CVM

**RIの購入**

- 予算とリソース状況に応じてRIのタイプ（モデルの構成）、お支払いタイプ、リージョン、有効期間、購入数を選択することができます。

- 現在、Tencent Cloud APIを通じてRIの購入をサポートしており、詳細については、CVM製品の説明をご参照ください。

- RIは返金をサポートしていません。

**RIがサポートするインスタンスタイプおよび価格：**　

RIがサポートするインスタンスタイプの設定、マッチングルールおよび定価の説明については、CVM製品の説明をご参照ください。

**お支払いタイプ：**

- 全額前払い（All Upfront）：購入時に費用を全額前払いし、RIの使用期間内にその他費用をさらに支払うことはありません。上記2種のオンデマンドインスタンスの定価に比べ、この支払いオプションは最大の割引となります。

- 一部費用前払い（Partial Upfront）：購入時にやや少額を前払いし、RIの使用期間に、月額料金または割引適用後の時間料金でRI費用を支払います。

- 前払いなし（No Upfront）：購入時に一切の費用を支払う必要はなく、RIの使用期間中に、月額料金または割引適用後の時間料金でRI費用を支払います。

注：RIを使用する場合は、実際の使用状況の如何を問わず、全期間にわたって支払いを行う必要があります。

**有効期間のタイプ**

1年または3年。

例：2019-05-25 11:15:24 に有効期間1年のCVM RIを購入した場合、RIの有効期間は：2019-05-25 12:00:00 \~ 2020-05-24 12:00:00となります。2019-05-25 11:15:24に有効期間3年のCVM RIを購入した場合、RIの有効期間は：2019-05-25 12:00:00~2022-05-24 12:00:00となります。

説明：RIの有効期間が切れた後もマッチングする従量課金制インスタンスは正常に動作しますが、従量課金インスタンスの請求額を引き続き差し引くことはできません。

**課金ルール**

- RIの決済サイクルは1時間（3600秒）であり、1時間単位の決済（例：10:00:00-10:59:59）が採用されます。同一決済サイクル内における複数の従量課金制の物理インスタンスを、同時に同じRIに一致させることができます。料金明細中にはRIにマッチング成功の割引記録とRIにマッチングしなかった割引記録がそれぞれ表示されます。

- 購入成功後、RIは正時にて有効期間の計算を開始します。従量課金制インスタンスとマッチングできるかどうかを問わず、有効期間内にはRIの費用をお支払いいただく必要があり、予算とリソース状況に応じて、適切な支払いタイプと有効期間を選択できます。有効時間は正時を起点として計算し、失効時間は期限到来日の対応する正時とします。例えば、2019-05-25 11:15:24に有効期間1年のCVM RIを購入した場合、このRIの有効時間と課金開始時間は2019-05-25 12:00:00となり、失効時間は2020-05-24 12:00:00となります。このRIの購入時にマッチング可能なCVMリソースをすでに所有している場合は、2019-05-25 11:00:00-11:59:59から課金が開始され、時間ごとの課金率で決済の割引が実施されます。

**RIの割引：**

RI購入費用の割引がサポートされています。
