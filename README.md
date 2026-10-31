# muse-tools

Muse の日常業務用ツールの保管庫です。トピックごとにフォルダを分けて、スクリプトや小さなツールを置きます。

## ルール

- **シークレット類は絶対に入れない。** API キー、トークン、パスワード、秘密鍵、認証情報ファイルはコミット禁止です。認証情報は各ツールの実行環境（Secure Vault やコネクタの仕組み）から取得し、リポジトリには置きません。
- **コミット／プッシュ前検査を必須とする。** Lefthook + Betterleaks（gitleaks の後継）で、コミット時とプッシュ時にシークレット混入を自動検査します。クローン直後は必ず `lefthook install` を実行してください。
- 成果物や共有物の置き場ではありません（共有は Artifact Share が優先です）。ここは道具の保管専用です。

## 共通設定テンプレート

`template/` には、今後 Muse が作る全リポジトリ共通の初期設定が入っています。

- `lefthook.yml` — pre-commit / pre-push で Betterleaks を回すフック定義
- `.betterleaks.toml` — Betterleaks の既定ルールセットを使う設定
- `.gitignore` — シークレット類と生成物を対象外にする設定

新しいリポジトリは、原則としてテンプレートリポジトリ [muse-repo-template](https://github.com/kotaroAi-1031/muse-repo-template) から作ります（この `template/` はその内容の控えです）。

## 中身

トピックごとのフォルダを随時追加します。
