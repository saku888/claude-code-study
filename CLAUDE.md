# CLAUDE.md
This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# 概要
Claude Code 学習用アプリ

# 開発環境
- Rails 8.1.4
- Ruby 4.0.1
- MySQL
- フロントエンド: Hotwire（Turbo / Stimulus）+ Importmap + Propshaft
- バックグラウンド処理など: Solid Queue / Solid Cache / Solid Cable

# 開発方針
- Railsの標準的な構造・慣習に従う

## 環境
開発環境・gemのバージョンアップに関することは変更しない

## コーディング規約
- インデントは2スペース
- コメントアウトする際は理由を日本語で書いて
- コメントアウトはシングルクォートで囲む

## git
- mainブランチで対応は行わない
- mainブランチへの直接マージは行わない
- 対応後コミットまででPRへのpushは指示があるまで行わない

## viewファイル
- HTML テンプレートはerbファイルを使用する