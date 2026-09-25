# ci-workflows

5つのリポジトリで共有する GitHub Actions の再利用可能ワークフローです。

## ワークフロー

- `gitleaks.yml`: 呼び出し元を履歴全体で checkout し、呼び出し元の `make gitleaks` を実行します。
- `make.yml`: 呼び出し元を checkout し、必要なら `mise` で `.mise.toml` のツールチェーンを用意してから、指定された `make` ターゲットを実行します。
- `lint.yml`: このリポジトリ自身の GitHub Actions 定義を `actionlint` で検査します。

## 呼び出し方

呼び出し元のジョブから、安定版の `v1` タグを指定して呼び出します。

```yaml
jobs:
  gitleaks:
    uses: mu5dvlp/ci-workflows/.github/workflows/gitleaks.yml@v1

  check:
    uses: mu5dvlp/ci-workflows/.github/workflows/make.yml@v1
    with:
      target: check
      setup: mise
```

呼び出し元は `v1` タグに固定します。互換性を壊す変更を入れるときは `v2` を作り、既存の `v1` は維持します。

このリポジトリを public にしているのは、public の `open-audioware` から private な再利用可能ワークフローを呼び出せないためです。ここには秘密情報、トークン、環境固有の認証情報を決して置きません。

ライセンスは MIT-0 です。
