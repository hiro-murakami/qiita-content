---
title: フレームワークに縛られないガントチャートを作った — Web Components製「moguchart-core」の紹介
tags:
  - TypeScript
  - WebComponents
  - Lit
  - OSS
  - ガントチャート
private: false
updated_at: '2026-09-06T14:33:00+09:00'
id: 0e4859951a9f652c26c3
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---

![demo-light.png](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/demo-light.png)

## はじめに

プロジェクト管理ツールを自作しようとしたとき、こんな経験はありませんか？

- 既存のガントチャートライブラリが **特定のフレームワーク（React / Vue / Angular / Svelte）に依存** していて、技術選定に制約が出る
- 高機能な商用ライブラリは **ライセンス料が高く**、個人や小規模チームでは導入しにくい
- 無料の軽量ライブラリは **機能が不足** していて、実用レベルのUIが作れない

こうした課題を解決するために、**フレームワーク非依存・高機能・MIT ライセンス** のガントチャート Web Components ライブラリ「**moguchart-core**」を開発しました。

https://github.com/hiro-murakami/moguchart-core

デモサイトも公開していますので、実際に動く様子をぜひお試しください！
https://moguchart-core.vercel.app

## moguchart-core とは

`@mogura/moguchart-core` は、[Lit](https://lit.dev/) をベースに構築された **Web Components 製のガントチャートコンポーネント** です。

Custom Elements（`<gantt-chart>`）として動作するため、**Vue、React、Angular、Svelte、あるいはバニラ HTML** — どの環境でもそのまま使えます。

### 主な特徴

| カテゴリ | 内容 |
| :--- | :--- |
| **フレームワーク非依存** | Web Components (Custom Elements) として実装。どの環境でも動作 |
| **仮想スクロール** | 大量のタスク・行でもスムーズで軽快なパフォーマンス |
| **矩形範囲選択** | チャート背景ドラッグによる複数タスク一括選択（ラバーバンド選択、AABB交差判定、Shift/Ctrl/Cmdでの累積追加選択、オートスクロール対応） |
| **タスク進捗管理** | バー内進捗インジケーター描画、ハンドル操作による直感的ドラッグ編集（スナップ・Escキャンセル対応）、進捗ラベル表示、進捗率計算ユーティリティ |
| **豊富なインタラクション** | D&D でのタスク移動（行間移動・同一行内制限対応）、リサイズ、行の並び替え、複数選択＆一括ドラッグ |
| **ミニマップ（鳥瞰ビュー）** | 全体プレビュー、ビューポートパン操作、ドラッグ移動、リサイズ、透過率調整、折りたたみ、タスク進捗率の濃淡自動反映 |
| **依存関係＆クリティカルパス** | タスク間の依存を矢印付きの曲線/直角線で描画。最長経路（クリティカルパス）の自動ハイライト |
| **スムーズなズーム** | Ctrl/Cmd + ホイールズーム、全体を画面に収める `zoomToFit()` メソッド |
| **誤操作防止・ガード** | 行移動の縦方向制限（`enableCrossRowMove`）、チャート領域外ドラッグ時の自動キャンセル |
| **キーボード操作** | 矢印キーでのナビゲーション、Shift+矢印での移動、Deleteキーでのタスク削除 |
| **柔軟な表示モード** | 日 / 週 / 月 / 時間単位の切り替え、等幅月表示モード（最大100年スパン対応） |
| **テーマ対応** | ライト / ダーク / システム連動 + 30項目以上のカスタムカラーテーマ |
| **高度なカスタマイズ** | バー、行ヘッダー、ツールチップ、カレンダーセルなどの描画を関数でオーバーライド可能 |
| **エクスポート機能** | PNG 画像や PDF としての高解像度エクスポート（複数ページ分割・スクロール位置保持対応） |
| **日本語対応** | ロケール機能内蔵（日本語・英語）、祝日判定ロジックのカスタマイズ対応 |
| **ライセンス** | MIT |

## 開発のきっかけ

遡ること数年前、業務でガントチャートを作る機会がありました。当時は既存のライブラリをいくら調べても要件に合うものが見つからず、ほぼフルスクラッチで開発することになりました。

その頃から「使い勝手の良いガントチャートをOSSとして公開したい」と思っていましたが、なかなか第一歩を踏み出せずにいました。そんな中、2025年の年末に「いま話題のAIをフル活用したら、どれくらいのスピードで作れるだろう？」と思いつき、開発をスタート。結果は驚くほどで、わずか数日で基本部分が完成してしまいました（※コードは過去の使い回しではなく、完全な新規書き下ろしです）。

動くものが出来上がると開発がどんどん楽しくなり、ライブラリ単体にとどまらず、それを組み込んだ本格的なWebアプリまで一気に作り上げてしまいました。

## 既存ライブラリとの違い

JavaScript のガントチャートライブラリは多数存在しますが、大きく2つのカテゴリに分かれます。

### 商用エンタープライズ系（Bryntum, DHTMLX, Syncfusion など）

✅ 非常に高機能・サポート充実
❌ 有料ライセンス（年間数万〜数十万円）

### 無料 OSS 系（Frappe Gantt など）

✅ MIT ライセンスで無料
❌ 機能が限定的（D&D、依存関係表示、仮想スクロールなどが不足）

### moguchart-core の立ち位置

moguchart-core は **「商用ライブラリに迫る機能性を、MIT ライセンスで」** を目指しています。

```
                    機能の充実度
                        ↑
     Bryntum / DHTMLX   |   moguchart-core ← ここ
                        |
    ────────────────────┼──────────────────→ コスト
                        |
          Frappe Gantt  |
                        |
```

特に、以下の点で差別化しています：

- **Web Components ネイティブ** — React/Vue ラッパーではなく、Custom Elements そのもの
- **仮想スクロール** — 数百〜数千行でも軽快
- **直感的な操作感** — スムーズなD&D、矩形範囲選択、進捗ドラッグ編集、ホイールズーム、ミニマップ連携、キーボードショートカット
- **日本語ファースト** — ロケール、祝日判定を標準サポート

## インストール

```bash
npm install @mogura/moguchart-core
# または
pnpm add @mogura/moguchart-core
```

## クイックスタート（Vue.js）

```html
<script setup lang="ts">
  import { ref } from 'vue'
  import '@mogura/moguchart-core'
  import type { GanttRow, GanttChartOption } from '@mogura/moguchart-core'

  const rows = ref<GanttRow[]>([
    {
      id: 'row-1',
      name: '開発チームA',
      tasks: [
        {
          id: 't-1',
          name: 'API設計',
          start: new Date('2025-06-01'),
          end: new Date('2025-06-10'),
          progress: 100, // 進捗率 (0〜100)
          style: 'background-color: #60a5fa',
        },
        {
          id: 't-2',
          name: '実装',
          start: new Date('2025-06-10'),
          end: new Date('2025-06-25'),
          progress: 45,
          style: 'background-color: #34d399',
          dependencies: ['t-1'], // t-1 に依存
        },
      ],
    },
    {
      id: 'row-2',
      name: 'デザインチーム',
      tasks: [
        {
          id: 't-3',
          name: 'UIデザイン',
          start: new Date('2025-06-05'),
          end: new Date('2025-06-15'),
          progress: 80,
          style: 'background-color: #f472b6',
        },
      ],
    },
  ])

  const option = ref<GanttChartOption>({
    calendar: {
      start: new Date('2025-06-01'),
      end: new Date('2025-07-31'),
      pxPerDay: 30,
      showCurrentTime: true,
    },
    zoom: {
      enabled: true, // Ctrl + ホイールズームを有効化
    },
    dependency: {
      showCriticalPath: true, // クリティカルパスをハイライト
    },
    progress: {
      enabled: true,
      editable: true, // ドラッグによる進捗率編集を有効化
      showLabel: true, // 進捗ラベル (例: "45%") を表示
      snapStep: 5, // 5%刻みスナップ
    },
    selection: {
      marquee: true, // 矩形範囲選択（ラバーバンド選択）を有効化
    },
    minimap: {
      enabled: true, // ミニマップ（鳥瞰ビュー）を表示
      width: 240,
      opacity: 0.85,
    },
    theme: 'system',
  })
</script>

<template>
  <div style="height: 500px;">
    <gantt-chart :rows="rows" :option="option" />
  </div>
</template>
```

## クイックスタート（React）

React では Web Components の特性上、`ref` 経由でプロパティを設定します。

```tsx
import { useEffect, useRef } from 'react'
import '@mogura/moguchart-core'
import type { GanttRow, GanttChartOption } from '@mogura/moguchart-core'

export default function GanttDemo() {
  const chartRef = useRef<any>(null)

  const rows: GanttRow[] = [
    {
      id: 'row-1',
      name: '開発チームA',
      tasks: [
        {
          id: 't-1',
          name: 'API設計',
          start: new Date('2025-06-01'),
          end: new Date('2025-06-10'),
          progress: 100,
          style: 'background-color: #60a5fa',
        },
      ],
    },
  ]

  const option: GanttChartOption = {
    calendar: {
      start: new Date('2025-06-01'),
      end: new Date('2025-07-31'),
      pxPerDay: 30,
      showCurrentTime: true,
    },
    zoom: {
      enabled: true,
    },
    progress: {
      enabled: true,
      editable: true,
      showLabel: true,
    },
    selection: {
      marquee: true,
    },
    minimap: {
      enabled: true,
      width: 240,
      opacity: 0.85,
    },
    theme: 'system',
  }

  useEffect(() => {
    const chart = chartRef.current
    if (!chart) return
    chart.rows = rows
    chart.option = option
  }, [])

  return (
    <div style={{ height: '500px' }}>
      <gantt-chart ref={chartRef} />
    </div>
  )
}
```

## 機能ハイライト

### 🔲 矩形範囲選択（ラバーバンド選択 / Marquee Selection）

ガントチャートの日付グリッド領域（空白背景）をマウスでドラッグすることで、矩形選択ボックス（ラバーバンド）を表示し、交差・囲まれた複数のタスクバーを一括選択できます。

- **リアルタイム交差判定**: AABB（Axis-Aligned Bounding Box）判定により、ドラッグ操作中に交差したタスクバーがリアルタイムにハイライト選択されます
- **追加選択（累積選択）**: `Shift`、`Ctrl`、または `Cmd` キーを押しながらドラッグすることで、既存の選択状態を保持したまま追加で範囲選択が可能です
- **オートスクロール**: ドラッグ中にチャート端に近づくと、画面外に広がるタスクへ向かって自動的にスクロールします
- **誤操作防止**: 4px未満のマウス移動は通常のクリック（選択解除）として扱い、誤った矩形選択の発生を防ぎます
- **一括操作との連携**: 選択された複数タスクは、そのまま一括ドラッグ移動、キーボード移動（`Shift + 左右矢印`）、一括削除（`Delete` キー）と完全に連動します

```javascript
const chart = document.querySelector('gantt-chart')

chart.option = {
  // ...
  selection: {
    marquee: true,          // 矩形範囲選択を有効化 (デフォルト: true)
    borderColor: '#3b82f6', // 選択枠線の色 (未指定時はテーマ色)
    backgroundColor: 'rgba(59, 130, 246, 0.15)', // 選択背景色
  },
}

// 選択変更イベントリスナー
chart.addEventListener('bar-selection-change', (e) => {
  const { selectedIds } = e.detail
  console.log('選択されたタスクID一覧:', selectedIds)
})
```

### 📊 タスク進捗管理 ＆ インタラクティブドラッグ編集

各タスクの `progress` プロパティ（`0` 〜 `100`）を設定することで、タスクバー上に進捗状況を視覚的に表示できます。
さらに、`editable: true` を有効にすると、進捗バー端のハンドルをドラッグしてマウス操作だけで直感的に進捗率を変更できるようになります。

- **インジケータースタイル**: バー全体を塗りつぶす `full`（デフォルト）のほか、バー下部に帯状に表示する `bottom`、上部に表示する `top` から選択可能
- **インタラクティブなハンドル編集**: 進捗バー右端のハンドルをドラッグして進捗率を変更。ホバー・ドラッグ時にはハンドルが拡大表示されます
- **スナップ＆キャンセル**: `snapStep`（例: 5%刻み）で数値をキリよくスナップ。ドラッグ中に `Escape` キーを押すと即座にキャンセルされ元の進捗率にロールバックします
- **進捗ラベルの表示**: `showLabel: true` で進捗率（例: "45%"）を表示。配置位置（`inside`, `right`, `left`, `center`）やカスタムフォーマッタ（`labelFormatter`）も柔軟に指定可能
- **進捗計算ユーティリティ関数**: 単純平均や期間加重平均（タスク期間に応じた重み付け計算）を算出するヘルパー関数を標準エクスポート

```javascript
import {
  clampProgress,
  calculateRowProgress,
  calculateWeightedRowProgress,
  calculateProjectProgress,
} from '@mogura/moguchart-core'

const chart = document.querySelector('gantt-chart')

chart.option = {
  // ...
  progress: {
    enabled: true,         // 進捗表示を有効化 (デフォルト: true)
    editable: true,        // ドラッグによる進捗率編集を有効化 (デフォルト: false)
    showLabel: true,       // 進捗ラベル (例: "45%") を表示
    labelPosition: 'inside', // 'inside' | 'right' | 'left' | 'center'
    snapStep: 5,           // 5%刻みでスナップ (デフォルト: 1)
    indicatorPosition: 'full', // 'full' | 'bottom' | 'top'
    color: '#3b82f6',      // 進捗バーの色
  },
}

// 進捗変更イベント
chart.addEventListener('task-progress-change', (e) => {
  const { task, progress, originalProgress, cancelled } = e.detail
  if (cancelled) {
    console.log(`タスク ${task.name} の進捗変更がキャンセルされました`)
    return
  }
  console.log(`タスク ${task.name}: ${originalProgress}% → ${progress}%`)
})

// 行・プロジェクト全体の進捗率を計算
const rowSimpleAvg = calculateRowProgress(row)          // 行内タスクの単純平均
const rowWeightedAvg = calculateWeightedRowProgress(row) // 期間による加重平均
const projectProgress = calculateProjectProgress(rows)   // プロジェクト全体の期間加重平均
```

### 🗺️ ミニマップ（Overview Minimap）

ガントチャート全体のタスク配置・マイルストーン・現在時刻線を鳥瞰できるフローティング小窓型のミニマップです。

- **ビューポートナビゲーション**: ミニマップ内の半透明フレーム（現在の表示領域）をドラッグしてスクロール（パン）したり、任意の位置をクリックして瞬時にジャンプ移動できます。
- **ドラッグリサイズ ＆ ドラッグ移動**: 端のリサイズハンドルで拡大・縮小（アスペクト比維持対応）、タイトルバーのドラッグで自由な位置へ移動できます。
- **自動アンカー ＆ はみ出し防止**: 右下基準座標（`right`, `bottom`）で管理され、親要素のリサイズ時にも安定して表示位置を自動追従します。
- **透過率（不透明度）調整**: `opacity`（`0.1`〜`1.0`）を設定可能。半透明で背面のタスクを見通せ、ホバー時や操作時には自動で 1.0 に戻ります。
- **折りたたみ（最小化）**: 最小化ボタンでコンパクトなアイコンへ折りたためます。
- **進捗状況の自動反映**: 各タスクの進捗率がミニマップ上のバーにも濃淡として自動的に描画され、全体の進捗状況を一目で鳥瞰できます。

```javascript
const chart = document.querySelector('gantt-chart')

chart.option = {
  // ...
  minimap: {
    enabled: true,
    width: 240,
    preserveAspectRatio: true,
    resizable: true,
    position: { right: 16, bottom: 16 }, // 初期位置（右下基準 px）
    opacity: 0.85, // 不透明度 (0.1 〜 1.0)
  },
}

// 各種イベントリスナー
chart.addEventListener('minimap-resize', (e) => {
  const { width, height, position } = e.detail
  console.log(`Minimap resized: ${width}x${height}`, position)
})

chart.addEventListener('minimap-move', (e) => {
  const { right, bottom } = e.detail
  console.log(`Minimap moved to: right=${right}, bottom=${bottom}`)
})

chart.addEventListener('minimap-collapse', (e) => {
  const { collapsed } = e.detail
  console.log(`Minimap collapsed: ${collapsed}`)
})
```

### 🎯 タスクのドラッグ＆ドロップ ＆ 行間移動制御

タスクバーをドラッグして日程変更。行をまたいだ移動（上下移動）にも対応しています。
`Ctrl`（Mac: `Cmd`）+ クリックで複数選択し、一括ドラッグ移動（垂直移動含む）が可能です。

さらに、`enableCrossRowMove: false` を指定することで、**「同一行内でのみ日付移動を許可し、他の行への移動を禁止する」** といった制御も簡単に行えます。

```javascript
const option = {
  enableCrossRowMove: false, // 行間移動を禁止（横方向の日程移動のみに制限）
}

chart.addEventListener('task-update', (e) => {
  const { id, start, end, targetRowId, mode, selectedTaskIds, isCancel } = e.detail
  if (isCancel) {
    console.log('ドラッグ操作がキャンセルされました')
    return
  }
  console.log(`タスク ${id} を ${start} 〜 ${end} に移動 (移動先: ${targetRowId})`)
})
```

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/drag-and-drop.gif" width="700" alt="drag-and-drop.gif">

ガントチャートの外部から新規タスクバーをドラッグ＆ドロップして配置することも可能です。

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/task-template.gif" width="500" alt="task-template.gif">

### 📐 依存関係線 ＆ ⚡ クリティカルパス自動検出

タスクの `dependencies` に依存先のIDを指定するだけで、矢印付きの接続線が描画されます。

```javascript
const task = {
  id: 't-2',
  name: '実装',
  start: new Date('2025-06-10'),
  end: new Date('2025-06-25'),
  dependencies: ['t-1'], // t-1 の完了後に開始
}
```

接続線のスタイルは `orthogonal`（直角折れ線・角丸、デフォルト）と `curve`（ベジェ曲線）から選択できます。また、タスクバーの端にある接続ポイント（コネクター）からドラッグして視覚的に依存関係を作成することもできます。

さらに、`dependency.showCriticalPath: true` を有効にすると、**依存関係ネットワークから全体の遅延に直結する最長経路（クリティカルパス）を自動計算し、該当するバーと接続線を赤色でハイライト** します！

```javascript
const option = {
  dependency: {
    lineStyle: 'orthogonal',   // 'orthogonal' | 'curve'
    showArrows: true,
    showConnectors: true,      // ドラッグで依存作成可能
    showCriticalPath: true,    // クリティカルパスをハイライト
  },
}
```

![dependencies.gif](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/dependencies.gif)

### 🔍 スムーズなズーム操作＆自動フィット

`zoom.enabled: true` を設定するだけで、チャート上で **`Ctrl`（Mac: `Cmd`）+ マウスホイールによる直感的なズームイン・ズームアウト** が可能になります（カーソル位置を中心に拡大縮小）。

また、JavaScript メソッドからズームを自在に制御できます。

```javascript
const chart = document.querySelector('gantt-chart')

// 全タスクが表示領域に収まるようにズーム倍率を自動計算＆スクロール
chart.zoomToFit()

// 指定したピクセル幅（pxPerDay）にズーム
chart.zoomTo(60)

// オプション設定時の元のスケールにリセット
chart.resetZoom()
```

### ⌨️ キーボード操作

ガントチャートにフォーカスがある状態で、キーボードだけでタスクの選択・移動・削除が行えます。

| キー | 動作 |
| :--- | :--- |
| `←` `→` | 前後のタスクへフォーカス移動 |
| `↑` `↓` | 前後の行へフォーカス移動 |
| `Enter` / `Space` | フォーカス中のタスクを選択 |
| `Ctrl/Cmd + Enter` | 選択状態をトグル（複数選択） |
| `Shift + ←` `→` | 選択中のタスク（複数選択・矩形選択を含む）を左右に移動 |
| `Delete` / `Backspace` | `task-delete` イベントを発火（選択中タスクの削除要求） |
| `Escape` | 選択・フォーカスを解除 / ドラッグ操作のキャンセル |

矩形範囲選択（ラバーバンド選択）や `Ctrl/Cmd + クリック` で複数選択したタスクも、`Shift + 矢印キー` でまとめて一括移動したり、`Delete` キーでまとめて削除要求イベントを発行できます。

```javascript
chart.addEventListener('task-delete', (e) => {
  const { taskId, task } = e.detail
  console.log(`タスク ${task.name} (${taskId}) の削除要求`)
})
```

### 🎨 テーマ＆カスタムカラー

```javascript
const option = {
  theme: 'dark', // 'light' | 'dark' | 'system'
  customTheme: {
    bg: '#1a1a2e',
    currentTimeLine: '#ff6b6b',
    criticalPath: '#ef4444',
    saturday: '#1e3a5f',
    minimapBg: '#16213e',
    minimapViewport: 'rgba(255, 255, 255, 0.15)',
    taskProgress: '#3b82f6',              // 進捗バーのハイライト色
    taskProgressHandle: '#60a5fa',        // 進捗ドラッグハンドルの色
    selectionMarqueeBorder: '#3b82f6',    // 矩形選択ボックスの枠線色
    selectionMarqueeBg: 'rgba(59, 130, 246, 0.2)', // 矩形選択ボックスの背景色
  },
}
```

`ThemeColorPalette` では **30 以上のカラートークン** をオーバーライドでき、ブランドカラーに合わせた細かなカスタマイズが可能です。

![demo-dark.png](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/demo-dark.png)

### 🏁 マイルストーン

チャート上に縦線＋名前バッジでマイルストーンを表示できます。

```javascript
option.calendar.milestones = [
  {
    id: 'ms-1',
    name: 'α版リリース',
    start: new Date('2025-07-01'),
    color: '#8b5cf6',
  },
]
```

![milestone.gif](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/milestone.gif)

### 📍 マーカー（行内目印）

各行のタイムライン上に三角形アイコンやラベルで目印を表示できます。
同じ行内でマーカーが重なった場合は **自動的にマルチレーン配置** されるため、文字が被る心配がありません。
フォントサイズ（`xs`〜`xl`）の指定や、ダブルクリック（`marker-dblclick`）・右クリック（`marker-contextmenu`）イベント、選択中マーカーのパルスアニメーションにも対応しています。

```javascript
const row = {
  id: 'row-1',
  name: 'タスクA',
  tasks: [/* ... */],
  markers: [
    {
      id: 'marker-1',
      name: '中間レビュー',
      date: new Date('2025-06-15'),
      type: 'triangle-down',
      fontSize: 'sm', // 'xs' | 'sm' | 'md' | 'lg' | 'xl'
      color: '#ef4444',
    },
  ],
}
```

![marker.png](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/marker.png)

### 🖌️ タスクバーの塗りつぶしパターン

**13 種類** のパターン（ストライプ、ドット、チェッカーボードなど）をタスクバーに適用可能。ステータスの視覚的な区別に活用できます。

```javascript
import { PATTERN_DIAGONAL_STRIPE } from '@mogura/moguchart-core'

const task = {
  id: 't-1',
  name: '作業中',
  start: new Date('2025-06-01'),
  end: new Date('2025-06-05'),
  style: 'background-color: #60a5fa',
  pattern: PATTERN_DIAGONAL_STRIPE,
}
```

### 📅 表示モードの切り替え

| モード | 設定 | 用途 |
| :--- | :--- | :--- |
| **日単位** | `pxPerDay: 48` | 通常のプロジェクト管理 |
| **週単位** | `showWeeks: true`, `pxPerDay: 12` | 中長期の俯瞰 |
| **月単位** | `pxPerMonth: 120` | 年単位のロードマップ（等幅表示・最大100年） |
| **時間単位** | `pxPerDay: 960`, `showTime: true` | シフト管理・細かなスケジューリング |

![view-mode.gif](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-core-introduction/view-mode.gif)

### 🖋️ 高度なカスタムレンダリング

タスクバー・行ヘッダー・ツールチップ・カレンダーセル・行背景セル・**行ヘッダー用ツールチップ** などの描画を関数でオーバーライドでき、HTML文字列や Lit の `TemplateResult` を自由に返せます。

```javascript
const option = {
  customRendering: {
    // タスクバーの内部表示
    barContent: (task) => `<strong>${task.name}</strong>`,
    // 行ヘッダーの表示
    rowHeaderContent: (row) => `<div>${row.name}<br/><small>${row.id}</small></div>`,
    // 行ヘッダーにホバーしたときのツールチップ
    rowHeaderTooltip: (row) => `${row.name} (タスク数: ${row.tasks.length})`,
    // タスクのツールチップ
    tooltip: (task) => `${task.name}: ${task.start.toLocaleDateString()} 〜`,
  },
}
```

### 🌐 ロケール＆祝日判定

日本語/英語のビルトインロケールを切り替えるだけでなく、カスタムロケールや祝日判定関数の注入に対応しています。

```javascript
import { enLocale } from '@mogura/moguchart-core'

const option = {
  locale: enLocale,
  calendar: {
    isHoliday: (date) => {
      // 独自の祝日・休業日判定ロジック
      return checkCustomHoliday(date)
    },
  },
}
```

### 📤 高解像度 画像/PDF エクスポート

チャートを PNG 画像や PDF として書き出すメソッドを内蔵しています（`html2canvas-pro` / `jspdf` を利用）。Shadow DOM 内の描画コンテナを直接キャプチャするため正確に出力でき、エクスポート実行時も現在のスクロール位置が保持・復元されます。

`splitHeight` を指定すると、行の途中で切れないよう境界に合わせて **複数ページに分割されたPDF** を簡単に出力できます。

```javascript
const chart = document.querySelector('gantt-chart')
// PNG 画像ダウンロード
await chart.exportImage('png', { download: true, filename: 'gantt' })
// 複数ページ分割 PDF ダウンロード
await chart.exportImage('pdf', { download: true, filename: 'gantt', splitHeight: 1200 })
```

### 🛠️ 便利なパブリックメソッド

```javascript
// 指定タスクを選択してその位置まで自動スクロール
chart.selectTask('t-1')

// マウス座標（clientX, clientY）から該当する行IDと日付を取得（hitTest）
const hit = chart.hitTest(e.clientX, e.clientY)
if (hit) {
  console.log(`行: ${hit.rowId}, 日時: ${hit.date}`)
}
```

## アーキテクチャ

```
@mogura/moguchart-core
├── components/
│   ├── gantt-chart.ts                 # メインコンポーネント (Custom Element)
│   ├── gantt-minimap.ts               # ミニマップ（Overview Minimap）
│   ├── gantt-calendar.ts              # カレンダーヘッダー
│   ├── gantt-bar.ts                   # タスクバー
│   ├── gantt-row.ts                   # 行コンポーネント (マーカー・レーン配置)
│   ├── gantt-row-background.ts        # 行背景（土日祝ハイライト）
│   ├── gantt-chart-dependency-path.ts # 依存関係線の描画 (S字・直角・クリティカルパス)
│   ├── gantt-chart-export.ts          # PNG/PDF エクスポート
│   └── gantt-chart-styles.ts          # CSS スタイル定義
└── core/
    ├── types.ts         # 全型定義（充実したTypeScript型）
    ├── critical-path.ts # クリティカルパス自動計算ロジック
    ├── theme.ts         # テーマカラーパレット
    ├── patterns.ts      # バーパターン（SVG背景生成）
    ├── i18n.ts          # ロケール定義
    ├── utils.ts         # ユーティリティ関数
    └── constants.ts
```

Lit の Reactive Properties を活用し、`rows` や `option` が変更されると自動的に再レンダリングされます。仮想スクロールにより、画面外の要素はDOMに描画されないため、大量データでも軽快に動作します。

## 📱 moguchart-core を使ったアプリケーション「MoguChart」

moguchart-core は汎用ライブラリとして開発していますが、実は **このライブラリを活用した本格的なプロジェクト管理アプリケーション「MoguChart」** も並行して開発しています。

MoguChart は Vue 3 + Vuetify 4 をベースに、moguchart-core のガントチャートコンポーネントを中心に据えた Web アプリケーションです。ドラッグ＆ドロップ操作・リアルタイム共同編集・画像添付・権限管理など、実務で使える豊富な機能を備えています。

👉 **MoguChart アプリケーションの詳細は別記事で紹介しています！**

- **UX・機能詳細**: [無料で使えるWebガントチャート「MoguChart」を作った ─ 個人開発で追求した"ちょうどいい"プロジェクト管理UX](https://qiita.com/hiroyuki_m/items/bfdaf141de040cb387b9)
- **全体アーキテクチャ**: [個人開発で本格ガントチャートWebアプリ「MoguChart」を作った話 ─ 自作Web Components × Vue 3 × Firebase のアーキテクチャ全解剖](https://qiita.com/hiroyuki_m/items/d1d2b644890e49b796e7)
- **リアルタイム共同編集**: [ガントチャートWebアプリにリアルタイム共同編集を実装した話 ─ Firestore × Vue 3 で実現するプレゼンス・イベント同期アーキテクチャ](https://qiita.com/hiroyuki_m/items/9664fa9018efc06059f2)

ライブラリ単体の機能に興味を持っていただけた方は、ぜひアプリケーション側の記事もご覧ください 🙌

## おわりに

moguchart-core は、**「フレームワークに縛られず、高機能なガントチャートを手軽に組み込みたい」** という自分自身のニーズから生まれたライブラリです。

v0.12.0 では、ガントバーの矩形範囲選択（ラバーバンド選択）機能や、タスク進捗率の視覚的表示・直感的なドラッグ編集、進捗率計算ユーティリティ関数をはじめ、ミニマップ機能、クリティカルパスの自動ハイライト、スムーズなホイールズーム、高解像度エクスポートなど、商用ライブラリに匹敵する実用的な機能が一段と揃いました。

フィードバックや Issue、Pull Request を大歓迎しています！

https://github.com/hiro-murakami/moguchart-core

何か質問や要望があれば、お気軽にどうぞ 🙌

## 参考リンク

- [デモサイト](https://moguchart-core.vercel.app)
- [GitHub リポジトリ](https://github.com/hiro-murakami/moguchart-core)
- [API リファレンス（日本語）](https://github.com/hiro-murakami/moguchart-core/blob/develop/doc/API.ja.md)
- [Lit 公式サイト](https://lit.dev/)
- [Web Components - MDN](https://developer.mozilla.org/ja/docs/Web/API/Web_components)
