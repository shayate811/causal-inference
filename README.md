# Causal Inference Demo: "風が吹けば桶屋が儲かる" 🌪️

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Dev%20Containers-2496ED.svg)](https://containers.dev/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📖 Overview

日本の有名なことわざ**「風が吹けば桶屋が儲かる」**を題材に、データサイエンスの手法を用いて「相関関係」と「因果関係」の違いを検証するデモプロジェクトです。

回帰分析（OLS）による相関の確認から、ベイズネットワークを用いた**因果構造探索（Causal Discovery）**までを行い、データから真の因果グラフ（DAG）を自動的に導出するプロセスを実装しています。

🔗 **解説記事 (Zenn):** [https://zenn.dev/shayate811/articles/causal-inference]

## 🏗️ Architecture & MLOps

本プロジェクトは**再現性（Reproducibility）**を最優先に設計しています。
「手元の環境では動いた」という問題を排除するため、**Dev Containers** を採用し、誰でも完全に同一の環境でコードを実行可能です。

* **Environment**: Docker (Dev Containers)
* **Language**: Python 3.11
* **Key Libraries**:
    * `pgmpy`: 因果探索・ベイズネットワーク構築
    * `statsmodels`: 統計的解析（回帰分析）
    * `networkx`: グラフ構造の可視化

### Infrastructure as Code (IaC)
因果推論ライブラリはAPIの変更が頻繁に行われるため、`requirements.txt` にてバージョンを厳密に固定（Pinning）しています。特に `pgmpy` は互換性を保つために `0.1.25` を指定しています。

```text
# requirements.txt example
numpy<2.0.0
pandas>=2.0.0
pgmpy==0.1.25  # Pinned for reproducibility
```

## 🚀 Getting Started

VS CodeとDockerがインストールされていれば、コマンド一つで環境構築が完了します。

Clone the repository

```bash
git clone https://github.com/shayate811/causal-inference.git
cd causal-inference
```

**-Open in Dev Container**

VS Codeでフォルダを開きます。

左下の緑色のアイコン（><）をクリックし、"Reopen in Container" を選択します。（vscodeの拡張機能 DevContainersが必要）

自動的にDockerイメージのビルドとライブラリのインストールが始まります（初回は数分かかります）。

**-Run the Notebook**

analysis.ipynb を開き、セルを上から順に実行してください。

## 📊 Analysis Steps

本デモでは、以下の3段階で解析を行っています。

Data Generation (Simulation)

「気温」を共通の交絡因子（Confounder）として設定し、風速と売上のダミーデータを生成します。

あえて「風速」と「売上」の間に直接の因果関係を持たせない設定にします。

Spurious Correlation (OLS)

単回帰分析を行い、風速と売上に「統計的に有意な相関」が出ることを確認します（相関の罠）。

重回帰分析で気温を統制し、風速の係数が消滅する様子を観察します。

Causal Discovery (Bayesian Network)

pgmpy の HillClimbSearch アルゴリズムを使用し、データのみから因果グラフ（DAG）を推定します。

結果: 

風速と売上のリンクが切断され、条件付き独立（Conditional Independence）が可視化されます。

## 📂 Directory Structure

```
.
├── .devcontainer/       # Dev Container configuration (Dockerfile, devcontainer.json)
├── analysis.ipynb       # Main analysis notebook
├── requirements.txt     # Python dependencies (Version pinned)
└── README.md            # Project documentation
```

