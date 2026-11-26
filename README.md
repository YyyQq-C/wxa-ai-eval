# 微信小程序 AI 接入与评测

给编码 Agent 用的技能：接入微信小程序 AI（agent / skills / 账号卡片 handoff），并按评测要求一次把「评测文件检测」和「服务交付」做对。

不绑定某一个小程序。路径、接口名按自己的业务替换。

## 文件

| 文件 | 作用 |
|------|------|
| [SKILL.md](SKILL.md) | Agent 技能入口：工作顺序、一次通过项、完成前自检 |
| [reference.md](reference.md) | 完整规范：评测维度、落地页、超时、Intent、问题对照表 |

## 当作 Cursor Skill 使用

把本仓库放到个人技能目录（目录名保持 `wxa-ai-eval`）：

```text
~/.cursor/skills/wxa-ai-eval/
├── SKILL.md
└── reference.md
```

Windows 示例：

```text
%USERPROFILE%\.cursor\skills\wxa-ai-eval\
```

之后在对话里说「接入微信小程序 AI」或「按评测要求改服务交付」，Agent 会读取 `SKILL.md`，并按其中要求先读 `reference.md`。

## 评测上必须守住的点

- 每个原子接口至少 2 条 Intent，覆盖率按 100% 准备。
- 约一半用例是多步或带条件。时间语义八类都要有（今天、偏移、模糊时段、节假日、完整日期、星期、时刻、组合）。
- 未注册场景条数按当次规则卡死（常见恰好 2 条：未登录产品能力 + 私有数据）。
- 负例要拒答并说明原因，不要假装成功。
- 成功的工具返回要带 handoff；列表、搜索、规划、文案落到能展示**本次结果**的页面，不要一律打开首页。
- 登录和网络请求必须有超时，避免工具挂满 180 秒。

细节与自检清单见 [reference.md](reference.md)。
