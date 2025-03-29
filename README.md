# このプロジェクトについて

- オンライン上の政策熟議PFを構築する「いどばた」PJのリポジトリです。
    - PJ全体の意義・意図は[こちらのスライド](https://docs.google.com/presentation/d/1etZjpfj9v59NW5REC4bOv4QwVq_ApZMFDMQZqPDHb8Q/edit#slide=id.g339b8863127_0_989)のP20からP50を参照ください。
- 本PJは、以下に示す複数のモジュールで構築されています
    - [idobata-agent](https://github.com/takahiroanno2024/idobata-agent/) (フォーラムの投稿に反応し、モデレーションを行うモジュール)
    - [idobata-analyst](https://github.com/takahiroanno2024/idobata-analyst/)（フォーラムやSNSの投稿を分析し、レポートを作成するモジュール）
    - [idobata-infra](https://github.com/takahiroanno2024/idobata-infra/)（フォーラムのインフラを構築する設定）
    - [idobata-sns-agent](https://github.com/takahiroanno2024/idobata-sns-agent/)（SNSの投稿を収集したり、投稿を行うためのモジュール）

# 開発への参加方法について

- 本PJは、開発者の方からのコントリビュートを募集しています！ぜひ一緒に日本のデジタル民主主義を進めましょう！
- プロジェクトのタスクは[GitHub Project](https://github.com/orgs/digitaldemocracy2030/projects/1/views/1)で管理されています。
    - [good first issueタグ](https://github.com/orgs/takahiroanno2024/projects/4/views/1?filterQuery=good+first+issue?filterQuery=good+first+issue)がついたIssueは特に取り組みやすくなっています！
- プロジェクトについてのやりとりは、原則[デジタル民主主義2030のSlackの「開発_いどばた」チャンネル](https://w1740803485-clv347541.slack.com/archives/C08FF5MM59C)までお願いします
- コントリビュートにあたっては、本リポジトリのrootディレクトリにあるCLA.md（コントリビューターライセンス）へ同意が必要です。
    - 同意する手順は、Pull Requestのテンプレートに記載があります

## Issue/Pull Requestについて
- 重複して同じIssueに取り組むのを避けるため、Issueに着手される際はご自身のアカウントをasigneeに指定してください
  - イシュー上で、 `/assign` というコメントを記載していただくと、Issueのasigneeとして登録されます
    - 権限の関係で、一部のコントリビューターを除いてアサインの割当ができないためこのような運用にしています
  - 割当を解除したい場合は、 `/unassign` というコメントを記載していただくと、Issueのasigneeから外れます
- Issueはどなたでも起票いただいて構いません。ツールの利用時に感じた改善点やバグについてぜひIssueを起票してください。

# 論点整理モジュール

## セットアップと実行方法

### 1. 環数設定

以下のコマンドでアプリケーションのセットアップ実行します。

```bash
make setup
```

ここでは環境変数の設定ファイル `.env`、`packages/backend/.env`、`packages/frontend/.env` を作成しています。

各ファイルを確認し、必要に応じて以下の環境変数を設定してください：

- ADMIN_API_KEY は、あなたの環境における管理者認証用パスワードです。好きな文字列を設定してください。
- OPENROUTER_API_KEY は、OpenRouter の API キーです。[OpenRouter](https://openrouter.ai/) で取得してください（アカウントをお持ちでない場合はアカウントの作成が必要です。またサービス利用のためのクレジットが必要です）

### 2. アプリケーションの起動

以下のコマンドでアプリケーションを起動します。

```bash
make containers-start
```

Web ブラウザで <http://localhost:3000> にアクセスすると、自分の PC で起動している idobata アプリケーションが開きます。

### 3. 試し方

Web ブラウザでアプリケーションを開いた後、以下の手順で CSV データをアップロードし、論点整理を試すことができます：

#### 管理者モードへのアクセス

1. ブラウザで <http://localhost:3000/adminauth> にアクセスします
2. `.env`ファイルに設定した`ADMIN_API_KEY`を入力して認証ボタンをクリックします

#### CSVデータのアップロード

1. 認証後、<http://localhost:3000/csv-upload> にアクセスします
2. 以下の情報を入力してプロジェクトを作成します：
   - プロジェクト名：分析対象のプロジェクト名
   - プロジェクトの説明：プロジェクトの概要
   - 抽出トピック：分析したい主題（例：「再生可能エネルギー政策について」）
   - プロジェクトの背景情報：分析の文脈となる情報
3. 「プロジェクトを作成」ボタンをクリックします
4. CSVファイルを選択します（必須列：content, sourceType, sourceUrl）
5. 「アップロード開始」ボタンをクリックします
6. アップロード完了後、「処理開始」ボタンをクリックして論点生成と立場のラベル付けを行います
7. 処理完了後、「プロジェクトページへ」ボタンをクリックして結果を確認します

#### 例

例えば、この[YouTube動画](https://www.youtube.com/watch?v=CHCx9AUpE4U)に対するコメントを収集して作成したCSVが[こちら](https://drive.google.com/file/d/1Rs-rHrnmwoHngtUYC1hB4cw0QXVfwpyP/view?usp=sharing)になります。このCSVファイルをアップロードすると、以下のような結果が得られます。
[![Image from Gyazo](https://i.gyazo.com/1c8a7aee03de9cd1a7f7f54d621c91e2.png)](https://gyazo.com/1c8a7aee03de9cd1a7f7f54d621c91e2)
[![Image from Gyazo](https://i.gyazo.com/1c8a7aee03de9cd1a7f7f54d621c91e2.png)](https://gyazo.com/1c8a7aee03de9cd1a7f7f54d621c91e2)

## プロジェクト構成

```tree
.
├── compose.prod.yaml       # Docker構成ファイル
├── compose.yaml            # 開発環境用Docker構成ファイル
├── packages/
    ├── frontend/           # Reactフロントエンド
    │   │── Dockerfile      # フロントエンドのビルド設定
    │   └── Dockerfile.dev  # フロントエンドの開発用ビルド設定
    └── backend/            # Expressバックエンド
        │── Dockerfile      # バックエンドのビルド設定
        └── Dockerfile.dev  # バックエンドの開発用ビルド設定
```
