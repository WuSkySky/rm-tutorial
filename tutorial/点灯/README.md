#### 原理图

#### CubeMX介绍

#### 总是需要的配置
参考documentation/stm32.cd

#### GPIO

#### 项目结构

#### 可以了解一下
##### 引脚复用

##### 引脚重映射

#### QNA
- 点灯失败
    注意有些参数不能想当然,GPIO_PIN_x,不能直接填引脚编号对应的数字,而应该查看函数文档
    ```C
    HAL_GPIO_WritePin(GPIOC, GPIO_PIN_13, GPIO_PIN_SET); // 正确的
    HAL_GPIO_WritePin(GPIOC, 13, GPIO_PIN_SET); // 错误的
    ```
    函数文档写了怎么传参
    ```C
    /**
    * @param  GPIO_Pin: specifies the port bit to be written.
    *          This parameter can be one of GPIO_PIN_x where x can be (0..15).
    */
    ```
