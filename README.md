# komonjo-daily

Slackのchannelと日付を指定すると特定の日のchannelの発言を全てmarkdown化します。

現在開発中のため最新100件までしかとれません。

## 使い方

### 準備

環境変数あるいは`.env`ファイルにSlackのAPITokenを設定してください。

```.env
KOMONJO_SLACK_API_TOKEN=%YOUR_API_TOKEN%
```

また必要なGemをインストールしておいてください。

```zsh
% bundle install
```

### 実行

以下のコマンドを実行してください。

```zsh
% rake "messages[channel_name, 2015-11-12]"
```

この場合`md/channel_name/2015-11-12.md`というファイルに出力されます。
