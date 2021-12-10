## 什么是单元测试


In computer programming, unit testing is a software testing method by which individual units of source code—sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures—are tested to determine whether they are fit for use  _ wikipedia


对一个函数，模块，类进行运行结果正确性检验的工作就是单元测试，此外每个单元测试的对象应该是一个最简单的组件/函数。


- TDD (Test driven development)



> 测试驱动开发，在书写业务代码之前，先根据需求进行单元功能测试用例书写



这里驱动开发的测试不是简单的测试用例，即为能够持续验证、重构并且对需求功能极致细化的测试用例


- BDD (Behavior driven development)



> 行为驱动开发，通过具有辨识力的测试用例驱动项目开发团队所有人，使用自然语言来描述功能



单元测试的书写初期必定伴随着大量精力与时间的消耗，但长期持续维护的业务在搭建并完善好整个单元测试系统后，可大大提高项目稳定性和研发效率


## 前端单元测试


### 前端测试框架


- Karma
- Mocha: 功能丰富的 javascript 测试框架，运行在node.js和浏览器中
- Jest



### 测试断言库


- chai  expect()，assert()和should风格的断言
- should  BDD风格贯穿始终
- expect expect()样式断言
- assert Node.js 内置断言模块



[https://kulshekhar.github.io/ts-jest/docs/processing](https://kulshekhar.github.io/ts-jest/docs/processing)


在众多前端单元测试框架中，jest 目前凭借零配置，且对于断言，快照，覆盖率等都有很好的集成，目前是较为流行的一个单测框架


### jest 框架运行原理


这里我们简单来看下 jest 框架的特点以及大致的运行原理


jest 的整体框架特点大概归纳总结为以下几点:


- 在操作系统上高效的进行文件搜索以及相互依赖关系匹配
- 并行运行所有测试
- 内置断言框架进行测试编写同时进行结果断言
- 测试之间相互隔离，vm module 来进行沙河环境隔离



jest pacakges中大概有50多个包，这里我们挑选一部分包来做下介绍


通过 console 配置进行console的覆盖


第一步 jest-cli 读取配置
jest-cli require('../build/cli').run()


jest/core/build/cli/runCli


执行 jest-config 中的 readConfig方法 读取获得 configs


jest-cli  (读取) jest-config


jest-haste-map 分析项目并检索项目中的所有文件，获取项目中所有文件相互之间的依赖及它们之间的关系


- 爬行整个项目进行文件依赖分析和提取，根据当前cpu核数并行
- 只执行最小单元的内容，例如某个单测文件变动了只执行该单测文件
- 实时监听整个文件系统的变化，可以做一些实时交互的工作



fb-watch-man


jest-worker


7 search srouce （find tests to run）


Array
Test 包含 Path duration Context


8 Test Sequencer 大概是 test 执行顺序的确定？failed > duration > size  TestPriority ?


9 Test Scheduler


10 jest runner


runTests 方法, 使用jest-worker 中的 Worker 对象 new Worker，创建多个worker thread 或者是 child process 池子来进行 test parallel 执行


11 jest-jasmine jest-circus 提供 describe it 等API


12 jest-runtime  vm  require


12 jest-environment 提供沙盒环境的global   （resolvtion mocking transforms） 同步执行


test result


ts-jest 配置 babelConfig: true，来开启读取babel.config.js配置


## 小程序中的单元测试


### 小程序单元测试所依赖工具库


- miniprogram-simulate
- j-component
- miniprogram-exparser
- miniprogram-compiler



## Mpx 框架单元测试


## 简单的单元测试书写


对于单元测试的编写效率提升：


## 单元测试覆盖率


## 问题记录


### ts-jest 中 支持 require.context


### transform memory string code(require from string)


### moduleMapper 配置


### ts 部分的支持


### Mpx SPA 形式支持


### ts-jest 开启 babelConfig 对 ts 文件走一遍 babel-jest，主要解决require.context的问题


### 微信特有的全局变量通过继承 jest-environment-jsdom 来进行设置


Mpx 中的 computed watch 放到了实例的data，什么时候挂上去的呢？


- navigateTo 跳转测试下 wx
- resolve 形式下 测试 relations
- 单元测试支持 mode&env模式
- mpx.xxxx api 调用支持 mpx use api-proxy
- this.$t 等 i18n 功能支持
- 单元测试对网络请求进行手动mock



chunkAsset


assetEmit


file


key 对应 filename， 通过webpack提供的缓存检测钩子 进行 hash 检测 缓存是否生效，同时value对应的是上次检测结果
