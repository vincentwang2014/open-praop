> Kept as one file rather than split into `de-identification.md` /
> `evidence.md` / `confidence-and-promotion.md` (as the illustrative tree in
> §11 shows) — the sections cross-reference each other heavily (e.g. §9 and
> §10's anchor rule), and splitting them this early risks the copies
> drifting out of sync. Revisit the split once the document is stable
> enough that cross-references stop changing often.

# Open PRAOP v0.1-final — Minimum Viable Protocol

**Status:** v0.1-final
**Date:** 2026-09-04
**Purpose:** 建立一个开放、案例驱动、可证伪、可持续修正的 AI-native operational practice repository。

## Changelog from v0.1 draft

v0.1 draft (2026-09-03 discussion) was reviewed and converged to four required
fixes before being treated as final. All four are structural gaps, not
wording polish — three of them repair defects that already existed in this
project's own prior tiering system, not just gaps introduced by this draft.

1. **Confidence/Status split** (§9) — Pattern/Practice confidence was a
   single ladder that could only go up. Split into two independent axes so a
   claim can be `Operational + Contested` or `Canonical + Contested` without
   losing information.
2. **Anchor-or-demote hardened** (§10) — every promoted claim must name a
   concrete case anchor. Two loopholes closed explicitly: anchors must be
   `Accepted` cases (not `Submitted`/`Reviewing`), and "independent" means a
   different underlying incident, not a different write-up of the same one.
3. **Public-repo self-deidentification gate** (§7) — the de-identification
   protocol must be applied to Open PRAOP's own repository artifacts before
   public launch, not just to future case submissions. Recommended path is a
   clean new public repo, not flipping the internal repo public in place.
4. **Second-review gate for doctrine-changing decisions** (§13) — routine
   intake stays solo-maintainer; anything that changes PRAOP's own state
   (promotion, Contested↔Active, Deprecated, major reclassification)
   requires a second pair of eyes. Known limitation stated explicitly rather
   than solved: early-stage second-review capacity may be zero, in which
   case promotion stalls by design.

Scope for v0.1-final was deliberately held to these four items — no
committee, no automated scoring, no reviewer reputation, no certification.
Adding those now would repeat the exact failure shape (Control Accretion,
Case 004) these safeguards exist to catch.

**Post-convergence refinement pass (2026-09-04, still v0.1-final):** two
internal wording/logic gaps found on read-through, both closed without
adding new structure:

5. **Emerging threshold aligned across §9 and §10** — §9 defined `Emerging`
   as "multiple events or independent evidence," but §10 originally allowed
   promotion on a single `Accepted` anchor, which would have made the first
   real promotion a dispute about which section governs. §10 now requires
   1 anchor *plus* additional independent evidence or a second incident.
6. **"Original contributor as second reviewer" scope narrowed** — the
   original wording let a contributor's factual confirmation double as the
   second-review gate itself. Now explicit: it satisfies fact-checking only
   and never counts toward the promotion/status-change second-review
   requirement, closing a path to a single de-facto decision-maker being
   recorded as two-reviewer approval.

**Pre-launch validation (2026-09-04):** two internal pilot runs walked
existing cases through the full pipeline (raw → de-identification →
submission → evidence tag → Accepted → mapping → practice candidate) before
any public launch decision. Findings:

- Pilot 001 (Control Accretion case) confirmed the anchor-or-demote rule
  actually caps promotion — a detailed, compelling case stayed at
  `Observed/Active` because it had only one anchor, not because a reviewer
  chose caution.
- Pilot 002 (Lesson-Generalization Failure case, chosen for higher
  identity/secret density) confirmed identity and secrets can be fully
  removed while the causal chain survives intact, confirmed the evidence-
  level mechanism refuses to inflate E0 to E1 just because a write-up is
  detailed and well redacted, and — the most consequential finding — showed
  that de-identification has to be checked **repo-wide**, not file-by-file:
  sensitive terms recurring across an unrelated case's narrative body,
  outside the file actually being reviewed, would have shipped unnoticed
  under a per-file check.

No protocol changes resulted from either pilot. The repo-wide de-
identification finding shaped how this public repo's content was exported
(a repo-wide sweep at export time caught the protocol's own §7 worked
examples using real project identifiers as "before" text — fixed to use
placeholder examples instead), not the protocol text itself.

**Renhua (人话) formalized as an operating principle, tested by EDTCU
(2026-09-04, still v0.1-final).** §3's existing "Plain Language Required"
principle was renamed and elevated to **Renhua (人话)** — kept in Chinese
deliberately rather than fully translated, because the term carries an
attitude ("don't let terminology and fluent AI output stand in for real
understanding") that "Plain Language" alone doesn't fully capture. Three
layers: Renhua is the principle, a Plain-Language Version is the
practice, and the stress test is how it's checked — called **EDTCU**
(Even Donald Trump Can Understand), **Eddie-Q**, or **EQ**
interchangeably, three names for the same test (EQ here meaning the
test, not emotional intelligence). Comes with an explicit Evidence →
Interpretation →
Plain-language explanation (Renhua) → Human understanding →
Decision/ownership chain explaining *why* it matters (semantic
ownership, not writing style). It now also constrains content, not just
judgment: Pattern entries (§2.2), the Practice Template (§5), and the
Playbook Template (§6) each require a **Plain-Language Version（人话版）**
field. Not a new principle — it formalizes the Layer B (人话) convention
already used in the private origin project's own case notes, and extends
it to Patterns/Practices/Playbooks, which previously had no equivalent
requirement.

---

## 1. Open PRAOP 是什么

Open PRAOP 是一个开放的实践与案例库，用来研究：

> 人和 AI 在真实工作中怎样合作、怎样失败、怎样改进，以及哪些做法能够让下一次事故更便宜。

它不是：

* AI 模型排行榜；
* Prompt 技巧合集；
* AI 吐槽社区；
* 模型安全 benchmark；
* 一套声称已经完成的 AI governance standard；
* 任何单一厂商或模型的最佳实践手册。

Open PRAOP 主要研究的对象不是模型内部，而是：

* AI-assisted work；
* Agent workflow；
* human–AI coordination；
* verification；
* organizational memory；
* escalation；
* responsibility；
* reliability controls；
* operational learning。

一句话定位：

> **AI Security protects systems from attacks and unsafe model behavior. PRAOP focuses on protecting organizations from unreliable AI-assisted work.**

这只是边界说明，不意味着两者互斥。

---

# 2. Open PRAOP 的四类核心资产

Open PRAOP v0.1 只维护四类不断增长的知识资产，大致是一条链：

```text
Case → Pattern → Practice → Playbook
```

* **Case** — 一次具体发生的事。
* **Pattern** — 多个 Case 里反复出现、机制相似的失效（或成功）形状。
* **Practice** — 为了应对某个 Pattern，具体应该怎么做。
* **Playbook** — 把多个 Practice 组织成一套可执行流程。

人话：**Case 是一次事情，Pattern 是反复出现的套路，Practice 是具体怎么
做，Playbook 是一整套做法。**

这条链不是严格单向的产线——例如一个 Practice 也可能反过来促成新的 Case
被观察到——但从"发生了什么"到"该怎么系统化应对"，大方向是这四步。

**Principle 不是第五个平行资产。** 它是跨在这条链上方的一个小型基础层，
不持续大量增长：

```text
        Principles
      ↙     ↓     ↘
Case → Pattern → Practice → Playbook
```

Principle 可以从多个 Case、一个或多个 Pattern、甚至某个反复验证失败的
Practice 里提炼出来——但不是"每发现一个 Pattern 就再产一条 Principle"。
新增一条 Principle 的门槛明确高于新增一个 Pattern：

> 只有当它跨越多个事件/Pattern，并且会改变 Open PRAOP 通用工作方式本身
> 时，才值得成为 Principle。

人话：**Pattern 可以多，Principle 要少。**

Principle 的具体清单见 §3。它是小型、慢速增长的一层，不是 Case / Pattern
/ Practice / Playbook 那种持续累积的目录——这是刻意的，防止的正是 §18
"Doctrine Inflation" 警惕的那种膨胀，只是发生在 Principle 层而不是
Pattern 层。

## 2.1 Cases

回答：

> 真实发生了什么？

案例必须尽量基于真实事件，而不是假想故事。

---

## 2.2 Patterns

回答：

> 多个案例之间是否反复出现类似的 failure shape 或 success shape？

例如可能出现：

* Locked Inference Trajectory
* Provenance Drift
* Lesson Generalization Failure
* Control Accretion

Pattern 不是因为名字好听就成立。

必须从案例中长出来。

每条 Pattern 记录必须包含一个 **Plain-Language Version（人话版）**
（见 §3 Renhua / EDTCU Test）——用普通话回答"这到底是什么意思"，不能只有专业
定义。指不出人话版本的说法，和指不出 case anchor 的说法一样，不能算
已经被组织真正掌握。

---

## 2.3 Practices

回答：

> 面对已经有一定证据支持的问题，我们实际可以怎么做？

Practice 应该足够具体，可以被团队执行或测试。

---

## 2.4 Playbooks

回答：

> 一个团队或公司怎样把一组 Practices 组合成日常工作流？

例如未来可能有：

* Vibe Coding Starter Playbook
* AI Incident Review Playbook
* Agent Verification Playbook

v0.1 不追求大量 Playbook，只建立格式。

---

# 3. 基本方法

这是 Open PRAOP 的 **Principle 层**（见 §2 对 Principle 与四类资产关系
的说明）——小型、慢速增长，新增门槛明确高于 Pattern，不是持续累积的
目录。

Open PRAOP 遵守几个最小原则。

### Incident First

先记录发生了什么，再讨论理论。

人话：

> 先说发生了什么，道理以后再聊。

### Assert Incidents, Hedge Abstractions

已经观察到的事实可以明确说。

从案例抽象出的机制、规律和普遍性必须注明不确定性。

人话：

> 发生过的事可以说死；总结出来的规律别装成定律。

### Artifact > Memory

日志、输出、commit、截图、邮件、运行结果等实际 evidence，优先于人的记忆，也优先于 AI 对自己行为的解释。

人话：

> 能看日志、代码、commit，就别靠"我记得"。

### No Fit Is Valid

案例不需要强行落进 PRAOP 已有 taxonomy。

允许：

* Fit
* Partial Fit
* No Fit
* New Pattern Candidate
* Out of Scope

一个解释所有事情的 taxonomy 没有研究价值。

人话：

> 不是每个问题都非得塞进 PRAOP 已有的分类里。

### No New Axis Without Incidents

不要因为某一个案例难以归类，就急着扩展分类体系本身。

新增一个分类维度（新字段、新分类轴、新置信度维度等）之前，需要能指出
至少两个独立事件，证明现有维度确实表达不了；并且至少尝试过一次用现有
手段绕过，且失败了。两者都指不出来，就不加——先把这个压力记录成一条
观察，等下一个事件。

这是「No Fit Is Valid」的镜像：那一条挡住的是把事件硬塞进已有分类；这
一条挡住的是反过来，为了一个事件硬造一个新分类。

人话：

> 一个怪案例，不值得马上发明一个新分类。

### Knowledge Is Not Enforcement

写进 README、CLAUDE.md、prompt 或 handbook，不等于实践已经稳定执行。

Practice 和 Enforcement 必须区分。

人话：

> 知道这条规矩，不等于下次真的会照做。

### Renhua (人话)

> **Renhua (人话) — say it so the human who owns the consequence can
> actually understand it.**

这不只是要求文字浅显，而是在说：不要让术语、抽象概念和 AI 流畅的表达方式
盖住了真正的理解。英文里最接近的说法是 Plain Language，但"人话"多了一层
态度，这层态度值得原样保留，不完全翻译掉——Open PRAOP 本身是从真实工作中
长出来的，不必假装每个概念一开始就来自英语管理学词汇。

正式表述：

> **If the person responsible for the outcome cannot explain the issue in
> ordinary language, semantic ownership has not been established.**
>
> 如果负责这个结果的人没法用日常语言把问题讲清楚，semantic ownership 就
> 还没有真正建立。

人话：

> 说不明白，就别假装已经懂了。

这条原则解决的不是文风问题，而是 **semantic ownership** 问题：如果一个
组织里，AI 能流利地说出一整套术语，而真正对结果负责的人只能"嗯嗯，好像
懂了"，那这个组织已经失去了一部分对自己决策的语义所有权——即使流程上看
起来一切正常。

**理解分两层，只有第二层才真正算数：** 第一层——有人讲给你听（或者 AI
之间越聊越"高级"，术语来回飞），你点头"懂了"。这一层可以随时靠 AI 重新
讲一遍来补，供应无限，因此也最不可靠。第二层——过一阵，一个全新的、
没人提示的情况冒出来，你自己认出"这就是那个东西"，并且用它做了判断。
只有第二层是真落地，而且它长得最慢，只能靠真事一次次砸、自己一次次用，
慢慢长出来。

> Passing Renhua means a human can later recognize and apply the idea
> in a new situation without the AI prompting them — not that they
> nodded along when it was explained.

人话：

> 当场点头"懂了"不算数。算数的是：以后遇到一个新情况，没人提醒，你自己
> 认出这就是那个东西，并且用上了。

PRAOP 把 Renhua 拆成三层：

* **Renhua / 人话** — 原则本身。
* **Plain-language explanation** — 实践方式：见下方"谁必须有人话版"。
* **EDTCU / Eddie-Q / EQ** — 具体的 stress test，同一件事的三种叫法。

**谁必须有人话版：**

* **Principle**（本节 §3 各条原则）— 必须（Required）。
* **Pattern**（§2.2）— 必须（Required）。
* **Practice**（§5）— 必须（Required）。
* **Playbook**（§6）— 必须（Required）。
* **Accepted Case**（§9 Case Status）— 应该（Should），由 maintainer 在
  Accept 阶段补上（见 §13 Step 6），不是 contributor 的责任。
* **Raw case submission**（§4）— 不要求（Not required）。Contributor 的
  责任只是"报告事件"（见 §4）；人话版是 maintainer 把它处理成
  structured case 之后才补的东西，不能反过来变成提交门槛。

一条额外约束：

> **Plain-language version should explain the idea, not summarize the
> jargon.**

人话版是在把这件事解释清楚，不是把术语逐字换成更短的说法再抄一遍。读
起来像"翻译腔简化版"——只是把英文词换成对应的中文词——就还没有真正通过
EDTCU Test。

> **EDTCU is the stress test for Renhua.**
>
> EDTCU — Even Donald Trump Can Understand. Also informally called
> **Eddie-Q**, or simply **EQ**. All three refer to the same PRAOP
> plain-language test — use whichever reads best in context: EDTCU for
> the origin story, Eddie-Q for casual discussion, EQ for checklists
> and review comments (e.g. "EQ: Pass").
>
> A deliberately humorous plain-language test: if an important idea
> cannot be explained in ordinary, concrete language, we should not
> assume it is organizationally understood.

**关于这个名字：** EDTCU 借用一个知名度极高、说话风格极简直接的公众人物
作为记忆点，不代表任何政治立场，也不是在评价这个人本身——重点始终是
"能不能把话说到几乎所有人都听得懂"。**注意：这里的 EQ 指这个 plain-
language test，不是情商（emotional intelligence）。**

PRAOP 因此把"理解"拆成一条链：

```text
Evidence
    ↓
Interpretation
    ↓
Plain-language explanation (Renhua)
    ↓
Human understanding
    ↓
Decision / ownership
```

如果中间"Plain-language explanation"这一环断掉，后面的 human understanding
和 ownership 很可能只是名义上的——决策记录上写着"已批准"，但批准的这个人
其实没有真正掌握发生了什么。

一个实际用途：当多个 AI 系统就某个抽象说法互相认同（"两个模型都同意这是
一个 semantic authority topology 问题"），这本身不能当作 evidence 增加
（见 §18 "AI Consensus as Evidence"）。相反，这正是该停下来做 EDTCU Test
的信号——如果没有人能用三句话把这件事讲给真正对业务结果负责的人听懂，那
这本身就是一个 risk signal，而不是"已经达成共识"。

这条原则也不是新发明。私有源项目自己的 case notes 里，既有的 Layer B
（人话）restatement 惯例已经在实践它。这里只是把它从 case-level 的写作
惯例，提升为正式的 PRAOP operating principle，并要求 Pattern / Practice /
Playbook 同样遵守，不只是 case 才有。

---

# 4. Case Submission Protocol

Contributor 不需要先理解 PRAOP taxonomy。

Contributor 的责任是：

> **报告事件。**

Maintainer 的责任是：

> **解释和分类事件。**

这也包括人话版规则：raw submission **不要求** Plain-Language Version
（见 §3"谁必须有人话版"）——contributor 不需要写它。案例 Accept 之后，
maintainer 在处理成 structured case 时"应该"补上一个（见 §9 Accepted、
§13 Step 6）。

## Case Submission Template

### A. Basic Information

**Case title:**
给这个事件一个简单标题。

**Date / approximate period:**
可以使用模糊日期，例如 2026-08 或 "over several weeks"。

**Domain:**
例如 software engineering / mortgage / legal / customer service / writing / finance。

**AI system involved:**
可选。允许匿名或泛化。

---

### B. What Were You Trying to Do?

用几句话说明原始任务。

最好能回答：

> 如果一切正常，本来应该发生什么？

---

### C. What Actually Happened?

按时间顺序描述。

只写你实际观察到的行为。

尽量区分：

* observed fact；
* interpretation；
* later hypothesis。

---

### D. Why Did It Matter?

说明实际影响，例如：

* 时间；
* 金钱；
* 客户体验；
* 错误决策；
* 重复工作；
* compliance risk；
* operational disruption；
* trust loss。

---

### E. What Was Surprising?

什么行为与你原来的预期不一样？

这一项不是必须证明 AI "错了"，而是捕捉值得研究的行为差异。

---

### F. What Did You Try?

你采取了哪些纠正措施？

按实际顺序记录。

---

### G. What Happened Afterward?

结果属于哪一种：

* Resolved and verified
* Improved but not fully verified
* Failed
* Recurring
* Pending
* Unknown

**不能因为写了修复规则就自动写 Resolved。**

---

### H. Evidence

有哪些证据？

* log
* screenshot
* commit
* output
* email
* ticket
* conversation
* recording
* none

如证据不能公开，只需注明：

> Evidence retained privately.

---

### I. Your Interpretation — Optional

你认为这可能是什么类型的问题？

* Existing PRAOP pattern
* Maybe related
* New pattern
* No idea

Contributor 不负责最终分类。

---

### J. Anti-Mapping Question

> **为什么这个案例可能并不属于你认为的那个 PRAOP pattern？**

如果不知道，可以写：

> Unknown.

这一项用于降低 confirmation bias。

---

### K. What Would You Do Differently Next Time?

只写目前的 working recommendation。

不要求把它写成 universal principle。

---

# 5. Practice Template

Practice 必须可以追溯到案例或其他 evidence。

## Practice Title

一句话说明做什么。

### Plain-Language Version（人话版）

用日常语言，一两句话说清楚这条 Practice 到底在说什么——不能只有专业
表述。如果说不清楚，说明 EDTCU Test（§3）还没通过，先把这句话
写清楚，再往下填。

### Problem Addressed

这个 Practice 试图减少什么 failure shape？

### When to Use

什么环境或任务下适用？

### What to Do

必须是可执行行为。

### What Not to Do

说明常见误用。

### Evidence

列出支持该 Practice 的案例。

例如：

* Case 014
* Case 022
* External Case 008

### Known Limitations

什么情况下它可能不起作用？

### Enforcement Level

选择一个：

**Guidance**
主要依赖人或 Agent 自觉执行。

**Process**
已经进入明确 workflow。

**Mechanical Enforcement**
工具、preflight、gate 或自动检查会阻止明显违规。

### Confidence

见 §9 — Confidence 与 Status 分开记录，例如 `Operational / Active` 或
`Emerging / Contested`。

新 Practice 默认不能直接进入 `Canonical`。

---

# 6. Playbook Template

Playbook 是多条 Practice 组合后的工作流程。

## Playbook Name

例如：

> Vibe Coding Team Starter Playbook

### Plain-Language Version（人话版）

一两句话，用日常语言说清楚这个 Playbook 是让团队做什么。同样受 §3
EDTCU Test 约束。

### Who Is This For?

说明典型用户。

### Problem

这个团队目前遇到什么 operational problem？

### Entry Conditions

什么时候应该使用这个 Playbook？

### Workflow

尽量压缩成少数几个阶段。

例如：

1. Preflight
2. Execute
3. Verify
4. Escalate if needed
5. Capture incident

### Human Ownership

明确哪些结果最终必须由人负责。

### Automation / Enforcement

哪些步骤可以机械检查？

### Evidence

链接到支撑各步骤的案例与 Practices。

### Known Failure Modes

这个 Playbook 自己可能制造什么问题？

例如：

* excessive control；
* review bottleneck；
* false confidence。

---

# 7. De-identification Protocol

核心原则：

> **Redact identity, preserve causality.**
> 脱掉身份，保留因果。

Open PRAOP 不要求 contributor 公开完整原始材料。

建议保留两个版本：

### Raw / Private Version

可以包含完整事件细节。

默认不进入公开 repo。

### Public / Redacted Version

只保留理解 failure shape 所需要的信息。

---

## 必须移除或替换的信息

包括但不限于：

* 人名；
* email；
* phone number；
* API key；
* password；
* auth token；
* account number；
* loan number；
* customer identifier；
* private repository URL；
* private IP；
* internal endpoint；
* 未授权公开的客户名称；
* 未授权公开的公司内部信息。

Secrets 不得以 hash 形式代替后公开。

直接删除。

---

## 推荐泛化的信息

例如（占位示例，非真实项目名）：

`<person's first name>`
→ `Operator`

`<internal product codename>`
→ `<generic description of what it is, e.g. "the lending product">`

`<specific credential/env-var name>`
→ `<generic description, e.g. "repository authentication credential">`

`<specific cloud provider or host name>`
→ `<generic description, e.g. "cloud GPU environment">`

`repo-name`
→ `private repository`

**注意：** 这一节的示例本身也要经过 §7 末尾 "Public Launch Gate" 的检查——
如果示例直接使用了真实项目的真实标识符，那这份写着"如何脱敏"的文档，本身
就会把那个标识符发布出去。示例必须用占位符或虚构名称，不能用真实项目的
真实值，即使目的只是演示脱敏映射关系。

精确金额如果不是 failure mechanism 的必要组成：

`$73,482`
→ `$50k–$100k`

---

## Combination Risk Check

即使单项信息已经匿名，也必须问：

> 如果一个熟悉这个公司或行业的人看到剩余细节，能不能重新猜出这个人或组织是谁？

如答案可能是 Yes，继续泛化。

---

## 必须尽量保留的信息

脱敏不能破坏：

* 原始任务；
* 时间顺序；
* AI/system behavior；
* cause/effect relationship；
* impact；
* correction；
* outcome。

---

## Public Launch Gate: Repository Self-Deidentification Pass

这条规则的存在本身就是一个 PRAOP 教训：Open PRAOP 的脱敏 protocol 写出来的
那一刻，它还没有被应用到 Open PRAOP 自己身上——这正是 §3 "Knowledge Is Not
Enforcement" 的一个活案例。

在任何 Open PRAOP 内容公开发布之前，必须先对**仓库本身**跑一次完整的
self-deidentification pass，而不是只对新提交的 case 做检查。

**检查范围必须覆盖：**

* README 与所有说明文档；
* 已收录的 case files；
* 示例（examples）；
* 截图；
* 示例日志（sample logs）；
* issue / PR templates；
* **git commit history**——单独删除文件里的一行文字不会清除 `git log -p`
  里的历史记录，这是最容易被漏掉的一项；
* 任何会被引用或对外链接的 Claude Code session / conversation
  transcript——如果一段对话记录会被公开引用，它和 README 一样要过同一个
  脱敏检查，而不是被默认为"内部讨论所以安全"。

核心不是"把文件改干净"，而是**整条公开证据链**都不能反向暴露身份——单个文件
过关不代表组合起来仍然安全（见上文 Combination Risk Check）。

**推荐做法：**

不建议把现有内部 repo 直接一键公开。更安全的路径是：

> 新建一个 clean public repo，只迁移经过 review 的 public-safe 内容。

Private origin repo（保留完整历史与细节）与 Public Open PRAOP repo（只包含
已通过脱敏 pass 的内容）应当是两个独立仓库，而不是同一个仓库切换可见性。

---

# 8. Evidence Levels

v0.1 不设计复杂评分。

只分四级。

## E0 — Self-Reported

只有 contributor 的描述。

仍然可以收录，但必须标记。

## E1 — Supporting Artifact

至少存在一个支持关键事件的 artifact。

例如 log、commit、output、screenshot。

## E2 — Reconstructable

第三方可以根据 artifacts 大致重建事件轨迹。

## E3 — Independently Verified

关键事实已经被另一个 reviewer、system 或 independent reproduction 核验。

注意：

> Evidence level 不是 importance level。

一个非常重要的 case 仍可能只有 E0。

---

# 9. Confidence / Status / Promotion

Case 和 Pattern/Practice 不应使用完全相同的晋升逻辑。

## Case Status

### Submitted

刚收到。

### Reviewing

正在检查事实、脱敏和 evidence。

### Accepted

事件本身足够清楚，可以进入案例库。

进入这个状态后，应该（不是必须，但推荐）补上一个 Plain-Language
Version（人话版），由 maintainer 在处理时写，不需要 contributor
提供（见 §3"谁必须有人话版"、§13 Step 6）。

### Disputed

关键事实存在重大争议。

### Withdrawn

贡献者或 maintainer 决定撤回。

---

## Pattern / Practice: Confidence × Status (two independent axes)

v0.1 draft 曾经把 Pattern/Practice 的确定性写成一条单向阶梯
（Observed → Emerging → Operational → Canonical），并把 Contested /
Deprecated 也塞进同一条阶梯里。这隐含了"只会越来越确定"，和 PRAOP 自己的
falsification 精神冲突，也没法表达"以前很稳，但现在出现了反例"这种真实状态。

v0.1-final 把它拆成两条独立的轴。**Confidence** 回答"证据积累到什么程度"，
**Status** 回答"这个说法现在是不是还站得住"。两者正交，可以任意组合。

### Confidence axis

#### Observed

某个现象已经在至少一个案例中明确观察到。

只描述现象，不主张普遍性。

#### Emerging

多个事件或独立证据开始支持同一个解释。

仍然允许竞争性解释。

（晋升到 Emerging 的具体 anchor 门槛见 §10 Anchor-or-Demote：至少 1 个
`Accepted` case anchor，**加上**额外独立证据或第二个底层 incident——不是
单靠 1 个 Accepted case 就自动满足，两节定义在这一点上是对齐的。）

#### Operational

已经有足够重复证据，而且相关 Practice 在真实工作中表现出实际价值。

#### Canonical

长期、多来源、跨环境 evidence 支持，并且经过主动 falsification 后仍然成立。

**Canonical 应该非常难获得。**

### Status axis

#### Active

当前判断仍然有效，可以照常使用/引用。

#### Contested

出现了新的反例或重大争议，尚未裁定。

**Contested 不是删除**，也不要求先把 Confidence 降级——一个claim 可以是
`Operational + Contested`，甚至 `Canonical + Contested`：意思是"过去有较强
证据支持，也曾经实际使用，但现在出现了新的反例或重大争议"。"以前很稳"不等
于"现在不能被推翻"。

#### Deprecated

不再建议继续使用，但历史记录保留，不删除。

例如 `Operational + Deprecated`：曾经证据充分并实际使用过，后来被更好的
理解取代或被证伪，但作为研究材料仍然保留。

### 记录格式

Pattern / Practice 的确定性写作 `Confidence / Status`，例如：

* `Emerging / Active`
* `Operational / Contested`
* `Canonical / Contested`
* `Operational / Deprecated`

不写 Status 时默认视为 `Active`。

---

# 10. Promotion Rules

## Anchor-or-Demote（硬规则，不是判断题）

> **Every promoted PRAOP claim must name at least one concrete case anchor.
> If the anchor cannot be named, demote the claim.**
>
> 凡是要晋升 Confidence 的 Pattern / Practice，都必须能指出至少一个具体
> case anchor。指不出来，就降级——不靠表述漂亮维持级别。

这条规则从 v0.1 draft 里写得太软（只是 promotion 时"最好考虑"的一项）改为
硬性前置条件，因为它是防止 doctrine inflation（一个说法因为被反复重写而
看起来像已经被证明）的核心机制，不能靠自觉执行。

**Per-tier anchor requirements：**

* **Observed** — 至少 1 个具体 incident（对应的 case 本身即可，尚不要求
  用来支撑任何晋升）。
* **Emerging** — 至少 1 个 `Accepted` case anchor，**加上**额外的独立
  supporting evidence，或第二个独立的底层 incident。单靠 1 个 Accepted
  case 不足以晋升到 Emerging——这条是为了和 §9 的 Emerging 定义（"多个事件
  或独立证据开始支持同一个解释"）对齐，避免"1 个 Accepted case 到底能不能
  升 Emerging"成为第一场 promotion dispute。
* **Operational** — 至少 2 个**独立** `Accepted` case anchor，且已在真实
  工作中被实际使用过。
* **Canonical** — 多个独立环境下的 case anchor，并且在主动尝试
  falsification 之后仍然成立。

**两条必须现在就写死的 loophole 防护**（不是治理复杂化，是防止第一轮
promotion 就钻规则空子）：

1. **Anchor 必须是 `Accepted` 状态的 case。** `Submitted` 或 `Reviewing`
   状态的 case 不能用作 promotion 的依据——事实和脱敏还没审完，不能拿来
   支撑一个已经晋升的结论。
2. **"Independent" 指不同的底层 incident，不是同一事故的不同写法。**
   同一次事件写成两篇不同角度的 case、或者同一个 contributor 换个说法
   重新提交，都不能算作两个独立 anchor 来凑齐 Operational 的门槛。

指不出具体事件、只有抽象描述的说法，无论写得多有说服力，都不能进入
Pattern / Practice 正式条目，只能停留在 Discussion。

## 其他 Promotion 检查项（判断题，非硬性数字门槛）

v0.1 不设机械数字门槛，例如"不够 5 个 case 就不能升级"。除 anchor-or-demote
外，promotion 至少还要回答：

1. Supporting cases 是多少？
2. 是否来自独立环境？
3. 是否存在明显 selection bias？
4. 有没有 No Fit case？
5. 有没有 competing explanation？
6. 是否有 artifact support？
7. Practice 是否实际运行过？
8. 有没有失败过？
9. 结论能不能用人话解释？
10. 这次 promotion 是因为 evidence 增长，还是因为 wording 越写越漂亮？

最后一个问题尤其重要。

---

# 11. Repository Minimum Structure

v0.1 保持极简：

```text
open-praop/
│
├── README.md
├── CONTRIBUTING.md
├── LICENSE
│
├── cases/
│   ├── README.md
│   ├── TEMPLATE.md
│   └── accepted/
│
├── patterns/
│   └── README.md
│
├── practices/
│   ├── README.md
│   └── TEMPLATE.md
│
├── playbooks/
│   ├── README.md
│   └── TEMPLATE.md
│
├── protocol/
│   ├── de-identification.md
│   ├── evidence.md
│   └── confidence-and-promotion.md
│
└── discussions/
    └── README.md
```

v0.1 暂时不要建立：

* database；
* web app；
* contributor score；
* certification；
* automated taxonomy engine；
* complicated governance hierarchy；
* large ontology；
* dozens of issue labels；
* 公开的 `drafts/` 或 `case-drafts/` 目录。Private working draft（例如
  `praop-case-draft` 这类工具的输出）不应该出现在这个 repo 里，无论审核
  没审核。这个 repo 只应该看到两类 case 内容：已经完成 de-identification
  和 combination-risk check、正在等待 review 的 submission（PR 本身就是
  这个 review surface），以及已经 `Accepted` 进入 `cases/accepted/` 的
  case。没有中间的"公开草稿区"。

先观察真实使用。

---

# 12. Contributor Workflow

Contributor 的正常路径：

```text
Read short contribution guide
        ↓
Choose:
Case / Practice / Playbook
        ↓
Fill template
        ↓
Perform de-identification check
        ↓
Submit PR or Issue
        ↓
Maintainer review
```

**这个顺序不能反过来。** De-identification 发生在 PR 存在之前，不是在
PR 的 review 过程里才做。GitHub PR（连同它的评论历史）一旦打开就是公开
的——之后 close 或 reject 都不会让它变回不公开。不要为了"先拿到反馈"就
把还没通过 de-identification 和 combination-risk check 的草稿开成 PR；
先在私有草稿上做完这一步，再把已经脱敏的内容放进 PR。

最重要：

> Contributor 不需要正确使用 PRAOP jargon。

"我不知道这叫什么，但事情是这样发生的。"

完全是有效提交。

---

# 13. Maintainer Review Workflow

Maintainer review 只做六件事，外加一道横切的 second-review gate。

## Step 1 — Is This Real Enough to Review?

判断：

* firsthand？
* sourced external case？
* hypothetical？

Hypothetical content 不进入 Case Canon。

---

## Step 2 — Privacy / De-identification

这是安全网检查，不是 de-identification 本应该发生的地方——那应该在
contributor 打开 PR **之前**就做完（见 §12）。这一步是确认它确实做到
位了，而不是替代它。

检查是否仍存在：

* PII；
* secrets；
* proprietary details；
* re-identification risk。

不安全则退回修改。**但 PR 已经公开过这件事本身不会撤销**——如果这一步
发现的问题足够严重（真实姓名、凭证、可定位到具体个人或客户的细节），
除了退回修改，还要考虑是否需要请 contributor 删除该 PR 并联系 GitHub
支持处理已经公开过的内容，而不是只当作"改好再提交"处理。

---

## Step 3 — Separate Fact From Interpretation

例如：

**Fact**

> Agent attempted the same fix eight times.

**Interpretation**

> The agent was locked into an inference trajectory.

两者不能混为一句话。

---

## Step 4 — Evidence Tag

分配：

E0 / E1 / E2 / E3

不要因为案例符合 PRAOP 理论而提高 evidence level。

---

## Step 5 — Mapping

Maintainer 可以标：

* Fits existing pattern
* Partial fit
* No fit
* New pattern candidate
* Out of scope

必须写一句：

> Why might this mapping be wrong?

---

## Step 6 — Accept Without Over-Promoting

Case 可以 Accepted。

但 Pattern 不需要同步晋升。

也就是说：

> Accepting evidence ≠ accepting theory.

Accept 的同时，maintainer 应该补一个 Plain-Language Version（人话
版）——一两句话讲清楚"这件事到底是什么"，不是重新证明它，也不是把
分类套用上去。这是 Accepted Case 唯一需要 maintainer 主动补的
字段（见 §3"谁必须有人话版"）。

---

## Step 6.5 — PRAOP Case Admission: the ACCEPT decision must be an artifact, not a conversation

这条规则解决一个具体缺口：一个 submission 已经脱敏、已经开了 PR、
maintainer 也确实读完了——但"maintainer 说了一句 OK"本身不是可审计的
记录，它只存在于聊天记录里。Artifact > Memory 这条原则不应该在
promotion 这一步失效。

> **Human maintainer records ACCEPT in the submission artifact; only
> then may an agent promote that submission into the Accepted Case
> corpus.**

人话：

> 你拍板，文件留痕，AI 搬进去。

### 状态机

```text
Draft → Submission → Reviewing → Accepted / Rejected / Revise
```

* **Draft** — 私有草稿，尚未脱敏，不进入公开 review。
* **Submission** — 已完成脱敏和 combination-risk check，允许公开 review。
* **Reviewing** — PR 已经打开，正在被讨论。
* **Accepted** — maintainer 明确批准，进入正式 corpus。
* **Rejected** — 不进入 corpus。
* **Revise** — 退回 Submission 阶段修改。

### Maintainer Review 区块（模板）

每个 submission 文件的末尾附一个这样的区块，只有 maintainer 能改：

```markdown
## Maintainer Review

- [ ] Incident is concrete
- [ ] De-identification is sufficient
- [ ] Combination-risk checked
- [ ] Evidence level is honest
- [ ] Interpretation is separated from observation
- [ ] Anti-mapping is credible
- [ ] No duplicate underlying incident is being counted as independent

**Decision:** [ pending ]
Reviewed by:
Review date:
```

只有当 **Decision** 这一行明确写着 **ACCEPT** 时，agent 才被允许把这份
submission 提升为正式 Case：分配 Case ID、移动到 `cases/accepted/`、
把 Status 改成 Accepted、保留原 submission 的 provenance、commit。
在那之前，无论对话里说了多少次"这个可以了"，agent 都不得自行提升。

### Case Acceptance 和 Pattern Promotion 必须分开

Accept 一个 Case，只代表这个 Case 本身进入了 corpus——**不代表**它
所对应的 Pattern 自动升级：

```text
Case accepted
      ↓
Pattern 获得一个有效 anchor
      ↓
Pattern 的晋升资格被重新计算
      ↓
是否真的晋升，是另一次单独的决定
```

原因是同一个 underlying incident 可能同时说明好几个 Pattern（本
protocol 多处已经强调：一个 incident 可以支撑好几种机制解读，但不能
被偷偷算成好几个独立 anchor）。所以 agent 在 Case 被 Accept 之后，
只能说：

> Transformation Boundaries 现在有 1 个 Accepted anchor，够格重新评估
> Observed 状态了。

不能自己说：

> Pattern 已晋升。

那是一次独立的、需要单独触发的 promotion 决定，遵守 §10 的
Anchor-or-Demote 规则，不会因为某个 Case 被 accept 就自动发生。

---

## Step 7 — Second-Review Gate for Doctrine-Changing Decisions

如果一个 maintainer 单人决定 privacy、evidence、mapping、promotion、
contested、canonical 的每一步，Open PRAOP 很容易变成"某个人的个人
ontology"——这本身就是一种被相对化了的 Control Accretion（治理层面而非
工具层面）。v0.1-final 用最小的方式堵住这个风险，而不是引入委员会制度。

**单人可以完成（intake）：**

* Case `Submitted` → `Reviewing`；
* 基础脱敏检查（Step 2）；
* E0/E1 初步 evidence 标记；
* typo / formatting；
* 明显 out-of-scope 的判定。

**需要第二双眼睛（doctrine-changing）：**

* Pattern promotion（任何 Confidence 提升）；
* Practice → `Operational` 或 `Canonical`；
* `Contested` ↔ `Active` 之间的切换；
* 标记为 `Deprecated`；
* 重大 reclassification（例如推翻已有的 mapping 结论）。

第二 reviewer 不要求必须是 PRAOP core maintainer，可以是：

* another maintainer；
* domain reviewer；
* original contributor（仅对事实部分确认）。

> **The original contributor may serve as a second reviewer for factual
> accuracy only; this does not satisfy the second-review requirement for
> pattern/practice promotion, status changes, or major reclassification.**
>
> 原 contributor 对事实的确认，只能算完成了"事实核对"，**不能**计作
> doctrine-changing 决定（promotion / status change / major
> reclassification）所需的那道 second-review。否则会出现"maintainer 提出
> promotion，contributor 确认事情确实这样发生过"就被记录成 two-reviewer
> approval 的情况——实际上判断 promotion 是否成立的仍然只有一个人。这道
> second-review 必须由另一个能对 promotion 判断本身负责的人完成，而不是
> 对事件事实负责的人。

**Known limitation（现在就写明，不发明 fallback 机制）：**

> Early-stage second-review capacity may be zero. In that case promotion
> stalls by design.
>
> 早期项目可能只有一个 maintainer，此时 doctrine-changing 的决定会因为
> 缺少第二 reviewer 而停滞——这是设计上的结果，不是需要被绕过的 bug。停滞
> 应该读作"容量不足，按规则等待"，而不是被解释为神秘的流程卡死。

---

# 14. Practice Review

社区提交 Best Practice 时，maintainer 应额外检查：

### Is it actually actionable?

"Improve governance" 不算 Practice。

"Every production deployment must have an independent endpoint verification"
才算。

### Is it evidence-linked?

如果没有 evidence：

可以进入 Discussion。

不直接进入正式 Practices。

### Does it add friction?

必须记录 cost。

因为 reliability control 自己也可能制造新的 operational risk。

### Can it be enforced?

如果只能靠"记住去做"，必须明确标为 Guidance，而不是假装这是强控制。

---

# 15. Success Cases

Open PRAOP 不只接受失败案例。

允许专门提交：

> Something worked unusually well.

Template 基本相同，但问题变成：

* 原本什么风险存在？
* 采取了什么做法？
* 哪个行为发生了变化？
* 有什么 evidence？
* 有没有 alternative explanation？
* 是否复现过？

目的：

> PRAOP 不应该成为 AI Failure Museum。

我们研究的是怎样更好地与 AI 工作。

---

# 16. External Cases

来自 Reddit、blog、paper、news 等的案例可以进入 Open PRAOP，但必须与 firsthand case 区分。

必须记录：

* original source；
* publication date；
* direct artifact / quotation availability；
* whether facts can be independently verified。

AI 对网页内容的总结本身不是 provenance。

---

# 17. Minimal Governance

v0.1 只需要：

### Maintainers

负责：

* privacy；
* evidence classification；
* acceptance；
* mapping；
* promotion proposals。

doctrine-changing 的决定受 §13 Step 7 的 second-review gate 约束——不是
每个 maintainer 都能单独完成 promotion / contested / deprecated 的裁定。

### Contributors

提交案例和实践。

### Discussion

任何人都可以挑战：

* classification；
* pattern；
* practice；
* promotion。

不需要建立正式委员会。

---

# 18. What Open PRAOP Must Avoid

这些安全阀不是"我们担心以后可能发生"的抽象风险列表——它们存在，是因为
Open PRAOP 所依托的这个项目已经真实经历过其中一些失败形态。规则应该能
指向具体事件，而不是停在"我们觉得这是 best practice"。

### Taxonomy Capture

为了让新案例符合已有分类而扭曲事实。

### Doctrine Inflation

一个漂亮说法因为反复被 AI 重写，就逐渐看起来像已经被证明。

→ 这正是 §10 Anchor-or-Demote 存在的直接原因：没有具体 case anchor 的
说法，无论表述多精炼，都不能晋升。

### Control Accretion

为了保证 repo "严谨"，不断增加 contributor friction，最后没人愿意提交。

→ **锚定于 Case 004：The Rerun That Became a New Experiment.** 一次为了
审计 rerun 而搭建的可靠性层，逐步开始改动它本该审计的状态，最终把一次
重复实验膨胀成一个完整的工程项目——每一步局部看都合理。Open PRAOP v0.1
本身在收敛这四项修复时，也刻意把范围锁在这四项、拒绝顺势扩写成二十条
governance，就是为了不在治理层面复现同一个 failure shape。

### Translationese

把简单事件翻译成没人真正理解的抽象 jargon。

### AI Consensus as Evidence

多个 LLM 都同意，不等于 evidence 增加。

### Memory as Truth

"我们以前讨论过"不能代替 artifact。

---

# 19. Open PRAOP v0.1 Success Criteria

第一版不以 star 数量衡量成功。

只看：

1. 是否有外部 contributor 能不经培训完成 case submission；
2. 是否能成功完成脱敏；
3. 是否有案例无法落入现有 PRAOP taxonomy；
4. 是否能从多个案例形成至少一个 credible Pattern candidate；
5. 是否有 Practice 被真实使用并得到 outcome；
6. repo 是否保持简单，没有因为治理本身阻止参与。

---

# 20. v0.1 的一句话规则

对 Contributor：

> **Tell us what happened. You do not need to know what PRAOP calls it.**

对 Maintainer：

> **Preserve the incident before improving the theory.**

对整个项目：

> **Cases create patterns. Patterns suggest practices. Practices earn promotion through use and falsification.**

对 Open PRAOP 自身（v0.1-final 新增）：

> **Repair the state model, harden the anchor rule, clean the public boundary, and add one second pair of eyes for doctrine-changing decisions. Then stop.**
