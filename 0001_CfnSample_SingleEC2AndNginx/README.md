# 参考URL

* [長期サポート (LTS) を付随した Amazon Linux 2 が一般公開](https://aws.amazon.com/jp/about-aws/whats-new/2018/06/announcing-amazon-linux-2-with-long-term-support/)
* [Amazon Linux 2 に関するよくある質問](https://aws.amazon.com/jp/amazon-linux-2/faqs/)
* [Amazon EC2 インスタンス](https://aws.amazon.com/jp/ec2/instance-types/)
* [AWSのEC2で行うAmazon Linux2の初期設定](https://qiita.com/2no553/items/e87485e3fc4199bd5dcb)
* [Amazon CloudWatch Logs テンプレートスニペット](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/quickref-cloudwatchlogs.html)
* [CloudFormationの中で、UserData書きまくって、エラーハンドリングせずにノーガード戦法デプロイしていませんか？](https://techblog.recochoku.jp/820)
* [クイックスタート: 実行中の EC2 Linux インスタンスに CloudWatch Logs エージェントをインストールして設定する](https://docs.aws.amazon.com/ja_jp/AmazonCloudWatch/latest/logs/QuickStartEC2Instance.html)

# コマンド

```
aws s3 cp cfn-single-ec2-and-nginx.yaml s3://cf-templates-ksby

aws cloudformation validate-template \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml

aws cloudformation create-stack \
    --stack-name ksbysample-0001-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair \
    --capabilities CAPABILITY_NAMED_IAM

aws cloudformation update-stack \
    --stack-name ksbysample-0001-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair \
    --capabilities CAPABILITY_NAMED_IAM

aws cloudformation describe-stacks --stack-name ksbysample-0001-stack

aws cloudformation delete-stack --stack-name ksbysample-0001-stack

```

# メモ書き

* Amazon Linux 2 が出ていた。
* EC2 は T3 インスタンスを使用。
* `timedatectl set-timezone Asia/Tokyo` を実行すれば /var/log/nginx/access.log に出力される日時も日本標準時になる。
* UserData に書いたコマンドの実行ログは /var/log/ cloud-init-output.log に出力される。
