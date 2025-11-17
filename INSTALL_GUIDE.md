# 项目环境安装指南

## ⚠️ 重要提示

**确保使用项目虚拟环境（`.venv`），而不是 conda 环境！**

## 错误原因分析

从错误信息可以看到，你之前使用的是 conda 环境：
```
/root/miniconda3/envs/llm/lib/python3.10/site-packages/numpy/distutils/
```

这会导致：
1. 依赖安装到错误的环境
2. 项目运行时找不到正确的包
3. 环境混乱

## 正确安装步骤

### 1. 确保使用项目虚拟环境

```bash
# 检查当前 Python 路径
which python
# 如果显示 conda 路径，需要先退出 conda 环境
conda deactivate

# 激活项目虚拟环境
source .venv/bin/activate

# 验证（应该显示 .venv 路径）
which python
# 应该显示: /mnt/d/develop/ultralytics-YOLO-DeepSort-ByteTrack-PyQt-GUI/.venv/bin/python
```

### 2. 使用 uv 安装依赖

```bash
# 确保在项目虚拟环境中
source .venv/bin/activate

# 先安装 numpy（某些包需要）
uv pip install numpy==1.24.3

# 安装所有依赖（现在使用 lapx 替代 lap）
uv pip install -r requirements.txt
```

### 3. 验证安装

```bash
# 检查已安装的包
uv pip list | grep -E "lap|numpy|torch"

# 应该看到 lapx 而不是 lap
```

## 关于 lap 包的修复

**问题**：`lap==0.4.0` 使用了已弃用的 `numpy.distutils`，在 Linux/WSL 上构建失败。

**解决方案**：已将 `requirements.txt` 中的 `lap==0.4.0` 替换为 `lapx`。

- ✅ `lapx` 是 `lap` 的现代替代品
- ✅ API 完全兼容（`lap.lapjv()` 可以直接使用）
- ✅ 无需修改代码
- ✅ 更好的兼容性和性能

## 常见问题

### Q: 如何确认使用的是项目虚拟环境？

A: 运行以下命令：
```bash
source .venv/bin/activate
python -c "import sys; print(sys.executable)"
# 应该显示: /mnt/d/develop/.../.venv/bin/python
```

### Q: 如果还是安装失败怎么办？

A: 分步安装：
```bash
source .venv/bin/activate

# 1. 先安装基础包
uv pip install numpy==1.24.3 scipy==1.10.1

# 2. 安装其他依赖（排除有问题的包）
uv pip install beautifulsoup4==4.12.2 certifi==2023.5.7 charset-normalizer==3.1.0 cmake==3.26.3 coloredlogs==15.0.1 filelock==3.12.0 flatbuffers==23.3.3 humanfriendly==10.0 idna==3.4 Jinja2==3.1.2 lit==16.0.3 MarkupSafe==2.1.2 mpmath==1.3.0 networkx==3.1

# 3. 安装 lapx
uv pip install lapx

# 4. 安装剩余依赖
uv pip install -r requirements.txt
```

### Q: 如何重新创建虚拟环境？

A: 
```bash
# 删除旧环境
rm -rf .venv

# 创建新环境
uv venv --python 3.10 .venv

# 激活并安装
source .venv/bin/activate
uv pip install -r requirements.txt
```



