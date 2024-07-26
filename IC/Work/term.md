## PDK
Process Design Kit, 工艺设计套件。
PDK 包含了反映制造工艺基本的元素：晶体管、接触孔，互连线等。PDK 的内容中包括设计规则文件、电学规则文件、版图层次定义文件、SPICE 仿真模型、器件版图和期间定制参数等。
## CDF
Component Description Format, 组件描述格式。
器件的属性描述文件，它定义了器件的类型、名称、参数，以及参数调用关系函数集 Callback、器件模型、器件的各种视图格式等等
## Pcell
Parameterized Cell，参数化单元。
描述晶体管（及其他器件）的可能定制方法，供设计师在 EDA 工具中使用
## TechnologyFile
技术文件。
用于版图设计和验证的工艺文件，包含 GDSII 的设计数据层和工艺层的映射关系定义、设计数据层的属性定义、在线设计规则、电气规则、显示色彩定义和图形格式定义等。
## Memory Compiler
memory 分为两类 RAM 和 ROM。RAM 根据读写端口个数又分为三类即单端口 RAM（SP single port），伪双端口 RAM（TP triple port）和双端口 RAM（DP double port）。SP 只存在一个时钟和一套读写端口，读写复用地址总线，读写不能同时操作。TP 存在两个时钟（读、写）和一套读写端口，但是有各自地址总线，读写可以同时操作。DP 存在两个时钟和两套读写端口，每一套端口都支持读写操作，这两套操作互补影响。
一般的 memory compiler 提供五个 ram 脚本（rf_sp,sram_sp,rf_tp,sram_dp,rom）。考虑面积和性能又划分为 High Speed 和 High Density。
## CCI
calibre connectivity interface。
利用 calibre 的 lvs 结果，通过 calibre 的 CCI（calibre connectivity interface）生成 starrc 后提所需要的一些文件，然后 StarXtract 进行反标
https://bbs.eetop.cn/thread-557593-1-1.html
## CC
Couple C 寄生电容
## cdl
Circuit Description Language 电路表述语言，及网表。
## OBS
Obstruct
OBS 代表 cell 的不可布线区域，每个 standard cell 以及 memory 都有它的 OBS 区域，定义在 LEF 文件中，对 standard cell 来说，OBS 经常是底层 metal 的某一块区域，代表着工具不能在该区域走线，有点类似 routing blockage。Memory 以及其他 IP 的 OBS 区域面积更大，通常是除了单元端口以外的其他整个高层区域。
https://blog.csdn.net/Tao_ZT/article/details/102456373
## lvs
layout vs. schematic
## lvl
layout vs. layout
## lpe
layout post extract 抽后仿网表
## QA
Quality Assurance（质量保证、验证）
## lvt/hvt/svt=rvt/ulvt=slvt
low/high/standard=regular/ultra=super low vth（低/高/标准/超低阈值电压）
## sd/ds/ls
shut down(sd)，deep sleep(ds), light sleep(ls)
## vdd/vddp/vddc
vdd为mc工作电压，vddp为外围电路电压，vddc为cell array电压.
如果有低功耗 memory retention 的需求，则两个电源分开供给；在低功耗模式下，可以关闭 VDDP，同时给 VDDC 供电以保持 memory 内容.
这两个一般是同一个电压，没有特殊要求的话可以接到一起，有的 sram 内部有 power switch 可以在内部关断电源来节省功耗。如果这个两个电压想要在 sram 外部分开控制开关，就复杂很多，也需要电路设计支持此功能的控制。
在 power management 或者 power sequence 或者 pin description 相关的章节有描述吧。
memory 一般有 bit cell array（core 区）和 peripheral circuits （peripheral 区） 两大部分，根据不同的功耗需求，形成两种供电方式，一种 single-rail  就是 core 和 peripheral 共用一个电源。
另一种就是 dual-rail 两个区域分别供电，方便进行 power management。
还有其他 bias 相关的 vdd。
提到的这几个电源，估计是
VDD    -----  single rail 的 vdd
VDDCE -----  core vdd
VDDPE  -----  peripheral vdd
## xrc/qrc/starrc
xrc 是 mentor 公司的 calibre 提后仿
QRC 是 cadence 公司的 Assura 提后仿
starrc 是 Synopsys 公司的 Hercules 提后仿
calibre LVS + QRC  -> QCI flow(Mentor EDA + Cadence EXT EDA)
calibre LVS + Star RC -> CCI flow(Mentor EDA + Synopsys EDA)
https://bbs.eetop.cn/thread-867813-1-1.html
## cci/qci
CCI 是只用 CALIBRE 做 LVS，然后用 STARRC 作寄生抽取的流程
QCI 的流程，也是先用 calibre 做 LVS，然后用 QRC 去做寄生抽取
https://bbs.eetop.cn/thread-846836-1-1.html
## PEX
post extract
## LPE
layout post(parameter) extract
## ckt
circuit 电路
## subckt
sub-circuit 子电路
## lut
look up table 查找表
## leafcell
For hierarchical design, leafcell is minimum cell, topcell is maximum cell
https://bbs.eetop.cn/thread-261994-1-1.html
## flatten vs. Hierarchy
版图设计从 TOP 到 BLOCK 到器件，是一级一级往下的，这是一个 Hierarchy 结构，当你在一个 layout 窗口操作，选中一个或多个 cell-->Hierarchy-->flatten-->one level 把选中的目标向下打散一级 --〉display level 是把选中的目标不管向下还有几级，全部打散，看到的是各个 LAYER 图形。
https://bbs.eetop.cn/thread-635259-1-1.html
大电路，用 flat 主要是为了防止别人有你的网表，推你的电路。ip 给出去的时候，高级用户可以得到 flat 的网表和 flat 的 layout。 大电路有这些东西反推到电路图，是很痛苦的事。
https://bbs.eetop.cn/thread-55517-1-1.html
## hcell
hierarchically corresponding cell，我把它翻译为层次化对应的单元。
hcell 是 GDS 与 netlist 的名称对应, 即声明版图的哪些模块和电路的哪些模块是一一对应关系，主要用于 lvs 做层次化检查。就是一个黑盒子，顶层只要 port 信息，内部的不管你如何，只要保证和 port 相关的没有问题就好了。
```
/ layout_name source_name
```
## MOM
metal oxide metal 电容
## ds
.ds: datasheet 数据手册