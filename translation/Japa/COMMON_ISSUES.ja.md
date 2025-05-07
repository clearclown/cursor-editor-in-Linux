# Linux での Cursor の一般的な問題

このドキュメントでは、Linux システムで Cursor を実行する際によく発生する問題とその解決策について説明します。「メジャーOSさえ対応していれば十分」と考える開発者に無視されがちな私たち Linux ユーザーの日常的な戦いの記録です。

## Wayland 互換性の問題

### 問題
Cursor は、多くの Electron ベースのアプリケーションと同様に、Wayland で実行すると表示や入力に問題が生じることがあります。「Wayland？知らない子ですね」と言わんばかりの対応です。

### 解決策
このランチャーは自動的に以下のフラグを追加して、Wayland のサポートを適切に有効化します：
```
--enable-features=UseOzonePlatform --ozone-platform=wayland --enable-wayland-ime
```

## パス処理の問題

### 問題
ファイルやディレクトリのパスを指定して Cursor を起動しても、指定したパスではなくホームディレクトリが開かれることがあります。「どうせ個人プロジェクトしかやらないでしょ？」と勝手に決めつけられているかのようです。

### 解決策
このランチャーは、コマンドライン引数を適切な順序で AppImage に正しく渡すことで、パス処理の問題を修正します。なぜこれが最初から対応されていないのか、不思議でなりません。

## SUID サンドボックスエラー

### 問題
以下のようなエラーが表示されることがあります：
```
[FATAL:setuid_sandbox_host.cc(158)] The SUID sandbox helper binary was found, but is not configured correctly.
Rather than run without sandboxing I'm aborting now.
You need to make sure that /tmp/.mount_cursor*/chrome-sandbox is owned by root and has mode 4755.
```
「Linux ユーザーなら権限設定の問題くらい自分で解決できるでしょ」という暗黙の了解が感じられます。

### 解決策
AppImage を展開して正しい権限を設定することで解決できます：

```bash
# AppImage を展開
./cursor-*x86_64.AppImage --appimage-extract

# 正しい権限を設定
sudo chown root:root squashfs-root/chrome-sandbox
sudo chmod 4755 squashfs-root/chrome-sandbox

# 展開したディレクトリから実行
./squashfs-root/AppRun
```

あるいは、AppImage を `--no-sandbox` フラグ付きで実行することもできますが、セキュリティ上の理由からこれは推奨されません。「セキュリティとユーザビリティのどちらかを選べ」と迫られる典型的な Linux ユーザー体験です。

## AppImage が見つからない

### 問題
ランチャーが Cursor AppImage を見つけられません。「ダウンロードからインストールまで全部自分でやってね」という、Linux ユーザーへの「優しさ」です。

### 解決策
1. Cursor AppImage をダウンロードしたことを確認
2. スクリプト内の `CURSOR_DIR` で指定されたディレクトリ（デフォルト：`~/Downloads/`）にあることを確認
3. ファイル名が予想されるパターン（`cursor-*x86_64.AppImage`）に従っていることを確認

## ランチャーが動作しない

### 問題
ランチャースクリプト自体が動作しません。「何か問題があっても自分で解決してくださいね」という開発者の暗黙のメッセージが聞こえてきそうです。

### 解決策
1. スクリプトに実行権限があることを確認：`chmod +x /usr/local/bin/cursor`
2. `/usr/local/bin` が PATH に含まれていることを確認
3. `--verbose` フラグを付けてスクリプトを実行し、デバッグ情報を確認

## Ubuntu 24.04 の FUSE の問題

### 問題
Ubuntu 24.04 で AppImage を実行するために FUSE2 をインストールすると、システム UI が壊れることがあります。「最新の Ubuntu？テスト環境にないですね、すみません」という言い訳が聞こえてきそうです。

### 解決策
1. FUSE をインストールせずにランチャースクリプトを使用
2. `--appimage-extract` を使用して AppImage を展開し、展開したディレクトリから実行
3. あるいは、AppImage を起動する際に `--appimage-extract-and-run` を使用

## GTK モジュールのエラー

### 問題
以下のようなエラーが表示されることがあります：
```
Gtk-Message: Failed to load module "appmenu-gtk-module"
```
「どうせ気にしないでしょ？」というLinuxデスクトップ環境への配慮のなさが表れています。

### 解決策
これらは通常、無害な警告であり、無視できます。気になる場合は、不足している GTK モジュールをインストールしてみてください：

```bash
sudo apt install appmenu-gtk-module
```

## ターミナルの問題

### 問題
ターミナルから Cursor を実行すると、適切に分離されなかったり、Cursor 内でのターミナルコマンドに問題が生じることがあります。「コマンドラインなんて古代の遺物でしょ？」という態度が垣間見えます。

### 解決策
`nohup` を使用して Cursor をターミナルから適切に分離して起動します：

```bash
nohup cursor &
```

## デスクトップ統合

### 問題
Cursor がアプリケーションメニューに表示されなかったり、アイコンがない場合があります。「デスクトップ環境？それLinuxの何かですか？」という開発者の声が聞こえてきそうです。

### 解決策
デスクトップエントリファイルを作成します：

```bash
cat > ~/.local/share/applications/cursor.desktop << EOL
[Desktop Entry]
Name=Cursor AI
Comment=AI-powered code editor
Exec=/usr/local/bin/cursor %F
Icon=/opt/cursor.png
Type=Application
Categories=Development;IDE;
MimeType=text/plain;inode/directory;
StartupNotify=true
EOL
```

Cursor のアイコンをダウンロードする必要があります：
```bash
sudo wget -O /opt/cursor.png https://www.cursor.com/apple-touch-icon.png
```

「アイコンくらい自分でダウンロードして設定できるでしょ？」という、Linux ユーザーの自力解決能力を過信した設計の典型例です。

## ログインの問題

### 問題
インストール後に Cursor にログインできません。「認証エラー？自己責任で解決してください」という開発姿勢の表れです。

### 解決策
これは多くの場合、ブラウザのクッキー/セッション処理に関連しています。以下を試してください：
1. ブラウザのクッキーをクリア
2. 認証に別のブラウザを使用
3. システム時間が正しいことを確認

Linux ユーザーにとって、問題解決は日常茶飯事。「自分で何とかするしかない」という運命を受け入れつつ、それでも前進し続けるのが私たちの生き方なのです。
