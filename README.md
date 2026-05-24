# Daniya GPT-SoVITS Training

达妮娅语音合成模型训练项目

## 🚀 快速开始（Kaggle）

### 方法1：从 GitHub 导入（推荐）

1. 打开 https://www.kaggle.com/code
2. 点击 **File → Import Notebook**
3. 选择 **GitHub** 标签
4. 输入仓库 URL: `https://github.com/huanx/daniya-gptsovits-training`
5. 或直接输入: `huanx/daniya-gptsovits-training`
6. 选择 `daniya_gptsovits_kaggle.ipynb`
7. 设置 **GPU: T4** + **Internet: On**
8. 依次运行所有单元格（8个步骤）

### 方法2：手动上传

1. 下载 [daniya_gptsovits_kaggle.ipynb](./daniya_gptsovits_kaggle.ipynb)
2. 在 Kaggle 上传 Notebook
3. 开启 GPU T4 + Internet
4. 运行所有单元格

## 📊 数据集

- **HuggingFace**: https://huggingface.co/datasets/huanx/daniya-voice-gptsovits
- **样本数**: 93个中文语音
- **总时长**: 约13分钟
- **格式**: WAV, 48kHz, 24-bit, Mono
- **说话人**: 达妮娅（游戏角色）
- **语言**: 中文

## ⚙️ 训练参数

| 模型 | Epochs | Batch Size | Save Steps | 预计时间 |
|------|--------|------------|------------|----------|
| SoVITS | 200 | 4 | 1000 | 30-60 min |
| GPT | 100 | 8 | 1000 | 30-60 min |

**总计**: 1-2小时 (Kaggle T4 GPU)

**保存策略**:
- 每 1000 步保存一次 checkpoint
- 最多保留 50 个 checkpoint
- 训练完成后自动打包所有模型

## 📁 文件结构

```
.
├── daniya_gptsovits_kaggle.ipynb  # Kaggle 训练 Notebook
├── configs/
│   ├── gpt_train.yaml             # GPT 训练配置
│   └── sovits_train.yaml          # SoVITS 训练配置
└── README.md
```

## 🎯 训练流程

Notebook 包含以下 8 个步骤：

1. **克隆仓库**: 从 GitHub 克隆 GPT-SoVITS
2. **安装依赖**: pip 安装所需包
3. **下载预训练模型**: 从 HuggingFace 下载（约5GB）
4. **下载数据集**: 从 HF 拉取达妮娅语音数据
5. **数据预处理**: 提取文本/音频/语义特征（3个子步骤）
6. **训练 SoVITS**: 声码器训练（200 epochs）
7. **训练 GPT**: 语言模型训练（100 epochs）
8. **打包下载**: 生成 `daniya_gptsovits_model.tar.gz`

## 📦 输出模型

训练完成后会生成：

```
daniya_gptsovits_model.tar.gz
├── logs_s2_v2/          # SoVITS checkpoints
│   └── daniya/
│       └── *.pth
└── logs_s1/             # GPT checkpoints
    └── daniya/
        └── *.ckpt
```

模型大小约 100-200 MB（压缩后）

## 🔧 自定义训练

如需调整训练参数，修改 `configs/` 目录下的配置文件：

- `gpt_train.yaml`: GPT 模型配置
- `sovits_train.yaml`: SoVITS 模型配置

主要可调参数：
- `batch_size`: 批次大小（显存不足可减小）
- `epochs`: 训练轮数
- `learning_rate`: 学习率
- `save_steps`: 保存间隔

## 📝 许可

MIT License

## 🙏 致谢

- [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS) - 原始训练框架
- 达妮娅语音数据来源于游戏《鸣潮》
