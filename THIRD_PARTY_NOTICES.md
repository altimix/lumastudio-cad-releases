# 第三者のコード・フォント・アイコン

LumaStudio CAD本体の自作コードはv0.14.1から非公開とし、LICENSEの利用条件を適用します。以下の第三者の部品には、それぞれのライセンスと著作権表示が適用されます。再配布するときも、部品に添付されたライセンス原文と通知を保持してください。

この一覧は2026-10-01にpackageとlockfile、実際のnpmパッケージ内のライセンスを照合したものです。バージョンを更新する際は一覧も確認します。推移的な依存先を含むすべての部品を、この表だけで列挙したものではありません。

Web版はメイン画面と各Workerへ実際に組み込まれたnpmパッケージをビルド時に収集し、ライセンスとNOTICEの全文を `THIRD_PARTY_LICENSES.txt`（公開先 `/app/THIRD_PARTY_LICENSES.txt`）へ同梱します。`third-party-licenses.json` には各パッケージの版・対象バンドル・原文のSHA-256を記録します。ライセンス原文が見つからない場合はビルドを停止します。TypeScriptの `ThirdPartyNoticeText.txt` も全文を含めます。フォント・Blocklyの素材の原文は、引き続き `licenses/` と `blockly-media/` に含みます。

## 画面・モデル・ファイル処理

| 部品 | 確認した版 | ライセンス | 用途・原文の所在 |
|---|---|---|---|
| [Blockly](https://github.com/RaspberryPiFoundation/blockly) | 13.3.0 | Apache-2.0 | ブロック編集。`node_modules/blockly/LICENSE`。画像等の原文は[public/blockly-media/LICENSE.txt](public/blockly-media/LICENSE.txt) |
| [Manifold](https://github.com/elalish/manifold) | 3.5.4 | Apache-2.0 | WASMによるソリッド演算。`node_modules/manifold-3d/LICENSE` |
| [Three.js](https://github.com/mrdoob/three.js) | 0.186.1 | MIT | 3D表示。`node_modules/three/LICENSE`。Copyright © 2010–2026 three.js authors |
| [React / React DOM](https://github.com/facebook/react) | 19.3.0 | MIT | 画面。`node_modules/react/LICENSE`、`node_modules/react-dom/LICENSE`。Copyright Meta Platforms, Inc. and affiliates |
| [Lucide React](https://github.com/lucide-icons/lucide) | 1.49.0 | ISC、一部の元アイコンはMIT | `node_modules/lucide-react/LICENSE`にはLucideのISCとFeather由来のMITを保持。Copyright 2026 Lucide Icons and Contributors、Copyright 2013–present Cole Bemis |
| [fflate](https://github.com/101arrowz/fflate) | 0.8.3 | MIT | ZIP処理。`node_modules/fflate/LICENSE`。Copyright 2026 Arjun Barrett |
| [TypeScript](https://github.com/microsoft/TypeScript) | 5.9.3 | Apache-2.0 | CAD用コードの構文解析。npmの`typescript-compiler`は`typescript@5.9.3`の別名。`node_modules/typescript-compiler/LICENSE.txt`と`ThirdPartyNoticeText.txt`を保持。Copyright Microsoft Corporation |

画面で使用するTypeScriptのライセンス原文は[public/licenses/typescript-LICENSE.txt](public/licenses/typescript-LICENSE.txt)にも保存し、Viteで`dist/licenses/typescript-LICENSE.txt`へコピーします。開発用の型検査に使う`typescript`とは、npm上の名前と版が異なります。

Manifoldの断面演算には[Clipper2](https://github.com/AngusJohnson/Clipper2)を使用しています。配布WASMのClipper2シンボルと型定義、および[Manifold 3.5.4の依存定義](https://github.com/elalish/manifold/blob/v3.5.4/cmake/manifoldDeps.cmake)を照合しました。この依存定義の固定先は`46f639177fe418f9689e8ddb74f08a870c71f5b4`です。Clipper2はBoost Software License 1.0、Copyright Angus Johnson 2010–2025で、原文を[public/licenses/clipper2-LICENSE.txt](public/licenses/clipper2-LICENSE.txt)に保存します。Viteで同じ通知を`dist/licenses`へコピーします。

## 文字・数字の形

Windowsの更新確認・ダウンロードには [electron-updater](https://github.com/electron-userland/electron-builder) 6.8.9（MIT、Copyright electron-userland contributors）を使用します。ライセンス原文は `node_modules/electron-updater/LICENSE` に保持し、依存ライブラリの通知も配布物へ残します。更新メタデータのCI検証には js-yaml 4.3.2（MIT）を使用します。

A–Zと0–9のシェイプ、および従来のTextシェイプには、Helvetiker Boldの字形の輪郭を使用します。Three.js本体のMIT Licenseとは別のフォントライセンスです。

- 原著作者：MAGENTA Ltd.、Copyright © 2004。
- [元の字形データ](https://github.com/mrdoob/three.js/blob/1d3022bc4dbb08dbed153bcbf9314303baa11859/examples/fonts/helvetiker_bold.typeface.json)。使用したコミットは`1d3022bc4dbb08dbed153bcbf9314303baa11859`。
- 原文：[public/licenses/helvetiker-LICENSE.txt](public/licenses/helvetiker-LICENSE.txt)。配布アプリ内では`dist/licenses/helvetiker-LICENSE.txt`。
- [採用データと作成手順](src/lib/fonts/README.md)。個別の英数字シェイプは36文字のレコードと元のメタデータを保持した抜粋です。Text用の`helvetiker-bold-text.json`は同じコミットの原本207字形をバイト単位で保持します。SHA-256は`bd68159ee0b8d10fe24b9daa2e32f19686f9d8269a79dc8d44203a66298bfa2f`です。PCへのフォントインストールは行いません。

HelvetikerのTextは半角英数字・記号、および実際の字形がある一部の欧文・ギリシャ文字に対応します。日本語Textでは、次のNoto Sans JPデータを使用します。各フォントに未収録の文字、改行、VS／IVSなどはエラーとして表示し、置換したり黙って欠落させたりしません。[Textの対応範囲](docs/TEXT_SHAPES.md)も参照してください。

日本語Textには、公式Google Fontsの **Noto Sans JP** を500（Medium）・700（Bold）へ静的化して変換した輪郭JSONを同梱します。これらはSIL Open Font License 1.1に従う派生フォントデータです。アプリ本体・converterの独自の利用条件とは区別します。

- 原著作権表示：Copyright 2014-2021 Adobe (http://www.adobe.com/), with Reserved Font Name 'Source'。
- [公式原本](https://github.com/google/fonts/blob/66a36c8c94b1a5d992ee4e7f392fccfe4945767c/ofl/notosansjp/NotoSansJP%5Bwght%5D.ttf)：Google Fonts commit `66a36c8c94b1a5d992ee4e7f392fccfe4945767c`。TTF SHA-256は `c2f3b4d463500a2ddcd3849cded1fceeb9fd6d1c32e6cbecd568453ba50fc68f`。実際の内部familyは `Noto Sans JP` です。
- 原文：[public/licenses/noto-sans-jp-OFL.txt](public/licenses/noto-sans-jp-OFL.txt)。固定原本SHA-256は `1c05c68c34f9708415aada51f17e1b0092d2cea709bf4a94cd38114f9e73d7d9`。Viteの `dist/licenses` とElectronの `app.asar` 内に同じ原文を保持します。
- 派生データ：`public/fonts/noto-sans-jp/{500,700}/*.json` と `src/lib/fonts/noto-sans-jp-manifest.json`。原本のbase Unicode cmap16,732件を各weightに収録し、空白の5字形もadvanceと空字形metadataを保持します。元のVS／IVSテーブルは使用しません。
- [固定sourceと再現手順](src/lib/fonts/README.md)、[source lock](scripts/fonts/noto-sans-jp-source.json)、[converter](scripts/convert-noto-sans-jp.py)。変換時だけFontTools 4.61.1（MIT License）を使用します。実行時にはFontTools・原本TTF・リモートフォントを読み込まず、PCへのフォントインストールも行いません。

フォントライセンスには、著作権表示と許諾文の保持、変更したフォントの名前、フォント単体の販売に関する条件があります。同梱した原文を確認してください。

## ローカルサーバーと起動の補助

| 部品 | 確認した版 | ライセンス | 原文の所在 |
|---|---|---|---|
| [express-rate-limit](https://github.com/express-rate-limit/express-rate-limit) | 8.7.1 | MIT | ダウンロード回数の制限。`node_modules/express-rate-limit/license`。Copyright 2023 Nathan Friedly, Vedant K |
| [Express](https://github.com/expressjs/express) | 5.2.1 | MIT | `node_modules/express/LICENSE`。Copyright TJ Holowaychuk、Roman Shtylman、Douglas Christopher Wilson |
| [Multer](https://github.com/expressjs/multer) | 2.4.0 | MIT | `node_modules/multer/LICENSE`。Copyright 2014 Hage Yaapa |
| [MQTT.js](https://github.com/mqttjs/MQTT.js) | 5.16.0 | MIT | `node_modules/mqtt/LICENSE.md`。Copyright 2015–2016 MQTT.js contributors、Copyright 2011–2014 Adam Rudd |
| [basic-ftp](https://github.com/patrickjuchli/basic-ftp) | 6.2.1 | MIT | `node_modules/basic-ftp/LICENSE.txt`。Copyright 2019 Patrick Juchli |
| [cross-env](https://github.com/kentcdodds/cross-env) | 10.1.0 | MIT | `node_modules/cross-env/LICENSE` |
| [tsx](https://github.com/privatenumber/tsx) | 4.23.15 | MIT | `node_modules/tsx/LICENSE` |

デスクトップの`app.asar`には、実行時のnpm依存先と各パッケージのライセンスが入ります。サーバーは依存先を外部パッケージとして読み込む構成です。開発・検査・ビルドだけで使う部品と、推移的な依存先の版は`package-lock.json`を参照し、それぞれのパッケージに付属する通知を保持してください。

## Electronとその内蔵部品

[Electron](https://github.com/electron/electron)の確認した版は44.5.1です。Electron本体はMIT License、Copyright Electron contributors、Copyright 2013–2020 GitHub Inc.です。内蔵するChromium、Node.js等には別の通知もあります。ElectronのMITだけを全内蔵部品のライセンスとして扱わず、実行ファイルに対応する`LICENSE`と`LICENSES.chromium.html`を保持してください。

Windows配布ファイルでは`LICENSE.electron.txt`と`LICENSES.chromium.html`を確認しています。配布設定では、実行環境に対応する両ファイルをMacの`Contents/Resources`、Windowsの`resources`にもコピーします。完成配布物の確認は、[オープンソース公開準備](docs/OPEN_SOURCE_RELEASE.md)で管理します。`app.asar`内のnpm通知と、アプリの外側にあるElectron実行環境の通知は、別々に確認します。

## Bambu Studio

Bambu Studioは、利用者がこのPCに別途インストールするアプリで、CLIを通じて利用します。実行ファイル、ネットワークプラグイン、プリセット、利用者のモデルは、このリポジトリやインストーラーへ取り込みません。Bambu Studio自身のライセンスと通知は、そのアプリに適用されます。

## Google Fonts Japanese catalog and Fontkit

The optional Japanese TEXT catalog includes 68 families listed by Google Fonts on 2026-10-07. Source file URLs, the immutable google/fonts commit, sizes and SHA-256 digests are in `src/lib/fonts/google-japanese-catalog.json`. Fonts are downloaded on first use and cached locally. License notices are bundled under `public/licenses/google-fonts/` (and `dist/licenses/google-fonts/` in the application). Kosugi and Kosugi Maru use Apache-2.0; the other catalog entries carry SIL Open Font License 1.1 notices. The small Aoboshi One font in `tests/fixtures/fonts` is the pinned upstream font, subject to its bundled OFL notice.

Fontkit (https://github.com/foliojs/fontkit), MIT license, provides local TrueType/OpenType outline extraction. Its license remains with the packaged dependency. See `docs/GOOGLE_JAPANESE_FONTS.md` for acquisition, offline behavior and geometric limits.
