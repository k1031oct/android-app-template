このプロジェクトは今後複数のAndroidアプリケーションを構築する上でひな形を作る意図がある。
開発サイクルとしては以下を構築する。

現在の状態はテンプレートからテスト作製をしたプロジェクトを用いて開発サイクルの構築を行っている最中。
各種エラーを解消し、開発環境の完成を目指す。

現時点のプロジェクトの状態と今後の構築計画を立ててみて。
以下が構築を目指している開発サイクル。

このテンプレートリポジトリを使用することで、以下の5ステップで開発が進みます。
Step 1: 【構築】プロジェクト初期化
リポジトリ作成: GitHub上で android-app-template を開き、「Use this template」ボタンから新しいアプリケーション用のリポジトリを作成します。
クローン: 作成した新しいリポジトリをローカルPCに git clone します。
初期化: ターミナルで ./init.sh を実行します。
スクリプトが「アプリ名」「パッケージ名」などを質問します。
入力に基づき、AndroidManifest.xml の書き換え、パッケージ名のディレクトリ変更などが自動で行われます。
Step 2: 【設定】手動設定
プロジェクトルートにある MANUAL_SETUP.md を開きます。
チェックリストに従い、手動で必要な設定を完了させます。
例: Firebaseプロジェクトの作成と google-services.json の配置。
例: GitHubリポジトリのSecrets（FIREBASE_TOKEN や署名キー）の設定。
Step 3: 【開発】Geminiを用いたプロトタイピング
Android Studioでプロジェクトを開きます。
PROMPT_TEMPLATE.md の内容をコピーし、開発したいアプリの仕様を追記します。
Android StudioのGemini（エージェントモード）にプロンプトを渡し、バイブコーディングを開始します。
Step 4: 【レビュー】自動レビューサイクル
開発: PC（Android Studio）または Android（Termux + Gemini CLI）でコードを編集します。
プッシュ: 変更を git push します。
CI/CD起動: GitHub Actionsが自動で review.yml ワークフローを実行します。
ビルド → テスト → Firebase App Testerへ自動配布。
レビュー: テスト機（Pixel 8）にApp Testerから通知が届き、すぐに最新のテストバージョンを確認できます。
どのデバイスからプッシュしても、レビュープロセスは完全に共通化・自動化されます。
Step 5: 【リリース】自動リリースビルド
タグ付け: リリース準備が整ったら、git tag v1.0.0 のようにバージョンタグを作成し、git push --tags でプッシュします。
CI/CD起動: GitHub Actionsが release.yml ワークフローを実行します。
署名済みのリリースAAB (App Bundle) がビルドされます。
公開: ビルドされたAABは、Google Play Consoleへ自動アップロード（またはドラフト作成）され、ストアリリースの準備が整います。
