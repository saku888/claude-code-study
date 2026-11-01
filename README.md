# claude-code-study

Claude Code の学習用リポジトリです
https://zenn.dev/sakurano

# 開発環境
- Rails 8.1.4
- Ruby 4.0.1
- MySQL（Homebrew / `root` ユーザー・パスワードなし、ソケット `/tmp/mysql.sock`）
- フロントエンド: Hotwire（Turbo / Stimulus）+ Importmap + Propshaft
- バックグラウンド処理など: Solid Queue / Solid Cache / Solid Cable

# セットアップ
```sh
bin/setup
```

# よく使うコマンド
```sh
bin/dev
bin/rails test
bin/rubocop
bin/brakeman
bin/ci
```
