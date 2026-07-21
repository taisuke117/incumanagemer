# incumanagemer

**A single-file cell culture passage manager — timeline, lineage tree, and daily task list. No install, no server, no account.**

単一HTMLで動く細胞培養パッセージ管理ツール。タイムライン・系統樹・本日のタスクを1画面で。インストール不要・サーバー不要・アカウント不要。

[English](#english) ・ [日本語](#日本語)

---

## English

### What it is

`index.html` is the whole application. Open it in a browser and it works — offline, with no build step, no dependencies and no data leaving your machine. It is aimed at wet-lab cell culture: you seed cultures, passage them, change medium, and harvest for RNA/DNA or freezing, and you need to remember what came from what.

### Features

- **Timeline** — every culture drawn from its seeding date to its planned harvest date, grouped by cell line, with weekend shading and a "today" line.
- **Lineage** — passages are linked parent → child and drawn as arrows. Drag the dot on a culture's right edge onto another culture to link them (useful when several dishes are merged into one plate — a culture can have multiple parents).
- **Lineage tree view** — a read-only left-to-right view of how cultures descend from each thaw.
- **Today's tasks** — what is seeded or harvested on a given day, with the purpose of each harvest; step through days with ◀ ▶.
- **Medium change (MC) log** — one click per row logs today's medium change; shown as pins on the timeline.
- **Records** — cell name, vessel (100 mm dish / 6, 12, 24, 96 well), passage number, seeding & planned harvest dates, genotype (WT or KO + gene), medium, seeding density (n × 10^x) or dilution (1:x), volume (per well optional), reagents, purpose (passage / ISOGEN RNA / DNA extraction / freeze stock / custom — multiple allowed), plate contents, notes.
- **Archive instead of delete** — hide finished cultures while keeping their history.
- **Sorting** — by seeding date, cell name, passage, vessel, order added, or manual drag.
- **Print** — today's tasks only, calendar only, or both.
- **Bilingual UI** — switch 日本語 / English at any time; the setting is remembered.

### Data & storage

Data lives in your browser's `localStorage` by default. For a durable file you can connect a JSON file:

1. **Save to…** → choose a location (e.g. `cell-passages.json`).
2. From then on every change is written to that file automatically.
3. Next time, **Open JSON** (or the *Connect* prompt) re-attaches the same file.

This uses the File System Access API, which needs a secure context — it works on `https://` (e.g. GitHub Pages) and usually from a local file, but some browsers restrict it on `file://`. If it is unavailable the app falls back to a normal download, and `localStorage` still holds your data.

**CSV / JSON exchange.** *Export CSV* writes UTF-8 (with BOM) so Excel opens it directly; *Import* accepts CSV or JSON. CSV column headers are Japanese, because they are the stable on-disk contract for existing files — the app translates the UI, not the data format.

**Nothing is uploaded.** There is no server component and no telemetry.

### Use it

- Download `index.html` and open it, or
- Enable GitHub Pages for this repository and use `https://<user>.github.io/incumanagemer/` (recommended — the JSON auto-save is most reliable over https).

Tested on current Chrome / Edge. Drag interactions are mouse-based, so a desktop browser is expected.

### Notes / limitations

- One record = one vessel-and-purpose line. A plate holding several cells or conditions is recorded as a single record with a "plate contents" list, not as individual wells.
- Deleting a culture unlinks its children rather than deleting them.
- The lineage tree is read-only; edit on the timeline.

---

## 日本語

### 概要

`index.html` 一つだけで動きます。ブラウザで開けばそのまま使えて、ビルドも依存パッケージもサーバーも不要。データは手元から出ません。「どの培養がどれから来たのか」を追いながら、播種・継代・培地交換・回収（RNA/DNA・凍結）を管理するためのツールです。

### 主な機能

- **タイムライン** — 各培養を播種日から回収予定日までのバーで表示。細胞株ごとにグループ化し、週末の網掛けと本日ラインつき。
- **系譜** — 継代を親→子でつなぎ、矢印で描画。バー右端の●を別の培養へドラッグしてもつながります（複数のディッシュを1枚のプレートにまとめる場合など、**複数の親**を持てます）。
- **系統樹ビュー** — 解凍を起点に、左→右へ世代が進む閲覧専用の俯瞰図。
- **本日のタスク** — その日に播種／回収する培養と、回収の用途を一覧。◀ ▶ で日付を移動。
- **培地交換（MC）記録** — 各行のボタンで本日分をワンクリック記録。タイムラインにピンで表示。
- **記録項目** — 細胞名／ディッシュ（100 mm・6・12・24・96 well）／Passage／播種日・回収予定日／遺伝子型（WT・KO＋遺伝子）／培地／播種濃度（n×10^x）または希釈（1:x）／ボリューム（ウェルあたり可）／添加薬品／用途（継代・ISOGEN回収・DNA抽出・凍結ストック・追加可、複数選択）／プレート内容／メモ。
- **削除ではなく非表示（アーカイブ）** — 終わった培養を履歴を残したまま隠せます。
- **並び替え** — 播種日・細胞名・Passage・ディッシュ・追加順・手動ドラッグ。
- **印刷** — 本日のタスクだけ／カレンダーだけ／両方。
- **日英切替** — いつでも切り替え可能。設定は記憶されます。

### データと保存

既定ではブラウザの `localStorage` に保存されます。ファイルとして持ちたい場合は JSON を接続します。

1. **保存先…** から保存場所を指定（例：`cell-passages.json`）。
2. 以降、変更のたびにそのファイルへ自動保存されます。
3. 次回は **JSONを開く**（または「接続」）で同じファイルに再接続。

File System Access API を使うため、`https://`（GitHub Pages など）では確実に動作します。ローカルの `file://` では環境により制限されることがあり、その場合は通常のダウンロードにフォールバックします（`localStorage` にはデータが残ります）。

**CSV / JSON の入出力**：*Excel書出* は UTF-8（BOM付き）なので Excel でそのまま開けます。*読込* は CSV・JSON の両方に対応。**CSVの列見出しは日本語のまま**です（既存ファイルとの互換を保つため、翻訳するのはUIであってデータ形式ではありません）。

**どこにもアップロードされません。** サーバーもテレメトリもありません。

### 使い方

- `index.html` をダウンロードして開く、または
- このリポジトリで GitHub Pages を有効にして `https://<user>.github.io/incumanagemer/` を使う（**推奨**。https のほうが JSON 自動保存が確実です）。

動作確認は Chrome / Edge の最新版。ドラッグ操作はマウス前提のため、デスクトップでの利用を想定しています。

### 制限事項

- 1レコード＝1つの容器・用途の行です。複数の細胞や条件を播いたプレートは「プレート内容」に列挙する形で、ウェル単位の個別管理ではありません。
- 培養を削除すると、その子の親リンクは外れます（子自体は消えません）。
- 系統樹は閲覧専用です。編集はタイムライン側で行ってください。

---

## Repository policy / このリポジトリの位置づけ

This repository is the **public, generic version**. The sample data it ships with is placeholder only (`HeLa`, `GeneX`); it contains **no real experimental data, cell line names or gene names**. Personal working data lives outside this repository, in the user's own JSON file.

このリポジトリは**公開用の汎用版**です。同梱のサンプルはプレースホルダ（`HeLa`, `GeneX`）のみで、**実験データ・実際の細胞株名・遺伝子名は含みません**。個人の実データはリポジトリ外（各自のJSONファイル）で管理します。

## License / ライセンス

[MIT](LICENSE) — free to use, modify and redistribute, with no warranty.

[MIT ライセンス](LICENSE)。改変・再配布とも自由（無保証）。
