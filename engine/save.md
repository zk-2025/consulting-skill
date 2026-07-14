# 诊断存档模块

> **解决什么问题**：用户诊断到一半想保存进度，下次继续。或者想记录重要的诊断结论。
> **什么时候用**：用户说"保存""记下来""存档""这个结论留着"时。
> **联动文件**：`restore.md`（恢复存档）/ `report.md`（生成报告）/ `tool-adapter.md`（工具适配）

---

## 触发条件

当用户说以下话术时，触发保存：

- "保存" / "记下来" / "存档" / "这个结论留着" / "帮我记一下" / "先存着"

---

## 执行流程

### Step 1：确认保存

用户触发保存后，反馈：

> 确定要保存这次诊断吗？需要我帮你起个名字吗？
> - 如果不起名，我会用"诊断+时间"作为默认名字
> - 你也可以自己输入一个名字，比如"张总商业模式诊断"

### Step 2：收集当前诊断状态

获取当前诊断的所有信息：
- 如果在 Phase 1-3 → 保存问题消解过程（含追问进度）
- 如果在 Phase 4 → 保存诊断结论
- 如果在 Phase 5 → 保存行动方案

### Step 3：构建存档 JSON

```json
{
  "archiveName": "用户自定义的名字",
  "createdAt": "ISO格式时间戳",
  "userId": "用户标识（无登录态时用'local'）",
  "userProfile": {
    "identity": "企业老板/创业者/营销人员/管理者/学生/IP创作者",
    "industry": "行业",
    "stage": "刚起步/有客户/规模化/成熟期",
    "languageStyle": "直接数据驱动/共情务实/专业术语/结构化/教学式/接地气"
  },
  "phase": "Phase 2 / Phase 4 / Phase 5",
  "mode": "问诊/体检/快速扫描",
  "originalProblem": "用户最初说的一句话",
  "realProblem": "消解后确认的真问题（摘要，非完整追问记录）",
  "probingProgress": {
    "currentLayer": "已追问到第几层（0-5），未开始追问时为0",
    "lastTwoRounds": "最近2轮问答摘要，用于中途恢复追问上下文",
    "trapDetected": "识别到的语言陷阱类型（如有，如假需求/因果混淆/不愿尝试等）"
  },
  "routedModule": "strategy / business-model / operations等",
  "diagnosisConclusion": "模块诊断后的结论（摘要）",
  "actionPlan": [
    {
      "priority": 1,
      "action": "xxx",
      "reason": "xxx",
      "detail": "xxx"
    }
  ],
  "keySignals": "验证方式说明",
  "nextStep": "下一步建议"
}
```

> **字段说明**：
> - `userId`：可选字段。有登录态/用户标识时填实际ID；无登录态填 `"local"`。文件名中 userId 为 `local` 时省略前缀，避免出现 `local_xxx` 这种无意义命名。
> - `probingProgress`：**仅 Phase 1-3 中途保存时填充**，Phase 4 及以后此字段可为空。用于解决"真问题未确认时保存，恢复后无法还原追问上下文"的问题。
> - **摘要压缩原则**：存档只保存真问题+当前Phase+关键结论+追问进度摘要，不保存完整追问记录。恢复时从摘要继续，避免上下文窗口溢出。

### Step 4：写入文件

**参考 `engine/tool-adapter.md` 检测环境并选择写入方式。**

| 环境 | 操作 |
|------|------|
| 文件可用环境 | 调用 `write_to_file`/`write_file`/`write` 写入 `data/archives/{timestamp}_{name}.json`（userId 非 local 时加前缀：`{userId}_{timestamp}_{name}.json`） |
| 纯对话环境 | 输出 JSON 到对话，提示用户复制保存 |

### Step 5：确认保存成功

> 已保存。存档名："{name}"
> 存档位置：data/archives/{filename}.json
> 
> 下次想继续时，说"继续"或"恢复存档"
> 想生成报告时，说"出报告"

---

## 使用示例

```
用户：先保存一下吧，我下次继续
AI：好的，要帮你起个名字吗？比如"张总商业模式诊断"
用户：好的
AI：已保存。存档名："张总商业模式诊断 2024-01-01 10:00"
    存档位置：data/archives/20240101T100000_张总商业模式诊断.json
    下次说"继续"可以恢复
```

---

## 降级示例（纯对话环境）

```
用户：保存
AI：当前环境不支持文件写入。请复制以下存档数据保存到本地：

```json
{...存档JSON...}
```

    下次对话时粘贴这段数据即可恢复。
```
