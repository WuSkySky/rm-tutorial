#### 项目结构
<details>

##### 工作空间 workspace
<details>
构建工作空间下的所有功能包
```bash
colcon build
```

构建工作空间下的指定的功能包
```bash
colcon build --packages-select 包名1 包名2
```

查看当前系统路径下加载了哪些功能包
```bash
ros2 pkg list
```
</details>

##### 功能包package
<details>

创建cpp功能包
```bash
ros2 pkg create 包名 --build-type ament_cmake --dependencies rclcpp
```

创建python功能包
```bash
ros2 pkg create 包名 --build-type ament_python --dependencies rclpy
```
</details>

##### 可执行文件 executable
<details>

添加可执行文件 cpp构建的功能包
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

添加可执行文件 python构建的功能包
在```setup.py```中添加
```
'可执行文件名 = python包名.模块名:函数名'
```

添加依赖 cpp构建的功能包
1. 在```package.xml```添加```<depend> NAME </depend>```
2. 在```CMakeLists.txt```添加```find_package(NAME REQUIRED)```
3. 在```CMakeLists.txt```添加
    ```
    ament_target_dependencies(
    可执行文件名
    依赖名
    )
    ```

添加依赖 python构建的功能包
1. 在```package.xml```添加```<depend> 依赖名 </depend>```
2. 在```setup.py```中的```finstall_requires```添加```'依赖名'```

查看某个功能包中有哪些可执行文件
```bash
ros2 pkg executables 可执行文件名
```

运行某个可执行文件
```bash
ros2 run 功能包名 可执行文件名
```
</details>

</details>

#### node
<details>

最小实现
```py
import rclpy
from rclpy.node import Node

class NODE_CLASS(Node):
    def __init__(self, name):
        super().__init__(name)

def main(args=None):
    rclpy.init(args=args)
    node = NODE_CLASS(NODE_NAME)
    try:
        rclpy.spin(node)
    except KeyboardInterrupt:
        pass
    finally:
        node.destroy_node()
```

</details>


#### 通信
<details>

##### 通用

<details>

查看某个类型的字段结构
```bash
ros2 interface show geometry_msgs/msg/Pose
```

</details>

##### 话题 topic
<details>

最小实现
<details>

订阅者 QOS可以填10
```py
self.sub = self.create_subscription(
    TYPE,
    NAME,
    CALLBACK,
    QOS,
)
```

发布者 创建 QOS可以填10
```py
self.pub = self.create_publisher(TYPE, TOPIC_NAME, QOS)
```

发布
```py
msg = TYPE()
msg.FIELD1​ = DATA
msg.FIELD2​ = DATA

self.pub.publish(msg)
```

</details>


命令
<details>

查看有哪些话题
```bash
ros2 topic list
```

查看某个话题的信息
```bash
ros2 topic info 话题名
```

查看某个话题的详细信息
```bash
ros2 topic info 话题名 -v
```

打印某个话题
```bash
ros2 topic echo 话题名
```

打印某个话题一次
```bash
ros2 topic echo 话题名 --once
```

测量话题的发布频率
```bash
ros2 topic hz 话题名
```

使用命令行发布某个话题
```bash
ros2 topic pub 话题名
```
</details>

</details>

##### 服务 service
<details>

查看有哪些服务
```bash
ros2 service list
```

查看某个服务的类型
```bash
ros2 service type 服务名
```

</details>

##### 动作 action
<details>

查看有哪些动作
```bash
ros2 action list
```

查看某个动作的信息
```bash
ros2 action info
```
</details>

</details>        

#### launch
<details>

luanch最小实现
```py
from launch import LaunchDescription

def generate_launch_description():
    ld = LaunchDescription()

    return ld
```

启动node
```py
node = Node(
    package='PKG_NAMW',
    executable='EXE_NAME',
    name='NODE_NAME',
    remappings=[
        (FROM, TO)
    ]
)
ld.add_action(node)
```

启动其他launch
```py
launch_file = os.path.join(
    get_package_share_directory('PKG_NAME'), 
    'launch',                      
    'LAUNCH_NAME'                
)

launch = IncludeLaunchDescription(
    PythonLaunchDescriptionSource(launch_file)
)

ld.add_action(launch)
```

执行命令行命令
```py
cmd = ExecuteProcess(
    cmd=[CMD1, CMD2],
    name=NAME,
)
ld.add_action(find_can_cmd)
```

使用launch启动
```bash
ros2 launch 功能包名 xxx.py
```

</details>