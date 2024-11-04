# AutoFish 自动钓鱼

- 作者: 羽学 少司命
- 出处: 无
- 这是一个Tshock服务器插件，主要用于：
- 自动钓鱼，当插件开启时会所有无视渔力与鱼饵力，
- 随机钓出本环境物品或【额外渔获】里的物品
- 可通过配置文件调整鱼钩数量，
- 消耗指定物品来换取插件使用时长，
- 还可以自定义配置钓鱼的额外物品。
- 配备完整的指令系统:管理与玩家可见的菜单指令是不一样的
- 甚至有些功能没开启是不会显示相关指令的
- 本插件无法在血月钓任何NPC请注意使用指令关闭

## 更新日志

```
v1.3.0
修复了首选鱼饵不会消失,变成无限饵,或卡线程BUG
修改了额外渔获也能与其他环境已存在的物品一起上钩
重构了消耗模式的代码逻辑，优化性能。
修复了消耗模式在背包里将手持物品乱放，
导致自动满足消耗数量，开启自动钓鱼的BUG

加入了设置多钩数量的指令：/af duo 数量
加入了额外渔获表的相关指令
把/af buff指令改为玩家可用，用来切换自身BUFF

v1.2.0
修复了钓鱼不消耗鱼饵问题
修复了鱼饵数量为1时线程卡住问题
加入了【消耗模式】配置项
加入了【钓鱼BUFF】配置项（上钩才会触发）
消耗模式为1.1.0版的扣除物品数量获取自动时长逻辑
完善了自动钓鱼的指令系统，并对其做了不同权限与模式下的内容显示

v1.1.0
成功完成Tshock版《自动钓鱼》，
加入了消耗鱼饵数量来换取自动钓鱼使用时长的逻辑
当身上有松露虫时，会自动钓上铁镐，并试图关闭玩家的自动钓鱼开关
玩家可通过/af on指令重新开启插件，并不会清空玩家的自动钓鱼时长

v1.0.0
试图制作Tshock版《自动钓鱼》，而失败的半成品：
服务器无法修改客户端玩家的操作，更没有相对数据包来处理上钩的状态。
尝试从AI[0]改为1来触发收线效果，但无法获取到实际的渔获。

```

## 指令

| 语法                             | 别名  |       权限       |                   说明                   |
| -------------------------------- | :---: | :--------------: | :--------------------------------------: |
| /af  | /autofish |   autofish    |    指令菜单（查询自动钓鱼所剩时长）    |
| /af on  | 无 |   autofish    |    开启玩家自己的自动钓鱼    |
| /af off  | 无 |   autofish    |    关闭玩家自己的自动钓鱼    |
| /af list  | 无 |   autofish    |    列出消耗模式指定物品表    |
| /af loot  | 无 |   autofish    |    列出额外渔获表   |
| /af buff  | 无 |   autofish    |    开启或关闭玩家自己的钓鱼BUFF    |
| /af more  | 无 |   autofish.admin    |    开启或关闭多线模式   |
| /af duo 数量  | 无 |   autofish.admin    |    设置多线的钩子数量   |
| /af + 物品名  | 无 |   autofish.admin    |    为额外渔获添加物品   |
| /af - 物品名  | 无 |   autofish.admin    |    为额外渔获移除物品   |
| /af mod  | 无 |   autofish.admin    |    开启或关闭消耗模式   |
| /af set 数量 | 无 |   autofish.admin    |    设置消耗物品数量要求    |
| /af time 数字  | 无 |   autofish.admin    |    设置消耗自动时长    |
| /af add 物品名  | 无 |   autofish.admin    |    添加消耗指定物品    |
| /af del 物品名  | 无 |   autofish.admin    |    移除消耗指定物品    |
| /reload  | 无 |   tshock.cfg.reload    |    重载配置文件    |

---
配置注意事项
---
1.本插件的权限名为`autofish` 你可以输入 `/group addperm default autofish`给玩家添加权限

2.`消耗模式`为1.1.0版本特性:消耗物品来换取自动钓鱼使用时长的逻辑，人多环境下可能存在性能问题。

3.`多钩钓鱼`为自动钓鱼开启连发模式，让钓鱼效率更高，`多钩上限`定义最多可以多少鱼钩同时自动钓
  
4.`消耗数量`为消耗多少个物品数量来换取玩家自动钓鱼使用`自动时长`，时长单位为`分钟`，可通过/af菜单指令查看

5.`消耗物品`为指定消耗的物品ID，用于开启自动钓鱼功能用。

6.`额外渔获`当其开启时，会无视环境要求和鱼获检查，钓上这个数组里的随机物品

## 配置
> 配置文件位置：tshock/自动钓鱼.json
```json
{
  "插件开关": true,
  "多钩钓鱼": true,
  "多钩上限": 5,
  "广告开关": true,
  "广告内容": "\n[i:3456][C/F2F2C7:插件开发] [C/BFDFEA:by] [c/00FFFF:羽学] | [c/7CAEDD:少司命][i:3459]",
  "Buff": {
    "80": 10,
    "122": 240
  },
  "消耗模式": false,
  "消耗数量": 10,
  "自动时长": 24,
  "消耗物品": [
    2002,
    2675,
    2676,
    3191,
    3194
  ],
  "额外渔获": [
    75,
    29,
    3093,
    4345
  ]
}
```
## 反馈
- 优先发issued -> 共同维护的插件库：https://github.com/UnrealMultiple/TShockPlugin
- 次优先：TShock官方群：816771079
- 大概率看不到但是也可以：国内社区trhub.cn ，bbstr.net , tr.monika.love
