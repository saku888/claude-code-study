# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Claude Code 学習用の Rails 8.1 アプリ（Ruby 4.0.1）。現状は `rails new` 直後の雛形で、ドメインモデル・ルート（`/up` 以外）はまだ無い。

## Commands

```sh
bin/setup                    # 依存インストール + DB 準備 + サーバ起動（--skip-server で起動なし）
bin/dev                      # 開発サーバ（bin/rails server のみ。CSS/JS ビルドプロセスは無い）
bin/rails test               # 全テスト（system テストは除く）
bin/rails test test/models/foo_test.rb:12   # 単一ファイル / 行指定
bin/rails test:system        # system テスト（Capybara + Selenium）
bin/rubocop                  # Lint（rubocop-rails-omakase）。-a で自動修正
bin/brakeman                 # セキュリティ静的解析
bin/bundler-audit            # gem 脆弱性チェック
bin/importmap audit          # JS 依存の脆弱性チェック
bin/ci                       # ローカル CI 一式（config/ci.rb で定義）
```

`bin/ci` は setup → rubocop → bundler-audit → importmap audit → brakeman → test → `db:seed:replant`（test 環境）を順に実行する。GitHub Actions（`.github/workflows/ci.yml`）も同等のチェックに加え system テストを実行する。

## Architecture / Environment

- **DB**: MySQL（mysql2）。開発/テストはローカル Homebrew MySQL に `root`・パスワードなし・ソケット `/tmp/mysql.sock` で接続。CI では `DATABASE_URL` で上書き。
- **Solid Queue / Cache / Cable**: production では primary とは別 DB（`*_cache`, `*_queue`, `*_cable`）を使い、スキーマは `db/{cache,queue,cable}_schema.rb`、マイグレーションは `db/{cache,queue,cable}_migrate`。development は `cache_store = :memory_store`。Puma 内で Solid Queue を動かす場合は `SOLID_QUEUE_IN_PUMA` を設定（または `bin/jobs`）。
- **フロントエンド**: Hotwire（Turbo + Stimulus）+ Importmap + Propshaft。Node/バンドラは無し。JS 依存の追加は `bin/importmap pin <pkg>`、Stimulus コントローラは `app/javascript/controllers/`。
- **テスト**: Minitest + fixtures（`test/`）。RSpec は未使用。
- **デプロイ**: Kamal（`config/deploy.yml`, `.kamal/`）+ Dockerfile + Thruster。
