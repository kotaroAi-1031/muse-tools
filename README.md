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
- `flake.nix` / `flake.lock` — ランタイムと CLI ツールの版管理（Nix Flakes）。各リポジトリのルートに置くものと同じ内容

なお、このリポジトリ自体のツール版管理もルートの `flake.nix`（+ `flake.lock`）が正です（`nix develop` で入ります）。Dependabot に Nix エコシステムは無いため、`flake.lock` の更新は定期ワークフロー `update-flake-lock` が PR で行います。

例外は `gh-share/` の gh-share です。版の正は `gh-share/go.mod`（Go tools パターン）で、Dependabot（gomod）が更新 PR を立てます。`flake.nix` にも同じ版の derivation がありますが、そちらは Dependabot の対象外なので、PR をマージする前に版とハッシュを揃える必要があります（CI の gh-share ジョブが一致を検査します。詳細は `gh-share/README.md`）。

新しいリポジトリは、原則としてテンプレートリポジトリ [muse-repo-template](https://github.com/kotaroAi-1031/muse-repo-template) から作ります（この `template/` はその内容の控えです）。

## 中身

トピックごとのフォルダを随時追加します。

- `gh-share/` — gh 拡張 gh-share（k1LoW/gh-share）の導入とバージョン管理。版の正は同フォルダの `go.mod` で、Dependabot が更新します。
