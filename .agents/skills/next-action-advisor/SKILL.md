---
name: next-action-advisor
description: プロジェクトの現状を必要な範囲で確認し、次にやるべき作業を1つに絞って提案するSkill。「次は何をすればいい？」「次の作業を提案して」「何をすべき？」と聞かれたときに使用する。提案のみを担当し、実装や計画作成は行わない。
---

# Next Action Advisor

## Overview

プロジェクトの現状を判断に必要な範囲で確認し、次にやるべき作業を**1つだけ**提案するSkillです。
候補を大量に並べるのではなく、理由・完了条件・その次の作業を簡潔に示します。

このSkillの責務は提案のみです。ユーザーから明確に依頼されない限り、実装・ファイル変更・コマンド実行・実行計画の作成は行いません。

## When to use

- 「次は何をすればいい？」
- 「次の作業を提案して」
- 「何をすべき？」
- 「プロジェクトの状況を見て次を教えて」

## Procedure

### Phase 1: 現状の確認

判断に必要な範囲だけ確認する。確認対象と除外対象は [references/scan-and-judgment-rules.md](references/scan-and-judgment-rules.md) に従う。

1. ディレクトリ構成を確認する（トップレベルおよび主要サブディレクトリ）
2. `README.md` を確認する
3. `AGENTS.md` を確認する（作業ルールとして参照。機能要件の根拠にはしない）
4. `docs/plans/` に実行計画が存在する場合は必ず確認する
5. `docs/worklogs/` のファイル名・更新日時を確認し、直近かつ判断に関係するWorklogだけを読む
6. 既存コード・設定ファイルを確認する

### Phase 2: 状況の整理

確認した情報をもとに、プロジェクトの状況を整理する。

1. 情報源間の食い違いがある場合は、[references/scan-and-judgment-rules.md](references/scan-and-judgment-rules.md) の「情報源の優先ルール」に従って判断する
2. 各項目を「未実装」「未決定」「候補」に区別する（区分ルールは同ファイルを参照）
3. 完了済みかどうかは成果物の存在で判断する（完了判定ルールは同ファイルを参照）

### Phase 3: 次の作業の提案

1. [references/scan-and-judgment-rules.md](references/scan-and-judgment-rules.md) の「優先順位ルール」に従い、今やるべき作業を**1つだけ**選ぶ
2. 次に着手でき、完了を確認できる最小の作業単位で提案する。大きな作業はその中の最初の1段階だけを提案する
3. [templates/proposal-output-template.md](templates/proposal-output-template.md) の形式でチャット上に出力する
4. 1つに決められない場合だけ、確認事項を最大3つ提示する

## Constraints

- **責務の限定**: このSkillは提案のみを担当する。ユーザーから明確に依頼されない限り、実装・ファイル変更・コマンド実行・実行計画の作成は行わない
- **質問の制限**: リポジトリ内のファイルで判断できる場合はユーザーへ質問しない。ユーザーしか決められない要件や方針が作業を止めている場合だけ確認事項を提示する。追加調査で判断できる場合は「必要な調査」を次の作業として提案してよい
- **Worklog不作成**: 通常の提案はファイル変更を伴わないため、Worklogは作成しない
- **保存は依頼時のみ**: ユーザーが保存を求めた場合だけMarkdownファイルとして保存する。保存する場合はAGENTS.mdのルールに従う。提案結果のMarkdownとWorklogは別の成果物として扱う
- **AGENTS.mdの扱い**: AGENTS.mdは作業ルールとして扱う。機能要件の根拠にはしない

## Output

通常はチャット上に出力する。出力形式は [templates/proposal-output-template.md](templates/proposal-output-template.md) を参照。

出力内容:
- 今やること
- 判断の根拠となった現状（ファイルパスと該当内容を含む）
- 優先する理由
- 完了条件
- その次の作業
- 未確認事項（ある場合のみ）

## References

- [references/scan-and-judgment-rules.md](references/scan-and-judgment-rules.md) — スキャン範囲、情報源の優先ルール、状態区分、完了判定、優先順位、作業単位、質問条件、Worklog参照方法
- [templates/proposal-output-template.md](templates/proposal-output-template.md) — 提案出力テンプレート

## Examples

ユーザー: 「次は何をすればいい？」

→ プロジェクトの現状を必要な範囲で確認し、提案出力テンプレートの形式で次の作業を1つだけ提案する。
