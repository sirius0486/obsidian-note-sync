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
  "workbench.iconTheme": "file-icons",
  "workbench.colorTheme": "Vitesse Light",
  "editor.fontSize": 13,
  "editor.fontFamily": "JetBrains Mono",
  "editor.fontLigatures": true,
  "editor.wordWrap": "on",
  "editor.formatOnSave": true,
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.tokenColorCustomizations": {
    "comments": "#1fd160"
  },
  "terminal.integrated.fontFamily": "MesloLGM NF",
  "explorer.confirmDelete": false,
  "git.suggestSmartCommit": false,
  "typescript.updateImportsOnFileMove.enabled": "always",
  "reactSnippets.settings.prettierEnabled": true,
  "unocss.root": ["packages/client"]
}


```

### .vscode/extensions.json

```json

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
- Svg Preview
- Image Preview
- MDX

### debug
- Import Cost
- Error Lens

### beauty

- file icons / vscode icons
- vitesse theme / atom theme
- Jetbrain Mono / Input Mono




## 备忘录
- markdown 打开自动预览
- 自动换行
- 连体字开启
- 绿色注释
- 自动格式化