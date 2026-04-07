# ファイルインデックス — career_dev リポジトリ

**最終更新:** 2026年4月6日  
**用途:** 相談・作業時にまず参照し、必要なファイルを素早く特定するためのナビゲーション一覧

> **使い方:** 作業前にこのファイルを参照し、目的に合うファイルのブランチ・パスを確認してください。

---

## ブランチ一覧と役割

| ブランチ名 | 役割・作成目的 |
|---|---|
| `main` | 元の職務経歴書（原本）のみ保管 |
| `claude/analyze-freelance-income-3EGdc` | フリーランス転向の収入・市場・戦略分析一式（中核ブランチ） |
| `claude/japanese-confirmation-KoaZO` | スキルシート日本語版の確認・整備、エージェント面談準備 |
| `claude/analyze-career-freelance-PCQl5` | 最新スキルシート（2026/4/6版）生成・出力 |
| `claude/analyze-career-freelance-Fqa1L` | 現在の作業ブランチ（このインデックスファイルを含む） |

---

## ファイル一覧（ブランチ別）

---

### main ブランチ

| ファイル名 | 種別 | 概要 |
|---|:---:|---|
| `Skill Sheet 男座員也 202601.docx` | Word | 原本スキルシート（2026年1月版）。すべてのブランチの出発点 |

---

### claude/analyze-freelance-income-3EGdc（中核：分析・戦略ブランチ）

| ファイル名 | 種別 | 概要 |
|---|:---:|---|
| `market_research_step1.md` | MD | **市場調査レポート**。フリーランスAI/DSコンサル市場の単価相場・エージェント別単価・買い手ニーズ・市場トレンドを調査。パターン1（300万×20%×2社）とパターン2（240万×50%×1社）の比較の前提データ |
| `feasibility_scoring.md` | MD | **実現性スコアリング**。楽観・慎重・実務・テックの4エージェント視点でパターン1・2・3を100点満点評価。パターン2（240万×50%）が最も実現性高（平均74点超） |
| `positioning_strategy.md` | MD | **ポジショニング戦略レポート**。4象限分析・競合比較・Tier1〜3ターゲット顧客定義・差別化メッセージ・営業チャネル戦略を網羅 |
| `action_plan_100tasks.md` | MD | **初期アクションプラン**（v2）。パターン2→1の二段階移行を前提に、Phase 0〜2のカテゴリ別タスク一覧。`weekly_action_plan.md`の前身 |
| `weekly_action_plan.md` | MD | **週次アクションプラン**（v3.0, 最新）。12週間・129アクションの全体計画。Go/No-Go判定基準・リスク管理表・依存関係マップ・Week 1〜3の目標を含む ★最重要参照ファイル |
| `week1_details.md` | MD | **Week 1（4/1〜4/7）詳細手順書**。エージェント10社登録・スキルシート提出・LinkedIn整備のDay別アクション・操作手順・時間目安 |
| `week2_details.md` | MD | **Week 2（4/8〜4/14）詳細手順書**。エージェント3社との初回面談・Claude Codeデモ作成・推薦文依頼のDay別アクション |
| `week3_details.md` | MD | **Week 3（4/15〜4/21）詳細手順書**。エージェント面談7社完了・紹介案件優先順位付け・コンテンツ充実のDay別アクション |
| `prompt_weekly_sparring.md` | MD | **週次壁打ちプロンプトテンプレート**。毎週の進捗確認セッション開始時にClaude Codeへ貼り付けるプロンプト。参照すべきファイル一覧・確認事項・出力形式を定義 |
| `skill_sheet_updated.md` | MD | スキルシート（このブランチ時点の版）。`japanese-confirmation-KoaZO`で更新された版と同内容 |
| `Skill Sheet 男座員也 202601.docx` | Word | 原本スキルシート（共通） |

---

### claude/japanese-confirmation-KoaZO（スキルシート整備・エージェント面談準備）

| ファイル名 | 種別 | 概要 |
|---|:---:|---|
| `skill_sheet_updated.md` | MD | **スキルシート（日本語版・確認済み）**。エグゼクティブサマリー・職務経歴・スキルマトリクス・資格・強み3点を含む。エージェント提出用の主要版（2026/4/2時点） |
| `skill_sheet_updated.docx` | Word | 上記の Word 出力版 |
| `skill_sheet_updated.pdf` | PDF | 上記の PDF 出力版 |
| `Oza_skill_sheet_20260403.docx` | Word | スキルシート（2026/4/3版）Word。`skill_sheet_updated`をベースに細部調整 |
| `Oza_skill_sheet_20260403.pdf` | PDF | 上記の PDF 出力版 |
| `agent_interview_prep.md` | MD | **エージェント初回面談 準備シート**（2026/4/3作成）。30分面談のアジェンダ・自己PR原稿・想定Q&A（なぜ独立？希望単価の根拠？稼働率は？）・逆質問例を収録 |
| `market_research_step1.md` | MD | 市場調査レポート（`analyze-freelance-income-3EGdc`と同内容） |
| `feasibility_scoring.md` | MD | 実現性スコアリング（同上） |
| `positioning_strategy.md` | MD | ポジショニング戦略（同上） |
| `action_plan_100tasks.md` | MD | 初期アクションプラン（同上） |
| `weekly_action_plan.md` | MD | 週次アクションプラン（同上） |
| `week1_details.md` | MD | Week 1 詳細手順書（同上） |
| `generate_skill_sheet.py` | Python | スキルシートをMarkdown→Word/PDF/HTMLへ変換するスクリプト |
| `skill_sheet_styled.html` | HTML | スキルシートのスタイル付きHTML版（印刷・共有用） |
| `男座員也_職務経歴書_データサイエンティスト_20250713_v3.docx` | Word | 旧職務経歴書（2025年7月版）。現スキルシートの元資料 |
| `Skill Sheet 男座員也 202601.docx` | Word | 原本スキルシート（共通） |

---

### claude/analyze-career-freelance-PCQl5（最新スキルシート生成）

| ファイル名 | 種別 | 概要 |
|---|:---:|---|
| `Oza_skill_sheet_20260406-2.md` | MD | **★最新スキルシート（2026/4/6 v2）**。強み3点を「企画戦略立案・実装力・変革推進力」に再定義した最終版。エージェント提出・クライアント面談に使用 |
| `Oza_skill_sheet_20260406-2.docx` | Word | 上記の Word 出力版（提出用） |
| `Oza_skill_sheet_20260406-2.pdf` | PDF | 上記の PDF 出力版（提出用） |
| `Oza_skill_sheet_20260406.docx` | Word | スキルシート（2026/4/6 v1）。v2の直前版 |
| `Oza_skill_sheet_20260406.pdf` | PDF | 上記の PDF 出力版 |
| `skill_sheet_updated.md` | MD | スキルシート（このブランチ時点の版） |
| `skill_sheet_updated.docx` | Word | 上記の Word 出力版 |
| `skill_sheet_updated.pdf` | PDF | 上記の PDF 出力版 |
| `generate_skill_sheet.py` | Python | スキルシートをMarkdown→Word/PDF/HTMLへ変換するスクリプト |
| `skill_sheet_styled.html` | HTML | スキルシートのスタイル付きHTML版 |
| `Skill Sheet 男座員也 202601.docx` | Word | 原本スキルシート（共通） |

---

### claude/analyze-career-freelance-Fqa1L（現在の作業ブランチ）

| ファイル名 | 種別 | 概要 |
|---|:---:|---|
| `_file_index.md` | MD | **このファイル**。全ブランチのファイル概要インデックス |
| `Skill Sheet 男座員也 202601.docx` | Word | 原本スキルシート（共通） |

---

## 目的別クイックリファレンス

| やりたいこと | 参照ファイル | ブランチ |
|---|---|---|
| 今週何をすべきか確認する | `weekly_action_plan.md` → `week{N}_details.md` | `analyze-freelance-income-3EGdc` |
| 今週の壁打ちをする | `prompt_weekly_sparring.md` | `analyze-freelance-income-3EGdc` |
| スキルシートを確認・提出する | `Oza_skill_sheet_20260406-2.md/docx/pdf` | `analyze-career-freelance-PCQl5` |
| エージェント面談の準備をする | `agent_interview_prep.md` | `japanese-confirmation-KoaZO` |
| 自分のポジショニングを確認する | `positioning_strategy.md` | `analyze-freelance-income-3EGdc` |
| 市場相場・競合を確認する | `market_research_step1.md` | `analyze-freelance-income-3EGdc` |
| 収入パターンの実現性を確認する | `feasibility_scoring.md` | `analyze-freelance-income-3EGdc` |
| スキルシートを再生成する | `generate_skill_sheet.py` | `analyze-career-freelance-PCQl5` |
| 旧職務経歴書を参照する | `男座員也_職務経歴書_データサイエンティスト_20250713_v3.docx` | `japanese-confirmation-KoaZO` |

---

## スキルシート バージョン履歴

| バージョン | ファイル名 | 日付 | 主な変更 |
|---|---|---|---|
| 原本 | `Skill Sheet 男座員也 202601.docx` | 2026年1月 | 原本 |
| v1（更新版） | `skill_sheet_updated.md/docx/pdf` | 2026年3月〜4月初旬 | 日本語版として整備。エグゼクティブサマリー追加 |
| v2 | `Oza_skill_sheet_20260403.docx/pdf` | 2026年4月3日 | 細部調整版 |
| v3（初日版） | `Oza_skill_sheet_20260406.docx/pdf` | 2026年4月6日 | 強み3点を再定義（v1） |
| **v4（最新）** | `Oza_skill_sheet_20260406-2.md/docx/pdf` | 2026年4月6日 | **強み3点を「企画戦略立案・実装力・変革推進力」に確定** |
