#### 总是需要的配置
<details>
##### debug模式
出问题看https://www.baud-dance.com/docs/stm32/FAQ/CompilationFailed/

##### 时钟源时钟树
时钟源的HSE选择Crystal/Ceramic Resonator
时钟树配置主频其余可自动配置

##### 工具链
Cmake

##### 为每个外设生成单独的.c/.h文件
勾选
</details>