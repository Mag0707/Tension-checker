# 過緊張チェックタイマー / Tension Check Timer

## 日本語

### 概要
集中しすぎによる身体の緊張に気づき、定期的に力を抜くきっかけを作るための個人用タイマーです。

### カラーテーマ
- パウダースカイ（初期値）
- ミスティラベンダー
- セージグレージュ
- スモーキーローズ

### フォントクレジット
- Klee One
- 提供: Fontworks Inc.
- URL: https://fonts.google.com/specimen/Klee+One?subset=japanese

### サウンドクレジット
#### カフェの環境音
- 提供: PWLPL
- URL: https://pixabay.com/users/pwlpl-16464651/
- 使用ファイル: `sounds/pwlpl-busy-coffee-shop-ambiance-with-crowd-chatter-481151.mp3`

#### やさしい雨
- 提供: DRAGON-STUDIO
- URL: https://pixabay.com/users/dragon-studio-38165424/
- 使用ファイル: `sounds/dragon-studio-gentle-midday-rain-499668.mp3`

### 音声ファイルの配置
以下の2ファイルを、ファイル名を変更せず `sounds` フォルダに配置してください。

```text
sounds/
├── dragon-studio-gentle-midday-rain-499668.mp3
└── pwlpl-busy-coffee-shop-ambiance-with-crowd-chatter-481151.mp3
```

---

## English

### Overview
A personal timer designed to help notice physical tension caused by over-focusing and create regular opportunities to relax.

### Color Themes
- Powder Sky (default)
- Misty Lavender
- Sage Greige
- Smoky Rose

### Font Credit
- Klee One
- Provided by: Fontworks Inc.
- URL: https://fonts.google.com/specimen/Klee+One?subset=japanese

### Sound Credits
#### Café Ambience
- Provided by: PWLPL
- URL: https://pixabay.com/users/pwlpl-16464651/
- File used: `sounds/pwlpl-busy-coffee-shop-ambiance-with-crowd-chatter-481151.mp3`

#### Gentle Rain
- Provided by: DRAGON-STUDIO
- URL: https://pixabay.com/users/dragon-studio-38165424/
- File used: `sounds/dragon-studio-gentle-midday-rain-499668.mp3`

### Audio File Placement
Place the following two files inside the `sounds` folder without changing their filenames.

```text
sounds/
├── dragon-studio-gentle-midday-rain-499668.mp3
└── pwlpl-busy-coffee-shop-ambiance-with-crowd-chatter-481151.mp3
```


## 身体チェック記録とエクスポート

集中時間が終了するたびに、身体の具体的なサインを確認する質問がランダムで1問表示されます。回答はこの端末内の `localStorage` に保存され、設定画面からCSVまたはJSONでエクスポートできます。

「今回は記録しない」を選んだ場合は、回答データは保存されません。設定画面の「記録を削除」では、確認メッセージの後に端末内の全履歴を削除します。

### 休憩中の回答動作
身体チェックの質問が表示されている間も、5分間の休憩カウントは進みます。質問画面には休憩の残り時間も表示されます。休憩時間内に回答されなかった場合は、質問を自動的に閉じ、`answerId` を `no_response`、回答を「回答なし（休憩時間内に未回答）」として保存してから次の集中時間へ移ります。

### エクスポート項目

| 項目 | 説明 |
|---|---|
| `recordVersion` | 記録形式のバージョン。将来の形式変更を判別するための番号です。 |
| `answeredAt` | 回答日時。端末のタイムゾーンを含むISO 8601形式です。 |
| `questionId` | 質問を識別する固定IDです。表示文を変更しても同じ質問として集計できます。 |
| `question` | 回答時に画面へ表示された質問文です。 |
| `bodyArea` | 確認した身体部位・カテゴリーです。例：`shoulders`、`jaw`、`breathing`。 |
| `answerId` | 回答を識別する固定IDです。言語に依存せず集計できます。休憩終了まで未回答の場合は `no_response` です。 |
| `answer` | 回答時に画面へ表示された回答文です。休憩終了まで未回答の場合は「回答なし（休憩時間内に未回答）」です。 |
| `soundId` | 回答前の集中時間に使用していたサウンドの固定IDです。 |
| `sound` | 回答前の集中時間に使用していたサウンドの表示名です。 |
| `focusDurationMinutes` | 設定されていた集中時間です。単位は分です。 |
| `actualFocusSeconds` | 完了した集中時間です。単位は秒です。 |
| `cycleNumber` | その回答が行われたセット番号です。 |
| `checkTiming` | 質問が表示されたタイミングです。現在は `focus_end`（集中終了時）です。 |
| `language` | 回答時の表示言語です。`ja` または `en` です。 |

CSVは表計算ソフトやChatGPTでの集計・分析に向いています。JSONはデータ構造を保ったバックアップに向いています。

---

## Body Check Records and Export

After each focus session, one randomly selected question asks about a specific physical sign. Answers are stored in this device's `localStorage` and can be exported as CSV or JSON from the settings screen.

Selecting “Do not record this time” does not save a response. The “Delete Records” button removes all locally stored history after a confirmation message.

### Answering During the Break
The five-minute break countdown continues while the body-check question is displayed, and the remaining break time is shown in the dialog. If no answer is selected before the break ends, the dialog closes automatically and a record is saved with `answerId` set to `no_response` and the answer text set to “No response before the break ended” before the next focus session begins.

### Export Fields

| Field | Description |
|---|---|
| `recordVersion` | Version number of the record format, used to identify future format changes. |
| `answeredAt` | Date and time of the answer in ISO 8601 format, including the device time-zone offset. |
| `questionId` | Stable ID identifying the question, allowing aggregation even if its displayed wording changes. |
| `question` | Question text displayed when the answer was recorded. |
| `bodyArea` | Body area or category checked, such as `shoulders`, `jaw`, or `breathing`. |
| `answerId` | Stable ID identifying the answer independently of display language. It is `no_response` when the break ends without an answer. |
| `answer` | Answer text displayed when the response was recorded. When unanswered at break end, it is “No response before the break ended.” |
| `soundId` | Stable ID of the focus sound used before the answer. |
| `sound` | Display name of the focus sound used before the answer. |
| `focusDurationMinutes` | Configured focus duration in minutes. |
| `actualFocusSeconds` | Completed focus duration in seconds. |
| `cycleNumber` | Session cycle number associated with the response. |
| `checkTiming` | Point at which the question was shown. Currently `focus_end`. |
| `language` | Display language at the time of the response: `ja` or `en`. |

CSV is suited to aggregation and analysis in spreadsheets or ChatGPT. JSON is suited to complete structured backups.

### iPhoneでのアラート音
集中中の環境音がMP3の場合でも、タイマー開始時のユーザー操作でWeb Audioをあらかじめ有効化します。これにより、集中終了時に操作なしで鳴るアラート音がiPhoneで無音になる問題を防ぎます。

### Alert Sound on iPhone
Even when the focus ambience uses an MP3 file, Web Audio is unlocked during the user's Start action. This prevents the focus-end alert from becoming silent on iPhone when it needs to play later without another user gesture.


## アラート音の再生方式

集中終了・休憩終了のアラート音は、Web Audioによるリアルタイム合成ではなく、アプリに同梱した短いMP3ファイルを使用します。

- `sounds/soft-chime.mp3`
- `sounds/bell.mp3`
- `sounds/digital-tone.mp3`

試聴とタイマー終了時のどちらも、同じHTMLAudioElement方式で再生します。これにより、iPhoneでWeb Audioが停止状態になってアラートが無音になる問題を避けます。

---

## Alert Sound Playback

Focus-end and break-end alerts use short MP3 files bundled with the app instead of real-time Web Audio synthesis.

- `sounds/soft-chime.mp3`
- `sounds/bell.mp3`
- `sounds/digital-tone.mp3`

Both previews and timer-end alerts use the same HTMLAudioElement playback method. This avoids silent alerts caused by a suspended Web Audio context on iPhone.


## iPhone向けアラート再生の保持方式

第38版では、アラート音をタイマー終了時に新しく作成しません。スタート操作時に選択中のMP3を同じ `HTMLAudioElement` で短く事前再生し、その要素を保持したまま集中終了時に再利用します。

- スタート時に選択中のアラート音を極小音量で約0.08秒だけ事前再生
- 事前再生後は停止して先頭へ戻す
- 集中終了時は新しいAudio要素を作らず、保持済みの同じ要素を再生
- アラート音の選択を変更した場合も、そのユーザー操作内で新しい選択音を準備

---

## Persistent Alert Playback for iPhone

Version 38 does not create a new audio element when the timer ends. During the Start action, the selected MP3 is briefly primed using the same `HTMLAudioElement`, which is retained and reused for the focus-end alert.

- The selected alert is primed at extremely low volume for about 0.08 seconds
- It is then paused and reset to the beginning
- The focus-end alert reuses the same retained audio element
- Changing the selected alert also primes the new selection within that user action
