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

- 查看当前系统路径下加载了哪些功能包
```bash
ros2 pkg list
```

##### 功能包 package
- 创建cpp功能包
    ```bash
    ros2 pkg create 包名 --build-type ament_cmake --dependencies rclcpp
    ```

- 创建python功能包
    ```bash
    ros2 pkg create --build-type ament_python --dependencies rclpy
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
    '可执行文件名 = python包名.模块名:函数名'
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

- 查看某个功能包中有哪些可执行文件
```bash
ros2 pkg executables 可执行文件名
```

##### 可执行文件 executable
- 运行某个可执行文件
```bash
ros2 run 功能包名 可执行文件名
```

#### 系统结构
##### node

##### 通信
- 话题 topic
    - 特点
    - 命令
        - 查看有哪些话题
        ```bash
        ros2 topic list
        ```

        - 查看某个话题的信息
        ```bash
        ros2 topic info 话题名
        ```

        - 查看某个话题的详细信息
        ```bash
        ros2 topic info 话题名 -v
        ```

        - 打印某个话题
        ```bash
        ros2 topic echo 话题名
        ```

        - 打印某个话题一次
        ```bash
        ros2 topic echo 话题名 --once
        ```

        - 测量话题的发布频率
        ```bash
        ros2 topic hz 话题名
        ```

        - 使用命令行发布某个话题
        ```bash
        ros2 topic pub 话题名
        ```

- 服务 service
    - 特点
    - 命令
        - 查看有哪些服务
        ```bash
        ros2 service list
        ```

        - 查看某个服务的类型
        ```bash
        ros2 service type 服务名
        ```

- 动作 action
    - 特点
    - 命令
        - 查看有哪些动作
        ```bash
        ros2 action list
        ```

        - 查看某个动作的信息
        ```bash
        ros2 action info
        ```        

##### 坐标变换 tf(特殊通讯途径)

##### 参数(特殊通讯途径)
- 命令行
- yaml

#### 其他功能和相关开发工具
##### launch启动方式
- 命令
    使用launch启动
    ```bash
        ros2 launch 功能包名 xxx.py
    ```
##### rqt
##### rviz2
##### gazebo