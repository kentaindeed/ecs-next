# ECS Next.js Application

AWS ECS上にデプロイされるNext.jsアプリケーションです。CodeBuildとECRを使用したCI/CDパイプラインが構築されています。

## 技術スタック

- **フレームワーク**: Next.js 15.5.4 (Turbopack対応)
- **ランタイム**: React 19.1.0
- **言語**: TypeScript
- **スタイリング**: Tailwind CSS v4
- **デプロイ**: AWS ECS Fargate
- **CI/CD**: AWS CodeBuild + ECR

## ローカル開発

```bash
# 依存関係のインストール
npm install

# 開発サーバーの起動
npm run dev

# ビルド
npm run build

# 本番サーバーの起動
npm start
```

開発サーバーは [http://localhost:3000](http://localhost:3000) で起動します。

## AWS デプロイメント

### 必要な環境変数

CodeBuildで以下の環境変数を設定してください：

- `AWS_ACCOUNT_ID`: AWSアカウントID
- `AWS_DEFAULT_REGION`: デプロイ先リージョン (デフォルト: ap-northeast-1)
- `IMAGE_REPO_NAME`: ECRリポジトリ名
- `IMAGE_TAG`: イメージタグ (デフォルト: latest)

### デプロイフロー

1. **CodeBuild**: `buildspec.yml`に基づいてビルド・ECRプッシュ
2. **ECS**: `taskdef.json`の設定でFargateタスクを実行
3. **ログ**: CloudWatch Logsで監視

### Docker

```bash
# イメージビルド
docker build -f docker/Dockerfile -t ecs-next .

# ローカル実行
docker run -p 3000:3000 ecs-next
```

## プロジェクト構成

```
├── docker/
│   └── Dockerfile          # マルチステージビルド設定
├── src/                    # アプリケーションソース
├── buildspec.yml          # CodeBuild設定
├── taskdef.json           # ECSタスク定義
└── package.json           # 依存関係・スクリプト
```
