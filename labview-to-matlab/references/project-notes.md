# 本项目经验与环境

这些是整理时的本地上下文，不是其他电脑必备路径，也不是本次重新验证的结果。

## 已记录环境

- 项目根目录：`D:\codex_ws\NI\labview-to-matlab`。
- 已确认 Python：`D:\codex_ws\NI\phase1_5\python_runtime\cpython-3.11.9\python.exe`。
- 源驱动目录：`D:\codex_ws\NI\rigol_dg1000_series`。
- Phase 9 报告记录 MATLAB：9.14.0.2206163，R2023a；当时可执行文件为 `D:\matlab\bin\matlab.exe`。
- 依赖声明：lvkit==0.8.7、pylabview==0.1.2、jsonschema>=4.18,<5。

不要把路径写死进新工程的处理逻辑；先定位用户当前工具和运行环境。

## 案例路线

1. Send Software Trigger：真实 IR 生成精确 `*TRG` 写入，核验 Connector Pane、错误 Cluster 与资源传递。历史 Phase 9 报告记录实际 MATLAB Fake 5/5；本次整理没有重跑。
2. Delay：用于积累等待能力；以实际 IR 为准，不按名称推断组成。
3. Write With Delay：围绕最小 SubVI 依赖闭包核验参数绑定、一次调用、写入和等待顺序。
4. Configure Trigger Delay：核验从参数到源命令字符串的格式化；不以新型号手册改写旧驱动命令。

后续三个案例的材料位于原工程 `phase9_output/second_rigol_vi`、`third_rigol_vi`、`fourth_rigol_vi`；整理过程仅确认目录存在，未重新审计其运行结论。复用时读取其中实际 IR、生成文件与报告，不能凭这里的简述宣布通过。

## 工程化交付

用户后来授权优先交付首版驱动，不再要求整个工程或每个 VI 先证明完整等价。原工程 `phase10_output/rigol_matlab_driver_v1` 保存该类交付及来源说明。此授权是那次任务的范围，其他任务仍按用户当前要求判断是否允许工程化改写。

原工程 `phase10_output/dsa800_manual_test` 是独立的 DSA800 手工测试入口，不应标成 RIGOL DG1000 VI 自动转换产物。用户已在其 DSA815 上手动获得身份字符串与 601 点频谱；这不证明 DG 系列兼容，也不等于全驱动验证。

## 容易重复踩的坑

- 根 `SKILL.md` 停留 Phase 2，README 停留 Phase 5；它们不能代表当前生成能力。新技能在本包，旧文件未改动。
- golden `ir_expected` 是摘要，不能替代完整 Project IR；`simple_add` 等文件名不能作为其真实语义证据。
- 子 VI 路径别名、连接器顺序、类型和调用端口绑定是独立证据问题，不能只凭一个 Call Site 记录判断都已解决。
- 物理 Connector Pane 槽位不连续是合法情况；保留原槽位并记录连续 MATLAB 参数位置。
- 历史 BLOCKED 是历史事实；后来范围获批改变时追加说明，不能抹除旧结论或伪填 execution_mode。
- 源哈希既不是支持节点的语义选择器，也不是行为证据。
- 生成器版本、支持范围及旧版候选限制可能变化，要读当前实现，不能把早期报告的特例限制当作最终能力。

## 恢复原工程证据

本备份只携带方法和选取的工具源码。完整 IR、Golden VI、原驱动、厂商资料、生成物、MATLAB Fake 与日志仍在原目录。恢复全量回归时按原布局取得这些材料，不在备份中制造替代 fixture。
