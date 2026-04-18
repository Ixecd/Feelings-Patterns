# Feelings-Patterns Handoff

> 写给下一个接手 Feelings-Patterns 工作的 Claude 实例（或人类协作者）
> 最近更新：2026-04-18
> 维护者：qc (Ixecd)

---

## 这个仓库是什么

Feelings 的**官方感受包库**。

```
Feelings 的感受包仓库分两层（见主仓库 docs/pattern-registry.md）

Feelings-Patterns（本仓库）    官方核心库
    严格审核，质量高
    保持哲学纯度
    带「Feelings Verified ✓」标识

Feelings-Store（未建）          社区生态库
    创作者自由上传
    创作者自选协议
    平台只强制最低门槛
```

---

## 当前状态（2026-04-18）

```
✅ 仓库已建立
✅ LICENSE 三件套已 commit
    - LICENSE           主说明
    - LICENSE-PATTERNS  CC BY-SA 4.0（感受包内容）
    - LICENSE-TOOLS     MIT（工具脚本）

❌ 尚未开始添加任何感受包
❌ 尚未建立目录结构
❌ 尚未有 validation / build 工具
❌ 尚未有 README.md（可选，qc 决定加不加）
```

---

## 许可证策略（重要）

本仓库**双协议**。不是复制粘贴 Feelings 主仓库的协议，是根据感受包的特殊性质专门设计的。

**两个协议的边界**

```
感受包内容（CC BY-SA 4.0）
    patterns/ 目录下的一切
    包括
        pattern.json / pattern.yaml（技术参数）
        description.md / narration.md（叙事文本）
        音频、视觉、触觉资源文件
        混音结构定义

为什么 copyleft
    感受包是创作内容
    衍生作品必须同样开源
    防止有人把开源感受包稍作修改闭源卖
    保证生态纯度

工具代码（MIT）
    scripts/validate/（验证感受包格式）
    scripts/build/（打包、签名）
    tools/（其他工具）
    tests/（测试）
    CI/CD 配置

为什么 MIT
    工具是基础设施
    最大化采用
    任何人可以用这些工具构建自己的感受包生态
```

**协议判断原则**

```
看文件位置
    patterns/           → CC BY-SA 4.0
    scripts/ tools/ tests/  → MIT

模糊情况
    感受包的 README？    → 如果是描述具体感受包 → CC BY-SA 4.0
                        → 如果是工具使用说明 → MIT
    感受包的 JSON schema？→ MIT（这是工具，不是内容）
    感受包的示例 JSON？  → 看放在哪个目录
```

---

## 感受包的完整结构（参考 `docs/pattern-registry.md`）

一个标准感受包应该包含：

```
patterns/
└── <pattern-id>/
    ├── pattern.yaml         元数据（ID、作者、版本、类型、安全参数）
    ├── description.md       感受描述
    ├── narration.md         AI 教练引导语
    ├── mixing.yaml          混音结构（主旋律+点缀+形状）
    ├── safety.yaml          安全边界（强度范围、禁用人群）
    ├── signals/             触发所需的生理信号模式
    └── resources/
        ├── audio/           音频文件
        ├── visual/          视觉素材
        └── haptic/          触觉反馈模式
```

**但这是未来的结构。当前没有任何实际的感受包。**

第一个实际感受包应该是在 Feelings-Server 能运行之后，作为端到端验证。

---

## 下一步（按优先级）

**紧迫程度低，等 Feelings-Server 有基础再做：**

```
1. 建立目录结构
   patterns/     感受包内容
   scripts/      工具脚本
   tests/        测试
   docs/         仓库自身的文档（可选）

2. 写最小的验证脚本
   scripts/validate.js（或 .go）
   检查 pattern.yaml 是否符合 schema
   检查 safety.yaml 的参数是否在允许范围

3. 设计第一个官方感受包
   建议从"平静"开始（最基础、最安全）
   完整走通创作流程
   作为其他感受包的模板

4. 建立 pattern schema（JSON Schema）
   定义合规感受包的结构
   为社区创作者提供标准
```

**短期内不需要做的：**

```
- 复杂的 CI/CD
- 自动签名系统
- 感受包市场功能（那是 Feelings-Store 的事）
- 多语言翻译系统
- 感受包评分系统
```

---

## 和主仓库的关系

```
Feelings（主仓库）
    定义什么是合规的感受包 → docs/pattern-registry.md
    定义审核标准 → docs/anti-abuse.md
    定义感受的分类体系 → docs/feeling-taxonomy.md
    定义感受的形状 → docs/feeling-shapes.md

Feelings-Patterns（本仓库）
    实现这些标准
    提供具体的感受包内容
    供 Feelings-Server 在运行时加载
```

**相关文档必读：**

1. `Feelings/docs/pattern-registry.md` — 仓库的整体设计
2. `Feelings/docs/feeling-taxonomy.md` — 感受分类体系
3. `Feelings/docs/feeling-shapes.md` — 感受的七种形状
4. `Feelings/docs/feeling-example-happiness.md` — 完整示例
5. `Feelings/GOVERNANCE.md` — 不可动摇的红线

---

## 质量门槛（qc 的标准）

官方感受包必须达到：

```
神经机制    有公开文献支撑，不是主观臆想
安全参数    经过至少 3 个独立用户的验证
跨用户数据  在不同基线的用户身上有一致的效果
完整文档    按标准结构完整填写
创作者签名  有可追溯的创作者（不允许匿名上架官方库）
```

达不到的感受包不进官方库，可以上 Feelings-Store（社区库）。

---

## 协作时的提醒

**不要创造感受**

```
不要自己生成"这是一个感受包"的内容
感受包的创作需要：
    真实的神经机制理解
    反复的用户测试
    安全参数的实验验证

AI 的角色是帮助整理和文档化，不是凭空创造感受
```

**严格引用 GOVERNANCE**

```
GOVERNANCE 里说的所有红线
    都对感受包直接适用
    特别是：
        未成年强度上限 20
        亲密感受维度的技术隔离
        原始神经数据不离设备
    任何违反的感受包提议，直接拒绝
```

---

## 一句话总结

**Feelings-Patterns 是 Feelings 的官方内容库。这里的每个感受包都要是真实的、可验证的、符合 GOVERNANCE 的。不急，等 Feelings-Server 能跑之后再开始填内容。**

---

*最后更新者：Claude（2026-04-18 实例）*
