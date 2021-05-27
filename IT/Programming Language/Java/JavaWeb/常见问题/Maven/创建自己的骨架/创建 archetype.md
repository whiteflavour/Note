# 自定义 archetype (2021.3.20)

1. 使用 IDEA 自带的 archetype-webapp 骨架创建一个有自己想要目录和 pom.xml 依赖的项目。—— 创建模板

> **注意**：每个目录下必须要有一个文件来占位（任意文件，可以是空文件），否则 IDEA 会认为它是空目录，不会创建。★

2. IDEA 右侧的 Maven 选项展开 -> 点击 Execute Maven Goal -> 在项目的根目录下（IDEA 2020.3.2 中自动选择该目录），执行：`mvn archetype:create-from-project`。—— 创建骨架

3. 完成后会出现 target 目录，展开，找到该目录下的 pom.xml 文件，打开，里面有 **自己创建的骨架的信息**。—— 查看自定义骨架信息

4. 在 Execute Maven Goal 中，选择 target 目录下的 archetype，在此目录下执行命令：`mvn (clean) install`。—— 安装骨架

5. （可选）可以在任意目录下生成日志文件：在任意目录执行命令：`mvn archetype:crawl`。—— 生成日志

6. IDEA New Project -> 勾上 Create from archetype -> Add archetype -> 输入 **第三步** 中的骨架信息，仓库那一栏不用管。—— 将自己的骨架添加进 IDEA 中

7. 使用自己创建的骨架。—— 使用

From：https://www.shaoyong.online/posts/ceb2a2ec/ 