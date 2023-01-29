> [!hint] > 你的 commit 信息应该是能帮助你 code diff 的时候快速定位
> >`git commit -m "feat: implement fetchData api"`


-   init - init Projects
    -   `项目初始化`
-   feat - A new feature
    -   `实现新的功能,特性`
-   fix -A bug fix
    -   `修复 bug,error`
-   docs - Documentation only changes
    -   `文档改进等`
-   style - Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
    -   `样式修改,如缩进,格式化,单引号等`
-   refactor - A code change that neither fixes a bug nor adds a feature Type of change
    -   `重构`
-   chore - Other changes that don't modify src or test files
    -   `配置文件但不影响核心代码src`
-   test - Adding missing tests or correcting existing tests
    -   `测试, 增加单元测试等`
-   perf - A code change that improves performance
    -   '性能优化'
-   build - Changes that affect the build system or external dependencies (example scopes: gulp, broccoli,npm)
    -   `构建变化, 如npm,maven,gradle等构建工具`
-   ci - Changes to our Cl configuration files and scripts (example scopes: - Travis, Circle,BrowserStack, SauceLabs)
    -   `持续集成配置,自动化脚本等`
-   revert - Reverts a previous commit
    -   `恢复先前的commit`