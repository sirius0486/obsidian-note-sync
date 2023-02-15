## JS 片段

```js
//imp
import moduleName from 'module'

//imd
import { destructuredModule } from 'module'

//fof
for(let itemName of objectName { }

//fin
for(let itemName in objectName { }

//anfn
(params) => { }
```

## React 片段

```js
//imr
import React from 'react'

//rfc
import React from 'react'

export default function $1() {
  return <div>$0</div>
}

```


## Vite.config.ts


```ts
import { defineConfig } from "vite";
import reactRefresh from "@vitejs/plugin-react-refresh";
import * as path from "path";
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [reactRefresh()],
  // 配置路径别名
      resolve: {
        alias: {
          "@": path.resolve(__dirname, "src"),
        },
      },
    server: {
        port: 3000,
        proxy: {
          "/api": {
            target: "https://yourBaseUrl",
            changeOrigin: true,
            cookieDomainRewrite: "",
            secure: false,
          },
        },
      },
});

```