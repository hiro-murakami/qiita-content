---
title: 【祝 v1.0】無料でここまで動く！WBS・サマリー自動集計に対応したWebガントチャート「MoguChart」を正式リリースしました
tags:
  - 個人開発
  - ガントチャート
  - プロジェクト管理
  - 生産性向上
  - Webサービス
private: false
updated_at: "2026-09-13T15:00:26+09:00"
id: 47f635a93c5e9d831b5a
organization_url_name: null
slide: false
ignorePublish: false
posting_campaign_uuid: null
agreed_posting_campaign_term: false
---

![top.png](https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-app-ux/top-2.png)

## はじめに

個人開発でガントチャート描画エンジンから自作してきた Web アプリケーション **「[MoguChart（モグチャート）](https://moguchart.jp)」** が、ついに **メジャーバージョン 1.0.0** に到達しました！🎉

https://moguchart.jp

「ガントチャートだけを徹底的に、かつ直感的にサクサク使いたい」という想いで開発を続け、実務レベルのプロジェクト管理に不可欠な **WBS（階層ツリー構造・行の開閉）** と **サマリータスク（自動集計・描画）** を搭載した正式版となります。

Google アカウントでのログインはもちろん、**登録不要の「ゲストログイン」** でアクセス後 1 秒ですぐにお試しいただけます。

---

## こんな人におすすめ

- 📊 **Excel やスプレッドシートのガントチャートで、セル結合や行追加のズレに疲弊している人**
- 🛠 **海外製のプロジェクト管理ツールは多機能すぎて重い、あるいは学習コストや費用が高いと感じている人**
- 🖱 **とにかくドラッグ＆ドロップで、直感的に日程や進捗率をグリグリ動かしたい人**
- 🤝 **チームメンバーと同じ画面を見ながらリアルタイムに共同編集したい人**

---

## v1.0 の最大の進化：WBS ＆ サマリー自動集計

v1.0.0 リリースの最大のハイライトは、中〜大規模プロジェクトを整理するために欠かせない **WBS（Work Breakdown Structure）** と **サマリータスク** の全面サポートです。

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-v1-release/WBS.gif" alt="WBS.gif">

### 1. 無制限の階層ツリー ＆ ワンクリック開閉

- 行のメニューから「インデント（子行化）」「アウトデント（親レベルへ昇格）」を直感的に切り替え可能。
- 親行の左側に表示される開閉トグルアイコン（▶ / ▼）で、配下の子孫タスクを**ワンクリックで展開・折りたたみ**できます。
- 親行をドラッグして並び替えると、配下の子孫行も**ブロックとして一体となって安全に追従移動**します（循環参照も自動防止）。

### 2. サマリータスクの期間・進捗率を自動集計

- 子階層を持つ親行には、配下の全タスクの「最小開始日」〜「最大終了日」、そして「期間加重平均進捗率」を自動集計した**サマリーバー（ブラケット形状）**が自動描画されます。
- 子タスクの期間や進捗率をマウスで変更すると、親のサマリーバーもリアルタイムに連動して更新されます。
- 親行自身に通常タスクが登録されている場合でも、上段にサマリーバー、下段に通常タスクが並んで描画される**二段共存描画**に対応しています。

---

## MoguChart のここが便利！推し機能 5 選

v1.0 に至るまでに磨き込んできた、直感的な操作感を支える機能たちです。

### ① 登録不要！1クリックで試せるゲストログイン

「試すためだけにアカウント登録するのはちょっと…」という方でも安心です。
トップページの「ゲストとして利用」ボタンを押すだけで、登録不要ですぐに全機能をブラウザ上でお試しいただけます。

### ② 空白ドラッグで一括操作！「矩形範囲選択（ラバーバンド）」

ガントチャートの空白エリアをドラッグすると、青い選択枠（ラバーバンド）が出現し、範囲内の複数タスクを一括選択できます。
そのまま一括ドラッグ移動、キーボードによる日付微調整、一括コピー＆ペースト（Cmd+C / Cmd+V）、一括削除がシームレスに行えます。

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-v1-release/rubber-band-select.gif" alt="rubber-band-select.gif">

### ③ つまんで動かす「進捗率ドラッグ編集」

タスクバーの右端にある進捗ハンドルをマウスでドラッグするだけで、進捗率（0〜100%）を 5% 刻みで直感的に変更できます。
進捗管理を行わないシンプルなプロジェクトでは、設定から進捗率表示をまるごと OFF にすることも可能です。

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-v1-release/progress.gif" width="300" alt="progress.gif">

### ④ 巨大なプロジェクトでも迷子にならない「ミニマップ（鳥瞰ビュー）」

画面右下にガントチャート全体を俯瞰できるミニマップを搭載しています。
ミニマップ内の表示枠をドラッグするだけで、見たい期間・エリアへ瞬時にジャンプできます。半透明化・リサイズ・最小化にも対応しています。

<img src="https://raw.githubusercontent.com/hiro-murakami/qiita-content/main/images/moguchart-v1-release/mini-map.gif" alt="mini-map.gif">

### ⑤ リアルタイム共同編集 ＆ 画像付き ZIP バックアップ

- **リアルタイム共同編集**: チームメンバーと同じプロジェクトを同時に編集でき、誰がオンラインかもアバターでひと目で把握できます。
- **画像添付 ＆ 完全復元**: タスクや行にクリップボード（Ctrl+V）から直接画像を貼り付け可能。画像ファイルを含めたプロジェクト全体を 1 つの ZIP ファイルとして丸ごとエクスポート＆完全復元（リストア）できます。

---

## その他の実務向け機能も充実

- **時間単位・日単位・月単位の表示切り替え**（最大 100 年の長期ロードマップにも対応）
- **クリティカルパスの自動検出 ＆ ハイライト表示**
- **マイルストーン（全体目標）と行マーカー（工程目標）の可視化**
- **高画質 PNG / PDF エクスポート**（印刷や社内報告用）
- **公開 URL 発行**（ログイン不要で第三者に閲覧専用リンクを共有）
- **REST API (OpenAPI 3.0 準拠) ＆ Google Apps Script (GAS) 連携**

---

## 🛠 技術的な裏話（興味がある方向け）

MoguChart のガントチャート描画部分は、[Lit](https://lit.dev/) で実装したフレームワーク非依存の **Web Components ライブラリ（[`@mogura/moguchart-core`](https://github.com/hiro-murakami/moguchart-core)）** として独立させて開発しています。

「大量のタスクを並べても 60fps で滑らかにスクロールする高速な仮想スクロール機構」をコアエンジンとして作り込み、アプリケーション層（Vue 3 + Vuetify + Firebase）と疎結合に連携させています。

:::note info
**アーキテクチャや設計の詳細をもっと知りたい方はこちら**

- [個人開発で本格ガントチャートWebアプリ「MoguChart」を作った話 ─ 自作Web Components × Vue 3 × Firebase のアーキテクチャ全解剖](https://qiita.com/hiroyuki_m/items/d1d2b644890e49b796e7)
- [フレームワークに縛られないガントチャートを作った — Web Components製「moguchart-core」の紹介](https://qiita.com/hiroyuki_m/items/0e4859951a9f652c26c3)
- [ガントチャートWebアプリにリアルタイム共同編集を実装した話 ─ Firestore × Vue 3 で実現するプレゼンス・イベント同期アーキテクチャ](https://qiita.com/hiroyuki_m/items/9664fa9018efc06059f2)
  :::

---

## おわりに

構想から開発を重ね、ようやく「実務で自信を持って使える」と胸を張れる **v1.0.0** をリリースすることができました。

すべての基本機能は無料でご利用いただけます。
ぜひ一度、ブラウザでサクサク動くガントチャートを体験してみてください！

👉 **[MoguChart を使ってみる（moguchart.jp）](https://moguchart.jp)**

機能のご感想や「こんな機能がほしい！」といったフィードバックがあれば、Qiita のコメント欄や [GitHub Issues](https://github.com/hiro-murakami/moguchart-app/issues) でお気軽にお寄せいただけると励みになります！
