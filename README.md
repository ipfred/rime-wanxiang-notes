# 万象输入法笔记 指南（rime-wanxiang-notes）

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/ipfred/rime-wanxiang-notes)


> 这是一个“文档仓库”，用于帮助新手更快上手「万象输入法 / rime_wanxiang」。方案文件与实现请前往源项目获取。

快速导航：`docs/index.md`（站点入口）、`docs/01-5分钟上手.md`（先跑起来）、`docs/07-功能亮点与配置速查.md`（收藏级速查）。

---

## 📁项目地址

[![GitHub Stars](https://img.shields.io/github/stars/amzxyz/rime_wanxiang?style=social)](https://github.com/amzxyz/rime_wanxiang/stargazers)
[![release](https://img.shields.io/github/v/release/amzxyz/rime_wanxiang?color=brightgreen)](https://github.com/amzxyz/rime_wanxiang/releases)
- 源项目（方案与实现）：https://github.com/amzxyz/rime_wanxiang
- 本仓库内容（文档）：`docs/`

## ✨ 核心亮点

### 🎯 为什么选择万象？

- ⚡ **智能整句输入** - AI筛选的大基数词库 + 语言模型，更精准的整句联想
- 🎵 **全声调标注** - 唯一支持整句拼音串上屏的方案，可显示/输入音调
- 🔧 **6种辅助码** - 墨奇/鹤形/自然码/虎码/五笔/汉心码，拼音+辅助码任意组合
- 🔍 **强大反查系统** - 支持两分/多分/笔画三种打法，U+Unicode完整覆盖
- 🎨 **丰富Lua扩展** - 成对符号、tips提示、手动排序、无感造词等创新功能

### 📸 效果预览

![效果展示](https://storage.deepin.org/thread/202502200358104987_效果.png)

---

## 🔀 版本选择

| 特性 | 标准版 | 增强版PRO |
|-----|-------|----------|
| **方案文件** | `wanxiang.schema.yaml` | `wanxiang_pro.schema.yaml` |
| **支持类型** | 全拼、任何双拼 | 只支持双拼 |
| **自动调频** | ✅ 默认开启 | ❌ 默认关闭 |
| **用户词记录** | 无差别自动记录 | 需手动造词（``引导） |
| **用户词位置** | `wanxiang.userdb` | `zc.userdb` |
| **辅助码** | 基于声调的辅助 | 7种辅助码可选，兼容声调 |
| **推荐场景** | 日常使用 | 喜欢精准控制、辅助码选字 |

---

## 🚀 快速开始（30秒上手）

整个rime配置生态都是通的，不了解rime基础的可以参考友情链接，初步了解rime运行的些许特性：
- [oh my rime](https://www.mintimate.cc/zh/guide/installRime.html)
- [rime参数配置](https://xishansnow.github.io/posts/41ac964d.html)

> 💡 **友情提示：** *如果你是第一次使用万象，可以不要用你过往经验来定义万象，按如下的步骤将万象跑起来后,体验一下万象的功能，然后学习一下万象的各项内容之后再考虑。*

### 方式一：快速部署 ⚡

1. 将方案文件 `rime-wanxiang-base.zip`、语法模型 `wanxiang-lts-zh-hans.gram` 置于Rime用户目录
2. 输入以下指令切换双拼/全拼类型
3. 重新部署，完成！

```bash
/flypy    → 小鹤双拼
/mspy     → 微软双拼
/zrm      → 自然码
/sogou    → 搜狗双拼
/pinyin   → 全拼
/wxsp     → 万象双拼
# ... 更多指令见下方
```

> 💡 **提示**：这些指令能一次性完成4个补丁文件的输入类型修改，无需手动配置！

### 方式二：plum一键安装 🛠️

安装环境可用plum命令简单安装与更新，在保证安装小狼毫、中州韵、鼠须管等前端的前提下。

<details> 
<summary><strong>👇  plum命令安装</strong></summary>

**环境要求**

> ⚠️ **注意**：Windows的PowerShell/CMD不能直接运行东风破，**必须用Git Bash**。
> macOS / Linux | ✅ 已内置bash

**步骤1：安装Plum**

这是维护在万象仓库plum分支的版本，去掉了默认方案，修改了默认路径。

```bash
# 打开终端，执行以下命令
git clone -b plum --depth 1 https://github.com/amzxyz/rime_wanxiang.git
cd plum
```

**步骤2：配置用户目录变量**

对于小狼毫、鼠须管、Fcitx5已经默认配置了变量：

```bash
# 小狼毫
export rime_frontend='rime/weasel'

# 鼠须管
export rime_frontend='rime/squirrel'

# Fcitx5
export rime_frontend='fcitx5/fcitx5-rime'
```

但对于Linux、Mac使用ibus、fcitx前端需要自己设置变量（可终端执行，最好写入~/.zshrc）：

```bash
# ibus-rime
export rime_frontend=rime/ibus-rime

# fcitx-rime
export rime_frontend=fcitx/fcitx-rime
```

**步骤3：执行安装命令**

切换到plum目录，执行对应的安装命令即可实现安装和更新。
</details> 

#### 快速安装

**基础版（完整）**
```bash
bash rime-install amzxyz/rime_wanxiang@wanxiang-base:plum/full
```

**自然码辅助版（完整）**
```bash
bash rime-install amzxyz/rime_wanxiang@wanxiang-zrm-fuzhu:plum/full
```

<details>
<summary>📦 查看全部Plum安装命令</summary>

**基础版**
```bash
# 完整版
bash rime-install amzxyz/rime_wanxiang@wanxiang-base:plum/full

# 仅词库
bash rime-install amzxyz/rime_wanxiang@wanxiang-base:plum/dicts
```

**辅助码版本**
```bash
# 自然码辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-zrm-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-zrm-fuzhu:plum/dicts

# 墨奇辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-moqi-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-moqi-fuzhu:plum/dicts

# 小鹤辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-flypy-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-flypy-fuzhu:plum/dicts

# 虎码辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-tiger-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-tiger-fuzhu:plum/dicts

# 五笔辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-wubi-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-wubi-fuzhu:plum/dicts

# 汉心辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-hanxin-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-hanxin-fuzhu:plum/dicts

# 首右辅助
bash rime-install amzxyz/rime_wanxiang@wanxiang-shouyou-fuzhu:plum/full
bash rime-install amzxyz/rime_wanxiang@wanxiang-shouyou-fuzhu:plum/dicts
```

</details>

### 方式三：脚本工具 👨‍💻

- **Windows**：[wanxiang-tools.exe](https://github.com/amzxyz/RIME-LMDG/releases/tag/tool) - 内置在线更新器
- **跨平台脚本**：[rime-wanxiang-update-tools](https://github.com/rimeinn/rime-wanxiang-update-tools)
---

## 🎯 核心功能详解

### 1️⃣ Lua扩展功能

万象拼音提供丰富的Lua扩展功能，让输入更高效。

##### 日期时间快捷输入
<details>
<summary>🔧 日期时间快捷输入</summary>

**引导键**：`/` 或 `o`

| 编码 | 功能 | 说明 |
|-----|------|------|
| `/sj` 或 `osj` | 时间 | 显示当前时间 |
| `/rq` 或 `orq` | 日期 | 显示当前日期 |
| `/rc` 或 `orc` | 日期差 | `/rc26p`（加26天）、`/rc26-`（减26天） |
| `/nl` 或 `onl` | 农历 | 显示农历日期 |
| `/xq` 或 `oxq` | 星期 | 显示星期几 |
| `/ww` 或 `oww` | 周数 | 今年第几周 |
| `/jq` 或 `ojq` | 节气 | 显示节气信息 |
| `/dt` 或 `odt` | 日期+时间 | 显示完整日期时间 |
| `/tt` 或 `ott` | 时间戳 | Unix时间戳 |
| `/jr` 或 `ojr` | 节日 | 显示节日信息 |
| `/day` 或 `oday` | 问候模板 | 显示问候语 |

**N模式**：`N0101`（月日）或 `N20250315`（完整年月日）

<img src="https://storage.deepin.org/thread/202509260107542641_N20250102.jpg" height="80">
<img src="https://storage.deepin.org/thread/202509260108069991_N0102.jpg" height="80">

> 💡 支持自定义格式和顺序，详见方案配置 `wanxiang.schema.yaml` 
</details>

##### 计算器模式
<details>
<summary>🔧 计算器模式</summary>

**引导键**：`V`

输入示例：
- `V3+5` → `8` 和 `3+5=8`
- 支持 `+ - * / % ^`
- 支持 `sin(x)` `cos(x)` 等函数
- 详见 `super_calculator.lua`

![计算器示例](https://storage.deepin.org/thread/202509260127113759_计算器1.png)
</details>

#### 超级Tips提示
<details>
<summary>🔧 超级Tips提示</summary>

化学式：<img src="https://storage.deepin.org/thread/202509260128462735_tips化学式.jpg" height="80">符号：<img src="https://storage.deepin.org/thread/202509260128454675_tips符号.jpg" height="80">表情：<img src="https://storage.deepin.org/thread/202509260128457494_tips表情.jpg" height="80">

**上屏触发键**：逗号 `,`（默认）

支持类型：表情|化学式|翻译|符号|货币|车牌|偏旁部首

**快捷键**：
- `Ctrl+T` - 开关Tips
- `,` - 上屏Tips内容

⚠️ **注意**：仓输入法、超越输入法需交由rime处理，设置中关闭前端接管

- 文字和超级提示的映射关系  参考配置文件 `lua\tips\tips_show.txt`
- 如果默认的tips_show.txt 满足不了你，也可以建立自己的配置文件 `lua\tips\tips_user.txt`(格式和上面文件一致)

</details>

#### /引导模式
<details>
<summary>🔧 /引导模式</summary>

通过输入 /sx 快捷输入关于“数学”的特殊符号，具体能输入什么可以打开 wanxiang_symbols.yaml学习。以及前述提到的日期、时间等的引导都共用斜杠开头，可以理解为一种命令模式。其中/wx可以查询仓库连接和当前版本  

<img src="https://storage.deepin.org/thread/202509260126183029_符号数学.jpg" height="80">
<img src="https://storage.deepin.org/thread/202509260126173818_符号大于.jpg" height="80">
<img src="https://storage.deepin.org/thread/202509260126167252_符号圆点.jpg" height="80">
</details>

#### 辅助码提示（仅PRO）
<details>
<summary>🔧 辅助码提示（仅PRO）</summary>

![辅助码提示示例](https://storage.deepin.org/thread/202509260134283927_辅助码提示.jpg)
**快捷键**：
- `Ctrl+A` - 循环切换：辅助码提示 → 声调全拼提示 → 关闭注释
- `Ctrl+C` - 开启拆分辅助提示（优先级更高）

默认显示1个字的辅助码，可在方案文件中自定义长度。

</details>

#### 快速符号（快符）
<details>
<summary>🔧 快速符号（快符）</summary>

输入 `a/` 快速上屏"！"符号

可自定义26个字母的映射关系：
- `repeat` - 重复上一次上屏的内容
- 修改正则表达式可改变引导策略

配置位置：`quick_symbol_text` 段落
</details>

#### 输入码音调显示

<details>
<summary>🔧 输入码音调显示</summary>

**快捷键**：`Ctrl+S`

实时动态显示全拼并加音调（万象特色功能）

`Shift+Enter` - 上屏当前显示的编码字符串
</details>

#### 用户造词
<details>
<summary>🔧 用户按需造词 中文无感造词（仅PRO）</summary>

**用户按需造词**：``` `` ```

三种造词方式：
1. ``` `` ``` 起始的主动造词
2. 编码后双击 ``` `` ``` 的主动造词（后触发）
3. 次选造词 - 次选是词库组合成的，上屏即记录

**中文无感造词Lua(仅PRO)**
1. 关闭调频情况下，通过`逐步选字选词`的方式上屏将为你记录整段
2. 遵循用户词管理的逻辑
3. 直接上屏不造词

> 💡 PRO版讲究自主可控，避免异常词汇污染词库
</details>

#### 手动排序
<details>
<summary>🔧 手动排序</summary>

**快捷键**：
- `Ctrl+J` - 向左一步
- `Ctrl+K` - 向右一步
- `Ctrl+L`（零）- 移除排序信息
- `Ctrl+P` - 置顶选中候选

支持：
- 词典候选排序
- 动态Lua候选排序（日期/时间等格式）

数据存储：`lua/sequence.userdb`  排序后的数据可以同步 参考 排序信息同步
</details>

<details>
<summary>🔧 更多Lua功能</summary>

| 功能 | 触发方式 | 说明 |
|-----|---------|------|
| 输入统计 | `/rtj` `/ztj` `/ytj` `/ntj` `/tj` | 日/周/月/年/生涯统计 |
| 翻译模式 | `Ctrl+E` | opencc中英文互译 |
| 字符集过滤 | `Ctrl+G` | 小字集/大字集切换 |
| 输入模式切换 | `Ctrl+Q` | 中文/英文/混合编码切换 |
| 声调辅助回退 | 直接输入7890 | 在声调间快速切换 |
| 候选切割机 | `Ctrl+1~0` | 上屏首选前N个字 |
| Tab循环切换 | `Tab` | 循环切换音节 |
| Unicode | `U` + 编码 | `U62fc` → 拼 |
| 符号输入 | `/sx` `/yd` 等 | 特殊符号快捷输入 |
| 错音错字提示 | 自动触发 | `gei yu` → `jǐ yǔ`提示 |

![错音提示示例](https://storage.deepin.org/thread/202509260127525844_错音给予.jpg)
</details>

---

### 2️⃣ 辅助码系统

万象拼音支持多种辅助码，让你在拼音基础上快速定位目标字。

<details>
<summary>📖 直接辅助码（仅PRO）</summary>

**使用场景**：想要"镇"字显示在前面

输入 `vf`（镇）+ `j`（金字旁声母）→ 快速出现"镇"字

如果继续输入其他主体字的声母，可以进一步缩小范围。

![直接辅助码示例](https://storage.deepin.org/thread/202407041147131421_截图_选择区域_20240704121809.png)
</details>

<details>
<summary>📖 间接辅助码（仅PRO）</summary>
**使用场景**：避免辅助码干扰双拼词语

输入 `ni/re` - 通过 `/` 引导辅助码
- 不加 `/` 时，与普通双拼无异，如 `vsg` 可以输出"中国"
- 加 `/` 后，进入辅助码筛选模式

**聚拢功能**：输入 `nire/` 让系统侧重于单字匹配
</details>

<details>
<summary>📖 声调辅助筛选</summary>

**7890** 代表 **1234** 声（轻声归并到4声）

输入示例：
- `ni9` → 你（三声）
- `niRE` → 大写字母代表辅助码
- `niR9E` → 混合使用声调和辅助码

![声调辅助示例](https://storage.deepin.org/thread/202505120222182012_截图_选择区域_20250512101814.png)
</details>

<details>
<summary>📖 输入后反查筛选</summary>

**使用场景**：通过反查字库定位词组或单字

输入主要拼音后，通过 `` ` `` 引导进入反查状态：

- `lkuiuo`jd`` → 筛选包含"老"字底的词
- `lkuiuo`gt`` → 筛选包含"实"字的词
- 支持 `.*t.*b.*g.*` 的正则匹配逻辑

**注意**：词组匹配不支持笔画，单字支持两分、多分、笔画
</details>

---

### 3️⃣ 输入前反查

<details>
<summary>📖 拆字模式</summary>

**使用场景**：不认识的字用部件组合输入

示例：输入"震"字
- 输入 `yu` `if`（雨 辰）+ `` ` `` → 出现"震"字
- 同时给出辅助码提示：`y`（雨声母）+ `i`（辰声母）

![拆字模式示例](https://storage.deepin.org/thread/202409280324599355_截图_选择区域_20240928112256.png)
</details>

<details>
<summary>📖 笔画模式</summary>

使用 `hspnz` 代表横竖撇捺折五笔画

示例：
- 两分：`ni`re``、`ni`rfer``
- 多分：`mu`ckrida``
- 笔画：`ni`pspzhpd``
</details>

---

### 4️⃣ 混合编码

所有混合编码功能统一在 `wanxiang_mixedcode.schema.yaml` 方案中，无需引导，直接输入。

| 功能 | 输入示例 | 输出 |
|-----|---------|------|
| 中英混合 | `1000wclips` | 1000wclips |
| 混合编码 | `AD钙奶` | AD钙奶 |
| 技术词汇 | `PN结`、`Type-C` | PN结、Type-C |
| 纯英文 | `hello` | hello |
| 金额大写 | `R1234` | 一千二百三十四、壹仟贰佰叁拾肆元整 |
| Unicode | `U62fc` | 拼 |

![混合编码示例](https://storage.deepin.org/thread/202509260105536966_混合编码.jpg)

---
### 5️⃣ 其他亮点功能

**自动上屏：**  例如：三位、四位简码唯一时，自动上屏如`jjkw岌岌可危` `zmhu怎么回事` 。默认未开启，方案文件中`speller:`字段下取消注释这两句开启 `#  auto_select: true  #  auto_select_pattern: ^[a-z]+/|^[a-df-zA-DF-Z]\w{3}|^e\w{4}`

**数字后自动半角：** 当中文状态输入数字的时候后面立即输入,。将自动转换为数字分割符，例如科学记数法1000,000 小数点 3.1415,如果你加入冒号:还可以优雅的输入时间12:30，当然你还可以双击输入的符号恢复全角符号的输出。但若你完全没有场景使用该功能，则可以通过patch，将其修改为commit  
```punctuator/digit_separators: ",."  >  punctuator/digit_separators: commit```

**错音错字提示：**  例如：输入`gei yu给予`，获得`jǐ yǔ`提示，此功能与全拼、双拼类型无关全部支持；

<img src="https://storage.deepin.org/thread/202509260127525844_错音给予.jpg" height="80">      <img src="https://storage.deepin.org/thread/202509260127524705_错音崩溃.jpg" height="80">

## 🎓 进阶配置

**用户词删除：** 使用Ctrl+del是rime系统删除用户词,就可以将用户词标记为c<=0，这在rime系统中就表现为不使用，假性删除。

**输入模式切换Lua：** 使用Ctrl+q来进行中文候选词、英文候选词、混合候选词之间切换，默认为混合编码输入模式。  

### 1️⃣ Custom Patch 个性化

⚠️ **重要**：
- Custom文件生效位置：**用户目录根目录**（与schema同级）
- custom目录仅用于携带和更新不覆盖
- 根目录的 `wanxiang.custom.yaml` 才是你的配置文件

```yaml
# wanxiang.custom.yaml
patch:
  # 方案列表
  schema_list:
    - schema: wanxiang

  # 简繁切换
  switches/@0/reset: 1

  # Tips快捷键（comma/period等）
  key_binder/tips_key: comma

  # 自定义短语文件名称
  translator/translation_file: custom_phrase.txt

  # 关闭自动调频（仅PRO）
  # engine/translators/@7/enable_user_dict: false
```

> 💡 详细配置方法见方案文件 `custom/` 目录下的教程

### 2️⃣ 自定义短语

万象的自定义短语文件名称默认为 `custom_phrase.txt`，参考文件里的配置示例

### 3️⃣ 词库迁移同步

万象提供了多设备用户词同步功能，让你在不同设备间保持一致的输入体验。

#### 基础配置

<details>
<summary>📱 单设备用户词编辑</summary>

**适用场景**：只有一个设备，想手动编辑用户词

**操作步骤**：

1. 点击"同步用户数据"，生成 `用户目录/sync/设备名/wanxiang.userdb.txt`
2. 使用工具将词库转换为万象格式（声调+辅助码）
3. 编辑txt文件，保持格式一致
4. 重新点击同步，导入数据库

> 💡 **格式要求**：
> - `db_name` 必须与用户词典文件名一致
> - `user_id` = 设备文件夹名 = `installation_id` 字段必须保持一致

</details>

#### 用户词库迁移

<details>
<summary>⚙️ 同步配置详解</summary>

**前置知识**: 同步是将用户词按时序合并导入导出的本地操作。

**同步目录配置**

默认同步目录为 `用户目录/sync`，如需自定义，在 `installation.yaml` 中添加：

```yaml
# Linux/Mac/Android
sync_dir: "/home/amz/sync"

# Windows (双引号)
sync_dir: "D:\\home\\amz\\sync"

# Windows (单引号)
sync_dir: 'D:\home\amz\sync'
```

**设备ID配置**

修改 `installation_id` 为可辨识的设备名称(建议按系统命名):

```yaml
installation_id: "windows"  # 或 "linux"、"mac"、"ios" 等
```

根据 `installation_id` 创建设备文件夹:

```
用户目录/sync/windows
用户目录/sync/linux
用户目录/sync/ios
```

**同步文件说明**

点击"同步用户数据"后,系统将用户词库导出为txt文件:

| 数据库文件 | 同步文件名(标准版) | 同步文件名(PRO版) |
|-----------|------------------|-----------------|
| `wanxiang.userdb` | `wanxiang.userdb.txt` | - |
| `zc.userdb` | - | `zc.userdb.txt` |

txt文件表头格式:

```
# Rime user dictionary
#@/db_name	zc
#@/db_type	userdb
#@/rime_version	1.13.1
#@/tick	793
#@/user_id	ff9b2823-8733-44bb-a497-daf382b74ca5
```

**关键要求**:
- `db_name` 必须与用户词典文件名一致
- `user_id` = 设备文件夹名 = `installation_id` 三者必须保持一致

</details>

<details>
<summary>🔄 多设备词库同步流程</summary>

**步骤1：配置设备ID**

打开用户目录的 `installation.yaml` 文件，修改 `installation_id` 为设备名称：

```yaml
installation_id: "windows"  # 或 "linux"、"mac"、"ios" 等
```

**步骤2：创建设备清单**

在 `/sync` 目录中创建 `sequence_device_list.txt`：

```
sequence_windows.txt
sequence_linux.txt
sequence_ios.txt
```

**步骤3：同步合并逻辑**

重新部署后，系统会自动：

1. **导出**：将当前设备数据导出到 `sequence_设备id.txt`
2. **合并**：读取清单中的所有文件，按时序去重合并
3. **回写**：将合并结果回写到当前设备的sequence文件
4. **导入**：将合并后的数据导入数据库

**步骤4：云同步**

1. 通过云同步软件（如坚果云、Dropbox）同步 `/sync` 目录
2. 在其他设备上，更新 `sequence_device_list.txt` 添加对应设备文件
3. 重新部署，完成多端数据合并

</details>

<details>
<summary>📝 单设备编辑与模拟同步</summary>

**单设备用户词编辑**

如果只有一个设备,可以直接编辑用户词:

1. 点击"同步用户数据",生成 `用户目录/sync/设备名/wanxiang.userdb.txt`
2. 删除用户目录的 `userdb` (避免冲突)
3. 使用工具将词库转换为万象格式(声调+辅助码)
4. 编辑txt文件,确保格式与万象编码完全一致
5. 点击同步,导入数据库

**格式要求**:
- 编辑的txt文件必须经过预处理
- 必须保持万象编码格式(声调+辅助码)
- `db_name`、`user_id` 等字段必须符合规范

**模拟多设备同步**

如果想测试多设备同步逻辑:

1. 将编辑好的txt文件内的 `user_id` 修改为其他设备名(如 `linux`)
2. 将文件放入 `用户目录/sync/linux/` 目录
3. 点击同步,系统会将其与当前设备数据合并

> 💡 **提示**：此功能可用于数据迁移和备份，也是真正的多设备同步逻辑的模拟。

</details>

#### ⚠️ 重要注意事项

- **同步目录**：只同步 `/sync` 目录，**不要**将整个rime文件夹放入同步软件，会导致数据库锁定
- **文件格式**：编辑用户词txt时必须保持万象编码格式（声调+辅助码）
- **设备ID一致性**：确保 `installation_id`、设备文件夹名、`user_id` 三者完全一致
- **可靠性说明**：此流程模拟Rime同步方式，为多端数据合并过程，iPhone设备可能遇到更多问题

#### 排序信息同步

<details>
<summary>📊 手动排序数据同步</summary>

**功能说明**：万象的手动排序功能支持词典候选排序和动态Lua候选排序（如日期/时间格式），排序数据存储于 `lua/sequence.userdb`，可在多设备间同步。

**同步方式**：排序信息的同步流程与用户词同步**完全一致**，只需复用上述配置：

1. **复用设备ID配置**：`installation.yaml` 中的 `installation_id`（已配置）
2. **复用设备清单**：`sequence_device_list.txt`（已创建）
3. **自动合并同步**：重新部署时，排序数据会与用户词一同合并

**数据文件说明**：

| 数据类型 | 文件位置 | 同步文件名 |
|---------|---------|-----------|
| 用户词 | `wanxiang.userdb` | `wanxiang.userdb.txt` (标准版)<br>`zc.userdb.txt` (PRO版) |
| 排序信息 | `lua/sequence.userdb` | `sequence_设备id.txt` |

**快捷键回顾**：
- `Ctrl+J` - 向左一步
- `Ctrl+K` - 向右一步
- `Ctrl+L` - 移除排序信息
- `Ctrl+P` - 置顶选中候选

> 💡 **提示**：排序信息同步无需额外配置，完成用户词同步配置后自动生效。每次点击"同步用户数据"时，排序信息会与用户词一同导出/导入。

</details>

#### 相关工具

- [用于Linux Mac的词库刷拼音辅助码工具](https://github.com/amzxyz/RIME-LMDG/releases/download/tools/wanxiang-dicts-tools-linux-mac)

- [用于Windows的词库刷拼音辅助码工具](https://github.com/amzxyz/RIME-LMDG/releases/download/tools/wanxiang-tools.exe)

### 辅助码切换指令

所有指令格式：`/` + 代码

```
/flypy    → 小鹤双拼
/mspy     → 微软双拼
/zrm      → 自然码
/sogou    → 搜狗双拼
/znabc    → 智能ABC
/ziguang  → 紫光双拼
/pyjj     → 拼音加加
/gbpy     → 国标双拼
/lxsq     → 乱序17
/pinyin   → 全拼
/wxsp     → 万象双拼
/zrlong   → 自然龙（反查全拼）
/hxlong   → 汉心龙（反查全拼）
/jjf      → 间接辅助
/zjf      → 直接辅助
```

### 反查配置

在你的 `wanxiang.custom.yaml` 中配置：

```yaml
wanxiang_lookup:
  tags: [abc]              # 生效的tag
  key: "`"                 # 反查引导符
  lookup: [wanxiang_reverse]  # 反查数据库
  data_source: [comment, db]  # 数据源优先级
  # comment: 从词库注释(辅助码)提取
  # db: 从反查数据库提取
```

---

## 🌟 平台特殊说明

### iOS 仓输入法

1. 方案下载：仓设置 → 输入方案 → "+" → 万象拼音
2. 切换方案：长按 `/` + 方案代码（如 `/flypy`）
3. **关键步骤**：文件管理 → 拷贝键盘词库至应用
4. 重新部署

### iOS 元书输入法

1. 从 `RimeSharedSupport` 复制 `include_keyboard_rime_files.txt`
2. 修改文件底部新增：```^.*[.]custom.*$```
3. 重新部署

### Android

⚠️ **注意权限问题**：
- 小企鹅等前端数据位于 `data` 目录
- 需通过系统文件管理器迁移（不是MT文件管理）
- 或通过root修改权限保持一致

---

## 🔗 常见问题

<details>
<summary>❓ PRO版为什么默认关闭调频？</summary>

[为什么PRO版本默认关闭调频的说明](https://github.com/amzxyz/RIME-LMDG/wiki/%E4%B8%BA%E4%BB%80%E4%B9%88%E8%A6%81%E5%85%B3%E9%97%AD%E8%B0%83%E9%A2%91%E4%BB%A5%E5%8F%8A%E4%B8%8E%E4%B9%8B%E5%85%B3%E8%81%94%E7%9A%84%E6%8E%AA%E6%96%BD%E6%9C%89%E5%93%AA%E4%BA%9B)   

```enable_user_dict: false # 是否开启自动调频，true为开启```

</details>

<details>
<summary>❓ 如何更新词库和方案？</summary>

**推荐方式**：
1. **Plum用户**：重新运行安装命令即可自动更新
2. **工具用户**：使用wanxiang-tools内置更新器
3. **手动更新**：下载Release包，保留 `*.custom.yaml` 后覆盖

**白名单保护**：wanxiang-tools支持白名单，保护自定义文件不被覆盖
</details>

<details>
<summary>❓ 自定义词库如何添加？</summary>

**步骤**：
1. 使用工具将词库刷成万象格式（声调+辅助码）
2. 固定词库（推荐）：
   ```yaml
   patch:
     translator/packs/+:
       - userxx  # 你的词库名
   ```
3. 或重命名 `wanxiang.dict.yaml` 为 `wanxianguser.dict.yaml`

> 💡 [词库工具下载](https://github.com/amzxyz/RIME-LMDG/releases/tag/tools)
</details>

<details>
<summary>❓ 按键设置思考</summary>
**核心理念：打破习惯，重塑效率**

输入法的设计本质是“有舍有得”。很多新手习惯于大厂软件的逻辑，但那些习惯未必是最优解。在 RIME 中，如果不经过逻辑思考就盲目套用旧习惯，很难发挥其真正的威力。

**万象方案的按键逻辑：**
1.  **斜杠 `/` 的唯一性**：作为核心功能键，不支持挪作他用，请勿尝试修改。
2.  **高效上屏逻辑**：逗号与句号在无提示（Tips）时倾向于随语句直接上屏，减少确认按键；句号在有提示时亦可直接触发。
3.  **筛选区设计**：`-=` 键位用于翻页，与 `7890`（对应 1234 声调）共同构成高效筛选操作区，复刻经典 ABC 时代的高效逻辑。

> 💡 **建议**：万象的键位布局是经过逻辑推演的效率闭环。与其强行修改配置以适配旧习惯，不如尝试适应这套更科学的方案。

</details>

<details>
<summary>❓ 模型文件很大，影响性能吗？</summary>

**回答**：不会！

- 模型是固定的二进制数据，**不会增大**
- 只占用少量CPU算力，内存占用极少
- 不同于热加载数据，应视为优秀的算法模块
- 非常值得投入，大幅提升整句准确度
</details>

---

## 📚 相关资源

### 官方文档
- [🚀 新手安装配置指南](https://docs.qq.com/doc/DQ0FqSXBmYVpWVFpy?rtkey=)
- [词库问题收集反馈表](https://docs.qq.com/smartsheet/DWHZsdnZZaGh5bWJI?viewId=vUQPXH&tab=BB08J2)
- [RIME-LMDG 词库与语言模型仓库](https://github.com/amzxyz/RIME-LMDG)
- [思维导图快速配置查询](https://github.com/amzxyz/rime_wanxiang/blob/wanxiang/custom/%E4%B8%87%E8%B1%A1%E8%BE%93%E5%85%A5%E6%96%B9%E6%A1%88.png)

### 友情链接
- [Oh My Rime](https://www.mintimate.cc/zh/guide/installRime.html) - Rime基础入门
- [Rime参数配置](https://xishansnow.github.io/posts/41ac964d.html) - 详细配置说明

### 工具下载
- [Windows词库工具](https://github.com/amzxyz/RIME-LMDG/releases/download/tools/wanxiang-tools.exe)
- [Linux/Mac词库工具](https://github.com/amzxyz/RIME-LMDG/releases/download/tools/wanxiang-dicts-tools-linux-mac)
- [更新脚本](https://github.com/rimeinn/rime-wanxiang-update-tools)

### 自定义数据
在线获取（不随方案包提供）：
- `jm_flypy.txt` - 小鹤简码
- `jm_zrm.txt` - 自然码简码
- `tips_user.txt` - Tips翻译数据

---

## 🎁 万象特色总结

### 🏆 独家功能

1. **唯一支持整句拼音串上屏** - 词库全部带声调标注
2. **错位构词法** - 长期死磕权重最优解、分词片段最优解
3. **最全面的反查数据库** - 支持到U+，两分/多分/笔画
4. **有趣且实用** - 成对符号、Tips提示、手动排序、无感造词
5. **6种辅助码兼容** - 头部全拼编码，可转化为任何双拼
6. **精益求精** - 从里到外追求最优、最精

### 💡 核心理念

> **万象词库中的带声调拼音标注+词组构成+词频是整个万象项目的核心，是使用体验的基石。方案的其它功能皆可自定义，我希望使用者可以基于词库+转写的方式获得输入体验。**

---

## 💬 反馈与贡献

- **问题反馈**：[GitHub Issues](https://github.com/amzxyz/rime_wanxiang/issues)
- **深度讨论**：[Ask DeepWiki](https://deepwiki.com/amzxyz/rime_wanxiang)
- **词库反馈**：[在线表单](https://docs.qq.com/smartsheet/DWHZsdnZZaGh5bWJI?viewId=vUQPXH&tab=BB08J2)



## 🤝文档有问题和疑惑，欢迎指正
