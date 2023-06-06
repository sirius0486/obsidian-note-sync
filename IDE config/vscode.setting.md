> [!info] > 参考自 一个托尼(antfu)的 vscode 配置

## Link
https://github.com/antfu/vscode-settings

```md
Anthony's VS Code Settings

.vscode/settings.json
.vscode/extensions.json
.vscode/global.code-snippets
```


## setting

### .vscode/settings.json
```json
{
  // Visuals
  "workbench.iconTheme": "file-icons",
  "workbench.colorTheme": "Vitesse Light",
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },

  "git.autofetch": true,
  "git.confirmSync": false,
  "git.suggestSmartCommit": true,
  "git.enableSmartCommit": true,
  "git.untrackedChanges": "separate",

  "files.eol": "\n",
  "files.insertFinalNewline": true,
  "files.simpleDialog.enable": true,

  "typescript.updateImportsOnFileMove.enabled": "always",
  "reactSnippets.settings.prettierEnabled": true,
  
  // Editor
  "editor.fontSize": 13,
  "editor.fontFamily": "Input Mono, JetBrains Mono, monospace",
  "editor.fontLigatures": true,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,
  "editor.tokenColorCustomizations": {
    "comments": "#1fd160"
  },
  "editor.accessibilitySupport": "off",
  "editor.cursorSmoothCaretAnimation": "on",
  "editor.find.addExtraSpaceOnTop": false,
  "editor.guides.bracketPairs": "active",
  "editor.inlineSuggest.enabled": true,
  "editor.multiCursorModifier": "ctrlCmd",
  "editor.renderWhitespace": "boundary",
  "editor.suggestSelection": "first",
  "editor.tabSize": 2,
  "editor.unicodeHighlight.invisibleCharacters": false,
  "editor.codeActionsOnSave": {
    "source.fixAll": false,
    "source.fixAll.eslint": true, // this allows ESLint to auto fix on save
    "source.organizeImports": false
  },
  
  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,

  "terminal.integrated.fontFamily": "MesloLGM NF",
  "terminal.integrated.cursorBlinking": true,
  "terminal.integrated.cursorStyle": "line",
  "terminal.integrated.fontWeight": "300",
  "terminal.integrated.persistentSessionReviveProcess": "never",
  "terminal.integrated.tabs.enabled": true,

  "search.exclude": {
    "**/.git": true,
    "**/.github": true,
    "**/.nuxt": true,
    "**/.output": true,
    "**/.pnpm": true,
    "**/.vscode": true,
    "**/.yarn": true,
    "**/bower_components": true,
    "**/dist/**": true,
    "**/logs": true,
    "**/node_modules": true,
    "**/out/**": true,
    "**/package-lock.json": true,
    "**/pnpm-lock.yaml": true,
    "**/tmp": true,
    "**/yarn.lock": true
  },

  // Extension configs
  "emmet.showSuggestionsAsSnippets": true,
  "emmet.triggerExpansionOnTab": false,
  "errorLens.enabledDiagnosticLevels": [
    "warning",
    "error"
  ],
  "errorLens.excludeBySource": [
    "cSpell",
    "Grammarly",
    "eslint"
  ],

}

```

### .vscode/global.code-snippets

```json
{
	"import": {
	  "scope": "javascript,typescript",
	  "prefix": "im",
	  "body": [
		"import { $1 } from '$2';"
	  ],
	  "description": "Import a module"
	},
	"export-all": {
	  "scope": "javascript,typescript",
	  "prefix": "ex",
	  "body": [
		"export * from '$2';"
	  ],
	  "description": "Export a module"
	},
	"vue-script-setup": {
	  "scope": "vue",
	  "prefix": "<sc",
	  "body": [
		"<script setup lang=\"ts\">",
		"const props = defineProps<{",
		"  modelValue?: boolean,",
		"}>()",
		"$1",
		"</script>",
		"",
		"<template>",
		"  <div>",
		"    <slot/>",
		"  </div>",
		"</template>",
	  ]
	},
	"vue-template-ref": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "tref",
	  "body": [
		"const ${1:el} = shallowRef<HTMLDivElement>()",
	  ]
	},
	"vue-computed": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "com",
	  "body": [
		"computed(() => { $1 })"
	  ]
	},
	"vue-watch-effect": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "watchE",
	  "body": [
		"watchEffect(() => {",
		"  $1",
		"})"
	  ]
	},
	"if-vitest": {
	  "scope": "javascript,typescript",
	  "prefix": "ifv",
	  "body": [
		"if (import.meta.vitest) {",
		"  const { describe, it, expect } = import.meta.vitest",
		"  ${1}",
		"}"
	  ]
	},
	"markdown-api-table": {
	  "scope": "markdown",
	  "prefix": "table",
	  "body": [
		"<table>",
		"<tr>",
		"<td width=\"400px\" valign=\"top\">",
		"",
		"### API",
		"",
		"Description",
		"",
		"</td>",
		"<td width=\"600px\"><br>",
		"",
		"```ts",
		"// code block",
		"```",
		"",
		"</td>",
		"</tr>",
		"</table>",
	  ],
	}
  }
  
```

### frontend.code-snippets
```json
{
	// $0 — tab stop final cursor position
	// $1, $2 for tab stops — tab stop to specify the cursor location and allow the user to customize the the name of the component
	// ${1:label}, ${2:another} for placeholders.
	// ${TM_FILENAME_BASE} — variable for getting the current filename
  // \t 
	// /capitalize

	// JS & TS import snippets
  "Print to console": {
  	"prefix": "log",
  	"body": [
  		"console.log($1);",
  		"$2"
  	],
  	"description": "Log output to console"
  },
	"JSON stringify": {
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
		"prefix": "jst",
		"body": [
			"<pre>{JSON.stringify($1, null, 2)}</pre>"
		]
	},
	"import": {
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "im",
	  "body": [
		"import { $1 } from '$2';"
	  ],
	  "description": "Import a module"
	},
	"export-all": {
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "ex",
	  "body": [
		"export * from '$2';"
	  ],
	  "description": "Export a module"
	},

	// React snippets
	"React.useState-Snippet": {
    "prefix": "state",
    "body": ["const [$1, set${1/(.*)/${1:/capitalize}/}] = useState<$2>($3)"],
    "description": "useState snippet"
  },
	"React.useEffect-Snippet": {
    "prefix": "effect",
    "body": ["useEffect(() => {", "  $1", "}, [$2])"],
    "description": "useEffect snippet"
  },
  "React.useRef-Snippet": {
    "prefix": "ref",
    "body": ["const $1 = useRef<$2>($3)"],
    "description": "useRef snippet"
  },
	"React.useMemo-Snippet": {
		"prefix": "memo",
    "body": [
			"const memoizedValue = useMemo(",
  		"\t() => ${3:performExpensiveCalculation}(${1:arg1}, ${2:arg2},",
  		"\t[${1:arg1}, ${2:arg2}]",
			")",
		],
    "description": "useMemo snippet"
	},
  "React.useCallback-Snippet": {
    "prefix": "callback",
    "body": ["const $1 = useCallback(($2) => {", "  $3", "}, [$4])"],
    "description": "useCallback snippet"
  },
	"React.Typescript-Function-Component": {
    "prefix": "fc",
    "body": [
      "import { FC } from 'react'",
      "",
      "interface ${TM_FILENAME_BASE}Props {",
      "\t$1",
      "}",
      "",
      "const $TM_FILENAME_BASE: FC<${TM_FILENAME_BASE}Props> = ({$2}) => {",
      "\treturn <div>$TM_FILENAME_BASE</div>",
      "}",
      "",
      "export default $TM_FILENAME_BASE"
    ],
    "description": "Typescript React Function Component"
  },
	"React.Typescript-Arrow-Function-Component": {
		"prefix": "rfc",
		"body": [
			"import React from 'react';",
			"",
			"import styles from './${TM_FILENAME_BASE}.module.scss';",
			"",
			"interface ${1:${TM_FILENAME_BASE}}Props {",
			"\tprop: string;",
			"}",
			"",
			"const ${1:${TM_FILENAME_BASE}} = (props : ${1:${TM_FILENAME_BASE}}Props ) => {",
			"",
			"\tconst {prop} = props;",
			"",
			"\treturn (",
			"\t\t<div className={styles.root}>",
			"\t\t\t{prop}$0",
			"\t\t</div>",
			"\t);",
			"};",
			"",
			"export default ${1:${TM_FILENAME_BASE}};",
			""
		],
		"description": "Create a React functional component using TypeScript and SCSS modules"
	},
	"React.Function-Component":{
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "rfce",
	  "body": [
		"import React from 'react'",
		"",
		"function ${TM_FILENAME_BASE}() {",
		"\treturn <div>${1:${TM_FILENAME_BASE}}${0}</div>",
		"}",
		"",
		"export default ${TM_FILENAME_BASE}",
	  ],
	  "description": "React function component"
	},
	"React.Export-Arrow-Function-Component-Default":{
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "rafc",
	  "body": [
			"import React from 'react'",
			"",
			"const ${TM_FILENAME_BASE} = () => {",
			"\treturn <div>${1:${TM_FILENAME_BASE}}${0}</div>",
			"}",
			"",
			"export default ${TM_FILENAME_BASE}",
			],
	  "description": "React arrow function component"
	},
	"React.Export-Arrow-Function-Component":{
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "rafce",
	  "body": [
		"import React from 'react'",
		"",
		"export const ${TM_FILENAME_BASE} = () => {",
		"\treturn <div>${1:${TM_FILENAME_BASE}}${0}</div>",
		"}",
	  ],
	  "description": "React arrow function component export default"
	},
	"React.Layout-Component":{
		"scope": "javascript,typescript,javascriptreact,typescriptreact",
	  "prefix": "lc",
	  "body": [
			"import React from 'react';",
			"",
			"const Layout = ({ children }) => {",
			" return (",
			"\t<>",
			"\t\t<${3:Header} />",
			"\t\t<${1:Navbar} />",
			"\t\t<main>{children}${0}</main>",
			"\t\t<${2:Footer} />",
			"\t\t</>",
			"\t);",
			"};",
			"",
			"export default Layout;",
	  ],
	  "description": "Export a React Layout Component"
	},

	// Vue3 snippets
	"Vue.body": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "<sc",
	  "body": [
		"<script setup lang=\"ts\">",
		"const props = defineProps<{",
		"\tmodelValue?: boolean,",
		"}>()",
		"$1",
		"</script>",
		"",
		"<template>",
		"\t<div>",
		"\t\t<slot/>",
		"\t</div>",
		"</template>",
	  ]
	},
	"Vue.template-ref": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "tref",
	  "body": [
		"const ${1:el} = shallowRef<HTMLDivElement>()",
	  ]
	},
	"Vue.computed": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "com",
	  "body": [
		"computed(() => { $1 })"
	  ]
	},
	"Vue.watch-effect": {
	  "scope": "javascript,typescript,vue",
	  "prefix": "watchE",
	  "body": [
		"watchEffect(() => {",
		"\t$1",
		"})"
	  ]
	},
	"Vue.if-vitest": {
	  "scope": "javascript,typescript",
	  "prefix": "ifv",
	  "body": [
		"if (import.meta.vitest) {",
		"\tconst { describe, it, expect } = import.meta.vitest",
		"\t${1}",
		"}"
	  ]
	},

	// test snippets
	"Test.describe": {
		"prefix": "desc",
		"body": [
			"describe('should $1', () => {",
			"\t$2",
			 "})",
		],
		"description": "describe body"
	},
	"Test.test": {
		"prefix": ["test"],
		"body": [
			 "test('should $1', () => {",
			 "\t$2",
			 "})",
		],
		"description": "test body"
	},
	"Test.it": {
		"prefix": ["it"],
		"body": [
			"it('should $1', () => {",
			"\t$2",
			"})",
		],
		"description": "test it body"
	},
	"Test.gwt": {
		"prefix": ["gwt"],
		"body": [
			"describe('test context', () => {",
			"\ttest('has no expected errors', {",
			"\t\t// given",
			" \t\t$0",
			" \t\t// when",
			"",	
			" \t\t// then",
			"",
			"\t});",
			"});",
		],
		"description": "test it body"
	},
	"Test.snapshot": {
		"prefix": ["snapshot"],
		"body": [
		"import React from 'react'",
		"import renderer from 'react-test-renderer'",
		"import { $1 } from '../$1'",
		"",
		"describe('<$1 />', () => {",
		"",
		"  const defaultProps = {}",
		"  const wrapper = renderer.create(<$1 {...defaultProps} />)",
		"",
		"  test('render', () => {",
		"    expect(wrapper).toMatchSnapshot()",
		"   })",
		"})"
		],
		"description": "test snapshot body"
	},
}
```

### markdown.json
```json
{
  "H1": {
    "prefix": "/1",
    "body": ["# $0"]
  },
  "H2": {
    "prefix": "/2",
    "body": ["## $0"]
  },
  "H3": {
    "prefix": "/3",
    "body": ["### $0"]
  },
  "H4": {
    "prefix": "/4",
    "body": ["#### $0"]
  },
  "H5": {
    "prefix": "/5",
    "body": ["##### $0"]
  },
  "H6": {
    "prefix": "/6",
    "body": ["###### $0"]
  },
  "bold粗体": {
    "prefix": "/b",
    "body": ["**$1**$2"]
  },
  "italic斜体": {
    "prefix": "/i",
    "body": ["*$1*$2"]
  },
  "underline下划线": {
    "prefix": "/u",
    "body": ["<u>$1</u>$2"]
  },
  "line-through删除线": {
    "prefix": "/x",
    "body": ["~~$1~~$2"]
  },
  "divider分割线": {
    "prefix": "/d",
    "body": ["------", "$1"]
  },
  "link链接": {
    "prefix": "/k",
    "body": ["[$2]($1)$3"]
  },
  "image图片": {
    "prefix": "/img",
    "body": ["![$2]($1)$3"]
  },
  "inline code行内代码": {
    "prefix": "/cl",
    "body": ["`$1`$2"]
  },
  "code block代码片段": {
    "prefix": "/c",
    "body": ["```$1", "$0", "```"]
  },
  "ul有序列表": {
    "prefix": "/ul",
    "body": ["- $0"]
  },
  "ol无序列表": {
    "prefix": "/ol",
    "body": ["1. $0"]
  },
  "task任务列表": {
    "prefix": "/task",
    "body": ["- [ ] $0"]
  },
  "quote引用": {
    "prefix": "/q",
    "body": ["> $1", "$2"]
  },
  "table表格": {
    "prefix": "/t",
    "body": [
      "|  $1  |  $2  |  $3  |  $4  |",
      "| ---- | ---- | ---- | ---- |",
      "|  $5  |  $6  |  $7  |  $8  |",
      "|  $9  |  $10 |  $11 |  $12 |",
      "|  $13 |  $14 |  $15 |  $16 |"
    ]
  }
}
```


## plugins

### git
- git lens
- git graph
- git history


### snippets
- volar 
- ES7+ React/Redux/React-Native snippets
- UnoCSS

### preview
> 增强文件预览
- Svg Preview
- Image Preview
- MDX

### debug
> 主要是调试相关
- Import Cost
- Error Lens

### beauty
> 这里包含 字体, 主题, icon 配置

- file icons / vscode icons
- vitesse theme / atom theme
- Jetbrain Mono / Input Mono

## 备忘录
- markdown 打开自动预览
- 自动换行
- 安装 Input Mono , Jetbrain Mono, 终端字体
- 连体字开启
- 绿色注释
- 自动格式化