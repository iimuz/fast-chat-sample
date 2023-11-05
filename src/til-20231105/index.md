---
title: lm-sys/FastChatのお試し
date: 2023-11-05
lastmod: 2023-11-05
---

## 概要

[lm-sys/FastChat](https://github.com/lm-sys/FastChat)の動作確認になります。

## 実行方法

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

|      開発主体      |   発表日   | モデルサイズ | HuggingFace のパス                                                                                                          | 備考                                      |
| :----------------: | :--------: | -----------: | :-------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------- |
|     CyberAgent     | 2023-05-17 |           7B | [`cyberagent/open-calm-7b`](https://huggingface.co/cyberagent/open-calm-7b)                                                 |                                           |
|     CyberAgent     | 2023-11-02 |           7B | [`cyberagent/calm2-7b`](https://huggingface.co/cyberagent/calm2-7b)                                                         |                                           |
|       ELYZA        | 2023-08-28 |           7B | [`elyza/ELYZA-japanese-Llama-2-7b-fast-instruct`](https://huggingface.co/elyza/ELYZA-japanese-Llama-2-7b-fast)              |                                           |
|   HuggingFace H4   | 2023-10-26 |           7B | [`HuggingFaceH4/zephyr-7b-beta`](https://huggingface.co/HuggingFaceH4/zephyr-7b-beta)                                       |                                           |
|     LMSYS Org.     | 2023-07-29 |           7B | [`lmsys/vicuna-7b-v1.5`](https://huggingface.co/lmsys/vicuna-7b-v1.5)                                                       |                                           |
| Preffered Networks | 2023-09-28 |          13B | [`pfnet/plamo-13b`](https://huggingface.co/pfnet/plamo-13b)                                                                 | `--load-8bit`オプションで起動できなかった |
| Stability AI Japan | 2023-10-25 |           7B | [`stabilityai/japanese-stablelm-instruct-gamma-7b`](https://huggingface.co/stabilityai/japanese-stablelm-instruct-gamma-7b) |                                           |

### 試したいモデル

|  開発主体  |   発表日   | モデルサイズ | HuggingFace のパス                                                                                                                          | 備考 |
| :--------: | :--------: | -----------: | :------------------------------------------------------------------------------------------------------------------------------------------ | :--- |
|    LINE    | 2023-08-14 |         3.6B | [`line-corporation/japanese-large-lm-3.6b-instruction-sft`](https://huggingface.co/line-corporation/japanese-large-lm-3.6b-instruction-sft) |      |
| LMSYS Org. | 2023-07-29 |          13B | [`lmsys/vicuna-13b-v1.5`](https://huggingface.co/lmsys/vicuna-13b-v1.5)                                                                     |      |
| CyberAgent | 2023-11-02 |           7B | [`cyberagent/calm2-7b-chat`](https://huggingface.co/cyberagent/calm2-7b-chat)                                                               |      |
