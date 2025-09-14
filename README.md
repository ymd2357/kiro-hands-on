# Kiro Hands-on Starter

## ダウンロード

常に最新の教材は [Releases ページ](../../releases/latest) から取得できます。

## 自動デプロイメント

このリポジトリは GitHub Actions を使用して、新しいリリースが公開されたときに自動的にデプロイされます。

### 🚀 運用方法

#### 自動デプロイメント（推奨）
1. **新しいリリースを作成**
   - GitHub の [Releases ページ](../../releases) で「Create a new release」をクリック
   - タグ名を入力（例：`v0.2.0`）
   - リリースタイトルと説明を記入
   - 「Publish release」をクリック
2. **自動実行確認**
   - [Actions タブ](../../actions) でワークフローの実行状況を確認
   - デプロイメントが完了するまで数分待機

#### 手動デプロイメント（必要時のみ）
1. **Actions タブ**から「Deploy Release to Production」を選択
2. **Run workflow**をクリック
3. オプションを選択：
   - `deploy_mode`: `dry-run`（テスト）または `deploy`（本番）
   - `release_tag`: デプロイするリリースタグ（空白で最新）
4. **Run workflow**で実行

#### 必要な設定
デプロイメントには以下のシークレットが必要です（リポジトリ管理者が設定）：
- `FTP_SERVER`: デプロイ先サーバー
- `FTP_USERNAME`: FTP ユーザー名  
- `FTP_PASSWORD`: FTP パスワード
- `FTP_SERVER_DIR`: デプロイ先ディレクトリ

詳細な技術情報は [DEPLOYMENT.md](DEPLOYMENT.md) を参照してください。

## 学習ドキュメントのダウンロード
- 個別ファイル: [docs/LEARNING.md](docs/LEARNING.md)
- まとめ版README: [README.full.md](README.full.md)
- 一括ZIP: [kiro-hands-on-starter.zip](kiro-hands-on-starter.zip)

## セットアップ
1. 新しいプロジェクトフォルダを作成
   ```bash
   mkdir hello-kiro-tutorial
   cd hello-kiro-tutorial
   git init
   ```
2. Kiro で `hello-kiro-tutorial` フォルダを開く

## クイックスタート（Hello, Kiro）
1. Kiro チャットに入力  
   **「`hello_kiro.ts` を作って `console.log('Hello, Kiro')` を出し、`npm start` を用意」**
2. `package.json` の `"start"` が生成されたら実行  
   ```bash
   npm start
   ```
3. 変更提案：**「メッセージに日付を付けて」**

---

## Kiro学習ログ

### 本セッションで学習した内容

#### 1. Vibe（発散的プロトタイピング）
- **体験内容**: TypeScript/ESMでのHello Worldアプリケーション作成
- **学習ポイント**: 
  - 自由な発想での迅速なプロトタイピングが可能
  - package.json、tsconfig.json、ソースコードを一括生成
  - 実行環境まで含めた完全な動作確認
- **実際の成果**: `hello_kiro.ts`とnpm scriptsによる実行可能なアプリケーション

#### 2. Steering（開発ルール統一）
- **体験内容**: `.kiro/steering/structure.md`でコーディング規約とGitワークフローを設定
- **学習ポイント**:
  - プロジェクト全体の開発方針を統一できる
  - 新規生成コードに自動的にルールが適用される
  - Gitコミットガイドラインも含めた包括的な開発標準化
- **設定したルール**:
  - TypeScript型注釈必須
  - `log()`関数経由でのログ出力
  - 構造化されたコミットメッセージ形式

#### 3. Spec（構造化開発プロセス）
- **体験内容**: タスク管理CLI「kiro-todo」の要件定義→設計→実装
- **学習ポイント**:
  - Requirements → Design → Tasks の段階的プロセス
  - 各段階での明示的な承認フロー（userInputツール）
  - タスクの段階的実行と検証による品質担保
- **実装機能**:
  - `npm start add "タスク名"` - タスク追加
  - `npm start list` - 全タスク表示
  - `npm start done 1` - タスク完了
  - JSONファイルでの永続化

#### 4. Hooks（自動化トリガー）
- **体験内容**: ファイル保存時の自動テストファイル生成
- **学習ポイント**:
  - イベントドリブンな開発補助の自動化
  - 保存→AI補助作業の自動実行フロー
  - Execution Historyでの実行ログ確認
- **設定内容**:
  - Event: File Saved (*.ts)
  - Action: 対応する*.test.tsファイルの自動生成

#### 5. MCP（外部知識活用）
- **体験内容**: TypeScript CLIツールのベストプラクティス調査と設計反映
- **学習ポイント**:
  - 外部情報取得→設計反映の一連フロー
  - リアルタイムな知識ベースとの連携
  - プロジェクト改善への実践的活用

#### 6. History（作業履歴管理）
- **体験内容**: 全セッションの作業履歴確認と振り返り
- **学習ポイント**:
  - 全作業の追跡・再現可能性
  - 失敗タスクやエラーの特定
  - 開発プロセスの可視化

### 機能連携の理解
- **Steering + Spec**: 開発ルールに従った構造化実装
- **Hooks + MCP**: 自動化と外部知識の組み合わせ
- **History**: 全機能の実行状況を統合管理

### 実際の開発ワークフローでの活用
1. **プロジェクト開始**: Steeringでルール設定
2. **機能開発**: Specで構造化実装
3. **日常作業**: Hooksで自動化
4. **知識補完**: MCPで外部情報活用
5. **品質管理**: Historyで作業追跡

### 次のステップ
- より複雑なSpecプロジェクトでの実践
- カスタムHooksの作成と運用
- MCP外部ツールとの連携拡張
- チーム開発でのSteering活用
