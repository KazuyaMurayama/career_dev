# CLAUDE.md — career_dev リポジトリ セッションガイド

## このリポジトリについて

**対象者:** 男座 員也（Oza Kazuya）、41歳  
**目的:** 2026年6月からのフリーランスAI/DSコンサルタントとしての独立準備  
**現フェーズ:** Phase 0（在職中の準備期 / 2026年4〜6月）

---

## セッション開始時の必須手順

**新しいセッションを開始したら、まず以下を参照すること：**

1. `main` ブランチの **`_file_index.md`** を読む
   - 全ブランチ・全ファイルの概要一覧
   - 目的別クイックリファレンス（何をしたいか→どのファイルを読むか）
   - スキルシートのバージョン履歴

2. ユーザーの質問・依頼に応じて、インデックスから該当ファイルを特定してから作業する

---

## リポジトリ構成（概要）

| ブランチ | 役割 |
|---|---|
| `main` | `_file_index.md` / `CLAUDE.md` など共通ナビゲーションファイル |
| `claude/analyze-freelance-income-3EGdc` | 市場調査・戦略・週次アクションプラン一式（**中核ブランチ**） |
| `claude/japanese-confirmation-KoaZO` | スキルシート日本語版・エージェント面談準備 |
| `claude/analyze-career-freelance-PCQl5` | 最新スキルシート（2026/4/6 v2）生成・出力 |
| `claude/analyze-career-freelance-Fqa1L` | 現在の作業ブランチ |

---

## 重要ファイル ショートリスト

| 優先度 | ファイル | ブランチ | 内容 |
|:---:|---|---|---|
| ★★★ | `weekly_action_plan.md` | `analyze-freelance-income-3EGdc` | 12週間の全体計画・Go/No-Go基準 |
| ★★★ | `week{N}_details.md` | `analyze-freelance-income-3EGdc` | 各週の日別アクション詳細 |
| ★★★ | `Oza_skill_sheet_20260406-2.md` | `analyze-career-freelance-PCQl5` | 最新スキルシート（提出用） |
| ★★ | `positioning_strategy.md` | `analyze-freelance-income-3EGdc` | ポジショニング戦略 |
| ★★ | `feasibility_scoring.md` | `analyze-freelance-income-3EGdc` | 収入パターンの実現性スコア |
| ★★ | `agent_interview_prep.md` | `japanese-confirmation-KoaZO` | エージェント初回面談準備シート |
| ★ | `market_research_step1.md` | `analyze-freelance-income-3EGdc` | 市場調査・単価相場データ |
| ★ | `prompt_weekly_sparring.md` | `analyze-freelance-income-3EGdc` | 週次壁打ちプロンプトテンプレート |

---

## 開発ブランチのルール

- 作業は `claude/analyze-career-freelance-Fqa1L` ブランチで行う
- `main` はナビゲーションファイル（`_file_index.md`, `CLAUDE.md`）のみ管理
- `_file_index.md` は新しいファイル・ブランチが追加されたら随時更新する
