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


## 第45版：第43版基準・一時停止中ボタン横並び

- 第44版の画面全体の縮小調整を取り消し、第43版を基準に戻しました
- タイマー、リング、文字、余白、カード、ボタンのサイズ感は第43版のままです
- 一時停止中に表示される「スタート」「リセット」ボタンだけを横並びに変更しました

---

## Version 45: Based on Version 43 with Horizontal Paused Controls

- Reverted the layout changes from version 44 and restored version 43 as the base
- Timer, ring, typography, spacing, card, and button sizing remain unchanged from version 43
- Only the paused Start and Reset buttons are displayed side by side


## 第46版：トップ装飾・操作ボタン・プルダウン調整

- トップの「TENSION CHECK TIMER」を削除
- トップの時計SVG画像を削除
- 第45版のタイマー、リング、文字サイズは変更なし
- トップの「スタート」と、集中中・休憩中の操作ボタンの高さ・角丸を統一
- 一時停止中の「スタート」「リセット」は横並びを維持
- iPhoneでプルダウンの選択矢印が内側にずれる問題を避けるため、標準矢印を無効化
- 独自SVG矢印を右端から一定距離の位置に固定

---

## Version 46: Header, Controls, and Select Arrow

- Removed the “TENSION CHECK TIMER” eyebrow
- Removed the clock SVG from the top
- Kept all timer, ring, and typography sizes from version 45
- Matched the height and corner radius of timer controls to the setup Start button
- Kept paused Start and Reset buttons side by side
- Replaced the inconsistent iOS native select arrow with a custom SVG arrow fixed to the right edge


## 第47版：トップ画面と操作ボタンの再調整

- トップの時計SVG画像を復元
- 英字「TENSION CHECK TIMER」は削除したまま維持
- 集中中・休憩中の下部ボタンを、トップのスタートボタンと同じ丸みに統一
- トップ画面のスタートボタンを残り高さの下側へ配置
- タイマー設定カード内の上下左右余白、項目間隔、説明文間隔を広げて見やすく調整
- 高さが小さいPWA表示では、一画面に収まるよう余白を自動的に少し縮小

---

## Version 47: Restored Clock and Layout Refinements

- Restored the clock SVG at the top
- Kept the “TENSION CHECK TIMER” eyebrow removed
- Matched the corner radius of focus and break controls to the setup Start button
- Positioned the setup Start button lower using the remaining screen height
- Increased spacing and padding inside the timer settings card
- Added a compact fallback for shorter PWA screens


## 第48版：トップのスタート位置をタイマー画面と統一

- トップ画面と集中中・休憩中画面で、ヘッダー下の利用可能な高さを共通化
- トップの「スタート」を、集中中画面の「一時停止」と同じ下端位置へ配置
- 一時停止中の「スタート」「リセット」も同じ下端位置を維持
- 高さが不足する場合は、タイマー設定枠内の余白だけを段階的に縮小
- リング、文字、入力欄、ボタン本体のサイズは変更なし

---

## Version 48: Aligned Bottom Control Position

- Shared the same available height between the setup and timer screens
- Positioned the setup Start button at the same lower location as the timer Pause button
- Kept paused Start and Reset controls aligned to the same bottom position
- On shorter screens, only spacing inside the settings card is reduced
- Timer, typography, input, and button sizes remain unchanged


## 第49版：タイマー画面の下部余白とボタン位置

- 集中中・休憩中画面の「1セット目」と「画面消灯防止」の間隔を縮小
- 「画面消灯防止」表示の下側余白を削除
- タイマーカードの下部余白を上部余白と同じ値に統一
- 余った高さを下部操作ボタンへ割り当て、トップ画面のスタートと同じ位置に合わせやすく調整
- リング、文字、カード幅、ボタンサイズは変更なし

---

## Version 49: Timer Footer Spacing and Button Alignment

- Reduced spacing between the cycle label and wake-lock status
- Removed extra space below the wake-lock status
- Matched the timer card's bottom padding to its top padding
- Used the freed vertical space to align timer controls with the setup Start button
- Ring, typography, card width, and button sizes remain unchanged


## 第50版：集中時間ホイールと休憩終了アラート固定

- 集中時間の手入力と「＋／−」操作を廃止
- 1〜120分を上下スワイプで選ぶ、常設の回転式ホイールへ変更
- 中央の数字が現在の選択値になり、指を離すと1分単位で吸着
- 追加のタップ操作や別画面は不要
- キーボード利用時は上下矢印でも変更可能
- 「休憩終了時にも同じ音を鳴らす」の表示を設定画面から削除
- 休憩終了アラートは常にオンとして固定
- ホイールは削除した設定項目のスペースを利用し、設定カード全体の縦幅を大きく変えない構成

---

## Version 50: Focus Duration Wheel and Fixed Break-End Alert

- Replaced manual input and plus/minus controls with an always-visible vertical wheel
- Supports 1–120 minutes with one-minute scroll snapping
- The centered value is the selected duration
- No extra modal or confirmation tap is required
- Removed the break-end alert toggle from the setup screen
- Break-end alert is now always enabled
- Used the freed space to keep the overall setup layout close to its existing height


## 第51版：時間・分の2ホイール

- 集中時間を「時間」と「分」の2つの縦ホイールに分割
- 0時間1分〜2時間0分の範囲で設定
- 1時間の場合は「1時間 0分」として設定可能
- 2時間を選んだ場合は分を自動的に0分へ補正
- 0時間0分は無効とし、自動的に0時間1分へ補正
- 初期値は0時間25分
- 中央の選択値を濃い文字色・太字・大きめ表示へ変更
- 選択帯を文字の背面に配置し、数字が薄く見える問題を修正

---

## Version 51: Separate Hour and Minute Wheels

- Split focus duration into separate hour and minute wheels
- Supports 0 hr 1 min through 2 hr 0 min
- Allows settings such as 1 hr 0 min
- Automatically forces minutes to 0 when 2 hours is selected
- Prevents 0 hr 0 min by correcting it to 0 hr 1 min
- Default value is 0 hr 25 min
- Made the selected center values darker, bolder, and larger
- Moved the selection highlight behind the numbers for better contrast


## 第52版：分ホイールの選択強調と説明文調整

- 分ホイールの中央選択値にも、時間ホイールと同じ濃い文字色・太字・大きさを明示的に適用
- `is-selected` と `aria-selected="true"` の両方を使い、iPhoneでスクロール後も選択状態が外れにくいよう修正
- プログラムによるホイール移動後にも、時間・分の両方の選択表示を再同期
- 説明文を「2時間まで分単位で指定できます。休憩は5分固定です。」へ変更

---

## Version 52: Minute Wheel Highlight and Help Text

- Applied the same dark, bold, large selected style to the minute wheel
- Used both selected classes and ARIA state for more reliable iPhone rendering
- Re-synchronized both wheel highlights after programmatic scrolling
- Shortened the duration help text


## 第53版：分ホイールの1分ずれ修正

- iPhone用CSSではホイール1行の高さが38px、JavaScriptでは44px固定で計算していた不一致を修正
- 実際に表示されている行の高さを毎回測定して、選択値とスクロール位置を計算
- 5分を選んだ際に4分として強調・保存される問題を修正
- 初回表示後と画面サイズ変更後にも、現在値を中央へ再配置

---

## Version 53: Fixed One-Minute Wheel Offset

- Removed the mismatch between the 38px iPhone row height and the previous fixed 44px JavaScript calculation
- Measures the actual rendered option height for scrolling and value selection
- Fixes the issue where selecting 5 minutes highlighted and saved 4 minutes
- Re-centers the selected values after initial layout and screen-size changes


## 第54版：集中時間ホイールの枠構成を整理

- 数字部分だけを枠で囲む構成へ変更
- 「時間」「分」は各数字枠の外側へ配置
- 時間側・分側の数字枠の横幅を統一
- 選択中の網掛けを削除
- 選択帯の上下罫線も削除
- 中央の選択値は濃い色・太字のまま維持

---

## Version 54: Refined Duration Wheel Frames

- Framed only the numeric wheel areas
- Moved hour and minute labels outside the frames
- Matched the width of the hour and minute numeric frames
- Removed the selected-row shading
- Removed the selection band's horizontal rules
- Kept the centered selected values dark and bold


## 第55版：集中時間枠線とプルダウン矢印

- 集中時間の時間・分ホイールの外枠線を削除
- ホイールの配置と中央の選択表示は維持
- 集中終了のアラート音と集中中の音のプルダウンへSVG矢印を再表示
- 矢印を各プルダウン枠内の右端へ固定
- iPhoneの標準矢印表示差を避けるため独自SVGを強制適用

---

## Version 55: Wheel Border and Select Arrow Fixes

- Removed the border around the hour and minute wheel frames
- Kept the wheel layout and centered selected values
- Restored SVG arrows for both sound selects
- Fixed the arrows inside the right edge of each select


## 第56版：試聴ボタンをアイコン化

- 「試聴」の文字ボタンをスピーカー＋音波アイコンへ変更
- 再生中は四角い停止アイコンへ切り替え
- アラート音と集中中の音の両方で、再度タップすると途中停止可能
- 読み上げ用の「試聴／停止」ラベルを維持
- アイコン化に合わせてボタン幅をコンパクトに調整

---

## Version 56: Icon Preview Buttons

- Replaced text preview buttons with speaker-and-sound-wave icons
- Shows a square stop icon while preview audio is playing
- Both preview buttons can stop playback when tapped again
- Preserved accessible Preview/Stop labels
- Reduced button width to fit the icon-based design


## 第57版：停止アイコンと音設定欄の位置調整

- 再生中の四角い停止アイコンを塗りつぶし表示へ変更
- プルダウンと試聴アイコンを1つのまとまりとして中央配置
- 左右の余白を同じ幅に調整
- プルダウン下の説明文を、プルダウンの開始位置に揃えて配置

---

## Version 57: Filled Stop Icon and Centered Sound Controls

- Changed the square stop icon to a filled shape
- Centered each select-and-preview-button group
- Equalized the left and right outer spacing
- Aligned the help text with the left edge of the select


## 第58版：音設定欄の中央配置とアラート試聴アイコン

- プルダウン・試聴アイコン・説明文を同じ親ブロックへ統合
- 音設定ブロック全体を固定幅で中央配置し、左右余白を同じに調整
- 説明文の左端を、プルダウンの左端と完全に一致
- 集中終了アラート音の試聴ボタンは、再生中もスピーカーアイコンのまま維持
- アラート試聴は1回再生し、再生後に再度スピーカーを押すと再生可能
- 集中中の音のみ、再生中は塗りつぶしの停止アイコンへ切り替え

---

## Version 58: Centered Sound Controls and Alert Preview Icon

- Grouped each select, preview button, and help text in one centered block
- Equalized the left and right spacing
- Precisely aligned help text with the select's left edge
- Kept the alert preview button as a speaker icon during playback
- The alert preview plays once and can be triggered again afterward
- Only the focus-sound preview changes to a filled stop icon while playing


## 第59版：集中時間ブロックの中央配置とスピーカー形状

- 集中時間のホイールと説明文を同じ親ブロックへ統合
- 音設定ブロックと同じ幅で中央配置
- 集中時間ホイール・説明文の左端を、集中終了アラート音プルダウンの左端と統一
- スピーカーアイコンを少し縦長に調整
- アイコンボタン全体の大きさは維持

---

## Version 59: Centered Duration Block and Taller Speaker Icon

- Grouped the duration wheels and help text in one centered block
- Matched its width to the sound-control blocks
- Aligned the duration block's left edge with the alert-sound select
- Made the speaker icon slightly taller without changing the button size


## 第60版：不要コードの整理

動作を変えず、これまでの改修で不要になったコードを整理しました。

- 旧「手入力＋／−」集中時間UIのCSSを削除
- 第50版の単一ホイール用CSSを削除
- 既に削除済みの休憩終了アラート切替UIのHTML・CSS・JavaScriptを削除
- 休憩終了アラートは、条件分岐を介さず常に再生する処理へ簡略化
- 旧装飾テーマや旧カラープレビューなど、現在使われていないCSSを削除
- 使用されていない翻訳キーを削除
- 累積していた版別コメントを本番CSSから削除
- 現在使用中のホイール、音声、身体チェック、履歴、テーマ、言語、PWA機能は維持

---

## Version 60: Code Cleanup

- Removed CSS for the obsolete manual plus/minus duration control
- Removed CSS for the obsolete single-wheel duration selector
- Removed the retired break-end alert toggle from HTML, CSS, and JavaScript
- Simplified break completion so the alert always plays
- Removed unused decorative and legacy theme CSS
- Removed unused translation keys
- Removed accumulated version-history comments from production CSS
- Preserved all current timer, audio, body-check, history, theme, language, and PWA behavior
