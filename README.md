# うさみみ道具屋さんとおさわり出稼ぎ冒険者生活 翻訳プロジェクト

ユーザーコミュニティによる **うさみみ道具屋さんとおさわり出稼ぎ冒険者生活** の翻訳プロジェクトです。

送っていただいた翻訳は、コミュニティ翻訳として次バージョンのゲーム本体に同梱されます。
翻訳者のお名前（実名・ハンドル・匿名など、ご希望の形式）をゲーム内クレジット画面と商品ページに掲載します。


## 協力者募集中の言語

| Language | Status | Contributors | Version |
|---|---|---|---|
| 繁體中文 (zh_TW) | 🎉 | Jason.H | v1.2.0 |
| 简体中文 (zh_CN) | 😢 | - | - |
| English (en_US) | 😢 | - | - |

担当したい言語があれば、ぜひ以下を読んでご参加ください。

**気になることがあれば気軽にご相談ください。**
担当したい言語の空き確認、どの言語から始めるか迷っているとき、翻訳中のニュアンスや表現の相談など、
[mochi2yama@gmail.com](mailto:mochi2yama@gmail.com) まで気軽にご連絡ください。


## 参加する前に

### ゲームのバージョン要件

> [!Important]
> `1.1.0` 以上のバージョンが必要です。DLSite より最新版をダウンロードしてください。

### 翻訳を送る前に知っておいてほしいこと

翻訳を PR またはメールで送っていただいた時点で、以下に同意したものとみなします。

- 翻訳の著作権は **翻訳者に帰属**します
- 翻訳のゲーム本編への組み込み、および有償版への同梱を許諾します
- ゲーム内クレジット画面と商品ページに、ご希望の形式で翻訳者名を掲載します
- 翻訳者自身による独自配布は自由に行っていただけます
- 本作への組み込み以外の商用利用（第三者による有償販売等）は不可です

詳しくは [LICENSE](LICENSE) を参照してください。

### 準備するもの

- ゲーム本体（1.1.0 以上）
- UTF-8 対応のテキストエディタ（VS Code 推奨）
- 翻訳先言語の入力環境
- Pull Request で送る場合: GitHub アカウント
- メールで送る場合: zip を添付できるメール環境


## 作業の流れ

1. 翻訳ベースファイルをダウンロードして mods/ に配置し、ゲームで起動確認する
2. `.po` ファイルを翻訳する（UI テキスト・アイテム名など）
3. シナリオ `.txt` ファイルを翻訳する（セリフ・地の文）
4. フォントを差し替える（任意。中国語・韓国語など CJK 系言語では実質必須）
5. ゲームで動作確認する
6. 翻訳を送付する（PR またはメール）

---

## Step 1: 翻訳ベースファイルの準備と起動確認

[Releases](../../releases) から作業したいロケールの zip をダウンロードして展開してください。

```
usa01.exe
mods/
  en_US/               ← 英語 (en_US) 用ベースファイル
    assets/
      locale/en_US/    ← .po ファイル（19ファイル）― UIテキスト等
      scenarios/en_US/ ← シナリオ .txt（139ファイル）― セリフ・地の文
      fonts/en_US/     ← フォントファイル置き場（任意）
  zh_CN/               ← 中国語簡体字 (zh_CN) 用ベースファイル
    ...（同じ構成）
```

1. `usa01.exe`（ゲーム本体）と同じディレクトリに `mods/` フォルダを作成
2. 展開したフォルダ（例: `en_US/`）をそのまま `mods/` 内に配置

中身はすべて元の日本語テキストです。この日本語を翻訳先の言語に書き換えていきます。

**配置が完了したら、まず一度ゲームを起動してください。**
タイトル画面の左下で言語を選択できれば、セットアップは正しく完了しています。
翻訳を始める前にここを確認しておくと、設定ミスを早期に発見できます。

---

## Step 2: .po ファイルの翻訳方法

全 .po ファイルの一覧は[ファイル一覧](#ファイル一覧)を参照してください。

`msgstr` の中身を翻訳してください。それ以外の行は変更しないでください。

```po
# OK — msgstr を翻訳する
msgid "UI_CLOSE"
msgstr "Close"

# NG — msgid を変えてしまっている
msgid "Close"
msgstr "Close"
```

アイテム名と説明のように、同じキーが複数の場面で使われる場合は `msgctxt` で区別されています。`msgctxt` はそのまま残してください。

```po
# OK — msgctxt はそのまま、msgstr だけ翻訳
msgctxt "item_name"
msgid "notebook"
msgstr "Mysterious Book"

msgctxt "item_description"
msgid "notebook"
msgstr "Might reveal the shopkeeper's secret!"

# NG — msgctxt を消してしまっている
msgid "notebook"
msgstr "Mysterious Book"
```

`{enemy_11}` のようなプレースホルダーはゲームが実行時に別のテキストに置き換えます。そのまま残してください。

```po
# OK — {enemy_11} を保持
msgctxt "item_description"
msgid "drop_11"
msgstr "Dropped by {enemy_11}."

# NG — {enemy_11} が消えている
msgctxt "item_description"
msgid "drop_11"
msgstr "A monster drop."
```

`%02d` や `%s` も同様に保持してください。

```po
# OK — %02d と %s をすべて保持
msgid "FMT_DAY_PERIOD"
msgstr "Day %02d %s"

# NG — %s が消えている
msgid "FMT_DAY_PERIOD"
msgstr "Day %02d"
```

`msgstr ""` になっているエントリは意図的に空です。そのままにしてください。

---

## Step 3: シナリオファイルの翻訳方法

シナリオファイルにはゲームへの命令行と、プレイヤーに表示されるテキスト行が混在しています。

**翻訳する行** — プレイヤーに表示されるテキスト:
- `me:` で始まる行（主人公のセリフ・独白）
- `???@rt:` `usa00@lb:` のように `キャラ名@位置:` で始まる行（キャラクターのセリフ）
- 上記のどれにも当てはまらない普通のテキスト行（ナレーション）

**そのままにする行** — ゲームへの命令:
- `bg:` で始まる行（背景画像の指定）
- `usa00:` の直後にインデントされたブロック（`posure:` `目:` `body:` など、キャラクターの表示制御）
- `usa00:exit`（キャラクターの退場命令）

```
# 翻訳前
bg: roji0

usa00:
  posure: front

振り返るとなんかちっちゃい子が立ってい――

???@rt:お兄さん、冒険者ですか〜？

me:「ｱ、ああ……今日来たばっかりで」

usa00:exit
```

```
# OK
bg: roji0                               ← そのまま

usa00:                                  ← そのまま
  posure: front                         ← そのまま

I turned around and saw a small girl standing there——

???@rt:Hey, are you an adventurer?

me: "Oh, uh... I just arrived today."

usa00:exit                              ← そのまま
```

```
# NG
bg: alley                               ← bg を変えてしまっている

usa00:
  posure: forward                       ← キャラクター表示を変えてしまっている

I turned around and saw a small girl standing there——

rt:Hey, are you an adventurer?          ← ???@rt: を消してしまっている

me: "Oh, uh... I just arrived today."

exit                                    ← usa00:exit を変えてしまっている
```

`[wave]` や `[shake]` などの BBCode タグはテキスト演出です。タグはそのまま残し、中のテキストだけ翻訳してください。

```
# OK — タグを保持して中身だけ翻訳
usa00@rt:[wave]Yes♥[/wave]

# NG — タグを消してしまっている
usa00@rt:Yes♥
```

`\n` はセリフ内の改行です。翻訳先の言語に合わせて位置を変えたり、増やしたりして構いません。フキダシからはみ出る場合はセリフ行を分割することもできます。

```
# 翻訳前
usa00@lb:わたし、この先で道具屋\nやってるんですけど〜

# OK — \n の位置を調整
usa00@lb:I run a tool shop\njust up ahead~

# OK — セリフを2行に分割
usa00@lb:I run a tool shop
usa00@lb:just up ahead~
```

---

## Step 5: 動作確認

1. ゲームを起動し、タイトル画面の左下から言語を選択する
2. 翻訳が反映されていることを確認する

> [!NOTE]
> ゲーム起動時に一度だけ最新の内容を読み込みます。内容を更新した場合は再起動してください。

> [!NOTE]
> すべての翻訳が揃っていなくても、部分的な翻訳に対応しています。翻訳しながら随時確認できます。

---

## Step 6: 翻訳を送付する

**PR でもメールでも、どちらでも同等に受け付けます。** 全体を翻訳しきれていなくても、部分翻訳でも問題ございません。  
メールでご送付頂いた場合は、自分がこちらのリポジトリに追加いたします。

### Pull Request で送る場合

1. このリポジトリを fork する
2. ブランチを作成して翻訳作業を行う
3. [Pull Request](../../pulls) を送る

PR には以下を記載してください。

- 対象言語（例: en_US）
- 翻訳のカバー範囲（全体 / .po のみ / シナリオのみ など）
- ゲーム内クレジットへの掲載名（実名・ハンドル・匿名など）

### メールで送る場合

翻訳済みファイルを zip にまとめ、[mochi2yama@gmail.com](mailto:mochi2yama@gmail.com) に添付して送ってください。

メール本文に以下を記載してください。

- 対象言語
- 翻訳のカバー範囲
- ゲーム内クレジットへの掲載名（実名・ハンドル・匿名など）

送り方や内容に迷ったときも、気軽にメールでご相談ください。

### 送付後の流れ

内容を確認し、必要に応じて調整のうえ、次バージョン以降の本編に同梱します。
ゲーム内クレジット画面と商品ページに、ご指定の形式で翻訳者名を掲載します。

### 独自に配布する場合

本プロジェクトへの送付なしに、ライセンスの範囲で独自に配布していただくことも自由です。
その場合は本編への追加は行いません。

翻訳 Mod は zip にまとめてゲームの `mods/` ディレクトリに配置すれば動作します。

```
usa01.exe
mods/
  en_US.zip   ← これでOK
```

---

## ファイル一覧

<details>
<summary>.po ファイル（UIテキスト・アイテム名など）</summary>

`assets/locale/{ロケール}/` 以下に 19 ファイルあります。

#### Core UI

| ファイル | 内容 |
|---------|------|
| `ui.po` | タイトルやインゲーム等共通 UI |
| `statistics.po` | 統計(秘密)画面 |
| `gallery.po` | 回想画面 |
| `time.po` | 時間帯名、日付 |

#### ゲームコンテンツ

| ファイル | 内容 |
|---------|------|
| `items.po` | アイテム名・説明・ヒント |
| `merchant.po` | 拠点での道具屋さんのセリフ |
| `quests.po` | クエスト名 |
| `enemies.po` | 敵の名前 |

#### おさわりシーン

| ファイル | 内容 |
|---------|------|
| `osawari_vfx.po` | エフェクト文字・擬音語 |
| `osawari_common.po` | 共通UI |
| `osawari_ticket_hand.po` | 握手券 |
| `osawari_ticket_foot.po` | 握手券(足) |
| `osawari_ticket_tail.po` | 握手券(尻尾) |
| `osawari_ticket_breath.po` | 握手券(顔) |
| `osawari_ticket_minuki.po` | ミヌキ券(初回) |
| `osawari_ticket_minuki_hanyou.po` | ミヌキ券 (2~4回) |
| `osawari_goal.po` | 小瓶 |
| `osawari_sleep_day.po` | すやすや(昼) |
| `osawari_sleep_night_on_back.po` | すやすや(よる) |

</details>

<details>
<summary>シナリオファイル（.txt）</summary>

`assets/scenarios/{ロケール}/` 以下に 139 ファイルあります。

```
scenarios/{ロケール}/
  day/           ← 日次イベント（朝・翌日シーン）
  events/
    1_prologue/  ← プロローグ
    9_sleep_day/ ← すやすや(昼) 前後の会話
    13_room/     ← おへやイベント, ミヌキイベント、すやすや(夜) 前後の会話
    21_tegami/   ← 手紙イベント
    24_goal/     ← 小瓶イベント
  osawari/
    goal/                 ← 小瓶 ノベルシーン
    ticket_breath/        ← 握手券(顔) ノベルシーン
    ticket_foot/          ← 握手券(足) ノベルシーン
    ticket_hand/          ← 握手券 ノベルシーン
    ticket_minuki/        ← ミヌキ券(初回) ノベルシーン
    ticket_minuki_hanyou/ ← ミヌキ券(2~4回) ノベルシーン
    ticket_tail/          ← 握手券(尻尾) ノベルシーン
  shop/
    level_up/ ← ぼったくりイベント
    purchase/ ← 特定アイテム購入前、購入後イベント
```

</details>

<details>
<summary>フォントの差し替え（任意）</summary>

`assets/fonts/{ロケール}/` 以下にフォントファイルを置くと、ゲーム内フォントを差し替えられます。

| ファイル名 | 用途 |
|-----------|------|
| `main.ttf` | 必須: UI・シナリオ・ボタン全般 |
| `effect.ttf` | 任意: エフェクト文字用（省略時は main.ttf を使用） |

デフォルトの日本語フォントは中国語・韓国語などのグリフを含まないため、**CJK 系言語では独自フォントの同梱を強く推奨します。**

</details>

---

## ライセンス

詳細は [LICENSE](LICENSE) を参照してください。

**翻訳 Mod を独自配布する方へ:**
- 翻訳 Mod の作成・無償配布: OK
- 翻訳 Mod 適用状態での実況・配信・スクリーンショット公開: OK
- 翻訳 Mod の商用利用（有償販売等）: NG
- Mod の形態を伴わない原文テキストの転載: NG
- ゲームの画像・音声・プログラムコード等テキスト以外の資産を含む配布: NG

翻訳を送付する方への条項については[参加する前に](#参加する前に)を参照してください。
