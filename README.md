# Velocis AI 專案

[![授權：MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Mojo 版本](https://img.shields.io/badge/Mojo-最新%20(預計1.0%20in%202026)-blue)](https://docs.modular.com/mojo)
[![MAX 平台](https://img.shields.io/badge/MAX-Platform%2025.x-green)](https://www.modular.com/max)

## 專案概述

**Velocis** 是一個雄心勃勃的開源人工智慧專案，目標是打造一款在**智能**與**效率**上超越 **Claude 3 Opus** 的大型語言模型（LLM）。  
本專案主要使用 **Mojo** 語言開發，結合 Python 的易用性與接近 C++/Rust 等級的極致效能，特別針對 CPU、GPU 與各種 AI 加速器進行深度優化。

Velocis 不僅追求更高的推理速度與更低的資源消耗，更致力於探索超越傳統 Transformer 的新一代模型架構，讓 AI 在長上下文理解、邏輯推理與能耗表現上達到全新境界。

## 核心特色

- **超越級智能**：採用 Linear Attention、Mamba（狀態空間模型）、Mixture of Experts（MoE）等先進架構組合
- **極致效率**：利用 Mojo 原生 SIMD、tiling、向量化與 GPU 程式設計能力，實現比 PyTorch 更快數倍的推理速度
- **可擴展訓練**：支援合成數據生成、RLHF / DPO / PPO 等先進對齊技術
- **模組化設計**：易於替換層結構、分詞器、路由邏輯，方便研究與客製化
- **硬體友好**：原生支援 NVIDIA、AMD GPU 與未來各種 AI 加速器（透過 Modular MAX 平台）

## 技術堆疊（Technology Stack）

Velocis 採用極致性能導向的精簡技術堆疊，核心全部使用 Mojo 打造關鍵效能部件，並與 Python 生態無縫整合：

### 主要程式語言
- **Mojo**（主語言）
  - 版本：最新穩定版（2026年預計進入 1.0 階段）
  - 優勢：強型別系統（struct）、ownership & borrowing 記憶體安全、原生並行（parallelize）、SIMD 向量運算、GPU 程式設計支援
  - 主要用途：完整推理引擎、張量運算核心（matmul、attention、ffn）、MoE 動態路由、模型各層實現

### 輔助與生態整合
- **Python 3.12+**（原型開發、資料處理）
  - Mojo 與 Python 完全互通，可直接 import Python 模組
  - 常用套件：
    - **numpy / scipy** → 初期數值原型驗證
    - **Hugging Face Datasets / Tokenizers** → 資料集管理與分詞器（後期轉為純 Mojo 實現）
    - **transformers**（選用）→ 權重轉換與參考

### 模型架構核心元件（全部 Mojo 實現）
- 自研高性能張量庫（Tensor Library）
  - 原生 SIMD + tiling 優化矩陣運算
  - 透過 MAX 平台支援 GPU 加速（NVIDIA / AMD）
- 先進架構模組：
  - **高效 Transformer**（優化版多頭注意力 + 前饋層）
  - **Linear Attention** / **FlashAttention-like** 機制（長序列利器）
  - **Mamba / State Space Models**（推理效率極高）
  - **Sparse Mixture of Experts (MoE)**（動態路由，Mojo 條件執行極快）

### 訓練與資料策略
- **資料管道**：
  - 合成數據（Synthetic Data）生成 → 利用當前最強模型產生高質量推理/思考鏈數據
  - 高品質開源資料集過濾 + 自製蒸餾數據
- **對齊技術**：
  - RLHF / DPO / IPO 等偏好優化（部分 Python 原型 + Mojo 高效實作）
  - 支援大規模分散式訓練（未來整合 MAX / Mammoth）

### 部署與服務
- **MAX Platform**（Modular 官方加速平台）
  - 用於最終生產級推理部署
  - 支援 speculative decoding、paged attention、batch inference 等最新優化
  - 可跨 NVIDIA / AMD GPU 執行，無 vendor lock-in

## 目前階段（2026年1月）

- 基礎推理引擎（類 llama.mojo 架構）已完成原型
- 正在開發 Mamba 與 MoE 混合架構
- 自研張量核心持續優化（目標超越 llama.cpp 在同硬體上的速度）
- 訓練資料管道建設中（首批合成數據生成完成）

## 快速開始

```bash
# 1. 安裝最新 Mojo SDK（透過 Modular 官網）
# https://www.modular.com/mojo

# 2. 克隆專案
git clone https://github.com/你的用戶名/velocis-ai.git
cd velocis-ai

# 3. 執行基礎 Llama-like 推理示範（純 Mojo）
mojo run examples/simple_inference.mojo
