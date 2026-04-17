# Claude Code プロジェクトルール — career_dev リポジトリ

## 📌 プロジェクト概要

- **リポジトリ**: KazuyaMurayama/career_dev
- **オーナー**: 男座 員也（Oza Kazuya）、41歳
- **目的**: 2026年6月〜7月からのフリーランス AI/DS コンサルタント独立支援
- **現フェーズ**: Phase 0（在職中の準備期 / 2026年4〜6月）
- **最終ゴール**: 2026年6月末〜7月末までに、月額300万円（フル稼働換算）の複数案件・合計稼働率60% = **月収180万円** の体制を構築

---

## 🌳 メイン開発ブランチ

- **作業ブランチ**: `claude/japanese-confirmation-KoaZO`（現在のメイン）
- **ナビゲーションハブ**: `main`（`CLAUDE.md` と `_file_index.md`を保持）

---

## 🚀 セッション開始時の必須手順（最優先）

**新しいセッションを開始したら、まず以下を実行すること：**

1. **[_file_index.md](https://github.com/KazuyaMurayama/career_dev/blob/main/_file_index.md) を必ず読む**（main ブランチ）
   - 全ブランチ・全ファイルの概要一覧
   - 目的別クイックリファレンス（何をしたいか→どのファイルを読むか）
   - スキルシート・職務経歴書のバージョン履歴（最新版の特定）

2. ユーザーの質問・依頼を受けたら、インデックスから該当ファイルを**特定してから**作業する

3. **古い版のファイルを「最新」として扱わない**。必ず `_file_index.md` の「★」マーカーで最新版を確認

---

## 🔴 最重要ルール1: リポジトリ内ファイルへの参照には必ずハイパーリンクを付ける

### 適用範囲（すべての場合に必須）

以下の**いずれの場合も**、GitHubハイパーリンクを**必須**とする:

1. ✅ ファイルを新規作成・更新してコミット・プッシュした時
2. ✅ **既存ファイルの内容を引用・要約した時**
3. ✅ **既存ファイルの名前を文中で言及した時**（「`market_research_step1.md` によると...」等）
4. ✅ **表形式でファイル一覧を提示する時**
5. ✅ **ユーザーからファイルについて質問された時**
6. ✅ **別ファイルの出典として名前を挙げる時**

### リンク形式（必須）

**Markdownリンク形式を必ず使う:**
```
[ファイル名](https://github.com/KazuyaMurayama/career_dev/blob/<ブランチ名>/<ファイルパス>)
```

**生URLは不可。ファイル名のバッククォート囲みだけの記述（`file.md`）も不可。**

### 報告例

**✅ 良い例:**
> [agent_email_template.md](https://github.com/KazuyaMurayama/career_dev/blob/claude/japanese-confirmation-KoaZO/agent_email_template.md) を保存しました。

**✅ 良い例（引用時）:**
> [market_research_step1.md](https://github.com/KazuyaMurayama/career_dev/blob/claude/analyze-freelance-income-3EGdc/market_research_step1.md) によると、POD は Tier S です。

**❌ 悪い例:**
> market_research_step1.md によると、POD は Tier S です。
> `skill_sheet_updated.md` を参照してください。

### 🔍 送信前セルフチェック（必須）

レスポンスを送信する前に、以下を**必ず**確認すること:

- [ ] 文中にファイル名（`.md` / `.docx` / `.pdf` / `.py` / `.html` / `.json` 等）が含まれているか？
- [ ] 含まれている場合、**すべての言及箇所**にMarkdownハイパーリンクが付いているか？
- [ ] ファイル名がバッククォート（`` ` ``）だけで囲まれていて、リンクがない箇所はないか？
- [ ] 別ブランチのファイルを参照する場合、**ブランチ名を正しく**指定しているか？（[_file_index.md](https://github.com/KazuyaMurayama/career_dev/blob/main/_file_index.md) で確認）
- [ ] 日本語ファイル名はURLエンコードされているか？

**上記チェックのいずれか1つでもNGならば、レスポンスを送信せず修正する。**

---

## 🔴 最重要ルール2: ファイル変更時は `_file_index.md` も同時に更新する

### トリガー条件

以下の操作を行った時は、**必ず [_file_index.md](https://github.com/KazuyaMurayama/career_dev/blob/main/_file_index.md) も同時に更新**する:

| 操作 | `_file_index.md` への更新内容 |
|---|---|
| 新規ファイル作成・コミット | 該当ブランチ・セクションに追記 |
| ファイル名変更・再命名 | 旧パスを削除、新パスを追記 |
| 最新版の更新（例：スキルシート新バージョン） | 旧「★」マークを外し、新ファイルに「★」を付与／バージョン履歴表に追記 |
| ファイル削除・廃止 | 該当行を削除 or「（アーカイブ）」マーク追加 |
| 新ブランチ作成 | 「ブランチ一覧と役割」セクションに追記 |

### 更新フロー

1. ユーザーの依頼でファイルを編集・新規作成する
2. コミット・プッシュする
3. **同じタイミング** で `_file_index.md` を更新し、別コミットで main ブランチにプッシュ（またはPR）
4. 報告時にも `_file_index.md` 更新済みの旨を明記

### 「同時更新」の重要性

- `_file_index.md` が古いと、次のセッションで Claude が**古い版を「最新」と誤認**する
- 過去実際にこの問題が発生し、整合性確認に多大な時間を費やした（詳細は改訂履歴参照）

---

## 📌 ブランチ構成（概要）

詳細は [_file_index.md](https://github.com/KazuyaMurayama/career_dev/blob/main/_file_index.md) 参照

| ブランチ | 役割 |
|---|---|
| `main` | ナビゲーションハブ（[CLAUDE.md](https://github.com/KazuyaMurayama/career_dev/blob/main/CLAUDE.md) / [_file_index.md](https://github.com/KazuyaMurayama/career_dev/blob/main/_file_index.md)） |
| **`claude/japanese-confirmation-KoaZO`** | **主要作業ブランチ**。スキルシート・職務経歴書最新版、エージェント対応、税務、契約書 |
| `claude/analyze-freelance-income-3EGdc` | 市場調査・戦略・週次アクションプラン |
| `claude/analyze-career-freelance-PCQl5` | 生成スクリプト・旧版ファイル（アーカイブ寄り） |
| `claude/check-repo-file-lists-desRY` | 並行セッション（税務） |

---

## 🎯 最終ゴールの詳細

### 収入目標

- **月収目標**: 180万円
- **算出式**: 月額300万円（フル稼働換算）× **合計稼働率60%**
- **案件構成**: 1案件あたり稼働20〜60%、複数案件を並行（例: 30%×2社、20%+40%等）
- **単価の段階的緩和**: 300万円が難しければ → 280万円 → 250万円
- **稼働率優先**: 収入が下がっても60%上限は死守（健康・品質確保）

### スケジュール

- 2026年4月29日（水）: STANDARD 退職日（確定）
- 2026年6月1日〜: フリーランス本格稼働（**理想**）
- 2026年7月開始: **バックアップ**（6月開始が難しい場合）

---

## 🌿 Git操作ルール

### ❌ 禁止
- ブランチ作成は一切禁止（Claude Codeがセッションを変えると読み取りにくいため）。禁止コマンド例：`git checkout -b` / `git switch -c` / `git branch <name>`
- ユーザーから明示的な指示がない限り、現在のブランチを変更しない。

### ✅ 許可
- 現在のブランチ上での `git add`, `git commit`, `git push`
- `git status`, `git log`, `git diff` などの読み取り操作
- `git pull` による最新化

---

## 📜 改訂履歴

| 日付 | 変更内容 |
|---|---|
| 2026-04-07 | 初版作成（ハイパーリンク報告ルール） |
| 2026-04-08 | ルール適用範囲を拡大（既存ファイル参照時も必須化）＋セルフチェック追加＋ブランチ別所在表追加 |
| 2026-04-15 | **全面統合版**: main/作業ブランチ間の CLAUDE.md を整合、`_file_index.md` 参照義務を明記、`_file_index.md` 同時更新ルールを追加、最終ゴール（月収180万円）を明記 |
| 2026-04-17 | Git操作ルールを追加（ブランチ作成禁止、現在ブランチでの操作に限定） |
