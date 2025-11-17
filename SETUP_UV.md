# 使用 uv 创建和配置项目虚拟环境

## 步骤 1: 创建虚拟环境

```bash
# 使用 Python 3.10 创建虚拟环境（项目根目录下的 .venv）
uv venv --python 3.10 .venv
```

## 步骤 2: 激活虚拟环境

```bash
# Linux/WSL
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1

# Windows CMD
.venv\Scripts\activate.bat
```

## 步骤 3: 安装依赖

### 方法 A: 使用 uv pip（推荐，在激活虚拟环境后）

```bash
# 激活环境后，uv 会自动使用当前环境的 Python
source .venv/bin/activate
uv pip install numpy==1.24.3  # 先安装 numpy（lap 需要）
uv pip install -r requirements.txt
```

### 方法 B: 使用 uv pip 并指定 Python（无需激活）

```bash
# 直接指定虚拟环境的 Python
uv pip install numpy==1.24.3 --python .venv/bin/python
uv pip install -r requirements.txt --python .venv/bin/python
```

## 步骤 4: 处理 lap 包的问题

如果 `lap==0.4.0` 安装失败，使用 `lapx` 替代：

```bash
# 先安装其他依赖（排除 lap）
uv pip install $(grep -v "^lap==" requirements.txt | tr '\n' ' ') --python .venv/bin/python

# 安装 lapx 替代 lap
uv pip install lapx --python .venv/bin/python
```

或者修改 `requirements.txt`，将 `lap==0.4.0` 替换为 `lapx`。

## 验证安装

```bash
# 激活环境
source .venv/bin/activate

# 检查 Python 版本
python --version  # 应该显示 Python 3.10.x

# 检查已安装的包
uv pip list

# 运行项目
python main.py
```

## 注意事项

1. **始终使用项目虚拟环境**：确保使用 `.venv` 而不是系统的 conda 环境
2. **激活环境**：在运行项目前记得激活虚拟环境
3. **lap 包问题**：如果遇到 `lap` 构建问题，使用 `lapx` 替代



