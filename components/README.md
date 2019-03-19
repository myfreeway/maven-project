# components
基础组件项目，通常是提供jar包。所有改动必须升级版本号。

本层内部定义了各种基础父pom和jar包的组合，方便灵活组合。

各大组件关系介绍：
1. top-parent 顶级父pom。定义源码deploy url，构建配置，定义公包依赖，业务项目不要直接继承
2. parent 业务项目的直接父pom。直接import各种聚合的bom，间接定义了公包和私包的依赖
3. bom/common-bom common项目的bom定义。依赖项可以是不存在的，尚未构建的。
4. bom/pack-bom 公包依赖项的组合包。方便业务项目引入。
5. pack/json-pack json组合包。目前只有jackson。可用于json序列化反序列化，springmvc的json输入输出。
6. common/common-parent common项目的直接父pom。单独一个父pom，是为了不造成循环依赖，也为了自由发展
7. common/common-demo1 common演示项目1。依赖一个公包。
8. common/common-demo2 common演示项目2。依赖common-demo1、json-pack

基础组件构建顺序：
1. components/top-parent/pom.xml
2. components/pom.xml
3. components/common/pom.xml

如何使用？
====
1. 修改top-parent的maven仓库路径
2. 修改包名
3. 规划自己的公包和私包，并修改
