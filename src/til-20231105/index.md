---
title: lm-sys/FastChatのお試し
date: 2023-11-05
lastmod: 2023-11-05
---

## 概要

[lm-sys/FastChat](https://github.com/lm-sys/FastChat)の動作確認になります。

## 実行方法

各スクリプトの実行方法は、スクリプトファイルの docstring に記載しています。
以下は、実行を想定しているスクリプトのファイル名と、スクリプトの簡易説明のみ記載します。
スクリプトのオプションは`python hoge.py -h`のようにしてオプションを出力して確認してください。

### CLI で起動

```sh
# GPUを利用する
python -m fastchat.serve.cli --model-path lmsys/vicuna-7b-v1.5
```

### GUI で起動

以下のコマンドは、それぞれプロセスを起動するためすべて別に実行する。

```sh
python -m fastchat.serve.controller

python -m fastchat.serve.model_worker --model-path lmsys/vicuna-7b-v1.5
# or 8bit
python -m fastchat.serve.model_worker --model-path lmsys/vicuna-7b-v1.5 --load-8bit

python -m fastchat.serve.gradio_web_server
```

## 環境構築

```sh
# torch cu118版を指定してますが、環境に合わせて適切なバージョンを指定してください。
# 動作確認したバージョンを固定で導入する場合
$ pip install -r requirements.txt --extra-index-url https://download.pytorch.org/whl/cu118
# or
# 最新のバージョンを確認して導入する場合
$ pip install -e . --extra-index-url https://download.pytorch.org/whl/cu118
```

### 開発環境構築

```sh
# 動作確認したバージョンを固定で導入する場合
$ pip install -r requirements-dev.txt --extra-index-url https://download.pytorch.org/whl/cu118
# or
# 最新のバージョンを確認して導入する場合
$ pip install -e .[dev] --extra-index-url https://download.pytorch.org/whl/cu118
```

### 実行環境の更新

既存の venv 環境を削除後に下記のコマンドで環境を構築する。

```sh
$ pip install -e . --extra-index-url https://download.pytorch.org/whl/cu118
$ pip freeze > requirements.txt
# requirements.txtに対して下記の変更を実施
#
# - pytorchのcudaバージョン指定を削除
# - `-e`で指定されている行を削除

# 開発環境の構築
# `-c`オプションでrequirements.txtの内容は一致させる
$ pip install -e .[dev] --extra-index-url https://download.pytorch.org/whl/cu118
$ pip freeze > requirements-dev.txt  # requirements.txtと同様に処理
```

## Tips

### お試ししたモデル

- `elyza/ELYZA-japanese-Llama-2-7b-fast-instruct`
- `lmsys/vicuna-7b-v1.5`
- `stabilityai/japanese-stablelm-instruct-gamma-7b`
