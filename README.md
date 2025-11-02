# Android App Template

## 概要

このリポジトリは、複数のAndroidアプリケーションを効率的に構築するための雛形（テンプレート）です。
このテンプレートを使用することで、以下の5ステップからなる効率的な開発サイクルを確立します。

## 開発サイクル

### Step 1: 【構築】プロジェクト初期化

1.  **リポジトリ作成:** GitHub上でこの `android-app-template` を開き、「Use this template」ボタンから新しいアプリケーション用のリポジトリを作成します。
2.  **クローン:** 作成した新しいリポジトリをローカルPCに `git clone` します。
3.  **初期化:** ターミナルで `./init.sh` を実行します。
    *   スクリプトが「アプリ名」「パッケージ名」などを対話的に質問します。
    *   入力に基づき、`AndroidManifest.xml` の書き換え、パッケージ名のディレクトリ変更などが自動で行われます。

### Step 2: 【設定】手動設定

1.  プロジェクトルートにある `MANUAL_SETUP.md` を開きます。
2.  チェックリストに従い、手動で必要な設定を完了させます。
    *   例: Firebaseプロジェクトの作成と `google-services.json` の配置。
    *   例: GitHubリポジトリのSecrets（`FIREBASE_TOKEN` や署名キー）の設定。

### Step 3: 【開発】Geminiを用いたプロトタイピング

1.  Android Studioでプロジェクトを開きます。
2.  `PROMPT_TEMPLATE.md` の内容をコピーし、開発したいアプリの仕様を追記します。
3.  Android StudioのGemini（エージェントモード）にプロンプトを渡し、コーディングを開始します。

### Step 4: 【レビュー】自動レビューサイクル

1.  **開発:** PC（Android Studio）または Android（Termux + Gemini CLI）でコードを編集します。
2.  **プッシュ:** 変更を `git push` します。
3.  **CI/CD起動:** GitHub Actionsが自動で `review.yml` ワークフローを実行します。
    *   ビルド → テスト → Firebase App Distributionへ自動配布。
4.  **レビュー:** テスト機（Pixel 8）にApp Testerから通知が届き、すぐに最新のテストバージョンを確認できます。
    *   どのデバイスからプッシュしても、レビュープロセスは完全に共通化・自動化されます。

### Step 5: 【リリース】自動リリースビルド

1.  **タグ付け:** リリース準備が整ったら、`git tag v1.0.0` のようにバージョンタグを作成し、`git push --tags` でプッシュします。
2.  **CI/CD起動:** GitHub Actionsが `release.yml` ワークフローを実行します。
    *   署名済みのリリースAAB (App Bundle) がビルドされます。
3.  **公開:** ビルドされたAABは、Google Play Consoleへ自動アップロード（またはドラフト作成）され、ストアリリースの準備が整います。
