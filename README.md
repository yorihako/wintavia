# Wintavia

Word・Excel・PowerPoint で開いている文書を、画面の左の細いタブバーにまとめて表示し、クリックで切り替えられる Windows アプリです。

*English follows Japanese.*

## できること

- 開いている Word・Excel・PowerPoint の文書を、アプリやウィンドウをまたいで 1 本のタブバーに並べる
- マウスを乗せると文書名が読める幅に広がる（幅はドラッグで調整）
- お気に入り・履歴から文書を開く、右クリックでフォルダを開く・パスのコピー・まとめて閉じる
- Win + 矢印キーでのウィンドウの整列に対応
- コマンド（`wintavia-cli`）や AI クライアント（MCP）からも、タブバーと同じ操作ができる
- 日本語 / 英語、ダーク / ライト

## 動作環境

- Windows 11 以降（64 ビット）
- Microsoft 365 / Office 2016 以降のデスクトップ版 Word・Excel・PowerPoint
- 管理者権限は不要です。.NET などの追加のインストールも不要です。

## ダウンロードとインストール

1. [Releases](../../releases) から最新の `Wintavia-Setup-<版>.exe` をダウンロードします。
2. ダウンロードしたファイルが本物か確かめます（下の「ファイルの確認」）。
3. 実行して「OK」を押すとインストールされます。

> **「Windows によって PC が保護されました」と表示された場合**
> Wintavia は有償のコード署名証明書を使っていないため、この表示が出ます。「ファイルの確認」で本物であることを確かめてから、「詳細情報」→「実行」を押してください。
> 会社の PC では、情報システム部門の方針で実行できない場合があります。その場合は、下のハッシュ値を添えて担当者にご相談ください。

### ファイルの確認（SHA-256）

各リリースの説明と `SHA256SUMS.txt` に、インストーラーの SHA-256 ハッシュ値を載せています。PowerShell で次を実行し、表示された値が一致することを確かめてください。

```powershell
Get-FileHash .\Wintavia-Setup-<版>.exe -Algorithm SHA256
```

一致しない場合は実行せず、ファイルを削除してください。

### サイレントインストール（管理者向け）

```powershell
.\Wintavia-Setup-<版>.exe /silent [/autostart] [/start]
```

アンインストールは「設定 > アプリ > インストールされているアプリ」から行えます。

## 利用規約・ライセンス

- 個人・法人、商用・非商用を問わず、無償で利用できます。
- 利用条件は [LICENSE.txt](LICENSE.txt)（利用規約）をご覧ください。インストールすると利用規約に同意したものとみなします。
- 同梱している第三者ソフトウェアのライセンスは、インストール先の `THIRD-PARTY-NOTICES.txt`（アプリの「設定」→「アプリの情報」からも開けます）をご覧ください。
- ソースコードは公開していません。

## プライバシー

Wintavia はパソコンの中だけで動作し、文書の内容・ファイル名・利用状況などを外部に送信しません。設定・お気に入り・履歴はパソコンの中にだけ保存します。

## AI ツールとつなぐ（上級者向け）

Wintavia には、Claude Code や Codex などの AI ツールから、開いている文書の一覧・内容の読み取り・切り替えなどを行うための **MCP サーバー（`wintavia-mcp`）** と、**コマンド（`wintavia-cli`）** が入っています。使わなくても、タブバーの機能には影響ありません。

### AI ツールに登録する（PowerShell で実行）

```powershell
# Claude Code
claude mcp add --transport stdio --scope user wintavia -- "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-mcp.exe"

# Codex
codex mcp add wintavia -- "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-mcp.exe"
```

- Wintavia を起動しておいてください（タブバーを隠していても使えます）。
- 文書の一覧・読み取り・切り替えは、そのまま使えます。
- 文書の**書き換え・保存・閉じる**は、タブバーの「設定」→「ほかのツールからの操作」でチェックを入れたときだけ使えます。この許可は AI ツールやコマンドからは変えられません。
- **AI ツールに読ませた文書の内容は、その AI サービスに送られます。** 会社の文書を扱うときは、社内の決まりを確認してください。Wintavia 自身は外部に送信しません。
- マクロの実行はできません。

### コマンドで使う

```powershell
& "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-cli.exe" list          # 開いている文書の一覧
& "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-cli.exe" list --json   # スクリプト向け
```

引数なしで実行すると、使い方が表示されます。インストール時に `/addtopath` を付けると、`wintavia-cli` だけで呼べるようになります。

## 不具合の報告・要望

- [Issues](../../issues) から「不具合の報告」または「要望」を選んで書いてください。**書いた内容は誰でも見られます。** 会社の文書名・ファイルのパス・画面の機密情報は書かないでください。
- 無償で提供しているため、すべての報告にお返事や対応をお約束するものではありません。
- セキュリティ上の問題は、公開の issue ではなく [SECURITY.md](SECURITY.md) の方法で非公開でお知らせください。

---

## English

Wintavia shows the Word, Excel and PowerPoint documents you have open in one slim tab bar on the left of the screen, so you can switch between them with a click.

### Features

- One tab bar for all open Word / Excel / PowerPoint documents, across apps and windows
- Hover to expand and read full document names (drag to resize)
- Favorites and history; right-click to open the folder, copy the path or close documents
- Works with Win + arrow window snapping
- The same operations are available from the command line (`wintavia-cli`) and AI clients (MCP)
- Japanese / English, dark / light themes

### Requirements

- Windows 11 or later (64-bit)
- Desktop Word / Excel / PowerPoint of Microsoft 365 or Office 2016 or later
- No administrator rights or additional runtimes required

### Download and install

1. Download the latest `Wintavia-Setup-<version>.exe` from [Releases](../../releases).
2. Verify the file (see "Verify the file" below).
3. Run it and click "OK".

> **If you see "Windows protected your PC"**: Wintavia is not signed with a paid code signing certificate, so Windows shows this warning. After verifying the file, click "More info" and then "Run anyway". On company PCs, your IT policy may block it; please contact your IT department with the hash value below.

#### Verify the file (SHA-256)

Each release lists the SHA-256 hash of the installer in its notes and in `SHA256SUMS.txt`. Run the following in PowerShell and make sure the value matches. If it does not match, do not run the file and delete it.

```powershell
Get-FileHash .\Wintavia-Setup-<version>.exe -Algorithm SHA256
```

### License

Free for personal and commercial use. See [LICENSE.txt](LICENSE.txt) (the Japanese text is the official version). By installing, you agree to the license terms. Third-party licenses are in `THIRD-PARTY-NOTICES.txt` in the installation folder. The source code is not published.

### Privacy

Wintavia runs only on your PC and does not send document contents, file names or usage data anywhere.

### Connect AI tools (advanced)

Wintavia includes an **MCP server (`wintavia-mcp`)** and a **command-line tool (`wintavia-cli`)** so that AI tools such as Claude Code and Codex can list, read and switch your open documents. You do not need them to use the tab bar.

```powershell
# Claude Code
claude mcp add --transport stdio --scope user wintavia -- "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-mcp.exe"

# Codex
codex mcp add wintavia -- "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-mcp.exe"
```

- Keep Wintavia running (the tab bar may be hidden).
- Listing, reading and switching documents work right away.
- **Changing, saving and closing** documents work only after you allow them in the tab bar: Settings > "Access from other tools". AI tools and the command line cannot change this permission.
- **Document contents read by an AI tool are sent to that AI service.** Check your company's rules before using it with work documents. Wintavia itself sends nothing.
- Macros cannot be run.

Command line: `& "$env:LOCALAPPDATA\Programs\Wintavia\app\wintavia-cli.exe" list` (run without arguments for help; install with `/addtopath` to call `wintavia-cli` directly).

### Bug reports and requests

Use [Issues](../../issues) and choose "Bug report" or "Feature request". **Issues are public**: do not include company document names, file paths or confidential screenshots. Wintavia is free, so we cannot promise a reply or a fix. Report security issues privately as described in [SECURITY.md](SECURITY.md).

---

Copyright (c) 2026 Yorihako Studio
