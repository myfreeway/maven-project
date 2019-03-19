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

项目思路
====
1. maven的dependencyManagement和dependencies特性。dependencyManagement预定义包，dependencies只需指定group和artifactId，版本号继承而来。好处是统一管理版本号，避免混乱，对升级友好。
2. 发挥maven的继承特性，将很多统一配置放在顶级父pom，简化子项目的配置。比如构建，源码上传路径等。
3. 使用bom对一系列jar包进行封装，简化使用。
4. 从工程角度考虑项目结构，提高组织的开发效率。
