# Kiro Hands-on Starter

## 概要
Kiro を使って「最小の生成→実行→確認」を通して学習するスターター。目的は **AIに何を渡すと何が返るか** を短時間で把握すること。

## 前提
- Node.js 18+ / npm
- Kiro（インストール・ライセンス済み）

## セットアップ
```bash
# 新しいプロジェクトフォルダを作成
mkdir hello-kiro-tutorial
cd hello-kiro-tutorial

# Gitリポジトリとして初期化
git init
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

## 学習フロー

# Kiro Learning Flow (Hello → 基礎運用)

## 0. 場づくり（5分）
- 新しいプロジェクトフォルダを作成してGit初期化（上記セットアップ参照）
- Kiro 起動 → 作成した `hello-kiro-tutorial` フォルダを開く
- チャット起動（Cmd/Ctrl+L）

## 1. Hello（最小生成→実行）
- プロンプト：
  「`hello_kiro.ts` を作って `console.log('Hello, Kiro')` を出し、`npm start` を用意」
- 実行：`npm start` → 出力確認

## 2. 変更→履歴を読む
- 依頼：「メッセージに日付を付けて」
- Kiro の *Execution History* で「何が変わったか」を確認

## 3. コンテキスト指定の練習
- `#current`：「#current このファイルの役割を3行で要約」
- `#codebase`：「#codebase ログ出力箇所を列挙」
- `#problems`：「#problems 3件とも修正案をパッチで」

## 4. Steering（恒常ルールを1行）
- Kiro パネル → Generate Steering Docs
- `.kiro/steering/structure.md` に 1 行追加例：
  「ソースは拡張子 `.ts` を使用」

## 5. Spec（超ミニ体験）
- 一文要求：「コンソールに “Hello, Kiro v2” を出すだけ」
- 自動生成の Tasks の先頭だけ **Execute** → 実行確認

## 6. Hook（保存トリガ1本）
- Agent Hooks → 新規作成
  - Event: File Saved / Pattern: `src/**/*.ts`
  - Instruction: 「保存時に対応する `*.test.ts` を作成・更新し基本の期待を1件追加」
- `src/foo.ts` を保存 → 自動生成を確認

## 7. MCP（外部情報の取り込み最小）
- MCP 設定で `fetch` を有効化
- 「#mcp 型安全なログ出力のベストプラクティスを要約」

## 8. 学習内容の言語化
- 依頼：「本プロジェクトの README 用に、本日の学習ポイント（チャット/履歴/コンテキスト/steering/spec/hook/mcp）を箇条書きで生成」

## 9. つまずき時のチェック
- Node/npm/ts-node の有無とバージョン
- `package.json` の `"start"`
- Kiro 再起動とプロジェクトの開き直し
