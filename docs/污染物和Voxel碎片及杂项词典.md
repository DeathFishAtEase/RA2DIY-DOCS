# 8.污染物和Voxel碎片及杂项词典
```{note}
因为语句过少，所以这些内容全部合在一个文件，顺便把一些内容并不太多的小教程也一并合入
```

## 污染物

```ini
[SmudgeTypes]
Crater=<boolean>
;是否为弹坑
Burn=<boolean>
;是否为烧焦痕迹
Width=<int>
;该污染物在↙↗方向上的占格
Height=<int>
;该污染物在↖↘方向上的占格
```
```{note}
污染物不是动画，无法使用动画相关语句，不是覆盖物，也无法使用 `[OverlayType] -> CellAnim`，这是显而易见的
```

## 对象
```{note}
泛指所有游戏内实体，包括但不限于四大类 Techno 与 Overlay、Terrain.etc

部分语句虽然列在 ObjectType 下，但对于特定子类而言部分语句显然是令人匪夷所思的，同样的也并非所有标签都能在所有子类上正常工作
```
```{hint}
以下标签均可在属性词典找到对应项，因此不作逐句翻译，仅添加部分特殊情况的注释
```
```ini
[ObjectTypes]
;===============================Rules===============================|
Image=<Image>
AlphaImage=<filename, excluding the .shp extension>
;原版下由TechnoType所挂的AlphaImage只有切屏才会刷新位置（Ares 0.1已修复）
;原版下由Animation所挂的AlphaImage存在无法正常移除等问题（Ares 0.5已修复）
CrushSound=<sound>
AmbientSound=<sound>
Crushable=<boolean>
;[TerrainType] -> Crushable=yes会有一些视觉错误
;-1-
;载具不会倾斜
;-2-
;需要切换镜头才能刷新图像
Bombable=<boolean>
NoSpawnAlt=<boolean>
AlternateArcticArt=<boolean>
RadarInvisible=<boolean>
;Phobos Build28前实际上TerrainType并不能正常使用这个功能，b28后进行了支持并将默认值从true改为false
Selectable=<boolean>
LegalTarget=<boolean>
Armor=<Armor>
Strength=<int>
Immune=<boolean>
Insignificant=<boolean>
HasRadialIndicator=<boolean>
RadialColor=<[R],[G],[B]>
;没蛋用，不少Terrain和Overlay的RadarColor数据直接都写在.tem文件里的
IgnoresFirestorm=<boolean>
;================================Art===============================|
UseLineTrail=<boolean>
LineTrailColor=<[R],[G],[B]>
LineTrailColorDecrement=<int>
;每帧的淡出量，游戏处于低细节级别时该值会×2
Theater=<boolean>
NewTheater=<boolean>
Voxel=<boolean>
```
```{important}
对应的，Particle 属于 Object 的子类，因此也可以在 art 中定义 `LineTrail`

故所谓 *Particle 无法在 art 中定义* 的言论是完全错误的，无非是作为 Particle 而无法使用独属于 Animation 的功能罢了
```

## Voxel 碎片
```{note}
有许多与 Shape 碎片（Animation）相通的语句，包括 `StartSound` 与 `StopSound`

在此仅列出 VoxelAnimType 专有部分和 VoxelAnimType 与 Animation 不同的部分
```
```ini
[VoxelAnimType]
Elasticity=<float>
;*对于 Voxel 碎片而言的确可以弹跳，并且会继承原有方向，默认0.8
Spawns=<VoxelAnimType>
;该 Voxel 碎片撞击后生成的子 Voxel 碎片类型
;似乎仅典型流星碎片可以正常生成子碎片，非流星和反向流星都不正常甚至还会导致007564BD
MinAngularVelocity=<float>
;Voxel 碎片在天上旋转的速率最小值
MaxAngularVelocity=<float>
;Voxel 碎片在天上旋转的速率最大值
;以上两条写太大可能会表现成只能在两帧间切换
Duration=<int>
;Voxel 碎片多少帧后消失，默认 30，有随机浮动
;这是一个对跳板玩家而言很有用的功能：
;因为与 Shape 碎片走完 End、LoopCount、SHPFileFrame、Rate 等决定的帧数后不同
;这句作用于 Voxel 碎片导致半空就爆炸的情况是可以正常生成 ExpireAnim 的！！！
;然而，与 Shape 流星碎片根据 MinZVel 决定起始生成位置未碰撞则不提前消失导致可以飞越原对象坐标的算法不同
;Voxel 流星如果为正整数（有限）Duration 则根据 Duration 与 ZVel 决定的速度区间决定从何处生成
;也就是说 Voxel 流星总会抵达原对象坐标位置然后爆掉。当然，反向流星可能因为撞地板提前引爆
MaxZVel=<float>
;碎片竖直速度的最大值，正数为向上飞，默认 15，该语句仅 Voxel 碎片拥有， Shape 碎片仅有 MinZVel
TrailerAnim=<animation>
;*对于 Voxel 碎片而言原版下会有一个竖直方向向上的偏移值
;并且偏移量大致根据 Voxel 碎片自身与地面高度差乘算而非固定值
;因此也曾用于一些使用特殊计算公式下调整 Animation 生成位置的特殊效果
;纯作为图像的话则通常换用 AttachedSystem 刷粒子来表现轨迹路径上的尾烟效果
AttachedSystem=<ParticleSystemType>
;Voxel 碎片的附加粒子系统，会在飞行轨迹上生成其设定的粒子
ShareSource=<TechnoType>
;从哪个单位的 Voxel 资源文件获取图像，需要下面三句至少一句否则仍用原规则
;如果是 DTRUCK 之类使用 Image 决定图像的单位则从其 Image 的对象调用
;想做一个载具被摧毁后脑袋飞上天的话这个逻辑是非常便利的
;并不检查目标单位的 Turret
;也就是写 V3ROCKET 用 ShareTurretData 去调用 V3ROCKETTUR.VXL 和 V3ROCKETTUR.HVA 也是可以的
;以下三句以本句设定 =HTNK 的情况举例
ShareBodyData=<bool>
;是否从这个 Voxel 资源文件的 Body 部分获取图像，也就是使用 htnk.vxl
ShareTurretData=<bool>
;是否从这个 Voxel 资源文件的 Turret 部分获取图像，也就是使用 htnktur.vxl
ShareBarrelData=<bool>
;是否从这个 Voxel 资源文件的 Barrel 部分获取图像，也就是使用 htnkbarl.vxl
;以上三句若不止一句为 yes 则只会生效一句，并且优先级 Body(本体)>Turret(炮塔)>Barrel(炮管)
VoxelIndex=<int>
;使用目标 Voxel 资源文件的哪个 Section
;例如 ShareSource=SHAD 下写 1 的话就是爆出螺旋桨
;如果 Image 或 ShareSource 调用的 Section 不存在则005AFB8B
;若是 Turret 的某个 Section 不存在则00756B2D
Image=<filename, excluding the .vxl extension>
;与 ShareSource 不同，可以直接写 HTNKTUR 这种形式
;但若对象不存在则007564BD
;而 ShareSource 则没有那么严格
;哪怕写个 TRUCKA 用 ShareTurretData 去调那并不存在的 Turret 文件也不会崩
;再甚至哪怕写个狗屁不通的 ShareSource=DTRUCKTUR 然后叠个 ShareBarrelData 去调 dtruckturbarl.vxl/hva 都只是没效果而已
```

## 矿石类型修改
```{note}
只有 4 类矿石，矿石实际以 `TIB` 开头的多个覆盖物的形式存在于地图上，而这个部分用于控制不同类型矿石生长和价值相关的数据
```
```ini
[Tiberiums]
0=Riparius;      ->  标准原版金矿
1=Cruentus;      ->  标准原版晶矿
2=Vinifera;      ->  原版金矿，实际上是第三类矿石，但是 Westwood 制作地图的时候常常与第一类标准金矿混用，可以使用 MapTools 的 "[Overlay] RA2 Fix Ore Types" 一条全部转换成第一类矿石
3=Aboreu  ;      ->  原版未使用，可以放心的作为新矿石类型且无需担心原版地图的兼容问题
;RA2 已经没有了那么丰富的泰伯利亚系列逻辑，但另两类矿石仍然可以用来做其他好玩的
;RA2 下矿井类 Terrain 只会生成该表中第一个 Tiberium 类型所对应的 Overlay，FS 与 Phobos 允许自定义

Name=<any str>
;无需多言
Image=[1|2|3|4]
;1 对应 OverlayType 内部表中 102 开始的 [TIB01]....[TIB20]
;2 对应 OverlayType 内部表中 027 开始的 [GEM01]....[GEM12]
;3 对应 OverlayType 内部表中 127 开始的 [TIB2_01]..[TIB2_20]
;4 对应 OverlayType 内部表中 147 开始的 [TIB3_01]..[TIB3_20]
;除 TS 中的蓝色泰伯利亚／ RA2 中的水晶矿仅 12 个外另 3 类多出的 8 个覆盖物用于该类型矿石延伸到斜坡上时使用，但 RA2 中已经禁用斜坡长矿
Power=<int>
;RA2 中无意义，TS 中泰伯利亚上高度低于 HoverHeight 的单位会持续受到 (Power/10) 的伤害
;Ares 0.5 已复原该逻辑，并且新语句允许使用负值伤害治疗单位和禁用特定类型矿石产生伤害，详见说明书，如果你获得本文档的同时没有配套这一文件，说明你的文档并非从原正式发布渠道获取，而是已经被第三方未经许可拆分修改过的
Value=25
;每 1 单位矿石的单价
Growth=<int>
GrowthPercentage=<float>
Spread=<int>
SpreadPercentage=<float>
;矿石生长与扩散相关的逻辑
*注：与 Terrain 产生矿石不同，这个是矿石覆盖物自身的生长而非借由其他对象生成
;Growth 是生长，即小矿石逐渐长成大矿石，每隔 Growth 帧有 GrowthPercentage 的概率生长一次
;Spread 是扩散，即矿石扩散到其他单元格，每隔 Spread 帧有 SpreadPercentage 的概率扩散一次
;上面四个值都设为 1 会见到矿石疯长
然后崩溃。
;因为 WW 这个逻辑处理的并不好，TS 里尚且一般，随后作为一个本就用不到但一直没删的逻辑跟着到 YR 里，稳定性再下一个台阶
;长太快很容易中后期莫名崩溃，或者一直不崩等到退出游戏或者重新开始任务的时候崩了
所以不建议设置太猛的数值
;如果真的需要长得特别快可以使用 [OverlayType] -> CellAnim 挂动画用碎片刷覆盖物的逻辑来模拟，而不是直接用这个
Color=<color scheme>
;当矿石类覆盖物使用 CellAnim 时强制其使用 unit 色盘并将其所属色映射为此处指定的配色方案
;不影响矿石的雷达图颜色，由覆盖物的 .tem 文件内部 RadarColor 数据决定，Phobos Build28 开始允许使用 MinimapColor 在此处定义
```

## 对战模式
```{tip}
对于使用 XNA CNCNet Client 的 MOD 而言应当使用客户端的模式 ini 配置
```
```{note}
就是原版 [巨富|海战|自由交战|.etc] 的修改

在 `mpmodesmd.ini` 中不同的 `[]` 中代表不同的多人游戏（与单人战役相对）类型

一般而言只需要在 `[Battle]` 中添加，例如：
```
```ini
[Battle]
9=GUI:TechLevelSpare, STT:ModeTechLevelSpare, TSpare.ini, techspare, true
```
|键值                    |含义
|------------------------|----
|9                       | 序号
|GUI:TechLevelSpare      | 模式选择和地图下面标注的模式
|STT:ModeTechLevelSpare  | 光标悬浮在这个模式上时底边栏的文本
|TSpare.ini              | 这个模式加载的模式 ini 文件
|techspare               | 这个模式的识别符<br>需要地图 `[Basic] GameMode=` 包含这个条目才能在这个模式使用这张地图<BR>例如直接填写 `standard` 就可以直接启用原版作战模式中的所有地图
|true                    | 这个模式是否允许使用随机地图生成器

## 音效相关
```{note}
文件为 `sound(md).ini`，新增音效需要加入注册表 `[SoundList]` 中
```
```ini
[SoundList]
+=NewSound

[NewSound]
Sounds=
;语音列表，对应文件名，若写多个则要在每个语音之间留一个空格并在各项前面添加“$”前缀
Volume=
;音量大小的百分比，填0-100的整数
Priority=[Lowest|Low|Normal|High|Critical]
;优先级，最低|低|中|高|紧急
;Sound 与 EVA 不同，EVA 是[Low|Normal|Important|Critical]
;TS 中的 Priority= 使用正整数值指定
;TS 不存在 eva(md).ini
FShift=
;频率浮动范围百分比，两个值代表 Min 和 Max，例如 FShift=-10 10 代表音效会使用比正常速度慢 10% 至比正常速度快 10% 的速度播放
VShift=
;音量浮动范围百分比，例如 Volume=45 而 VShift=10 那么浮动范围为 40%-50%
Limit=
;该音效在游戏中最多播放多少次

Control=[all|loop|random|predelay|interrupt|decay|ambient]
;控制方式
;all		按顺序播放 Sounds 列表中的每个
;loop		循环播放 Sounds 列表中的第一个
;random		在 Sounds 列表中随机选取一个播放
;predelay	搭配 Delay= 一句使用，见 Delay=
;interrupt	此音效可以打断其他正在播放的音效
;attack		进入音效
;decay		退出音效
;ambient	将声音视为环境音，无视 interrupt 效果

Delay=
;仅用于 Control=predelay，用于设定延迟时间，单位毫秒，两个值即为 Min 和 Max，若 Min>Max 则始终用 Min，若负值则会让音效只播放一次并且无延迟
Loop=
;仅用于 Control=loop，用于定义循环次数
Attack=7
;仅用于 Control=attack，用于指定前多少个音效用于淡入或循环开始
Decay=7
;仅用于 Control=decay，用于指定后多少个音效用于淡出或循环结束

Type=[ambient|violent|movement|quiet|loud|global|screen|local|player|normal|gun_shy|noise_shy|unshroud|shroud]
;播放类型
;ambient
;violent
;movement
;quiet
;loud
;global		全图所有玩家都可以听到
;screen		只有玩家视角内可见播放源时可以听到
;local		只能在播放源周围 Range 指定的距离内听到
;player		只有触发这个声音事件的玩家才能听到
;normal		无效果，正常的一批，无需多言
;gun_shy    覆盖其他效果，如果正在播放音量更大的音效那么这个音效不会播放
;noise_shy  覆盖其他效果，如果有正在播放其他音效那么这个音效不会播放
;unshroud   只有不在黑幕下时可以听到
;shroud     只有身处黑幕下时可以听到

MinVolume=
;仅用于 Type=global，用于定义最小音量
Range=
;仅用于 Type=local，用于指定可以听到音效的范围
```
```{note}
Westwood原有音效文件的命名约定如下：

i-步兵，a-环境，v-载具，u-用户界面，b-建筑，g-通用，s-超武，后接对象注册名的前（最多）三个字母

mo-移动，se-选择，att-攻击，fe-恐慌，pow-仅工程师断电，di/die-寄了，sta-载具启动，cra-战机坠毁
```
```{important}
注意文件应使用 wav 格式，采样率为 22050Hz，8 位或 16 位单声道，BGM 可以使用立体声
```
;by九千天华