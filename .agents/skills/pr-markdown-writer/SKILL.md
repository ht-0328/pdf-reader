---
name: pr-markdown-writer
description: 変更内容とプロジェクトルールを確認し、PR作成画面に直接貼り付けられるMarkdown形式のPR本文を作成するSkillです。
---

# PR Markdown Writer

## Overview

このSkillは、ユーザーの変更内容（`git diff`等）とプロジェクト独自のルール（`README`、`AGENTS.md`、`docs/`、`.github/pull_request_template.md`など）を読み込み、PR作成画面に貼り付けるためのMarkdown形式のPR本文を自動作成します。同時に、プロジェクトルールに基づいた事前チェック結果も出力します。

## When to use

ユーザーが「PRを作りたい」「PR本文を作成して」と依頼したときに使用します。
※このSkillはPR作成用のMarkdownテキストを出力するまでを担当します。実際にGitHub上でPRを作成する操作（`gh pr create`など）は行いません。

## Inputs

* 現在のワークスペースの変更内容（`git diff`などで取得）
* `.github/pull_request_template.md`（存在する場合）
* プロジェクトルール（`README.md`、`AGENTS.md`、`docs/` 配下の関連ドキュメント）

## Procedure

1. **変更内容の確認**: `git diff` 等を用いて、現在の変更内容を把握する。
2. **ルールの読み込み**: `references/pr-checklist.md` に記載された確認事項をもとに、プロジェクト内の関連ドキュメントやPRテンプレートを読み込む。
3. **内容の整理**: 変更内容、変更理由、影響範囲を整理する。テスト実行状況も確認する。
4. **Markdownの作成**: `templates/pr-markdown-template.md` に従って、PR本文となるMarkdownを作成する。（もしプロジェクトに `.github/pull_request_template.md` がある場合はそちらを優先またはマージして作成する）
5. **チェック結果の作成**: プロジェクトルールに基づく事前チェック結果と、未確認事項をまとめる。
6. **結果の出力**: PRタイトル案、PR本文Markdown、事前チェック結果、未確認事項を出力する。

## Constraints

* **実際のPR作成コマンド（`gh pr create`、`git push`等）は絶対に実行しないこと。**
* テストを実行していない場合は「未実行」、確認できていない内容は「未確認」と明確に記載すること。
* 明確なルールが存在しない状態で、レビュアーやラベルなどを勝手に推測して設定しないこと。

## Output

以下の形式でユーザーに提示してください。
1. **PRタイトル案**（複数提示）
2. **PR本文Markdown**（コードブロックで囲んでそのままコピーできるようにする）
3. **事前チェック結果**
4. **未確認事項**

## References

* `templates/pr-markdown-template.md`: PR本文出力用の雛形
* `references/pr-checklist.md`: 事前チェック用の項目リスト

## Examples

ユーザー: 「PR本文を作って」
=> 変更を読み取り、ルールをチェックして、Markdownテキストとチェック結果を出力する。
