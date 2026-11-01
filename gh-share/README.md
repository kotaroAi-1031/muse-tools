# gh-share

[k1LoW/gh-share](https://github.com/k1LoW/gh-share)（GitHub CLI 拡張。単一 HTML ファイルやファイル／ディレクトリを GitHub Actions の artifact として共有する。MIT ライセンス）の導入とバージョン管理です。

## バージョン管理（Dependabot）

- バージョンの正はこのフォルダの `go.mod` です。`tools.go` が `github.com/k1LoW/gh-share` を通常の（`// indirect` でない）依存として import する、いわゆる Go tools パターンで、`go.mod` の `require` に現在の版（導入時点 v0.5.2）が直接ピン留めされています。
- Dependabot の `gomod` エコシステムがこの `go.mod` を監視するので、新しいリリースが出ると更新 PR が自動で立ちます（`.github/dependabot.yml`）。Go 1.24 以降の `tool` ディレクティブは Dependabot が未対応（dependabot-core の機能要望が open のまま）のため、確実に更新対象になる tools パターンを採っています。
- ルートの `flake.nix` にも同じ版を固定出力 derivation として載せ、`nix develop` / `nix shell .#gh-share` で使えるようにしています。こちらは Dependabot では更新されないため、Dependabot の PR をマージする前に `flake.nix` 側の版と SHA-256 も同じ版へ揃えることが必要です。揃っていない PR は CI の `gh-share` ジョブ（版の一致チェック）が赤になるので、そのままマージされることはありません。

## 使い方

通常は GitHub CLI の拡張として使います（この VM には導入済みです）:

```bash
gh extension install k1LoW/gh-share
gh share path/to/file.html
```

Go 経由では、このフォルダで次を実行すると `go.mod` にピン留めされた版がインストールされます:

```bash
cd gh-share
go install github.com/k1LoW/gh-share
```

Nix 経由では、リポジトリのルートで:

```bash
nix shell .#gh-share --command gh-share --help
```
