---
title: lm-sys/FastChatのお試し
date: 2023-11-05
lastmod: 2023-12-31
---

## 概要

[lm-sys/FastChat](https://github.com/lm-sys/FastChat)の動作確認になります。

## 実行方法

環境構築などにはTaskを利用します。
代表的なコマンドを下記に記載します。他のコマンドについては`task -l`で確認してください。

- 環境構築
  - 実行のみする場合: `task init`
  - 開発環境を作成する場合: `task init-dev`
  - 環境を更新する場合: `task update-requirements`
- CLIの起動: `task cli -- --model-path=lmsys/vicuna-7b-v1.5`
- Web Serverの起動は以下のタスクを順に起動する。
  - 全てプロセスが起動するため、別のシェルで実行する。
    - model-workerは、controllerに登録するため先にcontrollerが起動している必要がある。
  - `task server-controller`
  - `task server-model-worker -- --model-path=lmsys/vicuna-7b-v1.5`
  - `task server-web`

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
