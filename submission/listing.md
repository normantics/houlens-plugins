# 掲載の材料の下書き

AnthropicとOpenAIのディレクトリへ法レンズを申請するときに、ポータルへ入れる文の下書きです。このフォルダは、リポジトリを公開にする前に消します。2026-11-04に、各社の公式の頁と、法レンズのリポジトリの `docs/proposals/connector-directory-submission.md`、`lib/mcp/server.ts`、`docs/mcp-usage-guide.md`、`app/privacy/page.tsx` を読んで書きました。法レンズの本番のMCPは呼んでいません。

## 3つの掲載に共通する項目

| 項目 | 案 |
|---|---|
| 名前 | 法レンズ (英字の表記は Houlens) |
| documentation URL | https://houlens.jp/connect |
| privacy policy URL | https://houlens.jp/privacy |
| terms of service URL | https://houlens.jp/terms |
| website URL | https://houlens.jp |
| support contact | info@normantics.co.jp |
| support URL (OpenAIだけが求める) | https://houlens.jp/company/contact (株式会社Normanticsの会社サイトのお問い合わせの節 https://normantics.co.jp/#contact へ転送する。会社サイトの置き場が変わっても転送の先を直せば済む) |
| icon | 法レンズのリポジトリの `public/logo.png` (PNG、640×640px、19,677バイト)。同じ図柄のSVGが `public/logo.svg` にある |

iconは、AnthropicのプラグインとOpenAIのパッケージの両方で、プラグインのフォルダの中にファイルとして置く必要があります。Anthropicの `claude plugin validate` は、512〜2048pxの正方形のPNGかJPEGを求め、SVGとWebPを受け付けません。最初にポータルで保存か申請をした時点のiconが掲載のiconになり、後から変えられません。`public/logo.png` はこの条件に合います。OpenAIは、正方形で48px以上のPNG、JPEG、WebP、SVGを `logo` に求めます。

### 一言の説明 (Anthropicは200字まで)

日本語の案 (53字):

> 日本の判例と条文を検索し、判決文の原文と出典 (裁判所・言渡日・事件番号) をAIへ返すMCPサーバです。

英語の案:

> Search Japanese case law and statutes, and get the decision text with its court, date, and case number.

### 説明 (Anthropicは2,000字まで)

日本語の案:

> 法レンズは、株式会社Normanticsが運営する日本の判例と条文の検索サービスです。Claudeとの会話の中で、判例と条文を調べ、判決文の原文と出典を返します。
>
> 判例は、相談の文章のまま意味の近さで探せ、語の一致でも探せます。裁判所の種別と言渡日の範囲で絞れます。判決文は、裁判所の判断や主文のように必要な区画だけを読め、特定の文言が判決文のどこにあるかも探せます。書面に引用された判例名や事件番号を収録データと照合し、食い違いがあれば引用の取り違えの疑いとして返します。
>
> 条文は、法令名か略称で引けます。判例の言渡日のように基準日を指定すると、その時点の版を返します。改正の前後の条文を並べて、変わった行と施行日も返します。
>
> 判例には、裁判所・言渡日・事件番号と法レンズの判例IDが付きます。判決文のテキストは原本PDFから機械的に抽出したもので、書面に引用する前には、法レンズにログインして原本PDFを確認します。検索が0件でも、判例が存在しないことの証明にはならず、応答には収録範囲が添えられます。
>
> 法レンズは検索の結果と原文だけを返し、法的な評価はしません。利用には、法レンズのアカウントと有効な契約が要ります。

英語の案:

> Houlens is a search service for Japanese case law and statutes run by Normantics Inc. It lets Claude look up court decisions and statutes during a conversation and returns the source text with its citation.
>
> Search decisions by meaning, using the wording of a consultation as is, or by keyword, and filter by court level and date of decision. Read only the parts of a decision you need, such as the court's reasoning or the operative part, and find where a phrase appears in a decision. Check case names and case numbers cited in a brief against the Houlens collection; a mismatch is flagged as a possible citation error.
>
> Look up statutes by name or abbreviation. With a reference date, such as the date of a decision, Houlens returns the version in force on that date. It can also compare an article before and after an amendment and return the changed lines and effective dates.
>
> Each decision comes with the court, date of decision, case number, and Houlens case ID. The decision text is extracted from the original PDF by machine; before quoting it in a filing, sign in to Houlens and check the original PDF. No results do not prove that no decision exists, and the response includes the coverage of the collection.
>
> Houlens returns search results and source text only and does not give legal opinions. Use requires a Houlens account with an active Houlens contract.

### カテゴリの案

AnthropicとOpenAIのどちらも、選べるカテゴリの一覧はポータルにしか無く、公式の文書から確かめられませんでした。決め方は、一覧にLegalがあればLegal、無ければResearchです (決定 2026-11-04)。申請の日にポータルの一覧を見て選びます。

- Anthropic (1〜5個): 一覧に Legal があればそれを先に、次に Research の類
- OpenAI (1個): 一覧に Legal があればそれ、無ければ Research。`openai/houlens/plugin.json` の Productivity は仮の値で、申請の日に一覧を見て書き換える

## Anthropicのコネクタの申請 (MCP connector)

### Connection

- URL: https://houlens.jp/api/mcp
- 利用者ごとにURLは変わらないので、Users connect to different URLs は選ばない

### Use cases

- 主な用途: 弁護士が、相談の見通しを立てるときと書面を書くときに、関連する判例と条文を探し、判決文の原文を読み、引用の書誌を確かめる
- 接続の前に要るもの: 法レンズのアカウントと、法レンズの有効な契約。ログインはhoulens.jpで行う
- 読み書き: 読むだけ。全ツールが readOnlyHint を true で持ち、書き込みのツールは無い

### Company

- 会社名: 株式会社Normantics (英字の表記は Normantics Inc.)
- website: https://normantics.co.jp
- 審査の連絡の窓口: info@normantics.co.jp

### Authentication

- Authentication requirement: Required
- 方式: OAuth 2.1。PKCEはS256だけを受ける。クライアントの登録は、クライアントIDメタデータ文書 (CIMD) と動的クライアント登録 (DCR) の両方に対応する
- Anthropicにclient IDとsecretを預ける必要は無い

### Data handling

| 問い | 答えの案 | 根拠 |
|---|---|---|
| 下のAPIは自社のものか | 自社のもの (Our own API)。判例と条文のデータベースと検索は法レンズが運用する | プライバシーポリシー1章、2章 |
| 個人の健康のデータを扱うか | 扱わない。取得する情報は、アカウント情報、検索の入力、AI接続の情報、運用の記録で、健康のデータを集める目的は無い。ただし、利用者が検索の文に書いた内容はそのまま検索に使う | プライバシーポリシー2章、5章 |
| sponsored content を含むか | 含まない | プライバシーポリシーに記述は無い。法レンズの応答は検索の結果と原文だけ |

### Test & launch

審査用のアカウントとログインの経路は、この下書きの範囲の外で別に作ります。

### Compliance (7つの確認)

確認する前に、各項目の本文をポータルで読みます。法レンズに当たる事実は次のとおりです。

- first-party API usage: 法レンズは自社のAPIを返す
- financial transactions: MCPのツールは決済も契約の変更もしない
- AI media generation: 画像や音声を生成しない
- prompt injection: サーバのinstructionsとツールの説明は、ツールの使い方と出典の示し方だけを書く。判決文の本文は資料として返す
- conversation data collection: 法レンズはAIのクライアントの会話を受け取らず、ツールの引数だけを受け取る。サーバ側のアプリケーションは検索の入力を保存せず、ログにも出さない (プライバシーポリシー3章、5章)
- public documentation: https://houlens.jp/connect

## Anthropicのプラグインのバンドルの申請 (Plugin bundle)

### Source

- Repository: normantics/houlens-plugins
- Plugin path: claude/houlens
- Branch or tag: 空欄 (既定のブランチの main を追う)

### Data handling

プラグインそのものはローカルでコードを動かさず、データを保存しません。宣言したMCPサーバ (houlens.jp) の側の扱いは、プライバシーポリシーの記述だけを根拠に書きます。

| 問い | 答えの案 | 根拠 |
|---|---|---|
| 個人のデータを読むか、保存するか | プラグインは読まず、保存しない。宣言したMCPサーバの法レンズは、ログインと権限の確認のために利用者の識別子、メールアドレス、表示名を扱い、AI接続の記録 (接続先の名前、接続日時、最終利用日時など) を保存する。検索の入力は保存せず、ログにも出さない | プライバシーポリシー2章、3章 |
| 宣言したコネクタの外へデータを送るか | プラグインは送らない。法レンズのサーバは、意味検索のために検索の文をGoogleのGemini APIへ送る。ログインにはFirebase、配信とデータの管理にはGoogle Cloudを使う | プライバシーポリシー4章 |
| データの保持の期間 | プラグインは保持しない。法レンズのサーバでは、AI接続は最後に使ってから30日を過ぎると使えなくなり、期限を過ぎた認証の記録は猶予の後に自動で削除する。Gemini APIは、利用ポリシー違反の検出のために入力と応答を55日保持する。アカウント情報と運用の記録は、利用目的と法令上の保存義務に応じて管理し、期間の定めは書いていない。退会すると、認証の記録、利用者情報、AI接続の記録を削除する | プライバシーポリシー4章、6章 |
| 18歳未満を対象にするか | 対象にしない | 利用規約の利用資格に「本サービスは、18歳以上の方を対象とします。」とある (https://houlens.jp/terms) |

### Compliance

連絡先のメールアドレスは info@normantics.co.jp にします。4つのacknowledgementsは、ポータルで本文を読んでから選びます。

## OpenAIのプラグインの申請

パッケージは `openai/houlens/` で、フォルダの中身を根にしたZIPを作って上げます。マニフェストは根の `plugin.json` (Agent Plugins の形式) で、MCPサーバの設定は `mcp.json` にあります。MCPサーバはOpenAI向けのエンドポイント https://houlens.jp/api/mcp/openai を指し、認証はOAuthでCIMDを優先します。

申請の前に足すもの:

- `assets/` に icon のファイルを置き、`extensions.com.openai.interface` の `logo` と `composerIcon` に指定する
- テストケースは `openai/houlens/plugin.json` の `extensions.com.openai.review.test_cases` に、動画のURL https://youtu.be/3cIDEeTAasE は `review.demo_recording_url` に入れた。動画は株式会社NormanticsのYouTubeのチャンネルに限定公開で置き、ChatGPTのデスクトップアプリで8件を順に流したようすを映している
- 審査の担当者の資格情報は、パッケージに入れず、ダッシュボードの Review details に入れる

### 掲載の項目 (`openai/houlens/plugin.json` に入れた値)

| 項目 | 値 | 上限 |
|---|---|---|
| displayName | Houlens | 30字 |
| shortDescription | Japanese case law and statutes | 30字 (この値はちょうど30字) |
| longDescription | 英語の説明。`plugin.json` を参照 | 4,000字 |
| developerName | Normantics Inc. | 80字。表示の名前は身元の確認を済ませた名義から自動で決まる |
| category | Legal、無ければ Research (決定 2026-11-04) | 申請の日にダッシュボードの一覧を見て選ぶ。plugin.json の Productivity は仮の値 |
| websiteURL | https://houlens.jp | |
| supportURL | https://houlens.jp/company/contact | 会社サイトのお問い合わせの節へ転送する |
| privacyPolicyURL | https://houlens.jp/privacy | |
| termsOfServiceURL | https://houlens.jp/terms | |
| publication.countries | JP (決定 2026-11-04) | 省くと全ての国。法レンズは日本の判例と条文を、日本語の画面と規約で扱う |
| 日本語の訳 | ja-JP の subtitle と description | subtitle は30字 |

### テストケース (正例5件)

どれも、法レンズの文書 (`docs/mcp-usage-guide.md`) に結果が返ると書かれた問いから作りました。2026-11-04に、オーナーのChatGPTのブラウザ版で法レンズのプラグインを選び、思考量をMediumにして、本番の法レンズに8件を流しました。下の期待の動きは、そのときの答えに合わせてあります。`tools_triggered` はOpenAI向けのエンドポイントのツールの名前です。

1. 相談の文章のままで判例を探す
   - description: Find decisions by meaning from a consultation written in Japanese
   - prompt: フリーランスへの業務委託を途中で打ち切ったときの損害賠償について、関連する判例を探して、出典を示して
   - tools_triggered: search_cases
   - expected_behavior: Returns related decisions, each with the court, date of decision, case number, and Houlens case ID, quotes short passages from the decision text, and notes that the text is machine-extracted from the original PDF.
2. 書面に引用された判例を照合する
   - description: Verify a cited decision by case number and read the relevant passage
   - prompt: 最高裁判所第一小法廷平成4年2月27日判決 (平成1(オ)1668) が収録されているか確かめて、判決文で民法424条に触れている箇所を見せて
   - tools_triggered: lookup_case_citation, find_in_case, read_case_text
   - expected_behavior: Matches the citation to Houlens case ID 052444 with its court, date, and case number, shows the passage that cites Civil Code Article 424 with its PDF page, and advises checking the original PDF before quoting it.
3. 略称で条文を引く
   - description: Look up a statute article by its abbreviation
   - prompt: 労基法20条の解雇予告の条文を見せて
   - tools_triggered: get_statute
   - expected_behavior: Resolves the abbreviation to the Labor Standards Act, returns the text of Article 20 with paragraph numbers, and shows the date up to which Houlens has imported amendments.
4. 改正の前後で条文を比べる
   - description: Compare a statute article before and after an amendment
   - prompt: 労働基準法115条を、2020年4月1日に施行された改正の前後で比べて
   - tools_triggered: compare_statute_revisions
   - expected_behavior: Returns the text of the article before and after the amendment, the lines that changed, and the date the change took effect. If transitional rules matter, it notes that they are in the supplementary provisions, which the comparison does not include.
5. 収録範囲を確かめる
   - description: Report the coverage of the case law collection
   - prompt: 法レンズに収録されている判例の件数と範囲を教えて
   - tools_triggered: get_coverage
   - expected_behavior: Returns the total number of decisions in the collection with its breakdown and the range of decision dates, and explains that a search with no results does not prove that no decision exists.

### テストケース (負例3件)

1. 法レンズの範囲の外の問い
   - description: General question unrelated to Japanese case law or statutes. The plugin should not call any Houlens tool.
   - prompt: 東京の明日の天気を教えて
2. 契約の申込みと支払い
   - description: Request to subscribe and pay for a plan. Houlens does not sell plans or process payments in ChatGPT, so the plugin should not act and should not show a checkout link.
   - prompt: 法レンズの有料プランに申し込んで、支払いまで済ませて
3. 法律の調べ物でない文章の仕事
   - description: Translation request unrelated to Japanese case law or statutes. The plugin should not call any Houlens tool.
   - prompt: 次の英文を自然な日本語に訳して: Thank you for your prompt reply. We will review the contract and get back to you next week.
