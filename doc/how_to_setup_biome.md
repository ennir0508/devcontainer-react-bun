# Biome 導入手順

本ドキュメントでは、Bun 環境のプロジェクトに高速なフォーマッター兼リンターである **Biome** を導入する手順について記載します。

## 導入手順

### ステップ 1: パッケージのインストール

以下のコマンドを実行し、Biome を開発用依存関係としてインストールします。バージョンを固定するために `--exact` フラグを使用することが推奨されています。

```bash
bun add --dev --exact @biomejs/biome
```

### ステップ 2: 初期化

以下のコマンドを実行して、設定ファイル `biome.json` を生成します。

```bash
bunx --bun biome init
```

### ステップ 3: ESLint からの移行 (必要な場合)

既存の ESLint 設定を Biome に移行する場合は、以下のコマンドを実行します。これにより、ESLint の設定を解析し、可能な限り Biome の設定に反映させます。

```bash
bunx --bun biome migrate eslint --write
```

## 実行方法

導入後は以下のコマンドで、プロジェクト全体のフォーマットチェックとリントを実行できます。

```bash
bunx biome check .
```

自動修正を適用したい場合は `--write` (または `--apply`) を付与します。

```bash
bunx biome check --write .
```