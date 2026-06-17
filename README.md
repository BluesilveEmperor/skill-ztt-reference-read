# ztt-reference-read

翻译研究文献 PDF 智能解析与结构化分析 Skill，专为翻译研究、语言学、比较文学等社科人文类学术 PDF 设计。

## 特性

- **双身份视角**：研究生视角（学习理解）和审稿人视角（评估评判）
- **智能 PDF 解析**：基于 MinerU SDK，支持中英文 PDF 高质量转换
- **结构化输出**：自动生成符合学术规范的分析报告或审稿意见
- **日用量跟踪**：自动记录 API 使用量，便于配额管理

## 快速开始

### 前置条件

- Python 3.8+
- MinerU SDK（`pip install mineru-open-sdk`）
- MinerU API Token（[获取地址](https://mineru.net/apiManage/token)）

### 配置

```bash
# 1. 安装依赖
pip install mineru-open-sdk

# 2. 创建配置目录
mkdir -p ~/.mineru

# 3. 配置 API Token
echo "token: '你的API密钥'" > ~/.mineru/config.yaml
```

### 使用方法

```bash
# 研究生视角（默认）
python scripts/ztt_pdf_extract.py "paper.pdf" --output-dir ./output

# 审稿人视角
python scripts/ztt_pdf_extract.py "paper.pdf" --output-dir ./output --perspective reviewer
```

## 使用场景

| 场景 | 推荐视角 | 说明 |
|------|---------|------|
| 课程作业 | 研究生视角 | 理解文献内容，提取关键信息 |
| 文献综述 | 研究生视角 | 系统梳理研究框架和方法 |
| 开题报告 | 研究生视角 | 学习研究设计和论证逻辑 |
| 期刊审稿 | 审稿人视角 | 评估研究质量和学术贡献 |
| 学位论文评阅 | 审稿人视角 | 专业评判方法论和结论 |

## 输出示例

### 研究生视角输出

```markdown
# [文献标题]
> 📖 **分析身份：研究生视角** — 以学习理解为导向

## 一、摘要（Abstract）
## 二、文献综述（Literature Review）
## 三、研究问题（Research Questions）
## 四、研究方法（Research Methods）
## 五、研究结果（Research Results）
## 六、讨论与评价
## 七、关键术语与概念
```

### 审稿人视角输出

```markdown
# 审稿意见：[文献标题]
> 🎯 **分析身份：审稿人视角** — 以评估评判为导向

## 一、总体评价（Overall Assessment）
## 二、研究问题与创新性评估
## 三、方法论评估
## 四、论证与证据评估
## 五、具体修改意见
## 六、写作与呈现质量
## 七、总结与建议
```

## 身份切换

| 命令 | 视角 |
|------|------|
| 默认（无关键词） | 研究生视角 |
| 包含 `审稿人`/`reviewer`/`审稿` | 审稿人视角 |
| `/ztt-reference-read 审稿人视角` | 审稿人视角 |

## 脚本参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--output-dir` | `./ztt-output` | 输出目录 |
| `--model` | `vlm` | 模型版本：`pipeline` / `vlm` / `html` |
| `--ocr` | 关闭 | 对扫描件启用 OCR |
| `--language` | `ch` | 文档语言（`ch`=中文，`en`=英文） |
| `--no-formula` | 开启公式识别 | 禁用公式识别 |
| `--no-table` | 开启表格识别 | 禁用表格识别 |
| `--pages` | 全部 | 页码范围，如 `"1-10,15"` |

## 文件结构

```
ztt-reference-read/
├── README.md           # 本文件
├── SKILL.md            # Skill 主文档
├── daily_usage.json    # 日用量记录
└── scripts/
    ├── ztt_pdf_extract.py  # PDF 提取脚本
    └── toc-newpage.tex     # LaTeX 目录模板
```

## API 限制

- 单文件 ≤ 200MB，≤ 600 页
- 免费版日限额：2000 页
- 上传链接有效期：24 小时
- 解析结果保存：30 天

## Windows 用户注意

如果遇到 GBK 编码错误，在命令前加 `PYTHONIOENCODING=utf-8`：

```bash
PYTHONIOENCODING=utf-8 python scripts/ztt_pdf_extract.py "paper.pdf"
```

## 许可证

MIT License
