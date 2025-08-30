# Kiro Learning Flow（Vibe → Steering → Spec → Tasks → Hooks → MCP）
> **目的**: Kiro固有のUI/エージェント挙動を"触って理解"します。VSCode相当の操作は最小限にし、Kiroで何を指示すると何が起きるかを明確化します。  
> **凡例**: **[K] = Kiro操作**, **[C] = 共通操作（Node/npmや一般的IDEでも同様）**

## 前提条件・事前準備
### 必要なソフトウェア
以下がインストール済みであることを確認してください：

- **Node.js** (v18以上推奨)
  ```bash
  node --version  # v18.0.0以上
  npm --version   # 9.0.0以上
  ```
- **Git**
  ```bash
  git --version   # 2.30.0以上推奨
  ```
- **Kiro IDE** (最新版)

### 動作確認方法
各セクション完了後、以下で動作確認を行ってください：
※ 以下の npm script は生成内容により存在しない場合があります。存在しなければスキップしてください。

**基本動作確認**：
```bash
cd hello-kiro-tutorial
npm start --help    # ヘルプ表示
npm start add "テスト"  # タスク追加
npm start list       # タスク一覧
npm start done 1     # タスク完了
```

**テスト実行**：
```bash
npm test            # 単体テスト実行
npm run test:coverage  # カバレッジ付きテスト
```

**ビルド確認**：
```bash
npm run build       # TypeScriptコンパイル
npm run clean       # ビルド成果物削除
```

### トラブルシューティング（事前確認）
- **Node.js/npmが古い場合**: 最新LTS版にアップデート
- **権限エラー**: `sudo`を使わず、Node.jsをユーザー権限でインストール
- **Gitが未設定**: `git config --global user.name/user.email`を設定
- **Kiro IDEが起動しない**: 最新版にアップデート、またはサポートに問い合わせ

---

## 0. 環境づくり（5分）
### プロジェクトフォルダの準備
- [C] ターミナルで新しいプロジェクトフォルダを作成：
  ```bash
  mkdir hello-kiro-tutorial
  cd hello-kiro-tutorial
  ```
- [C] Gitリポジトリとして初期化：
  ```bash
  git init
  git config user.name "Your Name"
  git config user.email "your.email@example.com"
  ```
- [C] `.gitignore`ファイルを作成：
  ```bash
  echo "node_modules/
  *.js
  *.js.map
  .DS_Store
  dist/" > .gitignore
  ```
- [K] **Open Project** で作成した `hello-kiro-tutorial` フォルダを開く  
- [K] **Chat** を開く（Cmd/Ctrl+L）

---

## 1. Vibe：発散で最小生成→実行→履歴確認（10分）
1. [K] **新規チャットセッション**で **Vibe** を選択  
2. [K] 入力（そのまま貼り付け可）：  
   ```
   注意: hello-kiro-tutorialディレクトリで作業してください。
   
   TypeScript/ESMで `hello_kiro.ts` を作成し、 `console.log("Hello, Kiro")` を出力。
   実行用に `npm start` を用意して、動くところまで通す。
   ```
3. [K] Kiroが提案したファイル作成・更新内容を**チャット出力で確認**  
  **出力例**
   - `package.json`: ESMモジュール設定とnpm scripts
   - `tsconfig.json`: TypeScript設定（ES2022、ESNext）
   - `hello_kiro.ts`: TypeScript型注釈付きのソースコード
4. [K] 提案内容を確認後、**実行ボタン**をクリックして適用  
5. [K] 生成されたアプリケーションを**実行ボタン**で指示通りに実行し、動作確認：
   - `npm install` → 依存関係インストール
   - `npm run build` → TypeScriptコンパイル
   - `npm start` → アプリケーション実行
6. [K] Kiroの Run/Terminalで `Hello, Kiro` の出力を確認
7. [C] 初回コミットを作成：
  ```bash
  git add .
  git commit -m "feat: initial Hello Kiro implementation"
  ```

※ Vibeの目的は「簡単な指示 → Kiroが自動生成・実行 → 履歴で変更内容を確認」の流れで、Kiroが何をしたかを素早く把握すること。

---

## 2. Steering：前提ルールを入れて効果を確認（8分）
1. [K] **Steering → Generate Steering Docs** を実行（`.kiro/steering/{product.md, tech.md, structure.md}` が生成）
2. [K] Steeringルールを適切に分けて設定：
   - `structure.md` に以下のコーディング規約を追記：
     ```
     コーディング規約：
     - すべてのソースコードは拡張子 `.ts` を使用する
     - ログ出力は `console.log` ではなく `log()` 関数経由で行う
     - 関数には必ず TypeScript 型注釈を付ける
     ```
   - `product.md` に以下のGitワークフローを追記：
     ```
     Gitワークフロー：
     - コミットメッセージはタイトル+ボディ形式
     - タイトル: `feat: complete task [番号] - [概要]`
     - ボディ: 各サブタスクの詳細を箇条書き
     - git diffは `git --no-pager diff` を使用してページャー回避
     - Kiroの自動フォーマット後は必ず `git add .` を再実行
     ```
3. [K] チャットで**新しいファイル作成**を依頼：  
   ```
   `utils.ts` を作成して、現在時刻を返す `getCurrentTime()` 関数とログ出力する `logTime()` 関数を実装して
   ```
4. [K] 生成されたコードが Steering ルールに従っているか確認：
   - `.ts` 拡張子 ✓
   - `log()` 関数使用 ✓  
   - 型注釈付き ✓

**チェックポイント**  
- ルール違反のコードを依頼しても、Kiroがルールに従って修正することを体感できたか
- Steeringルール（コーディング規約）が新規生成コードに自動適用されることを確認できたか
- Gitワークフローガイドラインが今後のタスク実行で参照されることを確認できたか
- [C] Steeringルール適用後の変更をコミット：
  ```bash
  git add .
  git commit -m "feat: add steering rules and utils implementation"
  ```

---

## 3. Spec：構造化された開発プロセス（18分）
1. [K] **新規チャットセッション**で **Spec** を選択  
2. [K] チャットで要件を**具体的に**入力：  
   ```
   注意: hello-kiro-tutorialディレクトリで作業してください。
   hello-kiro-tutorial/.kiro/specs/kiro-todoディレクトリにSpecを作成してください。
   
   タスク管理CLI「kiro-todo」を作成：
   - `npm start add "タスク名"` でタスク追加
   - `npm start list` で全タスク表示  
   - `npm start done 1` でタスク完了
   - データはJSONファイルで永続化
   - 不正な引数は使用方法を表示して終了コード1
   ```

3. [K] **Specワークフローの対話的承認**：
   Kiroは以下の順序で各ドキュメントを作成し、承認ダイアログ（確認プロンプト）で明示的に承認を求めてきます：
   
   **Step 1: Requirements**
   - Kiroが `requirements.md` を作成
   - 承認ダイアログ（確認プロンプト）で「要件ドキュメントを確認してください」などと表示される
   - → 「yes」「approve」「looks good」等の明確な承認が必要
   
   **Step 2: Design**  
   - Kiroが `design.md` を作成
   - 承認ダイアログ（確認プロンプト）で「設計ドキュメントを確認してください」などと表示される
   - → 明確な承認が必要（フィードバックがあれば修正→再承認のサイクル）
   
   **Step 3: Tasks**
   - Kiroが `tasks.md` を作成（タスクステータス記号：`[ ]`未開始、`[-]`進行中、`[x]`完了）
   - 承認ダイアログ（確認プロンプト）で「実装計画を確認してください」などと表示される
   - → 明確な承認でSpec完成

4. [K] **tasks.mdを開き、タスクを順次実行**：

   **実行手順**：
   - `hello-kiro-tutorial/.kiro/specs/kiro-todo/tasks.md` を開く
   - 最初の未完了タスクの横にある **「Start task」ボタン** をクリック
   - **重要**: 環境や指示内容により**複数タスクが連鎖実行される場合がある**ため、必要なら Steering に「一度に1タスクのみ実行」を追記してください。
   - Kiroがタスクを実行完了後、以下を確認：
     - コードが正常に動作するか
     - 要件を満たしているか  
     - エラーが発生していないか
     - tasks.mdでタスクステータスが正しく更新されているか（`[ ]` → `[-]` → `[x]`）
   - [C] **各タスク完了後にコミット**（重要：一度に複数タスクを実装してしまう問題の対策）：
   - タスク完了都度、手動で実行する必要あり
   - 推奨するがスキップ可能
   - **Gitワークフロー**：
     ```bash
     cd hello-kiro-tutorial
     git add .
     git status  # ステージングされたファイルを確認
     git --no-pager diff --cached  # 変更内容を確認（ページャー回避）
     git commit -m "feat: complete task [番号] - [概要]
     
     - [番号]: 具体的な実装内容の説明"
     ```
     例: 
     ```bash
     git commit -m "feat: complete task 1.1 - setup project structure
     
     - 1.1: Create src directory structure with interfaces, storage, business, cli folders and define core TypeScript interfaces"
     ```
   - **注意**: Kiroの自動フォーマット後は必ず `git add .` を再実行
   - 次のタスクに進む

   **動作確認方法**：
   - hello-kiro-tutorialディレクトリで以下を実行：
     ```bash
     # 基本動作確認
     npm start add "サンプルタスク"  # タスク追加
     npm start list               # 一覧表示
     npm start done 1             # タスク完了
     npm start list               # 完了状態確認
     
     # エラーケース確認
     npm start                    # 引数なし（使用方法表示）
     npm start invalid            # 不正コマンド（エラー表示）
     npm start done 999           # 存在しないID（エラー表示）
     ```
   - 期待される出力や動作を確認
   - テストがある場合は `npm test` を実行

   **問題が発生した場合**：
   - **軽微な修正**: Kiroに直接修正を依頼
   - **要件の問題**: `hello-kiro-tutorial/.kiro/specs/kiro-todo/requirements.md` を修正 → `design.md` を更新 → `tasks.md` を再生成
   - **設計の問題**: `hello-kiro-tutorial/.kiro/specs/kiro-todo/design.md` を修正 → `tasks.md` を再生成
5. [K] 最終的に全コマンドが動作することを確認
6. [C] 全タスク完了後の最終コミット：
   ```bash
   cd hello-kiro-tutorial
   git add .
   git commit -m "feat: complete kiro-todo CLI implementation"
   ```

**チェックポイント**  
- 要件→設計→実装の**構造化されたプロセス**を体験できたか
- タスクの**段階的実行と検証**により品質を担保できたか
- Specの**反復改善**で要件のズレを修正できたか
- [C] 完成したkiro-todoをコミット：
  ```bash
  git add .
  git commit -m "feat: complete kiro-todo CLI implementation"
  ```

**重要**: この時点で一度コミットを実行してください。Specプロセスの完了を記録し、次のHooksセクションに進む前に作業を保存します。

---

## 4. Hooks：自動化トリガーの体験（8分）

**Agent Hooksとは？**  
ファイル保存やボタンクリックなどのイベントが発生したときに、Kiroが自動的にタスクを実行する機能です。例えば「TypeScriptファイルを保存したら、自動でテストファイルを作成する」といった自動化が可能です。

**Agent Hooksの場所と設定方法：**

1. [K] **左サイドバーのKiroパネル**（ファイル一覧が表示されている場所）を確認
2. [K] **Agent Hooks**セクションを探す（ファイルツリーの下部にあります）
3. [K] **+ 新規作成**ボタンをクリック

**見つからない場合の代替方法：**
- [K] **コマンドパレット**（Cmd+Shift+P / Ctrl+Shift+P）を開く
- [K] 「Open Kiro Hook UI」と入力して実行

**Hook設定内容（以下をそのまま入力してEnterを押すと、次画面で各項目に分解されます）：**
```
Event: File Saved
Pattern: src/**/*.ts
Instruction: 保存されたファイルに対応する *.test.ts を作成/更新し、基本的なテストケースを1つ追加
```
4. [K] srcディレクトリ配下に新規ファイル `math.ts` を作成して簡単な関数を実装：
   ```typescript
   export function add(a: number, b: number): number {
     return a + b;
   }
   ```
5. [K] ファイル保存 → 自動で `math.test.ts` が生成されることを確認
6. [K] **Execution History**でHookの実行ログを確認
   - 右ペインのKiroパネル内「History」セクションを開く
   - Hook実行時の"Execute hook"ログとステータスを確認

**チェックポイント**  
- **保存→AIが補助作業を自動実行** する流れを体感できたか
- Hookの実行結果が期待通りか、履歴で確認できたか
- [C] Hook生成されたテストファイルをコミット：
  ```bash
  git add .
  git commit -m "feat: add automated test generation via hooks"
  ```

---

## 5. MCP：外部知識の活用（10分）
1. [K] **MCP 設定**で利用可能なツールを確認・有効化  
   ```
   MCPを有効にしてください
   ```
2. [K] Specチャットで外部情報を活用した依頼：  
   ```
   TypeScriptのCLIツール開発におけるエラーハンドリングのベストプラクティスを調査し、
   現在のプロジェクトに適用できる改善案をdesign.mdに追記して
   ```
3. [K] MCP経由で取得した情報の要約と、設計への反映案を確認
4. [K] 提案されたdesign.mdの変更を**差分プレビュー→適用**
   ※チュートリアルでは、この変更点の実装はスキップして構いません。

**チェックポイント**  
- MCP経由の**外部情報取得→設計反映**の一連の流れを体験できたか
- 取得した情報が実際のプロジェクト改善に活用されたか

---

## 6. 統合：学習内容の整理とドキュメント化（5分）
1. [K] Vibeチャット：  
   ```
   本セッションで学習した内容（Vibe/Steering/Spec/Hooks/MCP/History）を
   整理して、プロジェクトのREADME.mdに「Kiro学習ログ」として追記
   ```
2. [K] 生成された学習ログの内容を確認・承認
3. [K] **右ペインのHistory** で全セッションの作業履歴を最終確認

**チェックポイント**  
- 各機能の**役割と連携**を理解できたか
- 実際の開発ワークフローでの活用イメージが掴めたか
- [C] 学習ログを含む最終コミット：
  ```bash
  git add .
  git commit -m "docs: add Kiro learning log and project documentation"
  ```
- [C] 必要に応じてGitHubリポジトリを作成してpush：
  ```bash
  git remote add origin https://github.com/{yourusername}/hello-kiro-tutorial.git
  git push -u origin main
  ```

---

## 7. トラブルシュート（優先度順）
### Kiro固有の問題
- [K] **Execution History** にエラーが出ていないか（失敗タスク/コマンド）  
- [K] **Specの受入基準**と**実出力**が一致しているか（ズレはSpec修正で収束）  
- [K] **Steering ルール**が正しく適用されているか（新規生成コードで確認）
- [K] **Hooks/MCPの設定有効化**（disabled設定のままになっていないか）  
- [K] **承認ダイアログ（確認プロンプト）**で承認待ちになっていないか（明確な「yes」「approved」が必要）
- [K] **タスクステータス**が正しく更新されているか（tasks.mdで`[ ]` → `[-]` → `[x]`の流れ）

### 共通的な問題
- [C] **Node.js/npm/TypeScript**が存在・適切なバージョンか  
  ```bash
  node --version && npm --version && npx tsc --version
  ```
- [C] **package.json**の`"start"`が実行可能か（`npm start`で直接検証）
- [C] **ファイルパス**や権限の問題がないか
- [C] **依存関係**が正しくインストールされているか（`npm install`を再実行）
- [C] **TypeScriptコンパイル**エラーがないか（`npm run build`で確認）

### 実行時エラーの対処法
**「command not found」エラー**：
```bash
# Node.js/npmの再インストール
# macOS: brew install node
# Windows: 公式サイトからインストーラーをダウンロード
```

**「permission denied」エラー**：
```bash
# npmのグローバルディレクトリを変更
npm config set prefix ~/.npm-global
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

**「module not found」エラー**：
```bash
# 依存関係の再インストール
rm -rf node_modules package-lock.json
npm install
```

**Gitコミットエラー**：
```bash
# Gitユーザー情報の設定
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

---

### 付録：機能の境界と使い分け
**Kiro固有機能**：
- **Vibe**: 自由な発想での迅速なプロトタイピング
- **Spec**: 構造化された要件定義→設計→実装プロセス  
- **Steering**: プロジェクト全体の開発方針・ルール統一
- **Hooks**: 開発作業の自動化・補助
- **MCP**: 外部知識・ツールとの連携
- **Execution History**: 全作業の追跡・再現

**共通操作**：ファイルの直接編集/保存、Node/npmの実行、Git操作など（ただしKiroのUI経由でも実行可能）

---

### 付録：よく使うキーボードショートカット
**Kiro固有操作**：
- `Cmd/Ctrl + L`: チャット画面を開く
- `Cmd/Ctrl + I`: インライン補完・提案を表示
- `Cmd/Ctrl + Shift + P`: コマンドパレット（「Open Kiro Hook UI」「MCP」等で検索）
- `Cmd/Ctrl + Shift + E`: エクスプローラー（ファイルツリー）にフォーカス
- `Cmd/Ctrl + Shift + G`: ソース管理パネル（Git操作）※動作しない場合はターミナルやコマンドパレット経由で
- `Cmd/Ctrl + Shift + X`: 拡張機能パネル

**共通IDE操作**：
- `Cmd/Ctrl + S`: ファイル保存（Hooks発火のトリガー）
- `Cmd/Ctrl + N`: 新規ファイル作成
- `Cmd/Ctrl + O`: ファイルを開く
- `Cmd/Ctrl + W`: タブを閉じる
- `Cmd/Ctrl + Shift + N`: 新規ウィンドウ
- `Cmd/Ctrl + ,`: 設定画面

**効率的なワークフロー**：
1. `Cmd/Ctrl + L` でチャット開始
2. コード生成・修正を依頼
3. `Cmd/Ctrl + S` で保存（Hooks自動実行）
4. `npm start` 等で動作確認
5. `git add . && git commit -m "..."` でコミット