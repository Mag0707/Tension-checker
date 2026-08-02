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


## 集中BGMの2周目以降の再生

第39版では、集中BGM用の `HTMLAudioElement` を1セットごとに作り直さず、同じ要素をセッション中ずっと保持します。

- 最初の集中開始時にBGMを再生
- 集中終了〜休憩中はBGMを停止せず、音量を0にして無音化
- 次の集中開始時は新しい `play()` を行わず、同じAudio要素の音量を元に戻す
- 手動の一時停止ではBGMを `pause()` し、手動の再スタート時に同じ要素を再開
- リセット時のみ、BGMを停止して先頭へ戻し、保持しているAudio要素を破棄

これにより、iPhoneで2周目以降の自動開始時に新しい音声再生が拒否される問題を避けます。

---

## Focus BGM Playback Across Multiple Cycles

Version 39 keeps the same focus-BGM `HTMLAudioElement` alive for the entire timer session instead of recreating it for each focus cycle.

- The BGM starts during the first focus session
- During alerts and breaks, playback continues silently with volume set to 0
- The next focus session restores the volume without starting a new audio element
- Manual pause pauses the BGM, and manual resume restarts the same retained element
- Reset fully stops, rewinds, and discards the retained BGM element

This avoids iPhone rejecting a new automatic audio playback request when the second and later focus cycles begin.


## 第40版：休憩中のBGM停止方式

第39版では、休憩中もBGMを再生したまま `volume = 0` にしていましたが、iPhone実機で休憩中も音が聞こえ続ける事象が確認されたため、第40版では方式を変更しました。

- 集中終了時：BGMを `pause()` して確実に停止
- 休憩中：同じBGM用 `HTMLAudioElement` を保持したまま停止状態を維持
- 休憩中に一時停止・再開しても、BGMは停止したまま
- 次の集中開始時：新しいAudio要素は作らず、保持している同じ要素を `play()` して再開
- リセット時のみ、停止・先頭へ戻す・Audio要素を破棄

この版では「音量0で無音化」ではなく「休憩中は実際にpauseする」ことで、休憩中にBGMが聞こえ続ける問題を防ぎます。

---

## Version 40: BGM Handling During Breaks

Version 39 kept the focus BGM playing at `volume = 0` during breaks. Because the BGM could still be heard on iPhone, version 40 changes the behavior.

- At focus end: pause the BGM completely
- During breaks: keep the same retained `HTMLAudioElement`, but leave it paused
- Pausing and resuming the timer during a break does not restart the BGM
- At the next focus start: reuse the same retained audio element and call `play()`
- Only Reset rewinds and discards the retained BGM element

This replaces the volume-zero approach with a true pause during breaks.


## 第41版：カウントダウン表示のデザイン変更

第41版では、タイマー画面の見た目を次のように更新しました。

- 数字の周囲にSVGのリングを追加
- リングはテーマに合わせたグラデーション表示
- 省画面モード（黒背景）でもリングが見えるよう、黒背景用のグラデーション色を別指定
- リングは残り時間に応じて縮小
- 60分以上または1時間単位の設定では12時位置から開始
- 25分など1時間未満の設定では、終了時に12時位置へ到達する途中位置から開始
- 時刻表示は `mm:ss` から `mm m ss s` 表記へ変更

---

## Version 41: Countdown Ring and Time Format

Version 41 updates the timer screen design as follows.

- Added an SVG countdown ring around the timer
- The ring uses theme-based gradients
- Separate gradient colors are applied in dim mode (black background)
- The ring shrinks as the remaining time decreases
- For 60 minutes or exact hour-based durations, the ring starts at 12 o'clock
- For durations under 60 minutes, such as 25 minutes, the ring starts partway around the circle so that it finishes at 12 o'clock
- The time display format changes from `mm:ss` to `mm m ss s`


## 第42版：リング表示の位置・進行方向修正

- 時間表示をリング中央へ配置
- 数字がリングからはみ出しにくいよう文字サイズと横幅を調整
- リングのグラデーションを、淡色ではなく濃い同系色同士へ変更
- SVGリングの開始基準を12時位置へ修正
- 25分では、時計の5時位置まで色がついた状態から開始
- 残り時間が減るにつれてリングが反時計回りに縮み、0秒で12時位置へ戻る
- 60分・120分など1時間単位では、12時位置から一周分のリングで開始

---

## Version 42: Ring Position and Countdown Direction

- Centered the time display inside the SVG ring
- Adjusted typography so the timer stays within the ring
- Changed ring gradients to darker shades within each theme color
- Corrected the SVG ring origin to the 12 o'clock position
- A 25-minute timer begins with the arc ending at approximately 5 o'clock
- The arc shrinks back toward 12 o'clock as time counts down
- Exact hour durations such as 60 or 120 minutes begin with a full ring


## 第43版：身体チェック表示と集中終了アラート

- 第41版以降の時刻表示変更により、身体チェック表示時に存在しない旧関数を呼び出していた問題を修正
- 休憩開始時に身体チェック質問が再び表示されるよう修正
- 質問内の休憩残り時間も `05 m 00 s` 形式で表示
- 集中終了から休憩へ入る際のアラートを1回から2回へ変更
- 1回目と2回目の間に短い間隔を設け、2回目の再生後に休憩と質問画面を開始
- リセットなどで途中終了した場合に、予約済みの2回目アラートが後から鳴らないようタイマーを管理

---

## Version 43: Body Check and Double Focus-End Alert

- Fixed a regression where the body-check dialog called an obsolete time-formatting function
- Restored the body-check question when the break begins
- The remaining break time in the dialog uses the `05 m 00 s` format
- The focus-end alert now plays twice before entering the break
- The break and body-check dialog begin after the second alert finishes
- Pending replay timers are cleared on reset or interruption


## 第44版：PWAタイマー画面の高さ調整

- 画面上部の英字「TENSION CHECK TIMER」を削除
- iPhoneのPWA表示中だけ、タイマー画面を高さに合わせてコンパクト化
- タイトル、説明文、リング、カード内余白、状態表示を縮小
- 一時停止中も「スタート」「リセット」の両方が一画面内に収まるよう、操作ボタンの高さと間隔を調整
- 設定画面のサイズには影響しないよう、タイマー表示中のみ専用クラスを適用

---

## Version 44: PWA Timer Screen Fit

- Removed the upper “TENSION CHECK TIMER” eyebrow
- Added a compact layout used only while the timer screen is open on iPhone-sized PWA displays
- Reduced header, ring, card spacing, status text, and control sizes
- Adjusted paused controls so both Start and Reset fit within one screen
- The setup screen retains its existing layout
