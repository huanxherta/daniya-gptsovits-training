# Kaggle 导入指南

## 🎯 目标

从 HuggingFace Space 导入 Notebook 到 Kaggle 进行训练

## 📋 步骤

### 方法1：直接下载后上传（最简单）

1. **下载 Notebook**
   - 访问: https://huggingface.co/spaces/huanx/daniya-gptsovits-training/blob/main/daniya_gptsovits_kaggle.ipynb
   - 点击右上角 **Download** 按钮
   - 保存到本地

2. **上传到 Kaggle**
   - 打开 https://www.kaggle.com/code
   - 点击 **File → Upload Notebook**
   - 选择刚下载的 `.ipynb` 文件
   - 等待上传完成

3. **配置环境**
   - 点击右侧 **Settings**
   - **Accelerator**: 选择 **GPU T4**
   - **Internet**: 打开开关（必须）
   - 点击 **Save**

4. **开始训练**
   - 依次点击运行每个单元格（共8个）
   - 或点击顶部 **Run All** 一键运行
   - 等待 1-2 小时完成训练

### 方法2：通过 URL 导入（如果 Kaggle 支持 HF）

1. **尝试 URL 导入**
   - 打开 https://www.kaggle.com/code
   - 点击 **File → Import Notebook**
   - 选择 **URL** 标签
   - 输入: `https://huggingface.co/spaces/huanx/daniya-gptsovits-training/resolve/main/daniya_gptsovits_kaggle.ipynb`
   - 点击 **Import**

2. **如果失败，使用方法1**

## ⚠️ 重要提示

1. **必须开启 Internet**
   - Notebook 需要从 HuggingFace 下载：
     - 预训练模型（约5GB）
     - 数据集（约120MB）

2. **必须使用 GPU**
   - 推荐 **T4 GPU**（免费）
   - CPU 训练会非常慢（不推荐）

3. **预计时间**
   - 下载模型: 5-10 分钟
   - 数据预处理: 5-10 分钟
   - SoVITS 训练: 30-60 分钟
   - GPT 训练: 30-60 分钟
   - **总计**: 1-2 小时

4. **Kaggle 限制**
   - 免费用户每周 GPU 时长有限（约30小时/周）
   - 单次运行最长 12 小时
   - 本训练约占用 1-2 小时

## 📦 训练完成后

1. **下载模型**
   - 运行完第 8 个单元格后
   - 会生成 `daniya_gptsovits_model.tar.gz`
   - 点击右侧 **Output** 标签
   - 找到 `.tar.gz` 文件并下载

2. **模型大小**
   - 约 100-200 MB（压缩后）

3. **模型内容**
   ```
   daniya_gptsovits_model.tar.gz
   ├── logs_s2_v2/daniya/*.pth    # SoVITS 模型
   └── logs_s1/daniya/*.ckpt      # GPT 模型
   ```

## 🔧 故障排除

### 问题1：下载预训练模型失败

**症状**: Step 3 报错 `Connection timeout` 或 `Download failed`

**解决**:
- 重新运行该单元格
- 或等待几分钟后再试
- HuggingFace 服务器可能暂时繁忙

### 问题2：显存不足 (OOM)

**症状**: 训练时报错 `CUDA out of memory`

**解决**:
- 修改配置文件中的 `batch_size`
- SoVITS: 从 4 改为 2
- GPT: 从 8 改为 4

### 问题3：训练中断

**症状**: Kaggle 会话超时或断开

**解决**:
- 重新运行 Notebook
- 训练会从最近的 checkpoint 继续
- 不会丢失已训练的进度

## 📞 获取帮助

如遇到其他问题：
1. 查看 Notebook 中的错误信息
2. 检查是否开启了 GPU 和 Internet
3. 确认 HuggingFace 数据集可访问: https://huggingface.co/datasets/huanx/daniya-voice-gptsovits
