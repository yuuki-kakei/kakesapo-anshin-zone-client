# 02 安心ゾーン算定ツール クライアント版 デプロイ手順

## 概要
- **用途**: コンサルクライアント限定の本格設計ツール(上限+下限+自由に使えるお金)
- **公開度**: URL知ってる人のみアクセス(検索インデックス除外)
- **配布**: コンサル契約後にLINEでURL共有

---

## STEP 1: GitHub リポジトリ作成(ゆうき作業)

1. https://github.com/new を開く
2. Repository name: **`kakesapo-anshin-zone-client`**
3. Description: `カケサポ クライアント限定 安心ゾーン算定ツール`
4. **Public** を選択(GitHub Pages的なホスティングのため。Vercelデプロイのみなら Private でも可)
5. **Add a README file は チェックしない**(手元に既にコミットあり)
6. 「Create repository」をクリック

→ できあがったリポジトリのURLをClaudeに伝える

---

## STEP 2: git push

```bash
cd "/Users/yuki/.../yuki/sales/tools/02_安心ゾーン算定ツール_クライアント版"
git remote add origin https://github.com/yuuki-kakei/kakesapo-anshin-zone-client.git
git branch -M main
git push -u origin main
```

※認証は01のときに設定したKeychain credential helperが効くので、自動で通る想定。

---

## STEP 3: Vercel デプロイ(ゆうき作業)

1. https://vercel.com/new を開く
2. **Import Git Repository** で `kakesapo-anshin-zone-client` を選ぶ
3. Project Name: `kakesapo-anshin-zone-client` (デフォルトでOK)
4. Framework Preset: **Other** のまま
5. Root Directory: そのまま
6. **Deploy** をクリック
7. 1-2分でデプロイ完了

→ できあがったURL(例: `https://kakesapo-anshin-zone-client.vercel.app/`)を保管

---

## STEP 4: アクセス制御方針(現状)

### 現状の保護レベル
- `X-Robots-Tag: noindex, nofollow` で検索エンジンから除外
- URLが知られなければアクセスされない(security through obscurity)
- 真のパスワード保護はなし

### 真のパスワード保護を後で追加する選択肢
| 方法 | コスト | 強度 | 手間 |
|---|---|---|---|
| Vercel Pro Password Protection | $20/月 | 高 | 設定のみ |
| Cloudflare Access (Google認証) | 無料 | 高 | DNS切替必要 |
| JS-based パスワードゲート | 無料 | 低 | コード追加 |
| Basic Auth via middleware | 無料 | 中 | コード追加 |

→ 当面は noindex のみで運用、クライアント数が増えたら Cloudflare Access を検討。

---

## STEP 5: クライアント配布

### 配布タイミング
- 契約完了後、第1回コンサル前にLINEで送付

### LINE文面テンプレ
```
[クライアント名]さま

90日プログラムスタートにあたり、
専用の「お金の安心ゾーン算定ツール」をお渡しします。

▼ こちらからアクセスしてください
https://kakesapo-anshin-zone-client.vercel.app/

第1回コンサル(価値観マップ)が終わったら、
こちらに数字を入れていただきます。

このURLは検索しても出てきません。
クライアントさま専用ですので大切に保管お願いします。

ゆうき
```
