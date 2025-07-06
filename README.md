# copytorepo
リポジトリをまたいでビルド済みのファイル例えば`/dist`フォルダなどをコピーするためのアクション

## 🔐 GitHub Actions シークレット設定ガイド

このワークフローでは、`dist/` の内容を別リポジトリの特定ディレクトリに同期し、Pull Request を作成します。  
そのために以下のシークレットを GitHub リポジトリに設定する必要があります。

## 🚀 GitHub Actions ワークフロー設定（同期 & PR 作成）

### 📁 推奨フォルダ構成

```text
your-project/
├── .github/
│   └── workflows/
│       └── sync.yml     ← このファイルをここに配置
├── dist/                ← デプロイ対象のビルド成果物
├── ...
```

---


### 🧾 必要なシークレット一覧

| シークレット名   | 用途                                                             | 記入例 / 設定方法                                                                 |
|------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------|
| `GH_PAT`         | ターゲットリポジトリへのアクセスに使用する Personal Access Token（PAT） | GitHub の [Developer Settings > Personal access tokens](https://github.com/settings/tokens) から発行<br>**必要スコープ**: `repo` |
| `TARGET_REPO`    | ターゲットリポジトリの `ユーザー名/リポジトリ名` 形式                     | 例：`shotanet/tools-shotanet.info`                                              |
| `TARGET_DIR`     | ターゲットリポジトリ内で `dist/` の内容を同期するサブディレクトリパス     | 例：`src/nanaseg`（ルート直下に置く場合は空文字や `.`）                          |
| `TARGET_BRANCH`  | ターゲットリポジトリの変更対象ブランチ                                  | 例：`develop` や `main`                                                         |

---

### ⚙️ シークレットの登録手順

1. GitHub 上で対象リポジトリを開く
2. 上部メニューから「**Settings**」をクリック
3. 左メニューの「**Secrets and variables > Actions**」を選択
4. 「**New repository secret**」ボタンをクリック
5. 上記のシークレット名と値を1つずつ登録

---

### ✅ 例：`TARGET_REPO` の設定

| 項目           | 値                              |
|----------------|----------------------------------|
| シークレット名 | `TARGET_REPO`                   |
| 設定値         | `shotanet/tools-shotanet.info`  |

---

必要に応じてこのドキュメントを `.github/README.md` や `docs/deploy.md` に保存しておくと便利です。
