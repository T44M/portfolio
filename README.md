# プロジェクト名：ラズベリーパイゼロを用いた環境モニタリングシステム

## プロジェクト概要：

このプロジェクトでは、ラズベリーパイとBME280センサーを使用して、室内の温度、湿度、気圧をリアルタイムで監視する環境モニタリングシステムを構築しました。データはAWS IoT Coreを経由してInfluxDBに保存され、Grafanaで可視化されます。さらに、自宅にVPNサーバーを設置して、スマートフォンから安全にネットワークにアクセスし、ラズベリーパイにSSH接続できるようにしました。また、Terraformにて、AWS構築を簡易にしています。

## 技術スタック：

ハードウェア: Raspberry Pi, BME280（温度、湿度、気圧）

インフラ: AWS IoT Core, AWS Lambda, EC2, Cloudwatch

DB: InfluxDB

言語: Python, Json, hcl

プロトコル: MQTT, SSH, VPN(Wireguard)

その他: Grafana, Github, Slack

## 主要機能：

1, ラズベリーパイで環境データの収集: Pythonスクリプトを使用して、ラズベリーパイに接続された環境センサーから温度、湿度、気圧のデータを定期的に収集します。

2, AWS IoT Coreとの通信: MQTTプロトコルを使用して、ラズベリーパイから収集されたデータをAWS IoT Coreに送信します。これにより、データは安全かつ効率的にクラウドに転送されます。

3, データ処理と保存: AWS Lambdaを使用して、IoT Coreから受信したデータを処理し、InfluxDBに保存します。このデータベースは、時系列データの効率的な格納とクエリに適しています。

4, データの可視化: Grafanaを使用して、InfluxDBに格納されたデータをリアルタイムで可視化し、ダッシュボードを作成します。これにより、ユーザーは環境データの変化を簡単に把握できます

5, 自宅のVPNサーバーの構築: 自宅ネットワークにVPNサーバーを設置し、スマートフォンや外部デバイスから安全にアクセスできるようにしました。これにより、ユーザーは外出先からもラズベリーパイにSSH接続し、システムの状態を確認できます。

このプロジェクトは、スマートホームや管理システムへの応用が可能であり、IoTデバイス、クラウドサービス、データベース、データ可視化ツールを組み合わせたソリューションの構築経験を提供します。

## こだわり：
1, InfluxDBを採用し、時系列データの取得ができるようになった。

2, データ連携が止まると、Slack通知。(ラズパイのスペック問題で休止)

3, 自宅ネットワーク内のラズベリーパイに、外部からSSH接続できるようにVPNサーバを構築。


## 運用上の問題：
1, ラズベリーパイゼロのスペックが低すぎて、スクリプトがクラッシュする。
→ラズベリーパイ4の入荷待ち

2, EC2のコスト
→Fargateなどで、DBのコンテナ化と、AWS マネージド Grafanaの使用。

## 今後の展望：

1, Fargateへの移行: 現在のEC2インスタンスを考慮し、コストや運用面での効率化を図るため、AWS Fargateに移行することを検討しています。これにより、サーバーの管理やスケーリングが不要になり、より簡単な運用が可能になります。

2, IoTトリガーの実装: 温度、湿度、気圧で閾値を決め、アレクサなどスマートホームデバイスから、エアコンのオンオフなどを実装し、快適なら生活をサポートできます。

3, 機械学習モデルの実装: 収集されたデータを基に、機械学習を用いた天気予報モデルを開発し、短期・長期の予測精度を向上させることを目指しています。この機能は、自動化された気象予報や、農業・エネルギー業界での活用に繋がる可能性があります。例えば、水質センサーを接続し、水耕栽培のデータを分析できれば、どの環境での収穫量が最大になるのかがわかり、2のIoTトリガーで安定した環境を実装できます。
