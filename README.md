配电网线路与节点数据说明
本项目包含一个用于配电网模拟与规划研究的数据集，涵盖典型的馈线结构，包含线路（branch）参数与节点（node）信息。该数据可用于电力系统潮流计算、运行仿真、规划优化等场景，适配多种电力系统分析框架（如 OpenDSS、Pandapower、Matpower 等）。

📁 数据结构说明
数据文件主要包含两个核心部分：

1. branch_data
描述配电网中各条支路的参数，包括阻抗、容量、运行状态等。

字段含义：
字段名	含义	类型	单位
R	电阻（Resistance）	float	Ω
X	电抗（Reactance）	float	Ω
capacity	最大可承载容量	float	MVA
status	当前状态（closed/open）	string	-
expandable	是否支持扩容	boolean	-

示例：
json
复制
编辑
"branch_data": {
    "1152,15211": {
        "R": 0.0065,
        "X": 0.004,
        "capacity": 4.7,
        "status": "closed",
        "expandable": false
    }
}
2. node_data
描述各节点的类型、负荷、电压限制以及地理坐标信息。

字段含义：
字段名	含义	类型	单位
type	节点类型（如 load / substation）	string	-
Pd	有功负荷	float	MW
Qd	无功负荷	float	MVar
capacity	节点容量（如适用）	float/null	MVA
Vmin	最小允许电压幅值	float	p.u.
Vmax	最大允许电压幅值	float	p.u.
x, y	节点的平面坐标（用于可视化）	float	-

示例：
json
复制
编辑
"node_data": {
    "13507": {
        "type": "substation",
        "Pd": 0.0,
        "Qd": 0.0,
        "capacity": 5.0,
        "Vmin": 0.9,
        "Vmax": 1.1,
        "x": -10,
        "y": -2
    },
    "15211": {
        "type": "load",
        "Pd": 1.27,
        "Qd": 0.37,
        "capacity": null,
        "Vmin": 0.9,
        "Vmax": 1.1,
        "x": 9,
        "y": -2
    }
}
✅ 使用方式
将数据结构加载为 JSON 或 Python 字典；

可用于：

配电网可视化；

潮流分析建模；

节点负荷优化与运行决策；

配电网规划算法验证等；

推荐工具/库：

networkx / matplotlib：构建与绘图；

Pandapower：潮流与规划分析；

OpenDSS：配电网仿真与控制策略测试。

📌 注意事项
所有参数单位需保持一致；

capacity = null 表示该字段在该节点不适用；

节点坐标仅用于地图或可视化场景；
