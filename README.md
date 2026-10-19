# LabVIEW → MATLAB Skill

本目录提供 LabVIEW 转 MATLAB 的可复用处理方法，供 Codex 在读取真实 VI、分析依赖、生成或改写 MATLAB 驱动、进行离线验证时使用。

**只备份 Skill 时，上传本目录的全部内容即可。** 不需要上传上一级的 `converter/`、`test-sources/` 或其他备份文件。

## GitHub 仓库结构

将当前 `skills` 文件夹内的内容作为仓库根目录：

```text
你的仓库/
├── README.md
└── labview-to-matlab/
    ├── SKILL.md                 # 技能入口与核心规则
    ├── agents/
    │   └── openai.yaml          # Codex 展示信息
    └── references/
        ├── workflow.md         # 证据、解析、IR、生成与交付流程
        ├── semantics.md        # 接口、类型、数据流、SubVI 和通信语义
        ├── validation.md       # Python、MATLAB Fake 与硬件验证边界
        └── project-notes.md    # 既有项目经验与历史环境
```

请保留 `labview-to-matlab` 内部结构，确保 Skill 中的相对文档链接有效。

## 能做什么

- 根据真实 Block Diagram 核实接口、连线、嵌套结构、类型和 SubVI 调用。
- 优先复用既有解析器、IR 流程和 MATLAB 生成器。
- 区分真实 IR 自动生成与用户明确授权的工程化改写。
- 保留源命令、参数和终止符依据，不凭文件名或其他型号手册猜测行为。
- 指导离线 Fake 验证，并区分 Python 契约测试、实际 MATLAB 执行和真实仪器测试。
- 记录未知项、未实现功能、来源与转换限制，保留原 VI 和历史产物。

## 使用方法

下载仓库后，将整个 `labview-to-matlab` 文件夹复制到本机 Codex 的技能目录。Windows 默认位置通常为：

```text
%USERPROFILE%\.codex\skills\labview-to-matlab\SKILL.md
```

如使用了自定义技能目录，以本机配置为准。已有同名技能时先备份或合并；本说明不会自动执行安装或覆盖。

在能发现该技能的 Codex 会话中，可使用：

```text
使用 $labview-to-matlab 处理我提供的 LabVIEW 工程。
先检查实际接口和最小依赖闭包，优先复用已有生成器。
保留原始 VI，输出到新的独立目录，只进行离线验证，不连接仪器。
```

也可以明确要求只分析、只编写方案，或在授权范围内进行工程化改写。

## 依赖与适用边界

**这是方法型 Skill，不是独立可执行的转换器。** 仅安装 Skill 不会自动获得解析器、生成器、MATLAB 或完整测试工程。

| 任务 | 需要另外提供的工具或材料 |
|---|---|
| 只读分析、规划 | 原工程、实际 Block Diagram 或可核查的完整导出材料 |
| 真实 VI → IR → MATLAB 自动生成 | 兼容的 Python 环境、解析库、转换器源码、Schema 与真实源 VI |
| 实际 MATLAB 离线验证 | 可用的 MATLAB、生成文件及纯内存 Fake 验证材料 |
| 真实设备验证 | 另行准备适用的通信环境，并取得明确授权 |

本项目历史工具使用 Python 3.11.9、lvkit 0.8.7、pylabview 0.1.2、jsonschema 4.x，并曾使用 MATLAB R2023a。实际版本要求需结合当前转换器及目标环境确认；Skill 不会自行安装这些依赖。

`references/project-notes.md` 中的 Windows 路径和案例属于历史上下文，新电脑需要重新定位。历史通过记录不是本次运行结果，也不代表整个 LabVIEW 工程或仪器型号兼容性已验证。

默认离线，不创建真实 VISA 或网络会话。未实现部分需要明确报错，不以空函数或固定返回值代替实现。

## 备份范围

本目录只包含 Skill 与说明文档，不包含转换器源码、原始 VI、厂商手册、完整 IR、生成的 MATLAB 驱动或历史验证日志。恢复实际转换工作时，需要另外取得相应工程和工具。
