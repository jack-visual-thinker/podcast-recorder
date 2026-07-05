# 🎙️ ポケット収録 — Anchor復刻MVP

スマホのブラウザだけで完結するポッドキャスト収録アプリ。
収録（チャンク方式）→ 並べ替え → BGM挿入 → 1本に結合してWAV書き出し。
サーバー・ログイン・インストール、すべて不要。

## ファイル

- `index.html` — アプリ本体（これ1つで完結）
- `FABLE5-PROMPT.md` — 実装仕様書

## 使い方（スマホ）

1. `index.html` をどこかのURLで開く（下記「公開方法」参照）
2. 赤い●ボタンで録音開始／停止。停止するとチャンクとしてリストに追加
3. ⏸ で一時停止・再開
4. 「🎵 BGMを追加」で手持ちの音声ファイル（mp3/m4a/wav等）を挿入
5. ≡ をドラッグしてチャンクを並べ替え、🗑 で削除、▶ で試聴
6. 「📦 1本にまとめて書き出す」→ WAVファイルがダウンロードされる
7. そのファイルを Spotify for Creators に手動アップロード

⚠️ 収録中は画面を消さないこと（iOSはバックグラウンドで録音が止まる）。
⚠️ ページを閉じるとチャンクは消える（書き出してから閉じる）。

## 公開方法（どれか1つ）

- **GitHub Pages**（推奨・無料）：このフォルダをリポジトリにpushして Pages を有効化
- **Netlify Drop**：https://app.netlify.com/drop にフォルダをドラッグするだけ
- **ローカル確認**：`npx serve projects/podcast-recorder` → 同じWi-FiのスマホからMacのIPで開く

※ マイクは HTTPS（または localhost）でしか動かない。GitHub Pages / Netlify はHTTPSなのでOK。

## 技術メモ

- 収録：`MediaRecorder`（Safari=audio/mp4, Chrome=webm/opus を自動選択）
- 結合：`decodeAudioData` → `OfflineAudioContext` で直列レンダリング
- 書き出し：16-bit PCM WAV（確実に鳴ることを優先。約5MB/分・モノラル時）
- 依存ライブラリなし。素のHTML/CSS/JS 1ファイル。
