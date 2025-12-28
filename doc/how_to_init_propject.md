# 開発環境構築手順

本ドキュメントでは、DevContainer を用いた React + Bun 開発環境の構築手順について記載します。
本手順では、既存のリポジトリをクローンするのではなく、新規にアプリケーションを作成する流れを解説します。

## 1. 前提条件

以下のソフトウェアがインストールされていることを確認してください。

*   [Docker Desktop](https://www.docker.com/products/docker-desktop/)
*   [Visual Studio Code](https://code.visualstudio.com/)
*   [Dev Containers (VS Code Extension)](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## 2. 構築手順

### ステップ 1: プロジェクトフォルダの準備

VS Code で空のプロジェクトフォルダを開きます。

![空のプロジェクトフォルダを開いたVS Code](img/00_start.png)

### ステップ 2: Dev Container 設定の追加

コマンドパレット (`F1` または `Ctrl+Shift+P`) を開き、**Dev Containers: Add Dev Container Configuration Files...** を選択します。

 ![コマンドパレットでDev Containers設定追加を選択](img/01_add_dev_container.png) 

ワークスペースに設定を追加します。

 ![ワークスペースに設定を追加](img/02_add_to_workspace.png) 

### ステップ 3: コンテナイメージの選択

ベースとなるイメージ定義を選択します。ここでは **Bun** を検索して選択します。

 ![コンテナイメージ定義でBunを選択](img/03_select_image_bun.png) 

Bun のイメージ のバージョンを選択します（例: `debian` や `alpine` など）。

 ![Bunのバージョン選択](img/04_select_bun_version.png) 

### ステップ 4: 機能 (Features) の追加

コンテナに追加インストールするツール（Features）を選択します。

 ![追加機能(Features)の選択画面](img/05_select_tools.png) 

Git などを選択し、OK を押します。（任意）

 ![Git機能の選択](img/05-1_select_tools_git.png) 

設定を確定します。

 ![設定の確定](img/06_select_config.png) 

`.devcontainer` フォルダと `devcontainer.json` が生成されます。

 ![生成されたdevcontainer設定ファイル](img/07_generated_devcontainer_config.png) 

### ステップ 5: コンテナで開く

右下の通知やコマンドパレットから **Dev Containers: Reopen in Container** を実行し、コンテナをビルド・起動します。

 ![コンテナで再度開く(Reopen in Container) ](img/08_start_container.png) 

起動が完了すると、VS Code 左下のステータスバーに接続状態が表示されます。

 ![コンテナ接続状態のステータスバー](img/09_connected_container.png) 

### ステップ 6: React アプリの作成 (Vite)

コンテナ内のターミナルで以下のコマンドを実行し、Vite を使用して React アプリを作成します。

```bash
bun create vite
```

最後の質問で `Install with bun and start now?` の質問に `Yes` を回答すると、Bunによるインストールと起動が同時に実行されます。しかし、この時点ではアプリが動かせないと思うので、インストール完了後に `Ctrl + C` で停止します。 

 ![bun create viteコマンドの実行結果](img/10_create_vite.png) 

### ステップ 7: 設定の調整

必要に応じて `package.json` の `scripts` を編集します（例: ホストからのアクセスを許可するために `--host` オプションを追加するなど）。

```json
{
  ...
  "scripts": {
    "dev": "vite --host", // ← `--host` を追加
    "build": "tsc -b && vite build",
    "lint": "eslint .",
    "preview": "vite preview"
  },
  ...
}
```

### ステップ 8: 依存関係のインストールと起動

作成したプロジェクトフォルダに移動し、依存関係をインストールしてから開発サーバーを起動します。

```bash
cd my-app
bun run dev
```

 ![bun run devによる開発サーバー起動](img/11_bun_run_dev.png) 

> Tips: 今後、ディレクトリを移動しなくてもいいように、 `my-app` 内のすべてのファイルをプロジェクト直下に移動するか、 Dev Container 起動時の WORKDIR を `my-app` にするとよい。

### ステップ 9: 動作確認

ブラウザでローカルサーバー（例: `http://localhost:5173`）にアクセスし、React アプリが表示されることを確認します。

 ![ブラウザでのReactアプリ表示確認](img/12_open_browser.png)

また、 `/my-app/src/App.tsx` を修正すると、自動反映されます。