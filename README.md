- 👋 Hi, I’m @tdchen1998
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
tdchen1998/tdchen1998 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
```mermaid
sequenceDiagram
    participant Admin 
    participant HubConfig 
    participant DeviceManager 
    participant HubMapper
    participant FlashWorker 
    participant Device 

    Note over Admin,HubConfig: 1. 初始化阶段
    Admin->>HubConfig: 运行Hub扫描工具
    HubConfig->>HubConfig: 扫描USB Hub
    HubConfig->>HubConfig: 生成hub_mapping.yaml
    
    Note over DeviceManager,Device: 2. 运行阶段
    Admin->>DeviceManager: 启动监控
    activate DeviceManager
    DeviceManager->>HubMapper: 加载Hub映射
    
    loop 设备监控循环
        HubMapper->>HubMapper: 扫描已配置Hub端口
        alt 发现新设备
            DeviceManager->>Device: 创建设备实例
            DeviceManager->>FlashWorker: 启动刷机任务
            activate FlashWorker
            
            FlashWorker->>Device: 1. 刷入系统(20%)
            FlashWorker->>Device: 2. 检测传感器(40%)
            FlashWorker->>Device: 3. 安装Magisk(60%)
            FlashWorker->>Device: 4. 安装模块(80%)
            FlashWorker->>Device: 5. 配置系统(90%)
            FlashWorker->>Device: 6. 安装APK(100%)
            
            deactivate FlashWorker
        end
        
        alt 设备断开
            DeviceManager->>Device: 更新设备状态
            DeviceManager->>Device: 记录结束时间
        end
        
        DeviceManager->>DeviceManager: 更新显示进度
    end
    deactivate DeviceManager
```
