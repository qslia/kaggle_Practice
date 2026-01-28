这个报错**不是你的代码逻辑问题**，而是 **Matplotlib 新版本把 `seaborn-*` 样式移除了**。你现在的环境（detectron2 + 新 matplotlib）已经不再内置 `"seaborn-whitegrid"` 这个 style。

---

## ❌ 报错原因（核心一句话）

```python
plt.style.use("seaborn-whitegrid")
```

在 **Matplotlib ≥ 3.8** 中已经 **失效**，因此抛出：

```
OSError: 'seaborn-whitegrid' is not a valid package style
```

---

## ✅ 正确做法（3 种，推荐第 1 种）

---

## ✅ 方案 1（✅ 推荐）：**用 seaborn 自己设置风格**

这是官方推荐、最稳定、最不容易炸的方式。

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(
    style="whitegrid",
    context="notebook",
    rc={
        "figure.figsize": (11, 4),
        "axes.titlesize": 16,
        "axes.titleweight": "bold",
        "axes.labelsize": "large",
        "axes.labelweight": "bold",
    }
)
```

✅ 优点

* 不依赖 matplotlib 内置 style
* seaborn 风格不会被移除
* 和你后面 `sns` 完美兼容

---

## ✅ 方案 2：改成 Matplotlib 仍然支持的 style

先看看你现在**有哪些可用样式**：

```python
import matplotlib.pyplot as plt
plt.style.available
```

常见可用的替代：

```python
plt.style.use("ggplot")
# 或
plt.style.use("classic")
# 或
plt.style.use("tableau-colorblind10")
```

⚠️ 但注意：
这些 **不等价于 seaborn whitegrid**，只是视觉接近。

---

## ✅ 方案 3（不推荐）：安装旧 matplotlib

```bash
pip install "matplotlib<3.8"
```

❌ 不推荐原因

* detectron2 / 其他库可能冲突
* 为了一个 style 降级库不值得

---

## ✅ 你的完整「不炸版」代码（可直接复制）

```python
import matplotlib.pyplot as plt
import seaborn as sns

# seaborn 统一管理风格（替代 seaborn-whitegrid）
sns.set_theme(
    style="whitegrid",
    rc={
        "figure.figsize": (11, 4),
        "axes.titlesize": 16,
        "axes.titleweight": "bold",
        "axes.labelsize": "large",
        "axes.labelweight": "bold",
    }
)

plot_params = dict(
    color="#556B2F",
    style=".-",
    markeredgecolor="#4169E1",
    markerfacecolor="#8B0000",
    legend=False
)

# Jupyter 高分辨率
%config InlineBackend.figure_format = 'retina'
```

---

## 🧠 一句话记忆（很重要）

> **Matplotlib 现在不再负责 seaborn 风格**
> 👉 **seaborn 的风格，用 seaborn 自己设**

---

如果你愿意，我可以帮你

* 🎯 把这个配置封成一个 `plot_style.py`
* 🎯 调成 **Kaggle / 论文 / 报告级别**配色
* 🎯 完全不使用 seaborn，只用 matplotlib 复刻 whitegrid

你想走哪条？
