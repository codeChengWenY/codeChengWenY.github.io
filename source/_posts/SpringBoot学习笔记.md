SpringBoot学习笔记

1 约定大于配置



2 实现自动配置 

1. springbok应用启动
2. @ Spring Bootapplication起作用
3. @Enableauto Configuration
4. @ AutoConfigurationpackage：这个组合注解主要是@ import( Autoconfigurationpackages. Registrar. class),它通过将 Registrar类导入到容器中，而registrar类作用是扫描主配置类同级目录以及子包，并将相应的组件导入到springboote创建管理的容器中
5. @ import( AutoConfigurationlmportselector. class):它通过将
   Autoconfigurationlmportselector类导入到容器中， Auto Configurationlmportselector类作用是
   通过 electlmports，方法执行的过程中，会使用内部工具类 Springfactoriesloader，查找
   classpath上所有jar包中的META-INF/ spring, factories进行加载，实现将配置类信息交给
   Springfactory加载器进行一系列的容器创建过程  