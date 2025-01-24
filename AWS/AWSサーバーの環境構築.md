# **AWS 上のサーバーの環境構築**

## **1. サーバーの基本構成**
AWS のサーバー環境は、主に以下の 3 つの役割に分かれる
- **Web サーバー**（HTTP リクエストを処理）
- **アプリケーションサーバー**（アプリケーションロジックを処理）
- **データベースサーバー**（データを管理）

EC2 に  
Web サーバーソフトウェアをインストールすると **Web サーバー**  
データベースソフトウェアをインストールすると **データベースサーバー**
になります。

## **2. EC2 の初期設定手順**
EC2 の環境構築には、以下の手順を実行
1. **サーバーにログインするための鍵（キーペア）を作成**（SSH接続用の秘密鍵を作成し、安全にアクセスできるようにする）
2. **EC2 インスタンスの作成に必要な情報を選択**（OSやインスタンスタイプを指定）
3. **EC2 インスタンスの作成**（AWS上に仮想サーバーを起動）
4. **全世界からのアクセスを許可する準備（Elastic IP 設定）**（固定IPアドレスを割り当てる）
5. **セキュリティグループの設定**（ファイアウォール設定で安全な接続を確保）
6. **設定の確認と EC2 への接続**（問題なく接続できるかチェック）

---

## **3. AWS CloudShell から EC2 を作成**

### **(1) EC2 インスタンスを作成する前の準備**
#### **キーペアの作成（SSH認証用の秘密鍵）**
```bash
aws ec2 create-key-pair \
 --key-name my-key-pair \
 --key-type rsa \
 --key-format pem \
 --query "KeyMaterial" \
 --output text > my-key-pair.pem
```
作成した my-key-pair.pem はローカルにダウンロードし、安全に保管すること  
紛失するとサーバーにアクセスできなくなる
## AMI（Amazon Machine Image）の取得（EC2インスタンスのベースとなるOSの選択）
```bash
AMI_ID=$(aws ec2 describe-images --owners amazon \
 --filters 'Name=name,Values=amzn2-ami-hvm-2.0.*-gp2' 'Name=state,Values=available' \
 --query 'reverse(sort_by(Images, &CreationDate))[:1].ImageId' \
 --output text \
 --region ap-northeast-1)
```
