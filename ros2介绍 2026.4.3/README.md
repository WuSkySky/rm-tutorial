#### ros2 是什么
##### 先对 ros2 建立一个基本认识(先有一个基本的模型)
##### ros2 可以解决什么问题

#### 项目结构
##### 工作空间 workspace
- 构建工作空间下的所有功能包
    ```bash
    colcon build
    ```
- 构建工作空间下的指定的功能包
    ```bash
    colcon build --packages-select 包名1 包名2
    ```
##### 功能包 package
- 创建cpp功能包
    ```bash
    ros2 pkg create 包名 --build-type ament_cmake --dependencies rclcpp
    ```

- 创建python功能包
    ```bash
    ros2 pkg create --build-type ament_python --dependencies rclpy my_py_pkg
    ```

- 添加可执行文件 cpp构建的功能包
1. 在```CMakeLists.txt```中添加
    ```
    add_executable(
        可执行文件名
        文件1路径
        文件2路径
    )
    ```
2. 在```CMakeLists.txt```中添加
    ```
    install(TARGETS 可执行文件名
        DESTINATION lib/${PROJECT_NAME}
    )
    ```

- 添加可执行文件 python构建的功能包
    在```setup.py```中添加
    ```
    '可执行文件名 = python包名.模块名.函数名'
    ```
- 添加依赖 cpp构建的功能包
1. 在```package.xml```添加```<depend> NAME </depend>```
2. 在```CMakeLists.txt```添加```find_package(NAME REQUIRED)```
3. 在```CMakeLists.txt```添加
    ```
    ament_target_dependencies(
    可执行文件名
    依赖名
    )
    ```

- 添加依赖 python构建的功能包
1. 在```package.xml```添加```<depend> 依赖名 </depend>```
2. 在```setup.py```中的```finstall_requires```添加```'依赖名'```

##### 节点 node

#### 通信方式
##### 话题 topic
##### 服务 service
##### 动作 action

#### 坐标变换 tf

#### 参数
##### 命令行
##### yaml

#### launch启动方式



```bash
ls
cd 
```