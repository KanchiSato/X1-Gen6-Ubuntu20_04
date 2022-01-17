# rules
自分用のルールだったり、他の人にも守ってほしいルールだったり

## 運用ルール
pushする前に必ずscripts/check-rulesスクリプトを実行してください。

### gitルール
運用するbranchは基本的に下記の2つとします
- main
- draft

mainは完全版の文章となり、draftは書きかけでforce pushでガンガン履歴も変えていく予定です。

もしPRなどを送ってくださる方がいる場合はmainに送っていただければと思います。ただ、その際にコミットの分け方やcommitコメントについてとやかく言うかもしれないので、面倒くさいのが嫌な人はissueに書いてもらえれば大丈夫です。

### 編集ルール
Ubuntu全体の問題についての記載はこの場ですることはありません。あくまでもUbuntu20.04の入ったX1 Carbon Gen6に関する物のみを書きます。

### 使用するツールについて
基本的にEditorは何を使ってもいいと思っているので、Editorが限定されるプラグイン等の使用は避ける方針です。また、PRをしていただく際にあれこれインストールしろと要求するのも好きではないのでそこらへんは意識しています。

しかし、[EditorConfig](https://editorconfig.org/)と[Docker](https://www.docker.com/)だけは申し訳ないですが入れてほしいと思っています。

それぞれの役割は下記のようになります。

- `EditorConfig`: ファイル毎にフォーマットのルールを設定する
- `Docker`: 他に使いたいツールがあった場合には新たにインストールせずにDocker上で実行する

### EditorConfig使用（インストール）方法
各エディタのマニュアルに従う

### Docker使用（インストール）方法
各OSのマニュアルに従う。
実行時には必要に応じて管理者権限を付与する

### ShellCheck使用方法（scripts/check-rules記載済み）
```bash
docker run --rm -v "$PWD:/mnt" koalaman/shellcheck:stable <script or dir/*>
```
### shfmt使用方法（scripts/check-rules記載済み）
```bash
docker run --rm -v "$PWD:/mnt" -w /mnt mvdan/shfmt -l -w -i 2 -ci -bn <script or dir/*>
```
