# 【Android】プッシュ通知機能！

![画像1](/readme-img/OverView.png)

## 概要

* [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のプッシュ通知機能は、Googleが提供しているFirebase Cloud Messaging（以下、FCM）と連携することで、通知の配信を行っています

※ FCMはGCM(Google Cloud Messaging)の新バージョンです。
既にGCMにてプロジェクトの作成・GCMの有効化設定を終えている場合は、継続してご利用いただくことが可能です。

* Androidアプリでプッシュ通知を受信するまでの設定は以下のような流れとなっています
 * FCMプロジェクトの作成とAPIキーの取得
 * ニフティクラウド mobile backendでの設定
 * アプリでの設定
* 詳しい設定内容は[プッシュ通知（Android）](http://mb.cloud.nifty.com/doc/current/push/basic_usage_android.html)をご参照ください

## ニフティクラウドmobile backendって何？？
スマートフォンアプリのバックエンド機能（プッシュ通知・データストア・会員管理・ファイルストア・SNS連携・位置情報検索・スクリプト）が**開発不要**、しかも基本**無料**(注1)で使えるクラウドサービス！今回はデータストアを体験します

注1：詳しくは[こちら](http://mb.cloud.nifty.com/price.htm)をご覧ください

![画像2](/readme-img/SdkTypes.png)

## 動作環境
* Windows 7 Professional
* Android Studio v2.1.2  (※2016/06 時点での最新バージョン)
* Android ver 4x,5x

※上記内容で動作確認をしています


## 手順
### 0.プッシュ通知機能使うための準備

ニフティクラウド mobile backendと連携させるためのAPIキーを取得する必要があります。 以下のドキュメントを参考に、FCMプロジェクトの作成とAPIキーの取得を行ってください。

__[mobile backendとFCMの連携に必要な設定](http://mb.cloud.nifty.com/doc/current/tutorial/push_setup_android.html)__

### 1. [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)の準備

* 上記リンクから会員登録（無料）をします
* 登録後、ログインをすると下図のように「アプリの新規作成」画面が出ますので、アプリを作成します

![画像3](/readme-img/mBassNewProject.png)

* アプリ作成されると下図のような画面になります
* この２種類のAPIキー（アプリケーションキーとクライアントキー）は先ほどインポートしたAndroidStudioで作成するAndroidアプリにニフティクラウドmobile backendの紐付けるため、あとで使います

![画像4](/readme-img/mBassAPIkey.png)

* 動作確認後、端末情報が保存される場所（データストアのinstallationクラス）を確認しておきましょう

![画像5](/readme-img/mBassData.png)

* アプリ設定開いてプッシュ通知の設定をします
   * 「プッシュ通知の許可」で「許可する」選択、「保存する」をクリックします
   * 「Androidプッシュ通知」の「APIキー」には、FCMでプロジェクト作成時に発行された「Sender ID」を記入し、「保存する」をクリックします

![画像6](/readme-img/mBassPushEnv.png)

### 2. [GitHub](https://github.com/ncmbadmin/android_push_demo.git)からサンプルプロジェクトのダウンロード

* プロジェクトの[Githubページ](https://github.com/ncmbadmin/android_push_demo.git)から「Clone or download」＞「Download ZIP」をクリックします
* プロジェクトを解凍します

### 3. AndroidStudioでアプリを起動

* AndroidStudioを開き、解凍したプロジェクトを選択します

![画像7](/readme-img/SelectProject.png)

* プロジェクトを開きます

![画像8](/readme-img/ProjectDesign.png)

### 4. APIキーの設定

* `MainActivity.java`を編集します
* 先程[ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のダッシュボード上で確認したAPIキーを貼り付けます

![画像9](/readme-img/AndroidAPIkey.png)

* それぞれ`YOUR_APPLICATION_KEY`と`YOUR_CLIENT_KEY`の部分を書き換えます
 * このとき、ダブルクォーテーション（`"`）を消さないように注意してください！

### 5. AndroidのSender IDキーの設定

* `MainActivity.java`を編集します

![画像10](/readme-img/FCMAPIkey.png)

* `ANDROID_SENDER_ID`の部分を、FCMでプロジェクト作成時に発行された「Sender ID」に書き換えます
 * このとき、ダブルクォーテーション（`"`）を消さないように注意してください！

### 6. 動作確認

* インストールしたアプリを起動します
 * プッシュ通知の許可を求めるアラートが出たら、必ず許可してください！

![画像11](/readme-img/Action1.png)

* 起動されたらこの時点でAndroid端末はレジスタレーションIDが取得されます
* [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/)のダッシュボードから「データストア (installationクラス(端末情報))」を確認してみましょう！

![画像12](/readme-img/Action2.png)

* 端末側で起動したアプリは一度閉じておきます

### 7. プッシュ通知を送りましょう！

* いよいよです！実際にプッシュ通知を送ってみましょう！
* ニフティクラウドmobile backendのダッシュボードで「プッシュ通知」＞「＋新しいプッシュ通知」をクリックします
* プッシュ通知のフォームが開かれます
* 必要な項目を入力してプッシュ通知を作成します

![画像13](/readme-img/Action3.png)

* Android端末からプッシュ通知を確認しましょう！
* 少し待つとプッシュ通知が届きます！

![画像14](/readme-img/Action4.png)

* ダッシュボードからのプッシュ通知結果も確認する

![画像15](/readme-img/Action5.png)


## 解説
サンプルプロジェクトに実装済みの内容のご紹介

#### SDKのインポートと初期設定
* ニフティクラウドmobile backend の[ドキュメント（クイックスタート）](http://mb.cloud.nifty.com/doc/current/introduction/quickstart_android.html#/Android/)をご用意していますので、ご活用ください

#### ロジック
 * `activity_main.xml`でデザインを作成し、`MainActivity.java`にロジックを書いています
 *  installationクラス(端末情報)が保存される処理は以下のように記述されます

```java

    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //**************** APIキーの設定とSDKの初期化 **********************
        NCMB.initialize(this, "YOUR_APPLICATION_KEY", "YOUR_CLIENT_KEY");

        final NCMBInstallation installation = NCMBInstallation.getCurrentInstallation();

        //FCMからRegistrationIdを取得しinstallationに設定する
        installation.getRegistrationIdInBackground("ANDROID_SENDER_ID", new DoneCallback() {
            //installation.getRegistrationIdInBackground("senderId", new DoneCallback() {
                @Override
            public void done(NCMBException e) {
                if (e == null) {
                    installation.saveInBackground(new DoneCallback() {
                        @Override
                        public void done(NCMBException e) {
                            if (e == null) {
                                //保存成功
                            } else if (NCMBException.DUPLICATE_VALUE.equals(e.getCode())) {
                                //保存失敗 : registrationID重複
                                updateInstallation(installation);
                            } else {
                                //保存失敗 : その他
                            }
                        }
                    });
                } else {
                    //ID取得失敗
                }
            }
        });

        setContentView(R.layout.activity_main);
    }
```

## 参考
* ニフティクラウドmobile backend の[ドキュメント（プッシュ通知（Android））](http://mb.cloud.nifty.com/doc/current/push/basic_usage_android.html)をご用意していますので、ご活用ください
