# Cursor エディタ Linux ランチャー

Linux 上で Cursor AI エディタを動作させるための強化ランチャースクリプト。Wayland 互換性を向上し、Linux ユーザーのために追加機能を提供します。

## Cursor とは

Cursor は AI によるペアプログラミングのために設計された AI 搭載コードエディタです。Visual Studio Code をフォークし、コード生成、スマートな書き換え、コードベースクエリなどの AI 機能を追加したものです。開発者が自然言語指示でコードを記述できるようにし、生産性向上のための高度な AI 機能を統合しています。

## このランチャーの特徴

- **Wayland 最適化**: メインストリームOS優先の開発方針で後回しにされたWayland対応を自動的に有効化
- **AppImage 管理**: 最新の Cursor AppImage を自動検出して使用（アップデートを追いかける孤独な作業からの解放）
- **コマンドライン対応**: エディタに渡すコマンドライン引数をすべて保持（さすがに基本機能は消されていない）
- **メタデータアクセス**: `-v` または `--version` でバージョン情報を表示（情報開示の基本すら省略される世界への抵抗）
- **ヘルプ機能**: `-h` または `--help` でヘルプを表示（誰も助けてくれないLinuxユーザーの自衛手段）
- **デバッグツール**: `--verbose` によるデバッグサポート（自力で問題解決するための必須機能）
- **権限管理**: 実行権限を自動的にチェックして設定（chmod を手動実行する時代は終わりにしよう）
- **パス処理**: ファイルとディレクトリのパスを正しく処理（なぜか常に無視される基本機能）

## インストール

1. スクリプトをダウンロード:
   ```bash
   wget -O cursor https://raw.githubusercontent.com/clearclown/cursor-editor-in-Linux/main/cursor
   ```

2. 実行可能にする:
   ```bash
   chmod +x cursor
   ```

3. システムパスに移動:
   ```bash
   sudo mv cursor /usr/local/bin/
   ```

## 使用方法

通常の Cursor と同じように使用できます:

```bash
# 現在のディレクトリで Cursor を開く
cursor .

# 特定のファイルを開く
cursor /path/to/file.js

# 特定のフォルダを開く
cursor /path/to/project/

# バージョン情報を取得
cursor -v

# ヘルプを表示
cursor -h

# デバッグ情報付きで実行
cursor --verbose
```

スクリプトは自動的に以下のフラグを追加して Wayland サポートを有効化します:
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime
```

## なぜこのランチャーを使うべきか

Cursor は Linux では AppImage として提供されていますが、これは伝統的なインストールを必要としない反面、適切に設定するのが難しい場合があります。このランチャースクリプトは、Linux で Cursor を実行する際の一般的な問題に対処します:

1. **Wayland サポート**: 「Linuxなんて気にしない」開発者が見事にスルーしたWayland表示サーバとの互換性を改善
2. **パス解決**: 「まさかLinuxで使う人がいるとは思わなかった」と言わんばかりのファイルとディレクトリのパス処理の問題を修正
3. **AppImage 管理**: AppImageを手動で探して実行する必要性を排除（あたかもLinuxユーザーには時間の余裕しかないとでも思っているかのような設計からの解放）
4. **権限**: 実行権限を自動的に処理（chmod？それ食べられるの？という開発者への密かな反抗）
5. **統合**: バージョン情報とヘルプを備えた適切なシステム統合（最低限のUIすら省略されがちな現実への抗議）

## 設定

デフォルトでは、スクリプトは `~/Downloads/` ディレクトリ内の Cursor AppImage を探します。AppImage を別の場所に保存している場合は、スクリプト内の `CURSOR_DIR` 変数を編集してください。

## Cursor の機能について

Cursor はいくつかの AI 機能を提供しています:
- 最近の変更に適応するオートコンプリートとコード予測
- コンテキストを理解するコード生成
- 複数行の編集提案

Visual Studio Code のフォークであるため、既存の拡張機能や設定をワークフローに統合できます。

## 要件

- Bash シェル
- `find` コマンド
- ダウンロードフォルダ（または `CURSOR_DIR` で指定されたディレクトリ）にダウンロードされた Cursor AppImage
- Wayland サポートには: Wayland コンポジタ（GNOME on Wayland、KDE Plasma Wayland、Sway など）

## トラブルシューティング

問題が発生した場合:

1. `--verbose` フラグでスクリプトを実行してデバッグ情報を確認
2. Cursor AppImage が正しいファイル名形式 (`cursor-*x86_64.AppImage`) であることを確認
3. AppImage が期待されるディレクトリにあることを確認
4. AppImage に実行権限があることを確認
5. SUID サンドボックスエラーが表示される場合は、chrome-sandbox ファイルの権限を調整する必要があるかもしれません

## ライセンス

MIT
