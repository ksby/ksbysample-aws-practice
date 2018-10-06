# 参考URL

* [長期サポート (LTS) を付随した Amazon Linux 2 が一般公開](https://aws.amazon.com/jp/about-aws/whats-new/2018/06/announcing-amazon-linux-2-with-long-term-support/)
* [Amazon Linux 2 に関するよくある質問](https://aws.amazon.com/jp/amazon-linux-2/faqs/)
* [AWSのEC2で行うAmazon Linux2の初期設定](https://qiita.com/2no553/items/e87485e3fc4199bd5dcb)

# コマンド

```
aws s3 cp cfn-single-ec2-and-nginx.yaml s3://cf-templates-ksby

aws cloudformation validate-template \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml

aws cloudformation create-stack \
    --stack-name ksbysample-0001-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair

aws cloudformation update-stack \
    --stack-name ksbysample-0001-stack \
    --template-url https://s3-ap-northeast-1.amazonaws.com/cf-templates-ksby/cfn-single-ec2-and-nginx.yaml \
    --parameters ParameterKey=KeyPair,ParameterValue=ksby-keypair

aws cloudformation describe-stacks --stack-name ksbysample-0001-stack

aws cloudformation delete-stack --stack-name ksbysample-0001-stack

```
