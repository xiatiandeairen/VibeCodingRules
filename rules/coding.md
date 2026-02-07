{
  "version": "2.0.0",
  "changeAxes": [
    {
      "axis": "A1_BEHAVIOR",
      "description": "行为差异随业务场景变化",
      "rules": [
        {
          "id": "A1-01",
          "trigger": "当同一操作因类型不同而表现出不同行为",
          "action": "必须通过多态或策略对象承载行为变化",
          "verify": "不存在基于 type/code 的行为 if/else",
          "severity": "high",
          "tags": ["strategy", "polymorphism"]
        },
        {
          "id": "A1-02",
          "trigger": "当新增行为需要修改既有判断逻辑",
          "action": "必须引入可注册的行为扩展点",
          "verify": "新增行为不修改原有分支结构",
          "severity": "high",
          "tags": ["open-close", "plugin"]
        },
        {
          "id": "A1-03",
          "trigger": "当算法骨架一致但步骤细节不同",
          "action": "必须抽象流程并延迟可变步骤",
          "verify": "流程控制不被复制到多个实现",
          "severity": "medium",
          "tags": ["template-method"]
        }
      ]
    },
    {
      "axis": "A2_STATE",
      "description": "对象生命周期与状态演进",
      "rules": [
        {
          "id": "A2-01",
          "trigger": "当对象行为随内部状态变化而变化",
          "action": "必须显式建模状态并封装状态行为",
          "verify": "状态切换不依赖条件分支",
          "severity": "high",
          "tags": ["state-pattern"]
        },
        {
          "id": "A2-02",
          "trigger": "当状态通过裸值在多个位置被判断",
          "action": "必须将状态提升为强类型模型",
          "verify": "不存在 magic number/string 表示状态",
          "severity": "high",
          "tags": ["modeling", "state"]
        }
      ]
    },
    {
      "axis": "A3_RULE",
      "description": "业务规则与判断条件的变化",
      "rules": [
        {
          "id": "A3-01",
          "trigger": "当业务规则以分散条件表达式存在",
          "action": "必须将规则建模为独立对象",
          "verify": "规则可命名、组合、复用",
          "severity": "high",
          "tags": ["specification", "rule-object"]
        },
        {
          "id": "A3-02",
          "trigger": "当规则修改需要影响多个类",
          "action": "必须集中封装规则变化轴",
          "verify": "规则变化点只存在于单一模块",
          "severity": "high",
          "tags": ["change-axis", "maintainability"]
        },
        {
          "id": "A3-03",
          "trigger": "当规则优先级或组合方式可变",
          "action": "必须通过组合而非嵌套条件实现",
          "verify": "规则组合不依赖嵌套 if/else",
          "severity": "medium",
          "tags": ["composite", "readability"]
        }
      ]
    },
    {
      "axis": "A4_CREATION",
      "description": "对象创建方式的变化",
      "rules": [
        {
          "id": "A4-01",
          "trigger": "当对象创建依赖多个条件或上下文",
          "action": "必须封装创建逻辑",
          "verify": "业务代码中无条件 new",
          "severity": "high",
          "tags": ["factory", "builder"]
        },
        {
          "id": "A4-02",
          "trigger": "当构造参数跨越多个抽象层次",
          "action": "必须引入中间抽象或聚合参数",
          "verify": "构造参数语义一致",
          "severity": "medium",
          "tags": ["abstraction"]
        }
      ]
    },
    {
      "axis": "A5_EXTENSION",
      "description": "系统能力的横向扩展",
      "rules": [
        {
          "id": "A5-01",
          "trigger": "当模块预期支持未来扩展",
          "action": "必须通过接口或事件暴露扩展点",
          "verify": "扩展不修改核心模块",
          "severity": "high",
          "tags": ["extensibility"]
        },
        {
          "id": "A5-02",
          "trigger": "当继承体系随扩展不断膨胀",
          "action": "必须改用组合模型",
          "verify": "子类不覆盖父类核心行为",
          "severity": "high",
          "tags": ["composition"]
        }
      ]
    },
    {
      "axis": "A6_READABILITY",
      "description": "代码理解成本随规模变化",
      "rules": [
        {
          "id": "A6-01",
          "trigger": "当理解核心逻辑需要跨多个文件",
          "action": "必须调整结构以提高局部可读性",
          "verify": "核心流程在单一上下文中可理解",
          "severity": "medium",
          "tags": ["readability"]
        },
        {
          "id": "A6-02",
          "trigger": "当异常或边界逻辑干扰主流程阅读",
          "action": "必须重构为主流程优先结构",
          "verify": "主流程不被嵌套分支打断",
          "severity": "medium",
          "tags": ["clean-code"]
        }
      ]
    },
    {
      "axis": "A7_COLLABORATION",
      "description": "对象协作关系的变化",
      "rules": [
        {
          "id": "A7-01",
          "trigger": "当调用方需了解多个内部组件",
          "action": "必须引入统一协作入口",
          "verify": "调用方不直接依赖子组件",
          "severity": "medium",
          "tags": ["facade"]
        },
        {
          "id": "A7-02",
          "trigger": "当变化需通知多个协作对象",
          "action": "必须解耦变化传播机制",
          "verify": "不存在显式遍历通知逻辑",
          "severity": "medium",
          "tags": ["observer", "event"]
        }
      ]
    }
  ]
}
