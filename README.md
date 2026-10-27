# TeleAgent 高校 AI 创新大赛参赛项目

“电信杯”TeleAgent 高校 AI 创新大赛参赛仓库，用于团队协作开发参赛智能体、沉淀过程材料与作品文档。

## 项目信息

| 项目 | 内容 |
| --- | --- |
| 赛事 | “电信杯”TeleAgent 高校 AI 创新大赛 |
| 赛道 | 待定（揭榜挂帅 / 创意擂台） |
| 选题 | 待定 |
| 团队 | 待补充 |
| 开发平台 | 中国电信 TeleAgent（星辰超级智能体） |

> 确定选题后请队长及时更新上表，避免队友看到过期信息。

## 目录结构

```text
TeleAgent_Project/
├── code/                    # 源码、脚本、智能体配置、提示词
│   └── test.py              # 占位入口，后续替换为实际代码
├── doc/                     # 赛事资料、调研、会议记录、作品材料
├── .github/                 # Issue / PR 模板
├── .editorconfig            # 编辑器统一格式
├── .env.example             # 环境变量示例（复制为 .env）
├── .gitattributes           # 换行符与二进制文件规则
├── .gitignore               # 忽略规则
├── CONTRIBUTING.md          # 协作规范（必读）
├── README.md
└── requirements.txt         # Python 依赖
```

## 快速开始

### 1. 克隆仓库

```bash
git clone https://github.com/Starchaser19/TeleAgent_Project.git
cd TeleAgent_Project
```

### 2. 创建虚拟环境

需要 Python 3.11+（当前开发机为 3.13）。

```bash
python -m venv .venv
```

激活虚拟环境：

```bash
# Windows PowerShell
.venv\Scripts\Activate.ps1
# Windows CMD
.venv\Scripts\activate.bat
# macOS / Linux
source .venv/bin/activate
```

### 3. 安装依赖

```bash
pip install -r requirements.txt
```

### 4. 配置环境变量

```bash
# Windows
copy .env.example .env
# macOS / Linux
cp .env.example .env
```

编辑 `.env` 填入自己的配置。`.env` 已被忽略，不会提交到仓库。

### 5. 运行

```bash
python code/test.py
```

> 当前 `code/test.py` 是空占位文件，确定技术方案后替换为实际入口。

## 协作规范

完整流程见 [CONTRIBUTING.md](CONTRIBUTING.md)。先记住三条：

1. **不直接改 `main`**：一人一分支，通过 Pull Request 合并。
2. **开工前先同步**：`git switch main && git pull`。
3. **不提交**密钥、个人数据、模型权重和大文件。

## 当前进度

- [x] 仓库初始化（README、协作规范、忽略规则、模板）
- [ ] 确定赛道与选题
- [ ] 完成需求分析与方案设计
- [ ] 搭建 TeleAgent 智能体原型
- [ ] 准备作品报告与演示材料
- [ ] 提交参赛作品

## 参考资料

| 文件 | 说明 |
| --- | --- |
| `doc/notice_text.txt` | 校内培训会通知正文 |
| `doc/nepu_notice.txt` | 校内信息网通知页面存档 |
| `doc/poster_ocr.txt` | 赛事宣传海报 OCR 文本 |
| `doc/shaanxi_guide.txt` | 陕西赛区参赛指引（参考，规则以黑龙江赛区为准） |
| `doc/wx_article.txt`、`doc/wx_article2.txt` | 赛事相关公众号文章存档 |
| `doc/wx_imgs/` | 文章配图 |
| `doc/*.pdf`、`doc/*.docx` | 原始附件与文件 |

## 许可

比赛作品，暂未指定开源许可证。未经团队同意，请勿对外分发。
