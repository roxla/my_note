## Monorepo 架构目录说明

### 根目录

根目录是整个仓库的入口，包含全局配置文件、公共依赖声明以及工作区定义。

```
my-vue-monorepo/
├── package.json                # 根包描述文件，定义工作区和公共脚本
├── pnpm-workspace.yaml         # pnpm 工作区配置文件
├── pnpm-lock.yaml              # 全局依赖锁定文件
├── tsconfig.json               # 基础 TypeScript 配置，供子包继承
├── .gitignore                  # Git 忽略文件
├── .npmrc                      # npm/pnpm 配置（可选）
├── turbo.json                   # Turborepo 构建配置文件（如使用）
└── README.md                    # 项目说明文档
```

### `apps/` 目录

存放可独立部署的应用程序，每个应用都是一个完整的项目，有自己的 `package.json`、入口文件和配置。

```
apps/
├── main-app/                # 主应用
│   ├── src/
│   │   ├── main.ts
│   │   ├── App.vue
│   │   ├── router/
│   │   ├── stores/
│   │   └── views/
│   ├── index.html
│   ├── package.json
│   ├── vite.config.ts
│   └── tsconfig.json
└── admin-app/                # 后台管理应用（可选）
    ├── ...
```

- 每个应用**独立运行**，拥有自己的构建配置（如 Vite）。
- 可以引用 `packages/` 和 `internal/` 中的共享包。
- 通常使用 `workspace:*` 协议引入本地包，例如：
  ```json
  {
    "dependencies": {
      "@my-monorepo/ui": "workspace:*",
      "@my-monorepo/stores": "workspace:*"
    }
  }
  ```

### `packages/` 目录

存放共享的可复用模块，这些模块可以被多个应用或其他包引入。它们通常设计为**可独立发布**的包（但也可以标记为私有）。

```
packages/
├── ui/                        # 共享组件库
│   ├── src/
│   │   ├── components/
│   │   ├── composables/
│   │   └── index.ts
│   ├── package.json
│   ├── vite.config.ts         # 库模式构建配置
│   └── tsconfig.json
├── stores/                    # 共享 Pinia store
│   ├── src/
│   │   ├── counter.ts
│   │   ├── user.ts
│   │   └── index.ts
│   └── package.json
├── utils/                      # 工具函数库
│   ├── src/
│   └── package.json
└── types/                      # 共享 TypeScript 类型
    ├── src/
    └── package.json
```



---

### `internal/` 目录

存放仅供当前仓库内部使用的代码和配置，这些内容**不会对外发布**，主要用于支持开发流程。

```
internal/
├── eslint-config/              # 共享 ESLint 配置
│   ├── package.json
│   └── index.js
├── tsconfig/                    # 共享 TypeScript 配置
│   ├── package.json
│   └── base.json
├── scripts/                     # 内部脚本（代码生成、部署辅助）
│   └── generate-api.js
└── vitest-config/               # 共享测试配置
    └── index.js
```



---

### 其他常见目录

- `configs/`
  - 与 `internal/` 类似，但更侧重于构建工具配置（如 `configs/vite`、`configs/jest`）。有些项目将共享配置统一放在此目录
- `scripts/`
  - 存放根级别的脚本，如自动化发布、版本更新、依赖检查等。这些脚本通常被根 `package.json` 的 `scripts` 引用
- `docs/`
  - 项目文档，包括架构说明、API 文档、开发指南等
- `tests/` 或 `e2e/`
  - 端到端测试或集成测试，可能跨多个应用

---

### 依赖管理关键文件

#### `pnpm-workspace.yaml`

除了定义包目录，还可以配置 `catalog`、`overrides` 等：
```yaml
packages:
  - 'apps/*'
  - 'packages/*'

catalog:
  vue: ^3.4.0
  ant-design-vue: ^4.0.0

overrides:
  vue@3.2: 3.2.47   # 强制某些包使用特定版本
```

####  `pnpm-lock.yaml`

全局锁文件，确保所有安装的依赖版本一致。

####  `.npmrc`

可配置 pnpm 的行为，如：
```
registry=https://registry.npmmirror.com/
hoist-pattern[]=*eslint*
public-hoist-pattern[]=*vite*
```
---

### Monorepo 目录结构总结


> 1. **目录命名清晰**：`apps/` 放应用，`packages/` 放共享库，`internal/` 放内部工具。
> 2. **私有包标记**：内部包一律设置 `"private": true`，防止误发布。
> 3. **依赖管理**：使用 `pnpm` 的 `catalog` 统一核心依赖版本；利用 `workspace:*` 协议链接本地包。
> 4. **类型共享**：通过 `tsconfig.json` 的 `paths` 和项目引用（composite）实现跨包类型检查。
> 5. **构建缓存**：配合 Turborepo 或 Nx 实现增量构建，提高 CI/CD 效率。
> 6. **代码规范**：在 `internal/` 中放置共享的 ESLint/Prettier 配置，保证全仓库风格一致。
> 7. **版本发布**：使用 `changesets` 管理版本更新和发布日志。

#### 完整目录结构示例

```
my-vue-monorepo/                         # 项目根目录，包含所有应用、共享包、内部工具和全局配置
├── apps/                                # 存放可独立部署的应用程序
│   └── main-app/                        # 主应用目录
│       ├── src/                         # 应用源码（组件、页面、路由、状态管理等）
│       ├── index.html                   # 应用 HTML 入口
│       ├── package.json                 # 主应用的依赖声明和脚本，通过 workspace:* 引用本地包
│       └── vite.config.ts               # 主应用的 Vite 配置（开发服务器、构建、别名等）
├── packages/                            # 存放共享的可复用模块（可能对外发布或内部共享）
│   ├── ui/                              # 共享组件库
│   │   ├── src/                         # 组件源码、组合式函数等
│   │   ├── package.json                 # 包名一般为 @my-monorepo/ui，包含 peerDependencies 和构建脚本
│   │   └── vite.config.ts               # 库模式构建配置，输出为 ESM/UMD 格式
│   ├── stores/                          # 共享 Pinia store 定义
│   │   ├── src/                         # store 模块源码（如 user.ts, counter.ts）
│   │   └── package.json                 # 包名一般为 @my-monorepo/stores，依赖 pinia 和 vue
│   └── utils/                           # 共享工具函数库
│       ├── src/                         # 工具函数源码（日期格式化、请求封装等）
│       └── package.json                 # 包名一般为 @my-monorepo/utils，可包含通用依赖
├── internal/                            # 存放仅限当前仓库内部使用的代码和配置（不对外发布）
│   ├── eslint-config/                   # 共享 ESLint 配置
│   │   ├── package.json                 # 包名一般为 @internal/eslint-config，私有包
│   │   └── index.js                     # ESLint 规则配置，可被各子包继承
│   └── tsconfig/                        # 共享 TypeScript 配置
│       ├── package.json                 # 包名一般为 @internal/tsconfig，私有包
│       └── base.json                    # 基础 TypeScript 配置，供各子包通过 extends 继承
├── package.json                         # 根包描述文件，声明工作区、公共脚本和公共开发依赖
├── pnpm-workspace.yaml                  # pnpm 工作区配置文件，定义子包路径（apps/*, packages/*, internal/*）
├── tsconfig.json                        # 根 TypeScript 配置，通常包含路径别名和基础编译选项，供子包参考
└── README.md                            # 项目说明文档（架构、开发指南等）
```

---

## pnpm-workspace.yaml 文件说明



---

## package.json 文件说明



---

## tsconfig.json 文件说明

TypeScript 配置文件 `tsconfig.json` 是整个 Monorepo 类型安全和开发体验的基石。它定义了 TypeScript 编译器如何解析代码、生成类型声明以及进行类型检查。在 Monorepo 中，我们通常采用**分层配置 + 继承**的策略，以实现配置复用和按需定制。

**tsconfig.json 常用关键字说明表**

| 关键字                | 功能说明                                                     | 在 Monorepo 中的典型用法                                     |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **`$schema`**         | 指定 JSON Schema 的 URL，用于编辑器（如 VSCode）提供智能提示和自动补全。 | 在根配置或子包配置中添加，例如 `"$schema": "https://json.schemastore.org/tsconfig"`，以提升开发体验。 |
| **`extends`**         | 继承另一个配置文件的基础设置。当前配置会与继承的配置合并，当前配置的选项优先级更高。 | 子包（如 `apps/main-app`、`packages/ui`）通过 `extends` 引用根目录的基础 `tsconfig.json`，实现配置复用，避免重复定义。 |
| **`display`**         | 一个非编译性、用于人类阅读的标识字段。在 Monorepo 中，当有多个 `tsconfig.json` 文件时，此字段可帮助工具或开发者快速识别当前配置的用途。 | 例如在 `apps/main-app/tsconfig.json` 中设置 `"display": "Main Web Application"`，便于区分不同配置。 |
| **`compilerOptions`** | 编译选项对象，包含大量子选项（如 `target`、`module`、`strict`、`paths` 等）。这是配置的核心部分。 | 在根配置中统一设置基础编译选项（如 `moduleResolution: "bundler"`），子包可根据需要覆盖或补充。 |
| **`files`**           | 列出需要被编译的单个文件列表。通常用于小型项目或明确指定入口文件的场景。 | 在 Monorepo 中较少使用，因为 `include` 模式更灵活。但可用于明确指定库的入口文件（如 `"files": ["src/index.ts"]`）。 |
| **`include`**         | 指定需要被 TypeScript 编译的文件或目录（支持 glob 通配符）。只有匹配的文件才会被包含进编译。 | 每个子包通常设置 `"include": ["src"]`，将编译范围限制在自己的源码目录内，避免意外包含无关文件。 |
| **`exclude`**         | 指定在编译时需要排除的文件或目录（通常用于排除 `node_modules`、测试文件等）。优先级高于 `include`。 | 默认排除 `node_modules`；若项目中有测试文件不希望被编译，也可通过此字段排除。 |
| **`references`**      | 定义项目引用（Project References），声明当前项目依赖的其他 TypeScript 项目。配合 `composite: true` 使用，支持增量构建。 | 用于有依赖关系的本地包之间。例如 `packages/ui` 可能引用 `packages/stores` 的类型，通过 `references: [{ "path": "../stores" }]` 建立依赖关系。 |
| **`watchOptions`**    | 配置 TypeScript 的监视模式行为（如监听文件变化的策略）。     | 可用于优化开发体验，例如在大型 Monorepo 中调整文件监听的排除规则，减少 CPU 占用。 |
| **`typeAcquisition`** | 控制自动类型获取（Typing Acquisition）的行为，主要用于 JavaScript 项目。 | 在纯 TypeScript 项目中较少使用。                             |
| **`ts-node`**         | 为 `ts-node` 运行时提供独立配置（如指定 transpiler 或 `swc` 支持）。 | 当 Monorepo 中使用 `ts-node` 执行脚本时，可通过此字段设置特定选项，例如 `"ts-node": { "transpileOnly": true }` 加速执行。 |
| **`compileOnSave`**   | 告诉 IDE 在保存文件时是否自动编译。现代编辑器通常忽略此字段。 | 已较少使用，编辑器一般通过自身配置控制。                     |

> **说明**：`compilerOptions` 内部包含大量子选项（如 `target`、`module`、`strict`、`paths`、`declaration`、`noEmit` 等），具体可参考 [TypeScript 官方文档](https://www.typescriptlang.org/tsconfig)。在 Monorepo 中，建议在根配置中设置公共子选项，子包仅覆盖必要项。

---

### 1. 根目录 `tsconfig.json`（基础配置）

根目录的 `tsconfig.json` 作为所有子包的“基础配置”，通常包含**跨包共享的编译选项**和**路径别名映射**，而不包含具体的文件包含规则（如 `include`），以便子包可以灵活覆盖。

```json
{
  "compilerOptions": {
    "target": "ESNext",
    "module": "ESNext",
    "moduleResolution": "bundler",         // 与 Vite 等打包工具完美配合
    "strict": true,                         // 开启所有严格类型检查
    "jsx": "preserve",                       // 保留 JSX 语法，交由插件处理
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "baseUrl": ".",                          // 路径解析基准目录
    "paths": {
      "@my-monorepo/*": ["./packages/*/src"], // 内部包的路径别名
      "@internal/*": ["./internal/*/src"]
    }
  }
}
```

- **`paths` 配合 `baseUrl`**：允许在代码中使用像 `@my-monorepo/ui` 这样的别名导入本地包，编辑器（VSCode）和 TypeScript 编译器都能正确解析。
- **`moduleResolution: "bundler"`**：专为现代打包工具设计的解析策略，能正确识别 `package.json` 中的 `exports` 字段，是 Vite 项目的推荐配置。

---

### 2. 应用层 `tsconfig.json`（如 `apps/main-app/tsconfig.json`）

应用层的配置**继承**根配置，并添加应用特有的选项，例如指定源码范围、输出目录和是否生成声明文件。

```json
{
  "extends": "../../tsconfig.json",
  "display": "Main Web Application",          // 人类可读的标识，方便识别
  "compilerOptions": {
    "lib": ["ESNext", "DOM", "DOM.Iterable"], // 浏览器环境类型
    "jsx": "preserve",                         // 若使用 Vue JSX
    "useDefineForClassFields": true,
    "declaration": true,                       // 生成 .d.ts 文件（若需）
    "noEmit": false,                           // 允许输出编译产物
    "outDir": "./dist"                          // 输出目录
  },
  "include": ["src"]                           // 只编译 src 目录
}
```

- **`display`**：仅用于工具或编辑器显示，不影响编译行为，但在 Monorepo 中能帮助开发者快速识别当前配置的用途。
- **`extends`**：从根配置继承，实现“一次定义，多处使用”。

---

### 3. 共享库层 `tsconfig.json`（如 `packages/ui/tsconfig.json`）

共享库通常需要生成类型声明文件（供消费者使用），并可能声明对其它本地包的**项目引用**以实现增量构建。

```json
{
  "extends": "../../tsconfig.json",
  "compilerOptions": {
    "outDir": "./dist",
    "declaration": true,
    "declarationMap": true,                // 便于调试跳转
    "noEmit": false,
    "composite": true,                      // 启用项目引用，支持增量构建
    "rootDir": "./src"
  },
  "include": ["src"],
  "references": [                           // 声明依赖的其他本地包
    { "path": "../stores" }                  // 若 ui 依赖 stores 的类型
  ]
}
```

- **`composite: true`**：启用项目引用功能，配合 `references` 字段，让 TypeScript 能够增量构建依赖图，大幅提升大型 Monorepo 的类型检查速度。
- **`references`**：列出当前项目直接依赖的其他本地包（需配置 `composite: true`），TypeScript 会确保这些依赖先被构建。

---

### 4. 继承第三方配置包（如 `@vben/tsconfig/library.json`）

如果你的共享库希望遵循社区最佳实践，可以直接继承已发布的 npm 配置包：

```json
{
  "extends": "@vben/tsconfig/library.json",
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

- 这种方式将配置标准化、可复用化，尤其适合跨项目共享的库开发。
- 继承后，只需关注项目自身的 `include` 和 `exclude` 即可。

---

### 5. 关键 `compilerOptions` 详解

| 选项                                | 作用                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| **`moduleResolution: "bundler"`**   | 支持 `package.json` 的 `exports` 和 `imports`，与 Vite 等工具完美集成。 |
| **`declaration: true`**             | 为每个 TypeScript 文件生成对应的 `.d.ts` 类型声明文件，是库发布的必要条件。 |
| **`noEmit: true/false`**            | `true` 表示只进行类型检查，不输出文件（常用于开发环境）；`false` 表示允许输出（用于构建）。 |
| **`composite: true`**               | 开启项目引用，要求 `rootDir` 和 `outDir` 必须设置，且文件需要被 `include` 明确包含。 |
| **`paths`**                         | 路径别名映射，需与构建工具（Vite）的别名配置保持一致，实现无缝导入。 |
| **`lib`**                           | 指定编译时包含的库类型文件，如 `DOM` 提供浏览器环境类型。    |
| **`jsx: "preserve"`**               | 保留 JSX 语法，交由下游工具（如 `@vitejs/plugin-vue-jsx`）处理。 |
| **`useDefineForClassFields: true`** | 遵循 ECMAScript 标准，与 Vue 的响应式系统配合更好。          |

---

### 6. 调试与显示辅助选项

TypeScript 提供了一些用于调试和查看编译过程的选项，可临时在配置中开启或通过命令行参数使用：

```json
{
  "compilerOptions": {
    "diagnostics": true,          // 输出编译性能诊断信息
    "listFiles": true,            // 列出所有参与编译的文件
    "traceResolution": true       // 跟踪模块解析过程（排查路径别名问题）
  }
}
```

或通过命令行查看：
```bash
npx tsc --showConfig              # 显示最终合并的配置
npx tsc --noEmit --diagnostics    # 只检查类型并输出诊断信息
```

---

