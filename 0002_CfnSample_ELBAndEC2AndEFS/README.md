# 参考URL

* [(2017年12月時点) 私的 CloudFormation ベストプラクティス](https://qiita.com/yasuhiroki/items/8463eed1c78123313a6f)
* [チュートリアル: Amazon マシンイメージ ID を参照する](https://docs.aws.amazon.com/ja_jp/AWSCloudFormation/latest/UserGuide/walkthrough-custom-resources-lambda-lookup-amiids.html)
* [CloudFormationでALBを構築する](https://dev.classmethod.jp/cloud/aws/cloudformation-alb/)
* [LoadBalancerAttribute](https://docs.aws.amazon.com/ja_jp/elasticloadbalancing/latest/APIReference/API_LoadBalancerAttribute.html)
* [AWSのログ管理ベストプラクティス](https://www.slideshare.net/akuwano/aws-77583244)
* [IPv6対応のELBとオートスケールなEC2をCloudFormationで作成してみた](https://dev.classmethod.jp/cloud/aws/ipv6-cfn-alb-autoscale-ec2/)
* [Classic Load Balancer のアクセスログの有効化](https://docs.aws.amazon.com/ja_jp/elasticloadbalancing/latest/classic/enable-access-logs.html)
* [awslabs/cloudwatch-logs-centralize-logs](https://github.com/awslabs/cloudwatch-logs-centralize-logs)

# コマンド

```
aws s3 cp cfn-elb-ec2-efs.yaml s3://cf-templates-ksby

aws cloudformation validate-template \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-elb-ec2-efs.yaml

aws cloudformation create-stack \
    --stack-name ksbysample-0002-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-elb-ec2-efs.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair \
    --capabilities CAPABILITY_NAMED_IAM

aws cloudformation update-stack \
    --stack-name ksbysample-0002-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-elb-ec2-efs.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair \
    --capabilities CAPABILITY_NAMED_IAM

aws cloudformation describe-stacks --stack-name ksbysample-0002-stack

aws cloudformation delete-stack --stack-name ksbysample-0002-stack

```

# メモ書き

* t3.nano, t3.micro は最大 1インスタンスしか使えない。2台のEC2サーバに指定したらエラーになった。EC2ダッシュボードの画面左側のリストから「制限」をクリックすると表示される。
* AMI のマシンイメージID はよく変わるようだ。0001 の時と Amazon Linux 2 のマシンイメージIDが変わっていた。構築時は必ず最新版を確認すること。
* EC2インスタンスに UserData に書いて実行するシェルスクリプトは別ファイルにして S3 に上げておいて、それを実行するようにした方が良いだろう。
