# 2.单位属性rules词典
```{hint}
前言，单位属性代码一大堆，绝对不要试图在本文中摘取代码从空白开始写单位，请复制原版已有的单位进行修改
```
```ini
 -A-
Accelerates =
可以设置为"yes"或者"no"来决定这个单位移动式是否慢慢加速至Speed定义的速度
与高级碾压（MovementZone=CrusherAll）共用有时候会莫名奇慢无比
AccelerationFactor =
填数值。这个代码要配合[TechnoType] -> Accelerates=yes使用，指定单位运动中加速的百分比，用小数表示，如设置为“.1”
ActivateSound =
单位被激活的音效，默认全局值
Adjacent =
填数值。这个代码指定建筑距离另一个[BuildingType] -> BaseNormal=yes的建筑在多少个单元格距离内可以放置，默认3。
Agent =
填yes或no。这个代码指定步兵单位是否为间谍单位，用于渗透[BuildingType] -> Spyable=yes的建筑获得不同效果
AIBasePlanningSide =
写阵营序号(0=GDI,1=Nod,2=ThirdSide，Ares新阵营依次往后排)，标明第几个阵营会建造该建筑(写-1时所有阵营都可造)
AIBuildThis =
填yes或no。这个代码指定建筑是否可以被AI所建造，但是只会在<=1个时造1次（通过克隆生产同时拔起多个），Ares已允许定义数量，详见说明书
如果建造厂这句写no那么Ares下AI最多出一个电厂，原版则会崩溃
AirportBound =
可以设置为"yes"或"no"来决定这个战机是否需要一个机场（通常是指一个带有[BuildingType] -> Helipad=yes的建筑物）的机位，如果没有机位，这个战机将会坠毁。这个战机一定要在PadAircraft=后面声明，否则会出现建造不受机位限制的问题
由于WW在RA2删了没机位时战机从地图外飞来的效果，现在不在[General] -> PadAircraft=声明的战机把机位满后你却不拉出去的话图标虽然依然不会灰掉，但是点下去会卡在一半的位置并且无法取消
如果没有武器还会有一些特殊的运动表现
AirRangeBonus =
单位瞄准空中目标时的额外射程，不影响攻击时仍会尝试将目标套进[WeaponType] -> Range=的范围
但追击目标时用上此句可以防止追一步停一步，搭配[TechnoType] -> OpportunityFire=yes食用效果奇佳
AllowedToStartInMultiplayer =
填yes或no。这个代码指定单位是否可以在游戏开始时伴随基地车出现（如苏军开始时的动员兵、犀牛坦克）。根据单位的Owner进行分配，会自动寻找距离预定位置最近且符合MovementZone的区域，例如出生点周围全是陆地那么船会生成在最近的岸边
AlternateArcticArt =
填yes或no。这个代码指定步兵单位是否在雪地地图和陆地地图有两种不同的形态，如盟军的海豹部队。注意：如果填yes，该步兵单位就必须准备一个雪地型的步兵文件（SHP文件），并且命名规则为：该单位的温和地图形态+A.SHP，如海豹部队的温和地图形态文件名为SEAL.SHP，那么雪地地图形态文件名则为SEALA.SHP。Ares已扩展该逻辑到所有气候，但需要使用新的语句，详见Ares说明书
AmbientSound =
填Sound.ini中定义的声音名。这个代码指定该单位在地图上存在的声音。注意：这个声音会在该单位被摧毁前不停播放，声音太大可能会影响人类玩家进行游戏
Ammo =
填数值。这个代码指定该单位的弹药数量。战机不能自动装填弹药，需要在机场降落后进行装填。默认为负一，无限
对于Aircraft类则是按开火行为计算，也就是因为乘客而将开火换为踹乘客、五连发抛射体一轮攻击射了5次武器等等均按1Ammo来计算，对应的Ares的自定义武器消耗弹药量也对Aircraft无效
并且Aircraft存在多种一样（一坨又一坨）的弹药计算规则，例如如果一个战机的剩余弹药量高于总弹药量的一半并且有目标那么它无法正常装填弹药（AI：这个我熟）
原版下Infantry和Building的弹药逻辑基本是废的，Ares已修缮与完善并进行了拓展，详见说明书
Armor =
填下表中的相应项。这个代码指定该单位的装甲。注意：装甲和防御能力没有任何关系，单位的受伤程度是由攻击方的弹头对相应装甲的百分比决定
------------------------------------------------
None 无护甲，不是“不存在护甲”而是使用名为“none”的护甲参与计算，物体必然拥有护甲
Flak 防弹衣
Plate 板甲
Light 轻型装甲
Medium 中型装甲
Heavy 重型装甲
Wood 木质结构
Steel 钢铁结构
Concrete 混凝土结构
special_1 特殊装甲1，用于恐怖机器人
special_2 特殊装甲2，用于子机导弹
装甲和单位类型不存在硬性对应关系，可以随意指定
------------------------------------------------
Artillary =
填yes或no。这个代码指定建筑是否为载具通过DeploysInto部署后变成的建筑并且载具部署前转向正北方
四句里这一句会导致vxl炮塔在Buildup时就绘制
部署转向：
Artillary↗
TickTank↘
IsJuggernaut↙
ICBMLauncher↘
怀疑原定有朝向↖的但是代码没写对，YR下疑似朝向效果全部报废，请用YR新增的[BuildingType] -> DeployFacing=[0-7]来控制
Armory =
填yes或no。这个代码指定建筑是否可以升级精英以下的步兵单位，任何进入该建筑的步兵单位都会升级为精英
注意：如果想限制升级步兵的数量，可以加入Ammo=来限制，Ammo=的数值为你想要的限制数量
在Ares中允许使用新的Academy系列逻辑直接设定所有单位生产出来的等级
Assaulter =
填yes或no。是否为突击者，这个代码指定步兵单位是否可以驱逐建筑中驻守的步兵单位而无须对该建筑造成任何损伤。这里的“驱逐”指将建筑中的所有驻守的步兵单位全部破坏
驱逐过程动画由主武代码的AssaultAnim=来设定，原版废设使用UCFLASH，也留有UCBLOOD和UCELEC
原版下无法设定某个建筑对于某个突击者步兵来说是否可以突击，Ares允许设定步兵与建筑各自突击等级进行比较，详见说明书
AttackCursorOnFriendlies =
填yes或no。这个代码指定该单位是否可以对自己一方单位展开攻击，一般用于医疗兵、疯狂伊文、维修车等单位
AttackFriendlies =
填yes或no。这个代码指定单位是否主动攻击自己一方单位，但也可以攻击敌人单位
在CanPassiveAquire=no时无效
AuxSound1 =
填Sound.ini中定义的声音名。这个代码指定飞机起飞时的声音，导弹类子机发射时也会使用
AuxSound2 =
填Sound.ini中定义的声音名。这个代码指定飞机降落时的声音，导弹类子机撞击时并不使用
AntiInfantryValue =
建筑反步兵权重
AntiArmorValue =
建筑反装甲权重
AntiAirValue =
建筑反空军权重
AI会检索敌军单位类型数量并按该权重选择多造哪个防御建筑
AirstrikeTeam =
普通鲍里斯召唤空袭的数量
特殊效果为这个语句只要非0那么会禁止Secondary开火时FireUp后接入Guard帧而一直保持开火状态，哪怕并没有补全空袭逻辑的单位语句和使用空袭指示的武器
此外如果为AircraftType使用这一写法，那么如果处于攻击任务中按 S 停止或失去目标会大概率直接飞出地图并删除。不过这个效果的触发成功率没有Landable和Selectable那套稳定
若要成功召唤空袭需要与武器弹头上的Airstrike配合
AirstrikeTeamType =
普通鲍里斯召唤空袭的飞机
AirstrikeRechargeTime =
普通鲍里斯召唤空袭的间隔
AltImage =
该单位在攻击时使用的代替图像。仅适用SHP单位，TS残留废弃，在TS中被器官兽使用
AlphaImage =
该物品使用哪个Alpha光，Alpha类似Ares的AE，不过AlphaImage是改变亮度
AlphaImage正常只有1帧，Ares下也可以使用多帧对应多个面，但必须是8的倍数，并且可以跟随对象移动，不过实现相当暴力，每2帧擦除并重新生成一次，性能炸弹
AlphaImage并不是动画，对应的无需也无法在Animations中有效注册，直接写不带后缀的文件名就可以了，注意透明色为127号而非Animation用的的0号，向前变暗向后变亮
AlphaImage的shp需要和鼠标动画一样使用ShpBuilder的Compression 1 Only模式（汉化版应该直接写为了“用于鼠标动画”）保存，保存常规单位的shp时要记得换回去否则Bug
AutoCrush =
TS开始该句出现在了矿车上，用于载具微定义自动碾压
AircraftCostBonus =
战机建造价格为原来多少倍

 -B-
BurstDelayX =
载具武器有Burst的情况下两发之间间隔的帧数
实际上无法降到0，当然在玩家眼里除非卡的要死也足够表现得尽量像立即射出了
BurstDelay0 =
第1发和第2发的间隔
BurstDelay1 =
第2发和第3发的间隔
BurstDelay2 =
第3发和第4发的间隔
BurstDelay3 =
第4发和第5发的间隔
注：如果只有X没有(X+1)则X+1继承X的值
原版下仅可用于VehicleType并且只能写在单位上，Infantry的会被Fireup、FireProne覆盖掉，Aircraft的则强制为0
Phobos改为了类似FS中写在武器上的形式，并可以直接使用BurstDelays指定每两Burst之间的间隔而不局限于0-3分别制定1-5发的间隔，详见说明书

BuildTimeMultiplier =
建造时间为正常的多少倍，越大越慢
BaseNormal =
是否延伸建筑范围，即Adjacent判定时是否可以将这个建筑视为扩展节点
仅用于玩家，Ares允许定义对AI而言的BaseNormal，原版下AI仅有建筑拥有UndeploysInto的同时拥有Foundation=1x1或ResourceGatherer=yes中的至少一个才不被视为扩展节点
Bunker =
填yes或no。建筑是否为坦克碉堡
神奇的是当这个建筑同时拥有ConstructionYard=yes的情况下进入过程会变得相当丝滑
注意：
坦克碉堡不会影响单位除了射程外的受击判定，这就是为什么AI的辐射工兵也喜欢对着坦克碉堡中的坦克一通爆射
而这个射程判定WW是直接硬编码了个384Leptons长度的距离，怀疑就是专门给2x2碉堡应对近战单位（大概是YR里狂兽人）定制化编写的，并且坦克碉堡的Foundation也对奇数x奇数支持的很不好
Bunkerable =
填yes或no。该载具能否进入坦克碉堡，在这句之前优先判定载具是否满足下述至少一项：
即是否[处于被寄生状态|没有炮塔|使用了Hover类SpeedType]，若满足则在更上层禁止入库
除此以外对于使用了Mech/Hover/Fly类Locomotor的单位虽然不会禁用进入光标但实际上只能移动到旁边无法进入，有时用于制作一些特殊的站点机制
*如果不手动设定，那么Locomotor=Hover的载具其SpeedType默认为Hover
对于Locomotor=Ship的载具在进入坦克碉堡的瞬间会EIP:006A0220
对于可以进入坦克碉堡且非Drive的Locomotor也会表现的比较奇怪，例如不会移动到正确的坐标
BalloonHover =
填yes或no。这个代码指定使用Jumpjet运动模式的单位不能落地。会打断CloakStop
此句生效时JumpjetHeight必须高于战车工厂的ExitCoord=的高度否则会卡住
同时该语句会限制单位可移动的单元格，例如点击建筑旁边的地面会自动避开建筑所在单元格，点击桥面时会将所有移动目标点均设在桥上而不考虑旁边的水面，PhobosBuild47允许全局设置这一规则
在RA2下只要有这句那么单位手动攻击时就总想着往对面头上飞，无论Locomotor如何
在YR开始额外检测当前所使用武器其抛射体上是否拥有Vertical=yes才决定该行为
没有这句的直升机原版下不会触发DeathWeapon，Ares已修复，但对应的你就得手动禁用一下原版直升机的死亡效果了，你也不想看见你的直升机被摧毁砸到地上突然爆出一堆子弹命中的动画吧.jpg
Bib =
填yes或no。让建筑最东（右下）侧一列单元格可以通行[载具]（矿场 车场）
由于国际社区认为PVP中载具堵重工门禁止出车是一种作弊，因此Ares硬编码仅对[友军]生效，不过社区论坛已经有大佬出手了https://bbs.ra2diy.com/forum.php?mod=viewthread&tid=23762
Bombable =
填yes或no。这个代码指定该单位是否能被疯狂伊文捆绑上定时炸弹
BombSight =
填数值。这个代码指定该单位对定时炸弹的警戒范围，当被捆绑上定时炸弹的我方单位进入警戒范围该单位会进行拆除定时炸弹的工作，该单位弹头要有BombDisarm=yes这个设置否则同样不能拆除。注意：当该单位本身被捆绑上定时炸弹时不能进行自我拆除定时炸弹的工作
BridgeRepairHut =
填yes或no。这个代码指定建筑是否为桥梁维修小屋，这种建筑可以维修附近的毁损桥梁或提供其他单位（如谭雅）来炸毁桥梁
BuildCat =
填下表的相应项。这个代码指定建筑的所属类型，用来给游戏分类和AI识别
注意：原版引擎下一个没有BuildCat的建筑建造后取消会IE，只能拍下来，但建造进度效果也会依旧保留到下一个正常建筑建造，并且同步播放一次，Ares已修复
--------------------------------------------------
Combat			防御建筑，该建筑会出现在防御栏中
Infrastructure	既没卵用，也没人用
Resource		资源建筑，给玩家提供金钱
Power			电力建筑，给玩家提供电力供给
Tech			科技建筑，用来作为其他单位的建造条件
--------------------------------------------------
BuildLimit =
填数值。这个代码指定单位的建造数量限制。负数为到达绝对值后删除图标，不能建造
对平民建筑（特指Insignificant=yes的）使用无法正常生效。此外AI生产也并不遵循这项，Ares已允许设定AI是否可以越过BuildLimit生产，详见说明书
BuildupSound =
填Sound.ini中定义的声音名。这个代码指定拔起播放建造动画时播放的声音
BerserkFriendly =
是否不会被狂暴单位攻击，指被YR里精神突击车那种混乱弹头影响的单位，而非TS中Cyborg的发狂
BarrelAnimIsVoxel =
炮管图像是否为VXL，用于开启VoxelBarrelFile
BarrelStartPitch =
炮管的初始俯仰角度，RA2下疑似废的彻底
以下4句用于原版巨炮炮管伸缩，需要TurretRecoil开启
BarrelTravel =
该建筑炮管可偏移的像素值，默认 2
BarrelCompressFrames =
该建筑炮塔恢复所需要的帧数，默认 1
BarrelHoldFrames =
该建筑炮管保持在受后坐力位置显示的帧数，默认 1
BarrelRecoverFrames =
该建筑炮管恢复所需的帧数，默认 1
BuildingsCostBonus =
普通建筑建造价格为原来多少倍

 -C-
CloseRange =
填yes或no。指定该单位是否使用近战武器（狂兽人），帮助AI判定选择目标的范围
C4 =
填yes或no。这个代码指定该步兵是否拥有C4炸弹
注意：当为yes时，不管是主副武是否可以对建筑物，对付建筑物的武器都会被C4代替，除非攻击目标有CanC4=no的设定
如果存在这句，那么单位无论是否可以进入建筑，都会选择炸掉它...
哪怕建筑存在CanC4=no，也会选择使用武器摧毁它，也就是会冲掉其他进入行为
如果光标为Sabotage，那么如果武器Versus=1%就会强行切换到另一个武器
C4=no且Loco非Walk的Infantry在水上停下时会直接死亡并留下空气墙
如果是军医类型的步兵使用负伤害治疗武器那么允许原本的禁止光标变得Ctrl下可以强制Attack
CanBeach =
填yes或no。这个代码指定该海军单位能否在沙滩上（接近陆地）的地方运行，同时还要有MovementRestrictedTo=Water这一项设定。但实际效果不怎么样，还不如改成两栖的，寻路智障
CanBeOccupied =
填yes或no。这个代码指定建筑单位是否可以被进驻
红色警戒2不同于尤里复仇，占领后的武器要在该建筑上设定
盟军占领后使用Primary=的武器，苏军占领后使用Secondary=的武器
这个建筑Buildup结束后就会改变所属为中立
并且如果你真的有给这个建筑写Buildup的话会被中立直接卖掉
RA2下一种创建经验包的方法就是与Buildup=none及MaxOccupants=0禁用进驻连用
YR为苏军NABNKR额外判定了是否拥有TechLevel=-1再作所属转换
然而只要有这句哪怕TechLevel>=0不改变所属AI也会倾向于视为一个平民建筑
在Ares下已经允许一个建筑设定自己可以被哪些步兵驻军，详见Ares说明书
原版下已经拥有所属的平民建筑建筑（已驻军且TechLevel=-1）无法进入其他人的步兵
但同样有所属造出来而无驻军的苏军碉堡（TechLevel>=0）也是如此，Ares的巷战相关拓展允许无人的碉堡允许敌方步兵驻军并转移所属方，详见说明书
CanOccupyFire =
该建筑被驻军后驻军单位能否向外开火，同时使射程为全局[CombatDamage] -> OccupyWeaponRange=的值+1
CanC4 =
填yes或no。这个代码指定该单位是否能被有C4=yes的步兵炸毁。默认值是yes
这句为no的建筑将无论如何至少受到1的伤害，LaserFence无视该效果可以放心用
这也导致Damage*Versus<0的弹头在打到该建筑时强制变为+1点，Phobos已允许在建筑上禁用这一规则
这就是维修圈会把油桶和弹药箱修爆炸的根源所在……
在YR这个标签也影响能否被鲍里斯的空袭引导武器锁定（WW偷懒），Phobos已添加新语句以分离控制
原版下你也可以使用ResourceGatherer和ResourceDestination连用来禁止被空袭
CanDisguise =
填yes或no。这个代码指定该单位是否可以伪装而敌人无法发觉（狗除外），用在间谍和幻影坦克上
CanPassiveAquire =
填yes或no。这个代码指定该单位是否能够自动攻击目标。默认yes
此外Aquire为Westwood错误拼写，正确的英文单词应当是Acquire
Ares允许分离控制Guard状态与隐形状态下的PassiveAcquire设置
如果开启的话一些其他的索敌类效果也会可以生效，但可能略显智障
例如防空车总是被伞兵机之类的吸引走，维修车总是会去追伤残友军
CanApproachTarget =
填yes或no。该单位是否停留在某地时追向接近的敌方单位进行攻击，幻影坦克原版为no，以防止它们在警戒模式下朝目标移动，否则会因为伪装消失而被攻击
在可对空单位上设置CanApproachTarget=no是一种防止它们追逐空中单位的方法
如果no掉那么它们只会在被空军攻击时才会追着打
CanRecalcApproachTarget =
填yes或no。这个代码指定带有CanApproachTarget=yes代码的载具是否能重新计算敌人所在路径点。实际上在游戏中，人类玩家选择了一个攻击对象，游戏并不是攻击该对象而是该对象所在的路径点，然后给击中的目标一些伤害
当然要选择yes，否则该载具就会变的极难操纵。其实就是是否会追着打最后一个攻击目标
CanRetaliate =
填yes或no。这个代码指定该单位是否能在遭到敌方攻击时进行反击
对于隐形单位这可能导致它们在目标过远时会显形一次
Capturable =
填yes或no。这个代码指定建筑是否能被工程师占领
CaptureEvaEvent =
指定这个建筑被工程师占领后播放的EVA
Carryall =
此战机是否可以吊运载具，一定是运动模式为Fly（{4A582746-9839-11d1-B709-00A024DDAFD1}）的战机。不要是直升机（就是重工造出的实际上是会飞的载具的那种）
同时强制落地踢出（放下）载员，并且把载员的图像绘制到自己身上（无论载具载员还是步兵载员），放下载员时把自己的ROT传给载员（被吊运的载具实际上是战机的载员）
并且载员被释放后会显得下沉了一部分，且光标悬浮在自己所在单元格会变成允许移动，停止移动时炮塔还会转向一定角度再自动回正，Ares已修复部分问题
被吊运载具的OpenTopped可以正常工作。此外该战机降落时可以播放一个动画，详见Locomotor词条下的注解
Category =
填下表中的相应项。这个代码指定单位的分类，用来给AI判断的（实际上然并卵）
--------------------------------------------------
AirLift		运输机，用来运输步兵的飞机
AirPower	战机，用在战机和直升机上，可以使用武器
Transport	运输车，用来运输各种单位的载具
Support		基地车，也可以用在其他可部署成为建筑物的载具上
LRFS		远射程载具，可以进行远程打击的载具
IFV			步兵载具，多功能步兵载具专用
AFV			载具，可以广泛运用于各种战斗用载具，如坦克
Recon		Reconnaisance载具
VIP			重要的步兵单位，没什么用
Soldier		步兵，所有步兵单位都用这个分类
--------------------------------------------------
ChargedAnimTime =
填数字。这个代码指定超级武器建筑在超级武器启动前多长时间播放启动动画，单位为分钟，动画由Art.ini中的SuperAnimThree=来控制。该值应该小于相应超级武器的RechargeTime=值
ChronoInSound =
填Sound.ini中定义的声音名。这个代码指定单位超时空运动开始的声效
ChronoOutSound =
填Sound.ini中定义的声音名。这个代码指定单位超时空运动结束的声效
Civilian =
填yes或no。这个代码指定该单位是否是平民单位，平民单位也就是大家说的中立单位。受地图触发“平民疏散” 事件影响
ClearAllWeapons =
填yes或no。该物体的武器均设为空白，无法执行攻击命令
IFV逻辑可以被载员给予武器，但是无法实际开火，也无法正常触发DeployToFire，只是有了攻击指针和红色瞄准线
限制：无法清除YR下由驻军单位引入的驻军武器，另外PhobosBuild37以后只要显示攻击指针立即崩溃
ClickRepairable =
填yes或no。这个代码指定建筑是否可以使用游戏建造栏的“维修小扳手”工具来维修
注意：当该设置为no时，建筑不能被“维修小扳手”修复，但仍然能被工程师进入修复
如果不想这样，可以在建筑代码中加入Repairable=no。Ares已允许单独设置能否使用工程师进入维修，详见说明书
Cloakable =
填yes或no。这个代码指定该单位是否可以隐形。注意：如果要给高于地面的悬浮单位和空军单位隐形，不能直接使用这个代码
不过隐身状态会导致程序中一些判定指针无效，例如隐形的航母发射子机子机会认为母舰不存在而坠毁，来自导弹类子机的击杀也无法为母舰提供经验，Ares已解决子机认为隐形母舰丢失问题
只能在VeteranAbilities=或EliteAbilities=加入Cloakable这个升级效果，不过只能在升级后才能隐形，Ares已解除该限制，允许定义能否隐形的判定高度，并将其默认为悬浮单位所用HoverHeight=的值，详见说明书
此外Ares还分离了部署状态、断电状态的隐形效果，详见Ares说明书
CloakingSpeed =
填1-10的数值。这个代码指定该单位的隐形速度（即出厂时的隐形速度和被发现后的再次隐形速度），要配合Cloakable=yes使用
实际上是每一个隐形阶段所需的时长，越小越快，总时长由本句与全局CloakingStages共同决定，Ares已允许单位微观定义CloakingStages
CloakGenerator =
填yes或no。这个代码指定该建筑是否可以将自身周围的已方单位全部隐形
注意：YR下只有高度0的单位才可以受到影响，也就是Locomotor为Hover这种不贴地的悬浮载具不受影响，Ares已允许定义高度判定值，并将默认值设为[General] -> HoverHeight=的值，因此Hover载具只要装上Ares就可以正常得到效果，如果希望还原原版的效果则使用Ares提供的语句手动设为0，详见说明书
CloakRadiusInCells =
填数字。这个代码指定建筑隐藏周围已方单位的隐藏半径，要和CloakGenerator=yes配合使用。由于WW的诡异算法，此处0会没有范围，但是false却恰恰相反
CloakStop =
填yes或no。停止运动时隐形，TS残留，Ares已复原，详见Ares说明书
Cloning =
填yes或no。这个代码指定建筑是否为复制中心。克隆中心会把所有从兵营出厂的单位再免费赠与一个同样的，也同样支持CreateUnitSound设定，仅克隆Factory=InfantryType的（也就是兵营）建筑生产的，Ares添加了用于克隆载具的同类功能，详见说明书
原本在YR1.001下针对[BuildingType] -> Factory=AircraftType的建筑禁用集结点的效果会被该语句覆盖
ConcentricRadialIndicator =
填yes或no。这个代码指定建筑是否拥有“心灵感应装置”（苏军的）那样的雷达扫描效果，但该建筑必须要有HasRadialIndicator=yes的设定
ConsideredAircraft =
填yes或no。基洛夫空艇和火箭飞行兵这种实际上是载具的飞行单位使用，是否被视为常规空军单位，Aircraft默认yes
和Organic一样用于一些判定
一些旧教程称控制是否从天窗飞出，实际与这句无关，检查的是JumpJet与BalloonHover是否拥有至少一条
ConstructionYard =
填yes或no。这个代码是基地建筑专用的，变卖后不会变回载具，让AI判定该建筑为基地
设置为no则不受基地重新部署选项的影响，但会导致该阵营AI智障
此外只要AI手动建造或载具DeploysInto出了有这个标签的建筑即被视为建设了新基地的判定
然后AI就会把自己所有可操纵的单位全部集结过去，哪怕是一些非战斗单位，例如矿车。Phobos已对此行为允许【全局】层面关闭
Cost =
填数值。这个代码指定该单位的价格。每个可以建造的单位都应该设定其价格
同时也决定了初始单位的实际生成数量，如果明明设置的是10但开一把基础兵从基地车向八个方向生成了几百个那么就该检查一下是不是有哪个单位Cost写的过小或者写了个负数之类的了
原版下如果Cost=0那么初始单位不会生成，也就是说你可以利用这个特性在无需Ares修复的情况下实现0初始单位
Crashable =
填yes或no。这个代码指定此Jumpjet单位在空中被摧毁后，是否坠落到地面，否则凌空爆炸。不要给HoverLocomotor的单位使用否则被摧毁卡最后一滴血死不了
Ares已拓展至Aircraft，并允许Aircraft坠落的情况下是否旋转，Phobos已允许Jumpjet设定坠落的情况下是否旋转，详见说明书
目前Ares引擎下母舰被毁时子机无视[TechnoType] -> Crashable=no强制可以坠毁
CrashingSound =
填Sound.ini中定义的声音名。这个代码指定空军单位被摧毁坠落时爆炸的声效。要配合[TechnoType] -> Crashable=yes使用
CarriesCrate =
填yes或no。这个代码指定载具被摧毁后是否会在附近生成一个箱子，例如原版[TRUCKB]就是
注意：如果想要让建筑物拥有这个效果要换成[BuildingType] -> CrateBeneath=yes
对于[VehicleType] -> CarriesCrate=yes且[TechnoType] -> IsTrain=no的情况由地图[Basic] -> TruckCrate=决定是否掉落
对于[VehicleType] -> CarriesCrate=yes且[TechnoType] -> IsTrain=yes的情况由地图[Basic] -> TrainCrate=决定是否掉落
该逻辑需要当前游戏开启箱子掉落，对于单人任务地图而言需要rules(md).ini中有[MultiplayerDialogSettings] -> Crates=yes
CrateBeneath =
填yes或no。这个代码指定建筑被摧毁时是否在附近生成箱子。箱子的内容在没有专门设定下是随机的
CrateBeneathIsMoney =
填yes或no。这个代码指定建筑摧毁后生成的箱子的内容是“获得金钱”。要配合[BuildingType] -> CrateBeneath=yes使用
CrateGoodie =
填yes或no。这个代码指定载具单位能否从箱子中获得，获得该载具的机率要看使用这个代码的载具数量
CreateSound =
填Sound.ini中定义的声音名。这个代码指定该单位被建造时的声音
CreateUnitSound =
填Sound.ini中定义的声音名。这个代码指定单位生成时Factory建筑（包括克隆工厂）播放的声音。每种类型单位出厂时工厂都可以播放不同的声音：默认全局CreateInfantrySound=，CreateUnitSound=，CreateAircraftSound=分别对应步兵、载具单位（包括海军单位）、战机
Crewed =
填yes或no。当此单位或建筑被摧毁后，是否有步兵从里面逃出（逃出的可能性在rules的开头有控制）
也控制建筑类对象出售是否给予步兵
如果物体被自己的Suicide=yes武器摧毁，强制没有幸存者，Phobos已添加新语句解除，详见说明书
Crushable =
填yes或no。这个代码指定物体是否能够被载具单位碾压。
适用于包括但不限于步兵、载具、建筑、围墙、地形对象的一切ObjectType，但工作方式略有不同
对于建筑类，若非[BuildingType] -> Foundation=1x1则只是单纯穿过，就像Ares引入的[BuildingType] -> IsPassabe=yes那样
对于地形对象，碾压后屏幕不会立即刷新，只有移动视角后原地形对象的图像才会消失
DeployedCrushable =
填写no，则步兵在部署状态下不被碾压（重装大兵）
该语句在Crushable之后工作，也就是你不能反过来让重装大兵只有部署时可以被碾压而站着时不能
Crusher =
填yes或no。这个代码指定载具单位是否能够碾压步兵和可碾压围墙，并且通过碾压也可以正常升级，当然需要Trainable语句上没有设为禁止升级
CrushSound =
填Sound.ini中定义的声音名。这个代码指定步兵（或围墙类建筑）被碾压的声效。要和Crushable=yes配合使用
Cyborg =
步兵是否为半机械人，允许受EMP效果影响但依然可以被铁幕秒杀
每次攻击该步兵至多打到红血，然后进入伤残状态转为匍匐图像
在该步兵不匍匐的情况下常规伤害无法将其击杀，可用Fearless禁用匍匐转换
损坏/破坏一个机器人会播放[General] -> InfantryExplode=的动画
如果[CombatDamage] -> BerzerkAllowed=yes则会发狂（仅限TiberiumSun）
部署和取消部署会导致取消机器人的爬行（伤残）状态，因此部署和半机械人无法很好的配合
进入再退出运输载具也会取消半机械人的爬行（伤残）状态

 -D-
DamageSelf =
填写yes。允许该单位发射的武器伤害自身。由于开火不伤自身实际上是找格子里的第一个对象，所以空中单位始终可以伤害
原本是YR中为了处理核弹井砸自己不掉血而添加的，并且并不影响非常规杀伤的其他效果，例如AresAE始终是允许给自己加的
不过这个语句作为单位语句自然对此单位的所有武器都生效，如果你要单个武器进行设置详见Phobos添加的弹头自定义是否杀伤开火者效果
Doggie =
是否为泰伯利亚恶魔，TS残留无效，Ares已还原相关逻辑，详见说明书
DontScore =
填写yes。该单位不计入杀伤统计和单位经验
实际上是对[ObjectType] -> Insignificant=语句效果的分离
但引入了一个新Bug：如果载具使用会导致程序始终认为载具依然存活，即所属方永不判负，进而导致游戏无法结束，同时也会导致 9 号触发条件永远无法被视为满足
DoubleOwned =
用于秘密科技实验室系列逻辑，新增于YR但没有做完，Ares重做的秘密科技实验室系统中有同类逻辑并更加方便，详见说明书
Drainable =
填写yes。则该建筑可以被飞碟吸
DeployToLand =
填写yes。让悬停在空中的直升机播放螺旋桨动画
和IsSimpleDeployer=yes连用可让Jumpjet单位悬停不落地（与BalloonHover类似）
不同的是BalloonHover会打断CloakStop，并且可以悬停在建筑上
当然也可以正常与BalloonHover一句合用
DamageParticleSystems =
填粒子系统名称。这个代码指定所有单位黄血时产生的粒子系统
只能使用Smoke和Spark类的粒子系统
只有单位高于地平面才会有粒子系统
只在原本无同类粒子时生成粒子系统
Smoke:
必然创建
真治疗(即不包括正伤害负比率弹头)、维修和回血在回到绿血后移除粒子系统
Spark:
根据
[General] -> ConditionYellowSparkingProbability=的值
和
[General] -> ConditionRedSparkingProbability=的值
决定创建几率，步兵需要拥有Cyborg=yes才能用Spark类粒子，Ares已允许使用新的语句分离控制，详见说明书
达到[ParticleSystemType] -> Lifetime=后删除
另有规则：当对象血量低于50%或[AudioVisual] -> ConditionRed=的比率时将创建Smoke粒子系统
与Spark不同，Smoke被硬编码为该阈值而不读取[AudioVisual] -> ConditionYellow=的设定
DamageReducesReadiness =
受伤掉弹药，这个代码指定单位受到伤害时是否会减少弹药
需要和ReadinessReductionMultiplier配合使用
当该单位没有Ammo=的设定时，这个代码无效
公式：rounds lost =damage inflicted (before warhead calculations) / Strength * ReadinessReductionMultiplier * Ammo
也就是填负数会补弹药，但是不检查单位Ammo值，也就是会超出Ammo继续装……
DamageSound =
填Sound.ini中定义的声音名。这个代码指定单位被攻击时被攻击方播放的损害声效
DamageSmokeOffset =
填X，Y，Z的数值。这个代码指定所有单位、建筑单位临近毁坏时冒烟的位置。默认为0，0，0
DamSmkOffScrnRel =
填X，Y，Z的数值。这个代码指定所有单位、建筑单位临近破坏时冒烟的位置，不过这个位置冒的烟比DamageSmokeOffset=冒的烟更难观察到。默认为0，0，0
DeaccelerationFactor =
填数值。这个代码指定单位接近攻击目标时减慢的速度的百分比，降低百分比是以该单位的Speed=的数值来作标准的
DeadBodies =
填动画列表，步兵死亡后的尸骨动画，列表内随机选取，不继承所属方，默认全局值，与下句同时生效
DeathAnims =
填动画列表，列表序数与弹头InfDeath=的序号一一对应，与原版死亡方式的序号一一对应，你也可以凭借它在原版添加更多种死亡动画，最主要的是：它的列表是定义在死者单位上的，而非仅由杀伤来源控制
如果想要指定它来实现原版的效果需要填入dummy,<die1>,<die2>,S_BANG34,FLAMEGUY,ELECTRO,YURIDIE,NUKEDIE,VIRUSD,GENDEATH,BRUTDIE;,……后面可以继续加
其中dummy要自己弄个有效的空动画，否则会直接跳过。而Die1、Die2序列可以刷个同素材步兵再死一次来调用序列，原版0-10之后的同样使用与弹头InfDeath=值对应的规则
不过【只有15个】有效，也就是InfDeath=0-14的范围，对应的如果想完全应用起来你得用拓展引擎的弹头自定义死亡动画逻辑把原版的通用死亡动画全部弹头微观定义一遍（一个简单的批量替换）来空出这14个位
在经过上述处理空出DeathAnims的可用空间后就可以借助这个实现在【单位上】自定义Die12345和WetDie12345678910X的效果，而不需要去复原原版未启用的Die3-Die5那套编码机制
使用规则见[Warhead] -> InfDeath=词条底端
通过这个语句创建的动画会使用死者的所属方，Ares允许动画上定义所属方的继承来源，详见Ares说明书
DeathWeapon =
死亡武器，用于[TechnoType] -> Explodes=yes的单位，特殊规则见[WeaponType] -> Suicide=yes
默认使用主武器（[TechnoType] -> Primary=/IFV 当前武器），主武器不存在使用[CombatDamage] -> DeathWeapon=的武器
对于处于空中的单位会爆两次，在空中被摧毁时先Explosioin并爆一次DeathWeapon，砸到地面再爆一次DeathWeapon
对于导弹类对象，其命中使用自己全局或Ares自定义导弹参数中所设定的弹头和武器，而被摧毁使用这里设定的死亡武器
DeathWeaponDamageModifier =
填数值。这个代码指定该单位DeathWeapon=武器增加或减少威力的倍数
DebrisAnims =
填动画名。这个代码指定该单位被摧毁时弹出的shp碎片列表，碎片用逗号隔开，默认[General] -> MetallicDebris=的列表
需要配合MaxDebris=和MinDebris=两条语句
温馨提示：WestWood在原版rules(md).ini中的Max/MinDebris有许多处使用了小写debris导致语句无效
DebrisTypes =
填动画名。这个代码指定该单位被摧毁时弹出的vxl碎片列表，碎片用逗号隔开
这个碎片一定要是在[VoxelAnims]里定义了的。那些坦克爆炸后弹出炮管和脑袋飞天的效果就靠的这个
还需要在全局
[General] -> ExplosiveVoxelDebris=<List of VoxelAnims>
[General] -> TireVoxelDebris=<VoxelAnimType>
[General] -> ScrapVoxelDebris=<VoxelAnimType>
后面写上来声明这是vxl残损爆出的碎片
DebrisMaximums =
填数值。这个代码指定该单位被摧毁时弹出的vxl碎片的最大数量，和上条对应，分别用逗号隔开
DefaultToGuardArea =
填yes no。这个代码指定该单位是否自动进入区域警戒(Area Guard)状态，一旦有敌方进入警戒范围，该单位会自动追上前去迎敌
当区域警戒的目标为建筑（相当于单元格）的情况下程序会从[2*GuardRange与4096Leptons(16格)]这两个值中取更小的那个再*1.1来获取单位的警戒范围
当区域警戒的目标是可移动的对象（保护己方单位）那么会使用GuardRange获取警戒范围，根据全局GuardModeStray来决定离开多远后返回
对于矿车(Harvester=yes)类载具其Area Guard状态的实际效果其实是会把这个矿车送去采矿
Deployer =
填yes或no。这个代码指定步兵能否部署。部署的样子由Art.ini中该步兵的Sequence控制
DeployFire =
填yes或no。这个代码指定步兵部署后是否能够开火。要和Deployer=yes配合使用
注意：它会覆盖整个武器选用优先级，例如YR中的GGI拥有一个可以对空的副武器，但非部署状态下哪怕你让他去攻击一个空中目标他也会用主武尝试发起攻击行为，然后由于主武无法对空而没有任何行为。该效果自YR加入，RA2没有
举个例子：让YR中的尤里复制人可以使用副武器攻击狗
首先[(Y)(A)DOG] -> ImmuneToPsionics=yes得换成[Controller] -> Versus=0%来使用正常的武器选用逻辑
然后禁用部署开火逻辑例如改为[YURI] -> DeployFire=no绕过部署开火所强制的一套武器选用规则限制
最后再去掉武器上必须部署的语句例如改为[PsiWave] -> AreaFire=no来允许步兵正常使用这个武器
DeployFireWeapon =
填0-1的数值。这个代码指定步兵部署后所使用的武器。填“0”为使用主武器，填“1”为使用副武器。默认值为“1”
当一个载具同时拥有部署逻辑和盖特逻辑时将始终使用它的Weapon1
就是说部署释放武器不随盖特逻辑升阶更换武器
Phobos允许使用-1来让部署态的单位也能使用两种武器
DeployingAnim =
部署时播放的动画，原版用于武装直升机IsSimpleDeployer=yes下部署与反部署状态切换，动画播放时IsLocomotor类弹头仍可尝试锁定但会失败然后放弃目标
DeployToFire =
填yes或no。攻击动作触发部署。要和DeploysInto=或IsSimpleDeployer=配合使用
它会执行攻击行为时转为部署，但是影响主动寻敌
YR下DeploysInto的建筑不会继承原载具的目标，Phobos已硬编码继承
如果该单位执行DeployToFire时恰好脚下有矿或其他情况妨碍部署，它还会自动移动到附近的空旷区域
DeployTime =
填时间。这个代码指定该单位部署的延迟时间。单位为帧
DeploysInto =
填建筑名称。这个代码指定载具部署后变成的建筑
被心控的载具部署后会断掉心控链接彻底改变所属，YR1.001为此禁用了被心控单位的该逻辑，Phobos已允许正常交接并解除了禁用效果
实际上是TechnoType通用标签，值的类型也是TechnoType，由于拥有跨类别T选同类对象的效果，曾也用于原版引擎下的类Ares中GroupAs功能的效果，原版下可能造成一些问题，Ares已进行修复，同时提供新的GroupAs作为另一种可选的实现方式
由于DeploysInto和UndeploysInto的单向跨类T选拥有层次效果，可结合GroupAs做出注入“第一次T选MTNK选中所有MTNK，第二次T选选中所有MTNK、HTNK、LTNK”的效果
由于原标签自身作用，载具应当确保不会执行原行为的情况下才适合这样使用，否则仍会正常执行标准操作即部署成建筑
此外这样的转变很多效果无法继承，例如铁幕，Phobos已允许继承其中一部分
DeploySound =
填Sound.ini中定义的声音名。这个代码指定载具DeploysInto成为建筑时或进入SimpleDeployer时的音效
DetectDisguise =
填yes或no。这个代码指定该单位是否能发现伪装的敌人并展开攻击（是用主武攻击）
DetectDisguiseRange =
填数值。这个代码指定该单位发现伪装的敌人的距离。要和DetectDisguise=yes配合使用
特指发现CanDisguise=yes的单位
DestroyAnim =
填动画名。这个代码指定建筑被摧毁时播放的动画，但是所属色映射错误，且可能导致RE，Ares已修复
DestroyParticleSystems =
填粒子系统名。这个代码指定该单位被摧毁时播放的粒子动画
DestroySmokeOffset =
填X，Y，Z的数值。这个代码指定该单位被摧毁时播放粒子动画的位置
DieSound =
填Sound.ini中定义的声音名。这个代码指定该单位被摧毁时的声音
Disableable =
填yes或no。这个代码指定该单位是否被遭遇战模式的选项所影响，与TS的残留逻辑有关，当选择'No Bases'多人游戏选项时，MCV实际上被禁用
DisguiseWhenStill =
填yes或no。这个代码指定伪装单位在不移动时会把自身伪装起来，如幻影坦克，需要与[TechnoType] -> CanDisguise=yes合用
DistributedFire =
填yes或no。这个代码指定该单位（神盾）在自动攻击状况下攻击一次后更换目标。只有一个敌人的话也会停顿一下再开火
Dock =
填建筑名称。这个代码指定单位可以进入的平台，如矿车能进入矿场，战机能回到机场
在原版下Dock对战机的作用仅限制生产，战机仍然能够自动停靠到Dock不允许的建筑并且占用相应机位影响其他战机生产，Ares禁止了这种情况
Ares下Dock=<none>的Aircraft不会在像那个名叫共和国之辉的古董mod那样近乎无限弹药还在取消指令后回机场补弹
但是由于YR对战机行为的更改，这样的战机取消命令后虽然到不会像原版空天母舰的子机那样飞出去并IE，但是会尝试停到地图边界
注意：在PadAircraft中声明为机场战机的战机类对象必须拥有非空的Dock否则0045ED61
DockUnload =
填yes或no。这个代码指定单位进入这个建筑后是否进行“卸货”即执行Unload命令。原版仅用在矿场上，一些应用见Weeder一句
对于矿场的矿车倒矿，矿车会在返回矿场前记录当时的格子坐标，因此倒矿后也是前往那个格子再开始寻矿，而不是倒矿时立即重新开始寻找最近的矿区
DeployFacing =
表示该载具部署为建筑前朝向哪个方向，0-7对应从北到西北的八个标准方向
DetectionDistance =
该步兵需要靠近拥有PsychicDetectionRadius的建筑这么多的距离才会被觉察，YR引入但实际废弃
DefensesCostBonus =
防御建筑建造价格为原来多少倍

 -E-
EligibleForDelayKill =
填yes或no。这个代码指定建筑是否为油桶一类的单位。血条为0后隔一段时间才爆炸
EligibileForAllyBuilding =
填yes或no。这个代码指定玩家能否在这个建筑上与其他玩家结盟
此代码会强制BaseNormal，只在“于盟友建造厂旁建设”选项激活时生效
EliteAbilities =
填下表中的相应项。这个代码指定单位升级精英时拥有的能力
所有升级过程获取的能力只能获得一次加成，也就是VeteranAbilities写过的再写一遍没用
对应的，老兵时通过VeteranAbilities获得的能力也不会当单位升级到精英时丢失
--------------------------------------------------
便于复制：
FASTER,STRONGER,SCATTER,FIREPOWER,ROF,SIGHT,CLOAK,SELF_HEAL,EXPLODES,RADAR_INVISIBLE,SENSORS,FEARLESS,GUARD_AREA,CRUSHER,C4
FASTER
单位移动速度加快（Speed*[General] -> VeteranSpeed=）
STRONGER
单位的生命值增加（Strength*[General] -> VeteranArmor=）
SCATTER
单位能自动分散以躲避炮火
FIREPOWER
单位攻击力加强（武器的Damage*[General] -> VeteranCombat=）
ROF
单位射速增快（武器ROF*[General] -> VeteranROF=）
SIGHT
单位的视力加大（Sight*[General] -> VeteranSight=）
CLOAK
单位可以隐形（Cloakable=yes）
GUARD_AREA
单位可以自动进入区域警戒（DefaultToGuardArea=yes）
CRUSHER
单位可以碾压（Crusher=yes）
SELF_HEAL
单位可以自动治愈（SelfHealing=yes）
EXPLODES
单位可以爆炸（Explodes=yes）
RADAR_INVISIBLE
单位可以不被雷达检测到（RadarInvisble=yes）
SENSORS
单位可以检测隐形单位（Sensors=yes）
FEARLESS
单位被杀伤时不会匍匐（Fearless=yes）
C4
单位拥有C4炸弹，TS残留，在RA2/YR中仅更改单位攻击建筑时的光标而不实际赋予绑炸弹的能力（C4=yes）
TIBERIUM_PROOF
单位可以免疫矿，TS残留无效（TiberiumProof=yes）
VEIN_PROOF
免疫泰伯利亚藤蔓，TS残留无效（ImmuneToVeins=yes）
TIBERIUM_HEAL
单位可以在泰矿上被治愈，TS残留无效（TiberiumHeal=yes）

原版缺少升级后免疫辐射、免疫超时空传送、免疫毒气、免疫精神攻击、免疫心灵控制的效果，Ares已补充并拓展，还给了单位升级后变成另一个单位的功能可以更方便的支持其他可设定的效果
--------------------------------------------------
EliteAirstrikeTeam =
精英鲍里斯召唤空袭的数量
EliteAirstrikeTeamType =
精英鲍里斯召唤空袭的飞机
EliteAirstrikeRechargeTime =
精英鲍里斯召唤空袭的间隔
ElitePrimary =
填武器名。这个代码指定单位精英时使用的主武
EliteSecondary =
填武器名。这个代码指定单位精英时使用的副武
EliteOccupyWeapon =
填武器名。这个代码指定步兵精英时使用的驻军武器
EliteWeaponX =
填武器名。这里的X指的是武器序号。这个代码指定精英级别多武器单位使用的武器
EliteStage1 =
EliteStage2 =
EliteStage3 =
EliteStage4 =
EliteStage5 =
EliteStage6 =
盖特武器[X]阶保持到计数器达到多少后转到下一阶，这里的[X]有效范围受制于WeaponStages的值
最后一阶由于不存在下一阶所以会保留当前阶段，想要跳到第一阶往往使用一个FireOnce的武器搭配RateDown=0来实现，但是会丢失原目标需要重新索敌，Ares引擎允许语句控制最后一阶跳转第一阶，详见Ares说明书
EmptyReload =
填时间。这个代码指定单位弹药完全用完后重装弹药的所耗时，覆盖Reload
原版下每次只能装1枚弹药，Ares允许定义
EMPulseCannon =
填yes或no。这个代码指定建筑可否用EMP武器。EMP武器是从TS遗留下来的。原版引擎无效，残留[硬编码]:EMPulseCannon=yes时该建筑不会主动发射它的Primary
Engineer =
填yes或no。这个代码指定步兵是否为工程师。强制单位不会主动攻击，也不会寻敌，当然手动攻击依然是可行的
EnterBioReactorSound =
复制中心回收的声音，实际只读全局，PhobosBuild47已修复
EnterGrinderSound =
部队回收厂回收的声音，实际只读全局，PhobosBuild47已修复
EnterTransportSound =
填Sound.ini中定义的声音名。这个代码指定的是单位进入运兵单位时的声音
EnterWaterSound =
进入水域时的声音，仅步兵可用
ExitCoord =
格式X,Y,Z。这个代码指定的是战车工厂或兵营制造出的单位初始创建的位置，例如https://www.bilibili.com/opus/637024588733087767
事实上兵营的出厂位置由[GDIBarracks|NODBarracks|YuriBarracks]那三条控制
战车工厂需要WeaponsFactory=yes才会尊重这句的设定，对于地面载具由于还有一个开出去的行为所以会瞬移到厂内通道
Explodes =
填yes或no。这个代码指定的是该单位是否能够在被摧毁时爆炸并伤害到邻近的单位，爆炸武器是主武。当然也可以用DeathWeapon=来专门设定
对于Aircraft类强制开启
同时爆炸必然同时杀死所有载员、建筑在Buildup与出售时也会正常引爆（Phobos允许更改这一行为结果）
会被单位当前主要武器（包括IFV的任何模式所对应的唯一武器）上的Suicide=yes覆盖并强制执行，例如原版IFV装了恐怖分子和伊文的情况
Explosion =
填动画名。这个代码指定的是单位和建筑爆炸时播放的动画。用于建筑时会在建筑所占的每个格子都播放一个
一种特殊情况下因为特殊设定启用了DeathWeapon而导致了Explosion被隐藏，这种情况下只是不绘制而TrailerAnim还是SpawnsParticle均正常执行，虽然一般也不会有人遇到这种情况
ExtraPower =
填数值。这个代码指定建筑特殊状态更改的额外电力
原版的使用实例是裂缝产生器与尤里电厂，且这两个逻辑可以共同使用，但工作方式略有不同
1.决定了部署行为（需要裂缝产生器相关逻辑）所改变电力值，可以使用一个负值进行设定，也就是部署后增加耗电量
2.设定了每有一个单位单位进入这个建筑所提供的额外电力
对于裂缝部署行为的ExtraPower，当电力低于-ExtraPower的情况下无法部署，已部署的会落回非部署状态
也就是如果使用了一个+50的ExtraPower那么基地欠电超过50点（当前电力<-50）的时候会禁用部署
同样也可以用-2147483647完全禁用一个建筑的部署（要求当前电力富余值达到2147483647）
对于生物科技发电的ExtraPower如果使用了一个负值那么进入单位不会对电力值造成影响
注：ExtraPower不会改变电力条的总长，只会改变绿色部分相对于现有电力条长度的占比
注：对于不使用GapGenerator的生物科技发电其部署释放单位效果不会受当前电力值限制
Enslaves =
奴隶矿场的奴隶类型，填步兵，当建筑被摧毁时奴隶会被释放

 -F-
Factory =
填下表中的对应项。这个代码指定工厂类建筑的生产类型
------------------------------------------------
InfantryType	步兵工厂，一般用在兵营
UnitType		战车工厂，一般用在重工
BuildingType	建筑工厂，一般用在基地
AircraftType	战机工厂，一般用在机场
注意：哪怕一个建筑纯粹用于生产Aircraft而Helipad=false不作为停机坪，那么它也仍然要有NumberOfDocks设置来避免生产卡住
此外原版下任何一个Factory类建筑都会被计入同类的多工厂加成中，也就是你可以在Ares中靠某个建筑存在时Deliver一大堆Factory=UnitType的假建筑来制作生产加速效果，Phobos已允许设定特定建筑被多工厂加成排除在外
------------------------------------------------
注意：
1、VesselType已经不再使用
2、船厂为Factory=UnitType+Naval=yes
并且对于Teleport的VehicleType会直接将其传送到集结点而不是需要先Drive到集结点后才开始使用Teleport
3、	CloningType可以使用但没有什么效果
4、如果AI已经没有了任何Factory类建筑，并且一段时间内没有被攻击，那么它就会开始卖家冲锋（然后被快速游戏毙了）
只有Buildup上禁止出售才能保留一些建筑，不让玩家直接爽到。Phobos已允许【全局】层面控制是否出售和是否冲锋以及执行这个操作的延时
Fake =
填yes或no。RA1残留无效，Ares已复原，详见说明书
Fearless =
填yes或no。这个代码指定步兵是否永不畏惧
注意：当为yes时，步兵的恐慌时的匍匐、哀叫将会被取消
实际上还有禁止匍匐切换的效果，例如Cyborg需要这句来让自己匍匐状态不会自动站起来
如果一个Jumpjet步兵拥有Fearless=yes，那么它会计算弹头的ProneDamage
注：原版[BORIS]下并没有此句，其不会爬倒是依靠在artmd.ini中为步兵图像设置Crawls=no实现的
Fighter =
填yes或no。这个代码指定Locomotor=Fly的单位能否在射程内正常发射任意抛体类型的武器。实际上也是导致战机抛双弹、开火有个随机前摇的元凶
FireAngle =
填0-64的数值。这个代码指定单位炮管的倾斜度。“0”为水平，“64”为竖直
默认值并不是0所以如果使用了炮管并希望无角度请记得手动调.jpg
在特定方向上存在视觉上突然变成FireAngle=0的问题，然而这个功能到RA2以后本就是纯粹的视觉效果，所以直接当这逻辑半残好了
FirestormWall =
填yes或no。这个代码是从TS遗留下来的，残留效果让建筑可通行单位，Ares已复原整套逻辑，并将可否通行的效果分离出了单独的语句，详见说明书
FlightLevel =
填数值。这个代码指定空军单位的飞行高度，同时要有Locomotor=Fly的设定。默认全局值
如果低于207那么会被影响空地判定，此外低于207高度的机场战机只有打空弹药后才会坠毁
并不会因为没有机位而坠毁，同时也无法正常探开黑幕，且弹药没打完就摧毁目标那么YR下会飞向地图边界
可以为负数，在地下，但开火踹乘客乘客会带着降落伞闪现到地面
ForbiddenHouses =
填国家名。这个代码指定该单位不能被指定的国家所建造，即使指定的国家所有条件都满足了
Fraidycat =
填yes或no。这个代码指定步兵是否在受到打击后做出逃跑的动作。逃跑的动作由Art.ini中步兵的Sequence中的Panic=指定
FreeUnit =
填载具名称。这个代码指定建筑建造后是否附带1个单位，原版用于矿厂
所赠予单位的生成地点硬编码按SpeedType=Wheel来寻找可用单元格
赠送单位的造价不能高于建筑，否则覆盖建筑造价
此外，如果多个工业工厂叠加造成建筑或载具至少任意一个的价格过低会导致FreeUnit不工作
这个语句附带将对象注册进VehicleTypes中的效果
也就是填写BEAG或APOC,APOC相当于向[VehicleTypes]中注册了名为[BEAG]和[APOC,APOC]的两个载具
并导致地图编辑器等使用注册Index序号的地方错号
出于对部分新手创造力水平的敬佩特注解上述示例
Phobos早期版本的CreateUnit也是如此，后来的版本去掉了这个效果并且生成的类型不再仅限载具类
FactoryPlant =
这个建筑是否是工业工厂，开启下面的这5个语句，Ares允许在单位上再单独定义一个倍率与此处相乘以微观控制
[BuildingType] -> InfantryCostBonus=<float>
[BuildingType] -> UnitsCostBonus=<float>
[BuildingType] -> AircraftCostBonus=<float>
[BuildingType] -> BuildingsCostBonus=<float>
[BuildingType] -> DefensesCostBonus=<float>
这五句用于设定工业工厂建筑导致的特定类型单位价格倍率，例如原版工业工厂第二项为0.75故载具生产成本*75%

 -G-
GapGenerator =
填yes或no。这个代码指定建筑是否为“黑幕产生器”
GapRadiusInCells =
填数值。这个代码指定“黑幕产生器”建筑产生的黑幕半径。要和GapGenerator=yes配合使用
Gate =
填yes或no。这个代码指定建筑是否为“门”型建筑，已方单位进入已方的“门”型建筑时，“门”型建筑就会打开。另外敌方间谍伪装进入时，已方“门”型建筑也会打开
GateCloseDelay =
填时间。这个代码指定“门”型建筑关闭的所花时间。要和Gate=yes配合使用
GDIBarracks =
填yes或no。这个代码指定该建筑是否为盟军兵营，步兵从相对建筑中心位于[1,2]的格子离开建筑，用来给AI判断的。所有南北向短于东西向的兵营都应该使用，否则会导致生产一个飞行步兵后无法继续生产其他步兵等问题
GuardRange =
填数值。这个代码指定该单位的警戒距离，用于围墙则代表围墙的连接距离，TS激光墙逻辑与Ares战壕逻辑的连接距离也是同理
默认的警戒距离使用当前主要武器的Range，如果指定则主副武器都使用此值而不是根据各自的Range分离计算范围，对于使用Range=-2武器的单位如果想要让它这个无限射程武器正常主动索敌那么是非常有必要的，拥有Organic=yes和Underwater=yes以及SelfHealing=yes的单位忽略该项直接使用GuardRange，例如原版巨型乌贼
如果你手动指定了GuardRange来控制警戒范围，并且GuardRange大于武器的Range，那么你应当与DefaultToGuardArea=yes搭配使用，以便单位进入区域警戒(Area Guard)然后前去迎击。否则单位会保持锁定状态但不靠近目标，由于射程够不到目标而无法开火，只能干愣着，可参考去掉DefaultToGuardArea的巨型乌贼
当然你仍可手动选中单位然后手动指定目标，用手动下令检查目标OutOfRange相关的判定来让单位接近目标并正常开火，但那也早已不是GuardRange相关逻辑的范畴了
此外原版并没有EliteGuardRange，当然你可以使用Ares的升级变形逻辑完全变为另一个单位来解决，详见Ares说明书
如果使用默认规则那么会考虑原武器实际能否射向目标，例如原武器有[Projectile] -> SubjectToWalls=yes那么默认寻敌不会越过墙类覆盖物，但是如果使用GuardRange设定相同的范围则会移动以绕过覆盖物来发起攻击
Gunner =
填yes或no。这个代码指定载具是否可以依据不同情况转换炮台。在红色警戒2中只能用在多功能步兵载具上
如果没有TurretCount则依然不会开启IFV逻辑，因为Weapon[X]系统的开启需要TurretCount>=1所以踢载员时依然是一脚全踢完
Ares修复了该BUG，现在即使不启用IFV逻辑也会保留第一个载员，但载员大于1时的格点会使用IFV的PassengerPips显示模式（把第一个放到前面）
也就是IFV位x1+载员位xN无拓展引擎的情况下仅注册名为[FV]的IFV可以显示炮塔
如果某辆IFV的武器数无法支持到IFVMode=那么程序会直接让IFV没有任何可以使用的武器
IsChargeTurret的优先级高于IFV逻辑，与其合用可像IFV一样两次踢人而不启用IFV逻辑
Grinding =
该建筑是否为部队回收厂
原版下与InfantryAbsorb和UnitAbsorb搭配使用并不正常，Phobos已修复

 -H-
HalfDamageSmokeLocation =
填X，Y，Z的数值。这个代码指定载具冒黄烟的开始位置
HalfDamageSmokeLocation1 =
填X，Y，Z的数值。这个代码指定建筑冒黄烟的开始位置
HalfDamageSmokeLocation2 =
填X，Y，Z的数值。这个代码指定建筑冒第二个黄烟的开始位置
Harvester =
填yes或no。这个代码指定单位是否为矿车。用于超时空载具可取消其超时空移动的硬直时间
也就是直接用于没有Teleporter的Locomotor=Teleport的单位会无CD超时空移动
HasRadialIndicator =
填yes或no。这个代码指定建筑是否拥有攻击范围圆弧（如机枪碉堡的那种圆弧），Ares已允许所有科技类型使用，并允许使用专门的语句指定半径，详见说明书
圆弧的半径由CloakRadiusInCells=或GapRadiusInCells=或SuperGapRadiusInCells=指定
或者也可以设定成PsychicDetectionRadius=，这是另一种雷达扫描效果（苏军的“心灵感应装置”那种圆弧效果）
仅限于BuildingType的Primary，所以盖特机炮的圆环范围不取决于WeaponX
当武器Range=-2时该操作无效
原版下这个效果只能友军可见，Phobos已允许【全局】设定
HasTurretTooltips =
填yes或no。这个代码指定运兵单位运兵时是否显示武器名称，“<多功能步兵>载具”，而且运兵量必须为1。Ares已扩展全套逻辑，详见说明书
针对该句，IFV的名称显示规则如下：
如果不存在任何步兵（Infantry）Passenger，那么载具仅显示为UIName=指定的内容
如果为VehiclePassenger，不属于InfantryPassenger规则如上
如果为InfantryPassenger，UseOwnName=yes，显示为<Passenger> <UIName>
如果为InfantryPassenger，UseOwnName=no：
	若使用Tur[1]，显示为{(CSFLabel        Tip:MachineGun) ([TransportVehicle] -> UIName=)}
	若使用Tur[2]，显示为{(CSFLabel        Tip:Repair    ) ([TransportVehicle] -> UIName=)}
	若使用Tur[3]，显示为{([InfantryPassenger] -> UIName=) ([TransportVehicle] -> UIName=)}
	若使用Tur[X]，显示为{(CSFLabel        Tip:Rocket    ) ([TransportVehicle] -> UIName=)}
在RA2中不存在UseOwnName，但若主武弹头存在Bullets=yes则强制显示为“Machine Gun IFV”
HasSpotlight =
填yes或no。这个代码是从TS遗留下来的，在红色警戒2和YR除了给你个005F5155以外没什么作用。Ares已复原该逻辑，详见说明书
HasStupidGuardMode =
填yes或no。这个代码指定建筑是否能够自动攻击敌方目标。填yes时不能自动攻击
实际上决定建筑使用哪一套威胁值计算方式，详见全局DumbMyEffectivenessCoefficient部分
Helipad =
填yes或no。这个代码指定建筑是否为机场建筑。入侵者一类的需要机场的空军单位就从这里制造。注意：需要停在机场的战机应该在PadAircraft=的列表中声明
Hospital =
填yes或no。这个代码指定建筑是否为医院。进入医院的受伤步兵全部都会在短时间内痊愈。如果要限制治疗数量可以加入Ammo=来限制。注意：因为红色警戒2的内核问题看上去是治愈了步兵，其实是从医院出来了一个一模一样的同等级步兵，这时复制中心就会复制出另外一个一样的新兵。在尤里复仇中这个问题得到了解决
不要与兵营连用，弱智AI会倾向于这个兵是刷出来的新的单位而不是自己原本生产的单位于是一直造
HoverAttack =
填yes或no。这个代码原用于指定Jumpjet单位是否需要起飞以攻击目标，单位会在发起攻击时尝试起飞。但你也可以给地面单位使用，实际表现为打一枪移动一下（因为依然没能飞起来）
HoverPad =
填yes或no。这个代码是从TS遗留下来的
如果全局中的SeparateAircraft=no 则所有带HoverPad=yes的建筑会自动生成PadAircraft=的第一个单位
HunterSeeker =
填yes或no。这个代码是从TS遗留下来的，在红色警戒2中还有部分作用
该单位可以跟踪选定的目标，但是永久禁用实际开火和移动，Ares已复原，详见说明书
HarvestRate =
采集速率，YR中用于奴隶矿工

 -I-
IsGattling =
填yes或者no，该单位是否使用盖特武器系统，步兵无效
盖特逻辑即使Versus=0或LandTargeting=1导致当前武器无法发射也会继续升档
同样，它对地也不会根据LandTargeting=2换用偶数武器，你依然会看到最高阶奇数武器对地猛轰
注意：盖特逻辑单纯依照对地奇数武器对空偶数武器来处理，无法在奇数武器攻击不了时使用偶数武器，Phobos已硬编码改为允许
升档使用计数器实现，即处于开火状态每帧+RateUp，没有目标每帧-RateDown
通过这样的机制控制计数器的增减，当计数器超过Stage[X]指定的阈值后切换为[X+1]阶段
也就是说
WeaponStages=3
Stage1=100
Stage2=200
Stage3=300
代表计数器累加到100/200/300时进入第2阶段/第3阶段/保持3阶（因为没有4阶段可供3阶段升阶）阶段
而不是第一阶经过100帧后到第二阶，第二阶经过200帧后到第三阶
这也是旧时代实现一个单位多种武器的一种方法
例如

[VehicleType]
IsGattling=yes
Weapon1=FakeWeapon
Weapon3=Comet
Weapon5=120mm
Weapon7=M60
Weapon9=120mmx
WeaponCount=10
WeaponStages=5
Stage1=1
Stage2=1
Stage3=1
Stage4=1
Stage5=1
RateUp=1
RateDown=0

[CometWH]
Verses=0,0,0,0,0,0,1,1,1,0,0
[AP]
Verses=0,0,0,1,1,1,0,0,0,0,0
[SA]
Verses=1,1,1,0,0,0,0,0,0,0,0
[ApocAP]
Verses=0,0,0,0,0,0,0,0,0,1,1

那么由于一开火计数器立即达到1而所有阶段全开
由于Versus为0所以高阶武器攻击某个目标时会向下切回低阶武器
那么从弹头比率上区分类型靠盖特系统计数器武器选用规则来切换

上面的FakeWeapon是一个抹掉所有特殊效果Verses全100%的假武器，用于初始锁定目标和升阶
因为盖特的第一阶武器必然会先待命发射一次，哪怕StageX=0或RateDown<0初始累加计数器，那么也会先射一发一阶武器再跳到计数器所决定阶段的武器

InfantryAbsorb =
步兵能否进入该生化反应炉，同时开启特殊的建筑工作动画效果，即根据是否有步兵进入分别使用ActiveAnim1和2，不过3和4以及IdleAnim并不受影响
IdleRate =
填数值。单位空闲动画播放速率，素材中每帧实际播放多少帧。可用于shp载具vxl载具
IFVMode =
填多功能步兵载具的相关炮台数值。这个代码指定步兵进入多功能步兵载具后多功能步兵载具的状态
IgnoresFirestorm =
填yes或no。该单位是否无视火风暴墙，TS残留无效，Ares已复原，详见说明书
Image =
填Art.ini的图象定义名。这个代码指定该单位的图象
不设定时即和Art.ini中的名称相同。注意：Art.ini中的单位名称应该和单位对应的素材（SHP、VXL/HVA）名称相同，否则会无法显示单位的图象只会显示图标
重要问题：原版很多数据直接读取同名ART段落而非Image指定的ART段落，例如[A]Image=B则Foundation会先找ART中[A]的Foundation而不是[B]的
ImpactLandSound =
填Sound.ini中定义的声音名。这个代码指定单位被摧毁落地时的声效，如果有Crashable=no会半空爆炸
ImpactWaterSound =
AircraftType撞到水上的音效，已在全局定义默认值
Immune =
填yes或no。这个代码指定单位是否会受到损害
当为yes时单位为无敌状态，任何损伤都没有用。一般用于桥梁维修小屋一类的重要建筑
仅限物理伤害，心控/时空等特殊武器需要单独调用免疫条目
并且在指令上仅影响玩家手动锁定，所以主动寻敌或者卡光标Bug依然可以攻击只是不掉血
ImmuneToPsionics =
填yes或no。这个代码指定单位是否免疫精神武器。注意:建筑默认yes 其他单位默认no
ImmuneToPsionicWeapons =
填yes或no。这个代码指定单位是否免疫尤里气波类精神攻击武器，默认同上一句
YR下免疫神经车毒气的与否也跟随ImmuneToPsionics的设置，在Ares中可以独立控制
ImmuneToRadiation =
填yes或no。这个代码指定单位是否会受到辐射类弹头的影响
然而蛋疼的是这个标签只影响杀伤和手动索敌，所以你在原版就能见到AI家和你家的DESO激情对射，或者你的DESO靠近AI家附近开始对AI家的矿车射个不停
ImmuneToVeins =
填yes或no。这个代码指定步兵单位是否会受到泰矿废矿伤害，TS残留无效，Phobos已复原，详见说明书
Infiltrate =
填yes或no。这个代码指定步兵是否可以“渗透”建筑物，然而没有任何其他效果
C4=yes、Engineer=yes、Agent=yes、Assaulter=yes等可以独立于该语句使用，自带进入效果
不过各种针对建筑的进入和特殊攻击行为最终执行的只会有一种
大致优先级排序为[ occupier > assaulter > engineer > C4 > Ivan > agent > thief ]
InitialAmmo =
填数字。这个代码指定该单位出厂时的初始弹药数。当不设定时，初始弹药数为Ammo=的数值
Insignificant =
填yes或no。这个代码指定该单位是否为“无关紧要的单位”一般用于平民中立单位
即在破坏时EVA不会播发EVA_UnitLost的讯息，ai也不会主动攻击它
会使建造限制（BuildLimit）、机位限制、超武、触发事件等很多逻辑失效
在YR中被心控的单位会被AI视为有效目标
*对于可以正常播放EVA_UnitLost的单位Ares已经允许微观定义具体的EVA条目或关闭EVA播报而无需此类语句支持
注意：该句有时会导致手动建造的建筑在通过工程师占领或伤残等方式刷新状态前不显示图像
Invisible =
填yes或no。这个代码指定该单位是否无形，仅对非所属方有效，不过非所属方依然可以看到其生成的其他动画。建筑上不佳，直接用下句建筑专用的即可
InvisibleInGame =
填yes或no。这个代码指定建筑是否不能被游戏者发现和选中、攻击等，只能看见它的动画等特效。一般用于灯光建筑
可以攻击，但免疫物理伤害，不过例如海豚波的穿透伤害和粒子伤害等可以正常生效
不应该用于玩家可拥有的建筑，否则会导致重连错误（RE）
IsBaseDefense =
填yes或no。这个代码指定建筑是否为防御建筑，AI会根据选项来自动建造防御工事来防御自己，对于水上防御塔需要添加Naval=yes来让AI认识
IsChargeTurret =
填yes或no。充能炮塔如光棱坦克，用于Voxel炮塔，攻击一次后将TurretCount所指定量的炮塔逐个播放，来表现一种下次开火前逐步充能的效果
同时这个逻辑虽然使用WeaponX系统但实际上只会使用Weapon1和EliteWeapon1，也常被用于证明单武器效果
这个逻辑下最好武器ROF>=TurretCount因为逆序播放几号炮塔是根据ROF/BurstDelayX余量结合TurretCount计算的
以原版SREF举例，炮塔素材有sreftur+sreftur[1|2|3]共4个对应TurretCount=4参数设定
如果ROF=4，那么常态使用tur，开火后变为tur3，下帧变为tur2，再下帧变为tur1，然后满
如果ROF=3，那么常态使用tur，开火后因为ROF从一开始只剩3，于是直接跳过tur3使用tur2
Phobos已允许独立每个武器和Burst独立于ROF/BurstDelayX设定控制炮塔充能动画切换的这一参数，详见说明书
IsCanine =
填yes或no。RA1残留无效，因为已经被DetectDisguise=yes替代了
IsDropship =
是否为DropShip，实际上这个东西只在TS的战役里出现过，这句与吊运逻辑一样可以让FlyLocomotor的单位降落时播放一个动画，详见Locomotor词条注解
相较于吊运逻辑，这个语句不仅限Aircraft使用，并且可以禁用FlyLocomotor自带的硬编码上下浮动浮动效果，但也会引入其他硬编码效果
IsSelectableCombatant =
填yes或no。这个代码指定该单位是否能被玩家按N和M选中，也影响P选和框选，不过由于原程序发送事件的缓冲区限制因此一个指令同一帧内只能对最多128个对象下达
IsSimpleDeployer =
填yes或no。这个代码指定该单位部署后会变成另一个图像，但实际上仍然是同一个单位，例如原版武装直升机，部署后
武器使用Secondary与EliteSecondary或Weapon2与EliteWeapon2指定的副武器，盖特逻辑无法升档，光棱充能炮塔逻辑会失去武器，哪怕WeaponCount=2解开数量限制也无法手动控制其攻击，只能通过主动寻敌来开火，并且依然使用Weapon1所指定的武器
图像使用UnloadingClass=指定从哪个单位获取，例如UnloadingClass=MTNK，又由于原版MTNK使用Image=GTNK实际使用的是GTNK作为图像，因此Deployer状态下会变为GTNK
由于该标签仅对Vehicle有效，所以需要与这个标签合用的Ares的Convert.Deploy等功能也随之在实际应用范围上仅限Vehicle
事实上处于SimpleDeployer状态的VehicleType比常态BuildingType在超远程Arcing抛射体精度上问题上还要更高一些
IsTilter =
填yes或no。这个代码指定单位在斜坡上是否会倾斜，然而这个标签是废的
只要Locomotor为Drive(包括没钻地时的Tunnel)都会倾斜，于是原版超时空矿车静止时总是不倾斜，Phobos已修复
IsTrain =
填yes或no。这个代码指定载具单位是否为火车。可以碾压矿场之类可以踩上去的建筑
如果是从工厂开出来的可能造出来就把工厂压毁了而直接在仓内暴毙开不出来
多个火车之间不会互相考虑，也就是扎堆移动可能互碾
火车逻辑碾压一切，毕竟本来就不是所谓碾压等级，而是高度客制化的检查轨道上有没有东西如果有就一头创死。但是如果火车逻辑额外拥有碾压语句，那么再碾死目标时碾压逻辑优先执行诸如碾压触发死亡武器设定之类的效果
Ivan =
填yes或no。这个代码指定步兵是否为疯狂伊文类型的单位，作用是和电脑作区分强制步兵Attack光标为IvanBomb，绑不绑纯看单位是不是步兵和弹头能不能绑，Ares已允许非步兵单位正常使用IvanBomb类弹头
InfantryGainSelfHeal =
科技医院效果，回血血量的倍率，每隔SelfHealInfantryFrames时间，步兵恢复该值*[General] -> SelfHealInfantryAmount=数量的血量，此外Organic=yes的载具也被算入
IsPlug =
该建筑是否是插件塔，用于全局IonCannonValue判定
据说在TS中该语句会判定建筑注册名是否为[GAPLUG]然后强制启用一些诸如硬改Foundation的硬编码效果，RA2中倒是似乎砍完了
IsTemple =
该建筑是否被视为神殿，用于全局IonCannonValue判定
IsThreatRatingNode =
该建筑是否为威胁评级节点，使单位智能AI更好的评定威胁级，使用default threat来取代dumb threat
然而似乎没什么卵用，强制开启
InfantryCostBonus =
步兵建造价格为原来多少倍

 -J-
JumpJetTurn =
拥有[TechnoType] -> Locomotor=Jumpjet的飞行步兵能否使用正确的朝向绘制开火位置，并在移动和转向时禁止开火

JumpJet =
填yes或no。这个代码指定单位是否为Jumpjet式飞行，一般与Locomotor=Jumpjet合用，仅用于一些判定，实际运动模式由Locomotor决定
会导致单位不会自动采矿
以下语句在[TechnoType] -> Locomotor=Jumpjet且单位处于空中时使用
（也就是远距离飞行近距里步行的飞行兵仅在飞行时使用JumpjetSpeed在地上用Walk时正常使用Speed）
注：原版INI中WW大小写非常不规范，除上面两句外其余的Jumpjet系列语句第二个j均为小写
也就是原版很多单位下的JumpJetAccel和JumpJetTurnRate是无效的，实际取了全局默认值
但是你如果改回正确的标签让它生效了，你会发现WW那些无效标签填的值简直是瞎写，并且会导致并不正常的效果
JumpjetAccel =
填数值。这个代码指定飞行单位在移动中加速的比率，一般填整数
减速度为JumpjetAccel*1.5
如果写的很高会导致单位还没有抵达目的地就被减速而无法完成移动指令，例如尝试降落但永远无法降到地面而是卡在比平飞高度低一些的位置，并且会导致单位会重叠在同一个格子中，而且攻击非面向方向的目标可能会指令无效。但是以外的解决了原版的JumpjetLocomotor载具Turret=yes则炮塔始终朝向正东的问题，当然现在不需要用这种歪法了
JumpjetClimb =
填数值。这个代码指定飞行单位在越过山崖等高地时的攀登速度
JumpjetCrash =
填数值。这个代码指定飞行单位被摧毁时坠地的速度，一般不要大于15
一定要比JumpjetClimb大，否则可能在建筑上坠毁时永远转圈但不死的情况
原版下JumpjetLocomotor的单位坠毁时总会转着圈掉下来，Phobos已允许定义（毕竟像《世界轴承》中RITC阵营的NMSL号空天母舰那样的大型飞行载具转着圈坠地给人的感觉实在有些太蠢了）
JumpjetDeviation =
填数值。这个代码指定飞行单位浮动的幅度
JumpjetHeight =
填数值。这个代码指定飞行单位的飞行高度，通常设置为800
只要起飞，实际达到的平飞高度坐标最低255以上
JumpjetNoWobbles =
填yes或no。这个代码指定是否禁止飞行单位浮动。填yes时为禁止该单位浮动
JumpjetWobbles =
填数值。这个代码指定飞行单位的浮动频率，不能为0，不需要浮动请用上句
JumpjetSpeed =
填数值。这个代码指定飞行单位的平飞速度，即在没有地形影响时飞行单位的运行速度
JumpjetTurnRate =
填数值。这个代码指定飞行单位掉转方向的速率，当JumpjetSpeed/JumpjetTurnRate足够大时即可让Jumpjet像Fly那样盘旋，例如https://www.bilibili.com/opus/764036774809829440
原版写的过小可能反而瞬间转向，Ares下会崩溃

 -K-
KenosisBlessedIt =
让这段代码获得Kenosis的保佑（并不

 -L-
Landable =
填写yes或no。决定该AircraftType是否能够在地上、母舰甲板或是具有[BuildingType] -> Helipad=yes的建筑上着陆，与[TechnoType] -> Spawned=yes有一些令人疑惑的联动
默认为no，所以你必须手动把它设定为yes才能让[TechnoType] -> Locomotor=Fly的单位着陆
对于不回机场（AirportBound=no&Dock=none）且Landable与Selectable任意为no的战机在目标丢失后会离开地图，例如原版伞兵飞机
LeadershipRating =
用于AI小队中的队长判定，选择该值最高的单位作为队长进行寻路和目标判定，该值默认为5
LeaveRubble =
填写yes或no。表示建筑死亡后会不会留下残骸废墟地表（油井，医院等），实际使用RUBBLE_OVERLAY这个覆盖物在原Foundation占用的格子上占地，需要建筑素材自身的特定帧作为图像，可自行提取原版平民建筑了解
LeaveBioReactorSound =
脱离复制中心回收的声音，实际只读全局，PhobosBuild47已修复
LeaveGrinderSound =
脱离部队回收厂回收的声音
LeaveTransportSound =
填Sound.ini中定义的声音名。这个代码指定运兵单位中的单位释放时的声音
LegalTarget =
填yes或no。这个代码指定该单位能否被直接攻击（即在不按下Ctrl键强制攻击的情况下）。典型的应用是平民的医院不能被直接攻击。注意：当按住Ctrl强制攻击时，即使你设定了LegalTarget=yes，该单位都会遭到攻击
LeaveWaterSound =
离开水域时的声音，仅步兵可用
LeptonMindControlOffset =
这个单位被心控时心灵控制线的结束点向上偏移多少，起始点是心控方FLH
YR新增，算法非常智障，竟然是用Lepton而不是Pixel而且也不是等比扩大，默认70在大多载具炮塔的位置

Locomotor =
运动模式 与单位类型无对应关系 只是通常用法
注：
以下SpeedType默认值均默认用于Vehicle或Aircraft
步兵(Infantry)无论什么Locomotor都默认Foot

{4A582741-9839-11d1-B709-00A024DDAFD1} 地面载具载具
简称Drive
SpeedType默认Wheel，若Crusher=true则默认Track
如果步兵使用且设置了一个极低的速度那么在第一次接近目标单元格时会直接停下并永远完成不了移动动作也无法用新指令覆盖这一动作

{4A582742-9839-11d1-B709-00A024DDAFD1} 悬浮载具（遥控坦克 气垫船）
简称Hover
SpeedType默认Hover
Drive与Hover在不考虑加速度和SpeedType等因素下速度比大致为14:17
被瘫痪(YR遥控坦克断电、TS的EMP和离子风暴等)会落到地面静止或坠海喂鱼
使用该Locomotor的运输单位如果SpeedType不是Hover，那么释放乘客时虽然可以D键部署正常释放，但手动释放会显示为不能部署的光标也点不下去，除非你用IsSimpleDeployer等语句让它为别的行为显示可以部署的光标，不过那就又要引入其他语句的特性了~
使用该Locomotor的单位如果速度过高那么非直线移动时的轨迹会比较飘逸，并且原版Arcing类抛射体对这类目标的落点计算会很难精确处理

{4A582743-9839-11d1-B709-00A024DDAFD1} 钻地载具
简称Tunnel
SpeedType默认与Drive相同
并不存在Underground这个SpeedType！那是DeeZire教程中遗留下来的错误！
当目标地块的AllowBurrowing满足时才可以向下钻取
距离目的地的距离高于 11 个单元格则会选择钻地
潜地下潜速度由[TechnoType] -> Speed= * [General] -> TunnelSpeed=定义
潜地钻地动画与音效由全局[AudioVisual] -> Dig=与[AudioVisual] -> DigSound=定义，但是由于[AudioVisual] -> DigSound=还被WW在RA2开发过程中拿去做核弹警报音效（他们为了赶Demo版直接使用了由于RA2中并不使用而被他们认为毫无意义的这个INI标签作为接口）因此不便使用，Ares对钻地动画与音效以及超武生效音效全部微观定义，并且允许分离钻入和钻出时的不同效果，详见说明书
潜地平移速度与高度为硬编码，Phobos已允许定义
常规移动速度由单位Speed定义
原版下无法正常翻转与倾斜，Phobos已修复

{4A582744-9839-11d1-B709-00A024DDAFD1} 地面步兵
简称Walk
SpeedType默认与Drive相同(步兵情况见上文)
允许由Sequence的相关项控制在水里的移动图像
空投时步兵的阴影使用infshdw.shp，降落伞使用全局[General] -> Parachute=的动画，原版为parach.shp
空降仓超武的步兵在空中时，使用pod.shp，但是原版Ra2空降仓相关逻辑砍了
使用该Locomotor的步兵如果速度过低那么在向SW/NE方向移动时会总是中间想要向正S/N方向走两步再转回去

{4A582745-9839-11d1-B709-00A024DDAFD1}
简称DropPod
用于空降仓，TS残留。直接给单位用上会稳定炸裂祭天7C812FD3/7587845D
可以通过磁电弹头使用，但会留下空气墙，光标悬浮在单位上于原位置显示血条，Bug很多
载具可以用碾压和超时空碾爆，战机会崩并且极易内存损坏导致EIP只能抛出00000000或一个极大数而不是实际的崩溃地址

{4A582746-9839-11d1-B709-00A024DDAFD1} 机场飞机飞行运动模式
简称Fly
SpeedType默认Winged，然而寻路的时候实际按MovementZone=Normal和SpeedType=Track来找空地
于是因为原版[Water] -> Track=0%禁止SpeedType=Track的单位移动上去，原版战机直接点击移动到水上是无法正常执行的
也可以用于载具，但会造成一些问题，例如影子直接画在本体上
根据在Art中的Trailer可以拥有一个尾烟，然而这个尾烟哪怕降落在机场也不会停……
对于Aircraft使用该Locomotor可以使用Carryall=yes来吊运载具
* 原版雌鹿直升机是Vehicle并且Locomotor也不是这个所以Carryall无效
拥有Carryall=yes的Aircraft落地会播放名为[CARYLAND]的动画
拥有IsDropship=yes的Techno落地会播放名为[DROPLAND]的动画
最好不要用于Infantry，极易随机IE

当处于空中时被瘫痪(EMP/离子风暴)会直接祭天
根据Fighter的值决定是轰炸还是悬浮定点开火，Fighter=no且非五连发抛射体时为悬浮定点开火，此时遵照全局[General] -> CurleyShuffle=控制是否打一发换个位置

{4A582747-9839-11d1-B709-00A024DDAFD1} 超时空运动
简称Teleport
SpeedType默认与Drive相同
所以想要超时空移动到水上需要修改SpeedType
如果工厂具有Naval=yes，那么这个单位会生成后直接传送，而不需要慢慢开出来
原版下无法正常翻转与倾斜，Phobos已修复

{55D141B8-DB94-11d1-AC98-006008055BB5}机甲
简称Mech
SpeedType默认与Drive一样
使用该Locomotor的单位如果速度较低那么会走几步改变一次朝向(WW似乎打算以此表现一种“振动”的效果https://www.bilibili.com/opus/746197069772881955)，在非 Phobos 环境下还有速度限制，很多时候还不如用VXL地面载具通用的Drive
部分旧词典从DeeZire教程翻译来说这样的单位可以使用Powered，然而这个效果仅生效于TS，RA2下并不存在，但是从YR开始可以使用遥控坦克的PoweredUnit实现类似的效果
同时如果在水上下沉时会表现为竖直下沉而不是翻船

{92612C46-F71F-11d1-AC9F-006008055BB5} Jumpjet单位
简称Jumpjet
SpeedType默认Hover
该运动模式在JumpJet和BalloonHover至少一句为yes的情况下初始生成后就会立即尝试移动升空而无需等待玩家手动发出的移动指令
这一特性也可以与Teleporter=yes结合使用来做出DriveLocomotor的单位生成后先移动一下的效果
（例如使用Ares的Deliver超武搭配一个空降仓落地动画来假拟轨道投送单位那么可以用这个特性来做内部载具类单位着陆后立即开出空降区域的效果）
对于Infantry在判定某个格子能否移动上去时硬编码视为SpeedType=Hover的情况来处理，也因此Locomotor使用Jumpjet类的Infantry无法停留在建筑和悬崖上
原版部分Jumpjet单位的标签中第二个J的大小写可能是错误的导致它们实际上读取的是全局[JumpjetControls]中设定的默认值
如果想要保留原版的效果直接把那几句删了或者改小写后抄上默认值即可，如果直接用原版错误标签后面WW赋的值反而会被非常不合适的数值坑到
* 2025版词典中 -J- 部分的Jumpjet标签均为大小写正确的有效标签，可供对照
这个运动模式的单位起飞时总是突然转向正东方向，Phobos已修复
Aircraft也可以使用这个Locomotor但是如果Ammo清空则无视Crashable=no强制坠落到地面然后不死，如果弹药无限或通过其他方式避免打空则可靠Crashable=no禁用被攻击导致坠毁从而正常使用

{2BEA74E1-7CCA-11d3-BE14-00104B62A16C}舰船
简称Ship
SpeedType默认Float

{B7B49766-E576-11d3-9BD9-00104B972FE8}导弹
简称Rocket
SpeedType默认Winged
例如V3导弹，无畏导弹，雷鸣导弹。原版参数设置在[General]且无法新增，新增需要Ares

其他：
游戏硬编码单位注册名为[DESO]时强制根据脚下地面辐射残留量决定能否部署释放武器。Ares允许定义一个单位是否使用这样的效果
游戏硬编码单位注册名为[COW]时会到处乱走，无论什么Locomotor，哪怕是Teleport。Ares允许定义一个单位是否使用这样的效果


LightVisibility =
建筑对地面染色（效果类似辐射）的范围，单位为Leptons，256为一格
这个效果在读档后将无法由于建筑被摧毁消除，Phobos已修复
LightIntensity =
建筑对地面染色的强度
LightRedTint =
建筑对地面染色的红色量
LightGreenTint =
建筑对地面染色的绿色量
LightBlueTint =
建筑对地面染色的蓝色量
LaserFencePost =
该建筑是否为激光墙节点，公版引擎下墙体只能为第一个拥有下句的建筑，节点可无限
拥有此句的建筑可以在拥有下句的建筑上建造，就像加载物那样，但是会直接移除原建筑
像围墙那样根据GuardRange决定延伸距离
若不存在LaserFence建筑那么Post之间不会显示连接的格子
注：如果你单纯只是想让建筑像墙那样一造早一排大可使用Ares提供的战壕逻辑，详见2025教程包附赠的Ares说明书
LaserFence =
该建筑是否为激光墙墙体，与上句共用于同一建筑会导致崩溃
YR1.001因为WW的疏忽导致激光墙墙体建筑将始终处于不工作状态，Ares已修复
强制拥有Immune=yes的效果，但是为了防海豹还是需要添加CanC4=no的
拥有这句的建筑在摆下前会清空矿石覆盖物，哪怕实际上最后没生成成功
对应的生成时它同一单元格的实体会被摧毁，步兵强制使用电死的效果
同样，根据Post链接时哪怕中间的格子被前两句所说的物体占据也不影响建造
而手动建造时更是可以直接在存在单位的单元格上建造
你可以利用这个性质配合现代拓展引擎当中的单位BaseNormal实现类似向单位上放置加载物升级的效果
你也可以利用这个性质控制某个建筑的初始摆放设置，只不过为了摆下后正常受伤要再走一步转化

帧使用规则为（此处以ShpBuilder中的序号举例，从1开始）
1-东西方向的普通墙体
2-西端与节点相连的墙体
3-东端与节点相连的墙体
4-东西方向两个节点中间唯一一节墙体（东西方向与两个节点相连）
——
5-南北方向的普通墙体
6-南端与节点相连的墙体
7-北端与节点相连的墙体
8-南北方向两个节点中间唯一一节墙体（南北方向与两个节点相连）
————
9-16用于断电与罢工状态
————————
17-32影子帧
LightningRod =
是否为避雷针，TS残留无效，Ares已还原相关逻辑，详见说明书

 -M-
MoveToShroud =
是否可以命令该单位进入黑幕里，AircraftType默认no其他默认yes
MobileFire =
填写yes或no，指定此单位是否有移动中开火和自动装填弹药的能力
如果设置为no则OpportunityFire=yes时仍不能移动时开火
MaxNumberOccupants =
平民建筑能进驻多少人
MissileSpawn =
填写yes表示此子机单位为导弹类子机（V3 无畏），母舰发射后立即进入SpawnRegenRate
第一次开火后立即消失，而非命中撞击使用导弹参数定义的爆炸或被拦截摧毁爆出DeathWeapon
是否为导弹类子机并不限定Locomotor，FlyLocomotor的Aircraft同样可以使用，而RocketLocomotor的Aircraft同样可以删除该语句或设no来允许跟踪（每次武器开火时刷新目标位置）
没有此语句的子机生成位置只遵循FL而H无效，Ares已修复
建筑航母生成Locomotor=Rocket的子机将会导致IE，Ares已修复
拥有这个语句的子机无法追踪目标单位也不同步母舰命令，Kratos已允许，且Kratos下的导弹即便拥有这个语句（例如原版V3无畏雷鸣导弹）其武器的目标也会是目标单位而不再是地面
ManualReload =
是否必须进一个UnitReload=yes的建筑才能装弹，RA1布雷车残留逻辑但有效
建筑需要可以Dock和Enter也就是得是维修厂和坦克碉堡以及矿场那类的建筑
战机默认yes，其他默认no，有一个特殊效果是
和战机一样需要在Dock=写上这个建筑

这样的单位弹药装满后会被内部额外装填一次，也就是Ares下满Ammo(Techno)时实际上开火时弹药改变量会按Ammo(Techno)+ReloadAmount-Ammo(Weapon)来算，视觉上就是第一发会消耗Ammo(W)-ReloadAmount的Ammo(T)
对应的如果Ammo(W)<=ReloadAmount就会出现满弹药下一直不消耗Ammo(T)的问题，除非有ROF(W)<<Reload(T)

MoveSound =
移动时发出什么声音，盖特武器Report使用类似的系统
MindClearedSound =
精神控制车控制的单位脱离控制的声音，YR新增
MindControlRingOffset =
这个单位被心控时心灵控制的标记动画向上偏移多少
YR新增，算法非常智障，竟然是用Lepton而不是Pixel而且也不是等比扩大，默认140在大多步兵脑袋的位置
MaxDebris =
对象被毁爆出碎片的最大量
MinDebris =
对象被毁爆出碎片的最小量

 -N-
NormalTurretIndex =
NormalTurretWeapon =
RepairTurretIndex =
RepairTurretWeapon =
MachineGunTurretIndex =
MachineGunTurretWeapon =
FlakTurretIndex =
FlakTurretWeapon =
PistolTurretIndex =
PistolTurretWeapon =
SniperTurretIndex =
SniperTurretWeapon =
ShockTurretIndex =
ShockTurretWeapon =
ExplodeTurretIndex =
ExplodeTurretWeapon =
BrainBlastTurretIndex =
BrainBlastTurretWeapon =
RadCannonTurretIndex =
RadCannonTurretWeapon =
ChronoTurretIndex =
ChronoTurretWeapon =
TerroristExplodeTurretIndex =
TerroristExplodeTurretWeapon =
CowTurretIndex =
CowTurretWeapon =
InitiateTurretIndex =
InitiateTurretWeapon =
VirusTurretIndex =
VirusTurretWeapon =
YuriPrimeTurretIndex =
YuriPrimeTurretWeapon =
GuardianTurretIndex =
GuardianTurretWeapon =

多功能步兵车IFV专用，炮塔编号及武器编号
两句连用指定几号武器对应几号炮塔，其他XXXTurretIndex和XXXTurretWeapon同理
XXX名字代码为程序内定，原版不可新增

Ares已扩展全套逻辑，详见说明书

Natural =
填yes表示不能攻击带有Unnatural=yes的单位
典型运用:狗和狂兽人

Name =
填任何内容。这个代码指定该单位的注释内容，在游戏中没有实际作用。地图编辑器等其他外部工具可能会读，也可能使用自己的新读取方式，但那就和游戏自身无关了
Naval =
填yes或no。这个代码指定该单位是否为海军单位。所有海军单位都应该有Naval=yes的设置，有这个设置的单位会被船坞类建筑生产
在Factory=UnitType的建筑上使用指定这个建筑为船厂，否则为战场工厂，同时禁用ExitCoord
也就是同样有Factory=UnitType，有Naval的生产建筑生产有Naval的载具，没有Naval的生产建筑生产没有Naval的载具
对于建筑，Naval=yes会强制该建筑放置在Water地块上，而不像WaterBound那样可以相对自由的设定，Naval=yes的该效果无视WaterBound的设置（在Phobos前）而对于AI建造水上防御塔行为判定而言书写Naval是完全有必要的
巨型乌贼式寄生相关见Organic一条的注解
原版下重工和船厂会共用AI的同一条生产线，Phobos下可以分离生产
NavalTargeting =
默认0
填下表中的对应项。这个代码指定单位对海攻击规则
攻击对象位于LandType=Water或Beach的格子上时才启用
----------------------------------------------------------------
0=水下单位隐身(视为没有上浮)时无法攻击
1=对水下单位始终使用副武攻击（原版驱逐舰）
2=对水下单位使用主武攻击，其他单位无法攻击（原版反潜机）
3=对有生单位或非生物体使用副武攻击，其他单位使用主武（乌贼对雷鸣）
4=对悬浮单位或有生单位使用主武攻击，其他单位使用副武（海豹手撸乌贼却不用C4）
*由于逻辑仅在目标位于水和沙滩上时运作，一辆SpeedType非Hover的载具在正常陆地上仍会被使用主武攻击，直到它移动到水面和沙滩上才会根据NavalTargeting=4的效果换用副武
5=对一切对象使用主武器攻击，主武无法攻击则切副武
6=对一切水上物体都无法攻击，包括水面（原版狗和恐怖机器人）
7=对一切对象使用主武器攻击，主武无法攻击则切副武
（通过解析程序运作方式得出结论：除012346外的数值都一样，也就是-1/5/7/8都是相同的效果，因此5和7也是完全相同的，Westwood在原版INI中对7的注释纯属扯淡）

水下单位指Underwater=yes
有生单位指Organic=yes
非生物体指Unnatural=yes
悬浮单位指SpeedType=Hover

注：所有步兵默认Organic=yes
----------------------------------------------------------------
LandTargeting =
默认0
填下表中的对应项。这个代码指定单位对地攻击规则。较NavalTargeting更优先
----------------------------------------------------------------
0 可以攻击陆地
1 不能攻击陆地
2 用副武器攻击陆地，并且强制不主动攻击
虽然LandTargeting=2和盖特逻辑都是YR新增的，但是WW完全没有考虑二者的配合
所以盖特依然会正常升档
-----------------------
NeedsEngineer =
填yes或no。这个代码指定建筑是否占领后才生效，如油井占领后播放动画。对应的通过更改所属等方法直接获得的建筑将无法正常工作
原版下被超时空弹头冻结过的建筑会回到未被占领的工作状态也就是NeedsEngineer重新需要一个工程师来激活一次，Ares已修复
拥有这个语句的建筑被其他所属方占领时会为原所属方播放EVA_TechBuildingLost音效，Ares已允许建筑微观定义，并且还允许占领与失去播放CSF信息文本而不仅仅是EVA警报
NoAutoFire =
填yes或no。这个代码指定该单位能否自动攻击目标，会覆盖CanPassiveAquire，不过不影响还击
NODBarracks =
填yes或no。这个代码指定该建筑（兵营类）是否为苏联方兵营，步兵从相对建筑中心位于[2,2]的格子离开建筑，给AI判断用的。所有面积为【N*N】（正方形）的兵营都应该使用，否则会导致生产一个飞行步兵后无法继续生产其他步兵等问题
Nominal =
填yes或no。TS残留无效
NoShadow =
填yes或no。这个代码指定该单位是否没有阴影。当为yes时，单位没有阴影
NoSpawnAlt =
填yes或no。这个代码指定VXL单位发射出卵单位后是否会变成“无卵”图像。典型的运用是V3导弹发射车发射后车上的导弹会短暂的不见，变成一辆没有导弹的V3导弹发射车，还有无畏级战舰。注意：“无卵”图像实际上是调用另一个VXL文件，所以当NoSpawnAlt=yes时，要把准备的“无卵”图像VXL和HVA文件改名为 原单位VXL名+WO.VXL 和 原单位VXL名+WO.HVA。如V3，应该改名为V3WO.VXL和V3WO.HVA
无子机单位使用此代码会得到一个精致的6258CC3C
NoSpawnAlt与炮塔vxl使用同一存储空间，因此不能同时使用，Ares3.0版本已解决
NotHuman =
填yes或no。这个代码指定步兵单位是不是人类，通常用于各种动物，这种单位的死亡效果不受[Warhead] -> InfDeath=的值影响而始终播放单位自身的Die1序列
NotWorkingSound =
填Sound.ini中定义的声音名。这个代码指定建筑停止工作时的声音
NukeSilo =
填yes或no。这个代码指定建筑是否为核弹井。当为yes时，才可以成功发射“核弹攻击”的超级武器。没有这句却带MultiMissile或(TS的)ChemMissile类超武则无法释放
NumberImpassableRows =
填数值。须配合Bunker=yes 或 UnitRepair=yes 使用，这个代码指定建筑左侧多少列单元格不能通行载具（剩余列可通行载具）
NumberOfDocks =
填数值。这个代码指定可停载单位建筑的最大可停载量，如机场可以停载4架战机，矿厂能够停载1辆矿车
然而矿场是硬编码的一辆矿车Dock一个矿场Unload倒矿然后润掉换下一辆的，改了也没用
NumberOfWaitingPoints =
遗留自RA2开发版本的废弃语句，用于设定有多少个矿车等待位置，搭配ART中WaitingOffsetX使用，正式版中强制1辆倒矿1辆等待，等待坐标使用ART中的QueueingCell设定
NaturalParticleSystem =
该建筑拔起时生成的粒子系统
原版bug：解除隐形时也会生成一次
NaturalParticleLocation =
粒子系统出现的位置，使用XYZ坐标系
NonVehicle =
是否不被视为载具，TS残留，用于载具免疫被偷车贼逻辑影响，VehicleThief在其上会获得一个禁止进入光标，Ares下可以禁止成为被吊运的对象
无法被负伤害+正比例的武器所维修
不影响正伤害负比例和维修厂

 -O-
OpenTopped =
填yes或no。内部乘客是否可以向外开火（战斗要塞）
如果IFV有OpenTopped=yes，一个载员的武器为常规武器，但IFV武器为超时空武器，那么IFV释放后由于步兵出来仍会攻击目标但由于武器不再是超时空武器非Ares环境下将导致IE
OpenTransportWeapon =
指定该单位作为战斗要塞乘客时使用哪个武器，0代表主武器 1代表副武器，默认-1，和平时一样遵照武器选用规则不被强制使用特定武器
该语句强制力较高，例如使用OpenTransportWeapon=1强制BORIS使用副武器攻击同时拥有ResourceGatherer=yes和ResourceDestination=yes的对象
那么哪怕BORIS实际上无法对这类目标开火，它也会依然使用副武器，哪怕实际上不会产生任何效果，也不会和非载员一样切换回主武器来进行攻击
Occupier =
填yes或no。这个代码指定步兵单位是否可以进入可驻守的建筑物
OccupyPip =
用于指定步兵作为驻军时的格点，可用值和效果见Pip=条目
该功能新增于YR，在RA2中硬编码使用pips.shp的特定帧，盟军12苏军11其他10
（此处以第一帧为1算）Ares允许直接指定Pip使用pips.shp中的某一帧，详见说明书
OccupyWeapon =
步兵驻军武器
OmniCrusher =
填yes，可以碾压载具和围墙（战斗要塞）
仅Crusher=yes时工作，用于[代表]一种“更高级别”的碾压，但也不过是设定如此
此外这个语句会让载具更倾向于将目标碾毙而总是想要移动过去，哪怕速度慢的要死，Ares已允许单位上设定是否禁止这一效果，详见说明书
OmniCrushResistant =
填yes。不被战斗要塞碾压
注意：这与Crusher碾压Crushable并不冲突，彼此独立运作，因此实际上并不存在所谓的“碾压等级”设定
例如：Crusher=yes & OmniCrusher=yes 的载具可以正常碾死 Crushable=yes & OmniCrushResistant=yes 的载具
OpportunityFire =
填yes或no。是否移动开火，指定此单位是否可以在执行其他操作（例如移动、采矿）时开火。这个代码不能用于建筑物
优先级低于MobileFire一句的限制和步兵的移动状态检测
例如Jumpjet步兵在建筑上方由于JumpjetLocomotor决定的一些硬编码移动判定而无法开火（见Locomotor条目）
例如Walk步兵在移动时必须播放移动序列，而步兵序列与步兵许多动作关联，因而也常常无法移动时开火
优先级也低于Ctrl+Shift的移动中索敌效果，例如YR天启虽然没有写OpportunityFire=yes但可以通过Ctrl+Shift越过这个逻辑的规则在移动中检索到其他目标并发起攻击
不过Ctrl+Shift的优先级也低于上面Jumpjet和Walk步兵的硬限制，二者受制于移动状态直接无法发起攻击动作，更不会实际执行攻击行为
OrePurifier =
填yes或no。这个代码指定建筑是否为矿石精炼器。原版盟军矿石精炼器的逻辑
即从矿石精炼厂中获得的资金再增加一定百分比的额外资金
在建筑上决定是否启用这个逻辑但这个百分比却要在全局PurifierBonus=设定
Organic =
填yes或no。是否为活体单位，同时防止乌贼寄生（会改用副武拍打），被超时空和铁幕使用[CombatDamage] -> C4Warhead=的弹头秒杀，被寄生秒杀。步兵默认yes
步兵如果另有Teleporter=yes则仍可被超时空，只要满足Organic=no或Teleporter=yes其一即可
若载具使用则该载具会和步兵一样受医院加血效果影响，并且不能像正常载具一样受到科技商店的维修效果
无法被磁电坦克的运动模式弹头攻击，直接禁用IsLocomotor=yes的弹头瞄准该对象
如果该单位还有Naval=yes并且使用寄生类([Warhead] -> Parasite=yes)武器则硬编码为巨型乌贼类寄生行为，具体表现例如寄生一个步兵不会秒杀而是每40帧对目标造成一次武器Damage指定的杀伤，并强制从[CombatDamage] -> SplashList=的列表中抽取一个以作为攻击时的效果动画，使用名为[SQDG]的Animation对象作为开火缠绕效果和缠住摇晃效果，帧序号与行为硬编码对应，帧序列使用规则见https://gitee.com/PB_LAB/YR_MIX_Cataloging_Project/blob/master/ra2.mix/conquer.mix/sqdg.shp.md。此外会使得[Warhead] -> Culling=一句能够生效，并禁止攻击陆地对象（覆盖LandTargeting与NavalTargeting），若被这个步兵拖上岸那么它会被立即弹出到相邻的水域（为什么会有被拖上岸的情况见《6.武器系统代码词典2024.ini》中[Warhead] -> Paralyzes=一条的注解）
如果该单位处于水中那么一个拥有NavalTargeting=3的单位会使用副武器对其开火
如果该单位还有Underwater=yes和SelfHealing=yes那么它会直接去使用GuardRange而不是考虑主副武器中射程更长的那个武器的射程来寻敌，同样用于原版巨型乌贼
步兵被寄生弹头秒杀另有其他判定，并非单纯设为Organic=no即可免于一死
强制死亡时不会有沉船效果
Ares下可以禁止成为被吊运的对象
Ares3.0中[Warhead] -> Culling=yes不再要求巨型乌贼类寄生行为并得到了更多拓展，详见Ares说明书
YR1.000中巨型乌贼式寄生还会判定目标是否Naval=yes，也因此YR1.000中巨型乌贼寄生遥控坦克会使用它色盘错误的武器开火动画而不是硬编码的SQDG
Owner =
生产建筑必须拥有至少一个与被生产对象相同的Owner才可以正常生产
本条目独立于Prerequisite系统，不会被PrerequisiteOverride高优先级覆盖
新阵营单位生产不了之类的Bug往往可能是错在这里
新阵营基础建筑的Owner如果设置错误会导致AI无法识别甚至直接崩溃

在Ares中由于解除了单位生产够快时多个工厂同时生产单位的限制（原版仅搜索相同注册名对象，Ares下拓展到所有同类型工厂）所以可能出现原本Owner限制无法生产某单位的工厂由于排序规则被分配用于生产这个单位，需要使用Ares的狗窝逻辑手动限制，详见说明书，如果你获得本文档的同时没有配套这一文件，说明你的文档并非从原正式发布渠道获取，而是已经被第三方未经许可拆分修改过的

Overpowerable =
填yes或no。这个代码指定建筑是否为充能建筑，当类似磁暴步兵类的充能单位对其进行充电时，该建筑转为副武攻击，典型的运用是苏军的磁暴线圈

 -P-
PixelSelectionBracketDelta =
血条的高度，负值向上，仅用于非建筑类，建筑根据art中的Height计算
医院自愈与科技商店维修给予的标志并不遵循这个的设定，Phobos已修复

PowersUnit =
控制中心用，同时如果这个单位不是载具会注册一个载具，也就是这必然是个载具
只要有一个拥有PowersUnit=的建筑物PoweredUnit=yes的单位就可以保持活动
但如果是已瘫痪的单位重新唤醒，则必须是有PowersUnit=这个单位的建筑才行
原版每个建筑只能控制一个单位，Ares对此进行了扩展，详见Ares说明书
PoweredUnit =
遥控坦克用，如果没有PowersUnit=自己的建筑处于工作状态则瘫痪

PackupSound =
填Sound.ini中定义的声音名。这个代码指定建筑收回为载具时播放的声音，不设定时就为基地车收回的那种声音
Parasiteable =
填yes或no。这个代码指定该单位是否能被寄生，这里的寄生是指被像恐怖机器人一类的单位所寄生，默认yes
Passengers =
填数值。这个代码指定单位的乘客格子数量。如果要容纳占多格的单位，可以修改SizeLimit=这个代码。想要显示乘客格子需要手动添加PipScale=passengers
注意Aircraft类单位开火会甩出乘客为伞兵，直到没有乘客了才能正常发射武器，但即便没有发射武器而是转为踹出乘客也会按执行攻击任务扣除弹药
可用武器上的Burst指定一次踹出多个乘客，也可以用MovementRestrictedTo配合Ares的InitialPayload让乘客实际上无法被踹出把开火交给乘客
在TS中Vehicle无法作为Passenger在RA2开始允许，原版下也仅有Infantry类可以手动进入Aircraft而Vehicle会卡在Enter中始终进不去并且选中立即失去选中效果，Kratos解除了这一限制
Passive =
填yes或no。这个代码指定该单位是否会自动攻击敌人，TS残留，请用CanPassiveAquire=和CanRetaliate=控制
PermaDisguise =
填yes或no。这个代码指定伪装单位是否可以在移动中不会破坏自己的伪装。典型的运用是间谍，间谍在移动中不会轻易被敌人识破
如果载具使用这句那么他会使用Allied/Soviet/ThirdDisguise=的步兵图像而非DefaultMirageDisguises并且由于shp载具和shp步兵的序列书写方式不同在移动时他会像一个没写序列的shp载具那样从一直播放（旋转）
PhysicalSize =
指定步兵的Z-fudge值，所有步兵都应该设为1，具体功能未知
Pip =
填对应颜色名。这个代码指定单位进入运兵单位后下面小格显示的颜色，在红色警戒2中有green、yellow、white、red和blue
尤里的复仇中额外添加persongreen、personyellow、personwhite、personred、personblue、personpurple几个颜色可供选择。默认为green
步兵作为驻军时使用[InfantryType] -> OccupyPip=标签指定，一般使用尤里的复仇中新增的6种，但也不妨碍你用点别的
由于基于TS引擎开发RA2的过程中WW引入了一些代码错误，从RA2开始地图内置单位时必须重新指定这个标签，否则会显示成错误的效果，Ares已修复
Pip与OccupyPip可用值在pips.shp与pips2.shp中的序号规则如下（从00开始）：
empty			00	00	pips.shp为建筑菱形方块，pip2.shp为4x4空心小方块
*仅限TS，RA2/YR中不支持Pip=empty这样的写法
green			01	01	pips.shp为建筑菱形方块，pip2.shp为4x4小方块
yellow			02	02	pips.shp为建筑菱形方块，pip2.shp为4x4小方块
white			03	03	pips.shp为建筑菱形方块，pip2.shp为4x4小方块
red				04	04	pips.shp为建筑菱形方块，pip2.shp为4x4小方块
blue			05	05	pips.shp为建筑菱形方块，pip2.shp为4x4小方块
persongreen		07	07	pips.shp与pips2.shp均为人形标志
personyellow	08	08	pips.shp与pips2.shp均为人形标志
personwhite		09	09	pips.shp与pips2.shp均为人形标志
personred		10	10	pips.shp与pips2.shp均为人形标志
personblue		11	11	pips.shp与pips2.shp均为人形标志
personpurple	12	12	pips.shp与pips2.shp均为人形标志
此外，Ares允许直接指定Pip使用pips2.shp中的某一帧，详见说明书
PipScale =
填下表中的对应项。这个代码指定单位下方小格显示的类型。注意：小格数量在特殊状况下PipWrap=指定
---------------------------------------------------------------------------------------------------------
Passengers	乘客，小格数量由Passengers=这个代码的数值指定
Ammo		弹药，这里不是小格表示而是竖线方式表示，小格数量由Ammo=这个代码的数值指定
Power		电力，实际上从TS开始就没用，大概是WW开发阶段设计如此但最后选择了工具条
Tiberium	矿石，只能用在矿石精炼厂和采矿车上，小格数量由Storage=这个代码的数值的 逻辑 指定
Mindcontrol	心控目标数量，用于心灵控制单位，小格数量表示已经控制了多少格
注：子机格子并不受PipScale控制，想要禁止显示请使用Phobos，详见说明书
---------------------------------------------------------------------------------------------------------
PipWrap =
填数值。这个代码指定单位下方显示的小格的数量限制，不同阶段会用不同颜色表示，如弹药，不同阶段由不同颜色表示弹药的数量。要和PipScale=Ammo连用
PitchAngle =
填数值。指定此单位在飞行时向前倾斜的量。默认为20.0度
仅为图像效果，但实际飞行动作的仰角还是取决于Speed和FlightLevel
PitchSpeed =
填数值。指定此单位向前(PitchAngle)与向侧边(RollAngle)倾斜所需的速度百分比下限。默认为0.25
用于Locomotor为Fly或Jumpjet的单位，令其仅在(当前Speed/[TechnoType] -> Speed)大于PitchSpeed的比率时才会倾斜
PlaceAnywhere =
填数值。这个代码指定建筑的建造是否不会受到场地的影响，如凹凸等。当为yes时，建筑可以在任何场地建造。然而仍然受到Adjacent的限制
Points =
遭遇战积分统计数据，无实际意义，尤其并【不】影响经验计算，经验计算看的是Cost
Power =
填数值。这个代码指定建筑单位生产的电力。当为正数时，则为供电
Powered =
填yes或no。这个代码指定建筑单位是否会受到停电后影响，如不能使用武器、建筑动画不能播放等。
如果想设定建筑受到停电影响后可以继续播放动画，可以设定Art.ini中的ActiveAnimPowered=no，反之则设定为yes
如果Power>0又Powered=yes，建筑动画没有ActiveAnim[N]Powered还是会傻掉，需要手动设置
PowersUpBuilding =
指定该加载物可以加载到其上的主体建筑
拥有这个语句说明这个建筑是个加载物，也就是附属建筑
它只能放在主体建筑上面，不能放在空地或其他地方的建筑，同时原版下这样的建筑存在算法错误导致无法正常作为先决条件，Ares已予以修复
需要配合Upgrades与下句，可以参考TS中的组合塔
注意：如果加载物有武器，那么加载后将会表现为主副武器同时开火，但是副武器往往只能使用Arcing类
由于建筑使用主武射程，若主体建筑没有主武器而加载物也不赋予主武器，那么主体建筑原有的副武器还是通过加载获得副武器都是无法开火的
此外，第一个有武器的加载物其主武会覆盖主体建筑的参数
1.主体 Primary=none & Secondary=none
-1.如果PowersUp[1]给予Secondary，则如上文所述，并且PowersUp[2]摆大烂
-2.如果PowersUp[1]给予Primary，则可以开火，并且还能通过PowersUp[2]再加个Secondary
-3.也可PowersUp[1]一次性给予Primary与Secondary
其他组合暂不全列于此，可先自行测试，不排除拓展引擎下药修改结果

也就是如果先后加两个带武器的加载物分别给予主武器和副武器，那么需要先加装给予主武器的加载物，否则也无法刷新Range以进行开火，然而建筑原本拥有副武器由加载物提供主武器那么是可以开火的
PowersUpToLevel =
用于加载物建筑，指定这个加载物建筑的编号
可用1/2/3分别对应主体建筑Art中PowerUp1/PowerUp2/PowerUp3关联的动画
只能到3，因为程序内只做了3种，实际是TS遗留来的逻辑，只不过依然能用（勉强）
然而~~~很可惜的是在Phobos修复前这个对应关系并不是那么的一致。AlexB：真该把WW的程序员装进大炮里发射到太阳上
如果此值为1/2/3则同时也代表建筑已经从3种中选择了1种而无视主体建筑的Upgrades禁止其他加载物继续加载
特殊值-1代表自动适应，也就是使用排队模式，这种情况下对同一建筑加载的上限遵循主体建筑的Upgrades
而-1时对于上面PowerUp1/PowerUp2/PowerUp3则会在前三次每加载一次启用与次数相同的编号对象
对于玩过TS的玩家来说就很好讲了，用-1就是GDI发电厂，用1/2/3就是GDI插件塔
不过GDI插件塔使用不同炮塔的效果还有一些内部硬编码支持
可以前往RA2DIY论坛https://bbs.ra2diy.com/forum.php?mod=viewthread&tid=14548进行了解
Prerequisite =
填建筑名。这个代码指定该单位制造时所必须的建筑，当已方没有这些建筑时该单位不能建造
也可以填写先决条件组组名，在全局PrerequisitePower=前后部分，只要拥有组中任意对象即视为满足其中一个条件
例如Prerequisite=RADAR,NATECH就是拥有PrerequisiteRadar=列表中任意建筑+NATECH即可生产，以下是原版的先决条件组组名表：
------------------------------------------------------------------------------------------
RADAR		雷达类建筑，这种类型的新建筑应该同时在PrerequisiteRadar=中注册
BARRACKS	兵营类建筑，这种类型的新建筑应该同时在PrerequisiteBarracks=中注册
TECH		科技类建筑，这种类型的新建筑应该同时在PrerequisiteTech=中注册
PROC		矿厂类建筑，这种类型的新建筑应该同时在PrerequisiteProc=中注册
			YR中PrerequisiteProcAlternate=的载具也会被考虑在内
POWER		发电厂类建筑，这种类型的新建筑应该同时在PrerequisitePower=中注册
FACTORY		战车工厂建筑，这种类型的新建筑应该同时在PrerequisiteFactory=中注册
原版引擎无法新增先决条件组，需要使用Ares
也无法添加更多PrerequisiteProcAlternate那样使用载具作为先决条件的效果，需要Ares
也无法使用战机和步兵作为先决条件，需要Ares
也无法正常使用加载物作为先决条件，需要Ares
------------------------------------------------------------------------------------------
PrerequisiteOverride =
填建筑名。这个代码指定该单位可以在Prerequisite=之外另外指定必须建筑，相当于第二个Prerequisite=的作用
但列表中的单位是或的关系，也就是只要当列表中的单位满足任何一个时，强制允许建造，无视其他条件
优先级过高，存在许多无视其他限制的Bug，慎用
PreventAttackMove =
填yes或no。决定此单位是否支持移动警戒（ctrl+shift）
对于有Primary的单位默认为yes
PreventAutoDeploy =
遗留自RA2开发版本的废弃语句，这个代码指定该单位是否能够自动部署
Primary =
填武器名。这个代码指定该单位的主武，也就是所谓的主要武器、第一武器
对于AI而言如果基地正在受攻击（无论杀伤的来源是哪个所属）都会将拥有武器的建筑优先建造
ProduceCashAmount =
填数值。这个代码指定建筑在每隔固定时间就会给拥有者多少资金。典型的运用是科技钻油井。这里的时间由ProduceCashDelay=这个代码的数值指定
ProduceCashDelay =
多长时间给予玩家ProduceCashAmount量的金钱，超时空弹头打断油井效果相关的描述见NeedsEngineer一句下方
ProduceCashStartup =
填数值。这个代码指定当该建筑被占领时占领方获得的资金。典型的运用是科技钻油井
如果一次扣完现有资金，那么现有资金会正常的从0开始，而不是从负数开始
ProtectWithWall =
填yes或no。这个代码指定建筑在AI使用时是否会被围墙围住，该围墙由当前选择的国家的所属阵营来决定，也可以通过设定AIBasePlanningSide=来指定
PsychicDetectionRadius =
填数值。这个代码指定探测敌人动作的半径范围。典型的运用是苏军的“心灵感应装置”
Pushy =
配合DirectRocker=使用
确定该单位是否能够在“推”另一个对象后再次移动和发射
用于武器有一个已设置DirectRocker=yes弹头的单位
PlayerReturnFire =
玩家控制该单位时单位是否会主动的还击
例如AI一个单位攻击了玩家控制的一个单位，并且该单位PlayerReturnFire=no，那么即使它有CanRetaliate=yes也不会发起还击
PoweredSpecial =
该建筑被镭射幽浮或间谍断电而进入LowPower状态时是否播放LowPower动画，相关语句可见ART中+PoweredSpecial相关

 -Q-
没有收录以Q开头的语句

 -R-
RateUp =
攻击状态时盖特计数器每帧增加多少
RateDown =
非攻击状态时盖特计数器每帧减少多少
如果填负数则在无目标时仍旧累加计数器
如果填0实际上并不能保持档位而是瞬间清零
RadialFireSegments =
用于扇形开火，抛体射出方向水平转动的次数，从0到180度 （神盾导弹发射时呈扫射状），配合抛射体中的CourseLockDuration效果更佳
每次转动的角度无法自定义，只会使用180°/RadialFireSegments
可以用弹药逻辑中途切无弹药武器简单模拟
如果写1的话会只能向正右侧开火（炮斗术！）
Radar =
填yes或no。这个代码指定建筑是否拥有雷达功能
对于一个没电的建筑，如果使用Ares3.0电池超武的过载逻辑，哪怕依然没电，这个建筑的雷达也会正常工作
RadarInvisible =
填yes或no。这个代码指定该单位是否会被敌方雷达检测到，效果是敌人无法在小地图看见该单位
在Invisible、InvisibleInGame等逻辑中也都自带相同效果
注意：这是让原本会显示的对象不显示，如果是原本就不显示的对象开启显示需要用下句
RadarVisible =
填yes或no。这个代码指定该单位能否在非己方雷达上显示，原版用于让[ObjectType] -> Insignificant=yes的科技建筑也正常显示在玩家的雷达上
RadialColor =
无效语句，雷达上实际使用该建筑所属方的颜色，或者是遭遇战设置时的颜色
Refinery =
填yes或no。这个代码指定建筑是否为矿石精炼厂。给AI判断用的，比如AI会指定部队围着矿石精炼厂打。如果是Factory那么会强制无法将单位生产出来
RefinerySmokeOffsetOne =
填X，Y，Z的值。这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的位置，这是第一个位置
RefinerySmokeOffsetTwo =
填X，Y，Z的值。这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的位置，这是第二个位置
RefinerySmokeOffsetThree =
填X，Y，Z的值。这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的位置，这是第三个位置
RefinerySmokeOffsetTwo =
填X，Y，Z的值。这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的位置，这是第四个位置
RefinerySmokeParticleSystem =
填粒子系统名称，这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的类型，只能填一个
RefinerySmokeFrames =
填正整数类型值，这个代码指定矿石精炼厂在接受采矿车的矿石后冒烟的时间，单位为帧
ReadinessReductionMultiplier =
填数值。这个代码指定该单位的损害乘法器。要和DamageReducesReadiness=yes连用
RejoinTeamIfLimboed =
填yes或no。用于武器拥有LimboLaunch=yes的单位，这个代码指定处于一个team中的该单位limbo消灭目标后unlimbo时是否归队。通常用于寄生单位
ReselectIfLimboed =
填yes或no。用于武器拥有LimboLaunch=yes的单位，这个代码指定该寄生单位寄生前若处于被选中状态并且没有其他动作那么它从目标身上Unlimbo返回时是否仍是被选中状态，如果为no那么狗和恐怖机器人每寄生击杀一个目标你都要重新手动选中它一次
Reload =
填数值。这个代码指定该单位装填弹药的所需帧数。如果为0那么会立即装回
当弹药空仓时转为使用EmptyReload的值
原版下每次只能装1枚弹药，Ares允许定义
载员无法在载具内装弹，Phobos已修复
ReloadIncrement =
填数值。指定装弹速度根据PipWrap的修正值，默认0
公式：真reload帧数=Reload + ( ReloadIncrement * ( 当前弹药数 / PipWrap )^2 )
Repairable =
填yes或no。这个代码指定建筑是否能够被工程师所修复。当为no时工程师不能进入修复。实际上应该是用来限制扳手维修的，Ares下已允许分离控制
RequiredHouses =
填国家名。这个代码指定该单位只能被指定的国家所建造。对于其他国家，即使满足了Prerequisite=和TechLevel=，只要不是指定的这个国家，就不能建造
RequiresStolenAlliedTech =
填yes或no。这个代码指定该单位是否在已方间谍渗透[AI] -> BuildTech=第一项即原版盟军作战实验室后才能建造，Ares重做了一套新的渗透功能系统，详见间谍渗透功能强化一节
RequiresStolenSovietTech =
填yes或no。这个代码指定该单位是否在已方间谍渗透[AI] -> BuildTech=第二项即原版苏军作战实验室后才能建造，Ares重做了一套新的渗透功能系统，详见间谍渗透功能强化一节
RequiresStolenThirdTech =
填yes或no。这个代码指定该单位是否在已方间谍渗透[AI] -> BuildTech=第三项即原版尤里作战实验室后才能建造，Ares重做了一套新的渗透功能系统，详见间谍渗透功能强化一节
RevealToAll =
填yes或no。这个代码指定对象是否会生成雷达事件，例如雷达标记，并向敌方揭开该建筑Sight区域内的地图
RollAngle =
填数值。这个代码指定此单位转弯时的侧向倾斜角度。默认为30.0度
此外该单位需要满足PitchSpeed的条件，同时PitchAngle需要大于0
同时会导致VXL单位占用的画布过大而崩溃，与巨型VXL素材上斜坡和沉没同理
ROT =
填数值。这个代码指定该单位转弯的比率，数值越大转弯越快。默认值为0
同时对于Turret=yes的单位其炮塔旋转速度也使用此值，Ares允许分离设定
ResourceGatherer =
原版用于三方矿车和尤里矿场，用于AI处理矿石采集和存储任务，如果建筑用了会影响AI出矿场的数量计算
也用于AI的建筑扩展节点判定，详见BaseNormal一节
此外可以用于屏蔽载具DeploysInto成建筑失败时的EVA_CannotDeployHere语音
ResourceDestination =
原版用于三方矿场和尤里矿车，用于AI处理矿石采集和存储任务
以上两句用于让AI学会处理不同的矿石处理和储存方式
但是连用还有禁止BORIS空袭指示器武器攻击该建筑的效果，不过并不禁止被C4摧毁
可以屏蔽建筑UndeploysInto成载具时的EVA_NewRallyPointEstablished语音

 -S-
SAM =
填yes或no。TS残留代码，这个代码指定建筑是否为SAM导弹
目标必须为在[General] -> PadAircraft=列表中的Aircraft，否则根本不会锁定，也就是火箭飞行兵和夜鹰直升机那些实际上是Infantry与Vehicle的对象不会成为目标
此外目标Aircraft必须Dock为空，并且只有SAM获取目标时这个Aircraft就是在空中悬停的状态那么SAM才能正常发射武器，一旦Aircraft之后移动了一下，那么SAM就会哑火
只有一些特定的转弯情况偶尔会突然射两发，然后继续哑火，并且这种情况下SAM炮塔仍然会去重新同步到目标方向，但再次同步的间隔并不是武器的ROF，也并不是固定值
甚至前面说的突然射两发的情况可以并不面向目标开火，哪怕并不存在[WeaponType] -> OmniFire=yes
此外SAM还强制只能对空攻击，也就是不能对落到地面的目标开火
也就是SAM的目标只能是拥有AirportBound=yes与Dock=none且起飞过的Aircraft
只有一些原版引擎下需要特殊判定效果的地方会用到，现代引擎下已经没有必要死磕这个逻辑
Secondary =
填武器名。这个代码指定该单位的副武，也就是所谓的次要武器、第二武器。当主武不能攻击某目标时，游戏会自动转为副武攻击，当副武不能攻击时，游戏才会判断该单位不能攻击
建筑主副武器始终使用其主武器的Range作为射程，如果不存在主武器那么副武器相当于没射程也用不了
Selectable =
填yes或no。这个代码指定该单位能否被玩家选中。典型的运用是V3导弹，与Spawned有一些令人疑惑的联动
对于不回机场（AirportBound=no & Dock=none）且Landable与Selectable任意为no的战机在目标丢失后会离开地图，例如原版伞兵飞机
对应的：这些不应用于原版黄蜂类型的子机战机，否则完成（非中断）任务的子机不会返回母舰而是飞出地图后从游戏中移除，进而导致母舰传递指令时崩溃
SelfHealing =
填yes或no。这个代码指定该单位是否能够自动恢复生命点。间隔由全局[General] -> RepairRate=指定，Ares已允许微观定义，详见说明书
然而建筑如果依靠自愈回到了未损伤状态其图像也不会正常的转换，Phobos已修复
原版下无法设定单位是否脱战才能开始自愈，Ares已允许设定，并添加了多项拓展，详见说明书
SensorArray =
填yes或no。该【建筑】能否探测隐形和地下单位，范围由SensorsSight指定，建筑被断电、摧毁、移交所属、超时空冻结等均不会刷新(停止)效果，Ares已修复
Sensors =
填yes或no。这个代码指定此物体是否能够在周围3x3范围内探测隐形，并解除，但是对友军建筑也有效，并且一些情况下单位被摧毁会遗留反隐效果，Phobos已修复
SensorsSight =
填数值。这个代码指定此物体检测其它隐形单位的半径范围，但是并不解除，非建筑类填上就能用，建筑需要SensorArray=yes启用
该逻辑从TS就有死亡遗留反隐区等各种问题，RA2中对于Naval=yes且始终在地表的单位进行了特殊处理解决了部分Bug，然而依旧存在大量问题，Phobos已修复部分
ShowOccupantPips =
填yes或no。这个代码指定当建筑被步兵驻守后是否显示底下的小格
Sight =
填数值。这个代码指定该单位的视力范围。数值越高，该单位在探路时拨开的黑雾越大。单探开视野功能而言原版最大值11，想要更大需要Ares
SinkingSound =
填Sound.ini中定义的声音名。这个代码指定海军单位被摧毁后下沉的声音。该海军单位的Weight要大于3。如果想设定让海军单位下沉的Weight的阈值可以修改全局[General] -> ShipSinkingWeight=的数值
Size =
填数值。这个代码指定该单位的大小。默认为1。仅载具的乘客格子正常绘制多格，尤里电厂和驻军建筑始终为1格大小
SizeLimit =
填数值。这个代码指定运兵单位最大支持的单个乘客占格数，Ares允许对于运输载具设定任何单位在这个单位内也只占1格，但仍然遵循本语句设定检查是否允许进入
Soylent =
填数值。这个代码指定该单位被出售后所得的资金。对于步兵单位，只有通过进入RA2苏军的“复制中心”YR尤里的回收站（或同类型建筑）才能卖掉
默认0即不启用该逻辑，并非默认Cost/2。如果[TechnoType] -> Soylent=0
实际算法为：[TechnoType] -> Cost=<int>*[Country] -> Cost(Infantry|Units|Aircraft|Buildings|Defenses)Mult=<float>*[BuildingType] -> (Infantry|Units|Aircraft|Buildings|Defenses)CostBonus=<float>
若所属方为人类玩家，在此基础上再*[General] -> RefundPercent=<float>，原版为50%（0.5）。
Spawned =
填yes或no。这个代码指定是否为子机类单位。用来和一般单位作区分的，可以禁用Unit Lost警报。在战机上与Landable、Selectable有一些小绕的编码工作方式，参见https://t.bilibili.com/884748819012517897
Spawns =
填战机名。这个代码指定子机发射器发射的子机类型。子机发射器单位的武器需要有Spawner=yes来声明使用的是一个单纯用于发射子机的虚拟武器
原版下对于空中单位放出的子机需要母舰落回地面才可以返回，否则子机只会落到地上或飞出地图（然后崩溃），Ares已允许空中单位正常使用和回收子机，且无需额外设定
不过这依旧需要满足子机与母舰XY坐标一致的条件才能回收，所以也无法移动中回收，Phobos已拓展该逻辑，允许设定一个回收子机的最大范围，详见说明书
当然在现代拓展引擎下使用其他逻辑刻出子机管理器系统也并非不可能，例如https://www.bilibili.com/opus/994486096720035847，图中的航母就可以移动中回收子机和显示子机装弹进度。也可以突破仅能Aircraft类作为子机和子机不可手动操作的限制，如https://www.bilibili.com/opus/993682443903959046。甚至还能让子机根据目标数量自动分配https://www.bilibili.com/opus/1001916368673570822
如果由建筑类作为母舰，那么即便在断电状态下子机逻辑也仍然工作，Phobos已允许控制，详见说明书
原版下子机返航的朝向并不会检查是否与母舰一致，Phobos已修复
目前作为子机的Aircraft在母舰被毁时无视其Crashable=no坠毁
SpawnsNumber =
子机数目
SpawnRegenRate =
子机重生帧数
SpawnReloadRate =
子机装弹帧数

SpecialThreatvalue =
填0-1的数值。用于原版工程师和MCV等无威胁单位正常进入威胁计算，防止这些实际上并不简单的单位被主动寻敌无视掉
Speed =
填数值。这个代码指物体运动速度。每个非建筑物体都一定要设置这个项。最小值为0，最大值为100，程序内再*256/100换算
步兵类Walk与机甲Mech两种运动模式的实际Speed不得超过14，否则会卡在原地无法运动。考虑到升级捡箱子等因素，写速度时不要大于10，Phobos已解除
原版下只能整数，Phobos允许使用小数
注意：任何运动模式在极低速度下都可能出现一些不太正常的表现，具体效果与单位的类别也有所不同
SpeedType =
填下表中的对应项。这个代码指定该单位的速度类型
决定单位在不同的地形上能否运动及运动速度改变多少，见2025教程大包内附赠的《9.覆盖物词典.ini》开头[Water]部分
应该和Locomotor=以及MovementZone=适当配合使用
---------------------------------------------------------------------------------
Amphibious			两栖速度类型
在旧版本词典中有一个“Underground 潜地速度类型”，实际上这是二十多年前最早的一批教程中长期遗留下来的错误，并不存在Underground这个可用值
FloatBeach			滨海速度类型
Float				船舶速度类型，使用这个SpeedType的建筑可以无视Buildable依靠SpeedType控制建造地块类型，见WaterBound词条
Winged				飞机速度类型
Hover				悬浮速度类型
SpeedType=Hover的Jumpjet载具（例如夜鹰直升机）被超时空到水中时并不会沉没，甚至还能操作下达指令让它飞起来正常工作，这个问题在Ares中已被修复
Wheel				轮式载具速度类型
Track				半履带车速度类型
Foot				步兵步行速度类型
SpeedType=Amphibious/Hover会让一些vxl载具影子绘制在body之上
---------------------------------------------------------------------------------
MovementZone =
表示单位使用何种寻路方式，填下表中的对应项。（标有试图字样需要单位本身满足条件）
对于处于OpenTopped载具中的乘客只有在其可运动的MovementZone上才可以正常对外开火，Ares下用InitialPayload做多武器载具需要注意，可以用下面那句来限制不能踢出（不过Ares也提供了用于VehicleType与Aircraft的的禁止手动装载乘客NoManualEnter与禁止手动卸载乘客NoManualUnload直接用Ares提供的新语句就足够了，详见Ares说明书
---------------------------------------------------------------------------------
Amphibious			两栖，可以同时被船厂和维修厂维修
AmphibiousCrusher	两栖，并试图碾压步兵
AmphibiousDestroyer	两栖，并试图摧毁障碍物（树木 沙袋 铁丝网）两栖步兵卡树的原因之一
Crusher				陆地，并试图碾压步兵
CrusherAll			陆地，并试图碾压一切包括围墙，根据Crusher决定穿墙而过还是强行碾掉不能碾的墙（真正决定是否为高级碾压的语句）
Destroyer			陆地，并试图摧毁障碍物和碾压沙袋
Fly					寻路无限制
Infantry			陆地，一般步兵
InfantryDestroyer	陆地 步兵 试图摧毁障碍物
Normal				陆地，并试图摧毁地形障碍和碾压步兵
Subterannean 		钻地车用，移动距离远时试图钻地，不钻地时与Crusher类似。作为矿车且被水域或悬崖包围时无法正确找到矿场，PhobosBuild44已修复
Water				只在水中寻路
WaterBeach			可在水中和海滩寻路
---------------------------------------------------------------------------------
上表有效值中的Subterannean实际为Westwood的错误拼写，Ares中的新增标签例如[AudioVisual] -> SubterraneanSpeakDelay=等则使用的是正确的英文单词"Subterranean"

MovementRestrictedTo =
该【载具】只能在某类地形上运动。
如果你想要从Factory创建一个不能移动的单位并且正常开出来，那么你需要用Ares的Convert逻辑让它开出来以后再变成你要的限制了运动区域的单位
---------------------------------------------------------------------------------
Clear
Road
Rough
Rock
Tiberium
Water
Railroad
Tunnel
Beach
Weeds
Ice
Wall
---------------------------------------------------------------------------------


Spyable =
填yes或no。这个代码指定建筑是否能够被间谍渗透，被间谍渗透的建筑会根据建筑类型触发相应的事件，如渗透发电厂类建筑会导致停电等，然而效果判定语句同时也是建筑功能语句，无法分离控制，Ares重做了一套新的渗透功能系统，详见间谍渗透功能强化一节
SpySat =
填yes或no，是否开全图 （间谍卫星）
该功能无法用于加载物，Phobos已修复
Storage =
填数值。这个代码指定该单位能够储存的矿石数量。只能用在采矿车和矿石精炼厂，RA2下失去了建筑储矿效果所以矿石精炼厂上的已经失去意义，Ares已复原，详见说明书
Strength =
填数值。这个代码指定该单位的最大生命值点数，Phobos允许独立定义单位生成时的初始血量，详见说明书
如果把这个值设为负值会导致一些令人疑惑的效果，并且不同引擎可能修改相关逻辑引发不同的效果
StupidHunt =
填yes或no。当AI没有剩余建筑时（非快速游戏）这个单位会径直冲到玩家家里而不像其他单位一样被分配Hunt任务，这样的单位通常没有武器也没法执行Hunt所以用这个语句来让它们也加入填线的队伍
SuperGapRadiusInCells =
填数值。这个代码指定“黑幕产生器”类建筑部署产生的黑幕半径。要和GapGenerator=yes和ExtraPower=配合使用
SuperWeapon =
填超级武器名。这个代码指定该建筑产生后所激活的超级武器
同时还带有强制建筑只能手动寻敌、触发超武阶段动画等编码效果，如果不想要这些效果请使用下句
*如果是加载物提供的超级武器那么将不会读取超武的AuxBuilding设置，Ares已修复
SuperWeapon2 =
填超级武器名。这个代码指定该建筑产生后所激活的第二个超级武器，没有上一局那一堆编码限制
原版下一个建筑只能使用上面两个语句绑两个超武，加载物也无法超额，想要一个建筑挂更多请用Ares新功能，详见说明书
SuppressionThreshold =
填数值。乌贼和恐怖机器人等单位用。如果被寄生单位受到大于此数值的伤害，则在"伤害*2"的帧时间内，若被寄生的单位被摧毁，寄生者一并死亡
SlowdownDistance =
飞机单位在目标附近减速的距离，256为一格，适当增大有助于高Speed低ROT战机返仓（不然容易一直绕圈）
特殊值0可以让战机永远无法落地（毕竟距离目的地0Lepton才开始减速那就没法降到0了）
但是这个方法会打断AI行为，因为AI会倾向于视为移动任务始终没有成功完成
非五连发战机返仓和接近目标都会使用SlowdownDistance，五连发战机轰炸目标不看只在返航时看
SecretLab =
是否为秘密科技实验室
SecretBuilding=
占领秘密科技实验室后可生产的建筑
SecretInfantry=
占领秘密科技实验室后可生产的步兵
SecretUnit=
占领秘密科技实验室后可生产的载具
和全局一样没有Aircraft，并且建筑体自身的这个还只能单个对象而不是列表，不过Ares已经换了一套新的，直接把WW这套又老又残的扬了拉倒
SecretHouses =
未完成功能，无效代码，Ares已完成并扩展，详见Ares说明书
SlaveRegenRate =
奴隶重生帧数
SlavesNumber =
奴隶数目
SlaveReloadRate =
奴隶“倒矿”使用的时间，即奴隶回到奴隶矿场后到下一次出来时的间隔
Slaved =
这个步兵是否为奴隶矿工，奴隶矿场被摧毁时会得到解放，搭配HarvestRate控制收集矿石的速度
原版下被超时空弹头攻击可能引发崩溃，Phobos已修复
Stage1 =
Stage2 =
Stage3 =
Stage4 =
Stage5 =
Stage6 =
盖特武器[X]阶保持到计数器达到多少后转到下一阶，这里的[X]有效范围受制于WeaponStages的值
最后一阶由于不存在下一阶所以会保留当前阶段，想要跳到第一阶往往使用一个FireOnce的武器搭配RateDown=0来实现，但是会丢失原目标需要重新索敌，Ares引擎允许语句控制最后一阶跳转第一阶，详见Ares说明书
SprayAttack =
是否为喷洒单位
抛射需为Arcing
用于指定此单位Primary随机喷洒在单位周围，而不是使用武器的正常规则向目标射击
结果是武器在来自该单元的8个标准方向中的任何一个方向上的随机单元中发射
而不是在所选目标本身处发射
在目标在Range内时不会射击
在目标和自己距离为1或2时向目标方向以距离+1的射程随机发射武器
在原版引擎INI技术向MOD《VS_INI》中用于处理原版航母飞机在特定角度攻击船厂时不投弹一直盘旋的bug

 -T-
TypeImmune =
填yes或no，该单位是否不受己方相同单位的伤害，如尤里复制人，对于无所属方的粒子自然就无效了，不过对粒子武器的穿透伤害还是有效的，毕竟那是来自武器的
TogglePower =
该建筑是否能手动停电，TS残留无效，Ares已复原相关逻辑，详见Ares说明书，如果你获得本文档的同时没有配套这一文件，说明你的文档并非从原正式发布渠道获取，而是已经被第三方未经许可拆分修改过的
注意：仅在Powered=yes且Selectable=yes时有效，否则强制不能被断电
Power为正的建筑（例如电厂）并不会导致不能被断电，断电时会表现为不生产电力
ToTile =
建筑用，建造地形，填地形名 如Water01，Green01，Clear01注意如果想让此物在水面建造的话需要LaserFencePost=yes
实际上并不会严格根据Foundation来填充，而是根据Foundation决定的最大长宽，也就是原版的3x3REFINERY当标准3x3算
Ares的CustomFoundation逻辑直接遵照Foundation.[X|Y]直接填充矩形，而并不去看有没有挖掉格子
同时还会因为Tile自身的尺寸而影响实际范围，例如Water01实际上是一个2x2的tem
典型应用是TS中的硬化路面，在家里建造防止敌方钻地载具直奔基地中心
此外该逻辑改变地形并不会刷新寻路，因为寻路区域是地图载入时就决定完的，不过你依然可以用其他限制移动区域的方法加以配合来实现单位由于ToTile而正常改变自身运动区域的效果
TiltCrashJumpjet =
决定Jumpjet运动模式单位的坠毁方式，填写yes坠毁时会倾斜（飞碟）否则平稳坠毁（基洛夫）
TargetCoordOffset =
建筑被攻击时所被瞄准的坐标点，同时也是船厂出口位置
不影响AAAG判定，也就是说哪怕你第三个值定义了个4096高度，地面单位也照射不误
对于Arcing类虽然其弹道仍旧命中地面建筑中心，但爆点会移动到TargetCoordOffset
但是对于ROT类如果命中前建筑就已经被摧毁了，那么会重新将目标更新为被毁建筑空地上原应该攻击的位置而不是照常飞到TargetCoordOffset
这也不影响武器Range，哪怕它影响TargetLaser和瞄准线的绘制，但这不影响实际距离判定
并且对于Vertical的特殊工作机制，单位依然会开到建筑头上丢炸弹而不是去TargetCoordOffset
若抛射体拥有Inaccurate=true
对于Arcing和Inviso类爆点会正常计算，只不过IsLaser和TargetLaser瞄准线等绘制效果始终遵循TargetCoordOffset
若抛射体拥有FlakScatter=true
对于Inviso类开启不精准效果将会依照建筑实际中心计算而不是TargetCoordOffset
TargetLaser =
攻击时是否有瞄准激光(无实际意义)与Attack的那条线一样，使用palette.pal色盘08号色，Move使用palette.pal色盘03号色
TechLevel =
该值确定物体在建造栏中的顺序，越小的越在前，同样的按照注册顺序调整<=-2时相当于没有TechLevel限制
当建筑TechLevel=-1时人类玩家不可建造，AI可以建造建筑，对于小队中的单位则是AI也无法建造
TechLevel处于0到[MultiplayerDialogSettings] -> TechLevel=（或地图触发更改后的值）的区间中则正常生产
TechLevel>[MultiplayerDialogSettings] -> TechLevel=（或地图触发更改后的值）时，无法从箱子中开出
秘密科技实验室等特殊方式给予生产权限不受此限制
RA2下可驻军建筑放下后会立即转为中立所属，YR下TechLevel在正常生产区间的会保留所属并且不会在建筑损坏到红血时执行驻军撤出行为（苏军战斗碉堡）

AI建造前提:
建筑:
无视:【TechLevel=-1】,PrerequisiteOverride,RequiresStolenAlliedTech,RequiresStolenSovietTech,RequiresStolenThirdTech,SpyEffect.StolenTechIndex(Ares)
有效:TechLevel,Prerequisite,Owner,AIBasePlanningSide,RequiredHouses,ForbiddenHouses
;如果建筑A的Prerequisite为建筑B且Owner/AIBasePlanningSide均正常，但是建筑B因为RequiredHouses/ForbiddenHouses无法建造，AI会认为建筑A可造，但是实际上无法建造建筑A，且不影响其他符合条件的建筑建造
单位:
无视:Prerequisite,PrerequisiteOverride,Owner
有效:TechLevel,RequiredHouses,ForbiddenHouses,RequiresStolenAlliedTech,RequiresStolenSovietTech,RequiresStolenThirdTech,SpyEffect.StolenTechIndex(Ares)
;如果[TaskForces]里有无法建造的单位，则会跳过该项继续建造之后的单位。除非通过重组凑齐无法建造的单位，否则无法执行脚本
Teleporter =
超时空行动用语句，单位被超时空传送不会死亡
同时也用于非Dock回建筑对接时使用Drive替换原本的Locomotor
例如原版超时空矿车借由这句使其“行驶”(Drive)前往矿区，而不是全程超时空移动
ThreatAvoidanceCoefficient =
躲避高危险地区的几率，实际上由于寻路方式的优先级过高这逻辑的效果几乎表现不出来
ThreatPosed =
威胁值，电脑优先攻击高威胁的但是即便拥有威胁值如果没有武器AI也不会攻击，所以想要让单位主动攻击建筑除了威胁值外还需要添加虚拟武器。由于加载物不实际存在于地图上，AI并不能直接攻击加载物，所以不要给加载物加这个
TiberiumProof =
该对象是否免疫泰矿伤害，TS残留无效，Ares已复原并，详见说明书
TiberiumHeal =
在对象在矿石中是否能加血，TS残留无效，Ares已复原，详见说明书
ToProtect =
 写yes的单位受到攻击时，AI会出动闲置部队去保护。原版海军都有这句，但海军加这个意义不大
TooBigToFitUnderBridge =
是否无法在桥底停留
Trainable =
为no时不可升级
非建筑单位默认yes，建筑默认no，原版下来自子机和空袭机的击杀经验全给子机，现代拓展引擎可设置分配方式或强制同步等级，详见说明书
驻军建筑内的驻军步兵即便自身Trainable=no也强制获得经验！（Ares已修复）
Turret =
单位有无炮塔，当单位本体上同时拥有OmniFire时会受其影响导致没有炮塔此句无效
Turret=yes的Jumpjet运动模式且使用Shp素材的载具只有处于滞空状态时炮塔才显示阴影，且绘制在单位上而非正下方的地面
Turret=yes的幻影坦克伪装炮塔有问题且伪装图像色盘会强制改变为一坨奇怪的东西
对于一个Image=none或者图像不存在的单位虽然程序原本会将它绘制为一个空的shp但如果添加了Turret那么程序仍然会尝试去调用一个不存在的vxl进而导致崩溃
以上三条Ares已修复
Turret=yes的Jumpjet运动模式载具闲置时炮塔总是朝向正东方向，Phobos已修复
与驻军逻辑配合的并不好，拥有Turret的建筑会保留撤出时的UnloadMission导致下次再塞进去步兵会被立即Unload踢出来
除此以外拥有Turret的驻军建筑踹出驻军单位以后图像无法正常刷新，需要移动一下屏幕，就像TerrainType被碾压那样
TurretAnim =
炮塔图像，当TurretAnimIsVoxel=yes时可以使用Voxel类型的素材
TurretAnimDamaged =
建筑残血时的炮塔图像
TurretAnimGarrisoned =
建筑驻军时的炮塔图像，疑似无效
TurretAnimIsVoxel =
炮塔图像是否为Voxel类型的素材
TurretAnimX =
炮塔中心点X坐标，横向，正值向右
TurretAnimY =
炮塔中心点Y坐标，纵向，正值向下
TurretAnimZAdjust =
炮塔中心点Z坐标，控制遮挡层级
TurretAnimYSort =
建筑shp炮塔遮挡优先级调整
TurretCount =
炮塔种类数(IFV 盖特 光棱坦克)
如果单位Tur文件总量[小于]该值会导致无论Body还是Tur都不显示
TurretCount=0会直接导致Weapon[X]系统不被使用
TurretRecoil =
开炮时炮塔与炮管是否后退，原版巨炮就是炮管制退的典例
TurretTravel =
该建筑炮塔可偏移的像素值，默认 2
TurretCompressFrames =
该建筑炮塔恢复所需要的帧数，默认 1
TurretHoldFrames =
该建筑炮塔保持在受后坐力位置显示的帧数，默认 1
TurretRecoverFrames =
该建筑炮塔恢复所需的帧数，默认 1
TurretRotateSound =
炮塔旋转的声音
载具用的时候炮塔是只看相对地面是否旋转的
也就是炮塔跟着车体转的时候也会播放
TurretSpins =
该载具的炮塔是否永久旋转，例如飞碟，很神奇的是这个逻辑最早是TS遗留下来并且一直有效的
该单位在炮塔允许时（指向正确的方向或拥有OmniFire=yes）才能攻击其他单位，否则会卡住，并且卡住后炮塔也会停止旋转（于是也无法继续旋转到达到允许开火的朝向）
Thief =
是否为小偷，RA1残留，在RA2已经被Agent=yes的间谍逻辑替代了。不过仍有残余效果
RA2下和Infiltrate=yes连用可以让步兵走进矿场，但是不会有任何效果，YR对此又补了一刀
在RA2/YR这句与VehicleThief=yes连用可以开启偷车贼效果，但是Thief=yes恰恰又会影响AI执行目标
如果想要使用偷车贼逻辑，请直接使用Ares完整复原并拓展的专用逻辑VehicleThief=yes，详见Ares说明书
TiltsWhenCrushes =
当Crusher时碾压Wall=yes的覆盖物是否掀起，碾压步兵固定不倾斜，OmniCrusher压强制掀起，Phobos已允许定义

 -U-
UndeployDelay =
释放型武器造成的停顿(无法移动、攻击)时间(限步兵)
也决定步兵部署模式：此语句设定正值为尤里式部署
无此代码即默认值为-1，为美国大兵式部署（需手动解除部署 部署开火需art序列）
UndeploysInto =
填载具名称。这个代码指定建筑反部署后变成的载具
被心控的建筑反部署后会断掉心控链接彻底改变所属，YR1.001为此禁用了被心控建筑的该逻辑，Phobos已允许正常交接并解除了禁用效果
实际上是TechnoType通用标签，值的类型也是TechnoType，由于拥有跨类别T选同类对象的效果，曾也用于原版引擎下的类Ares中GroupAs功能的效果，原版下可能造成一些问题，Ares已进行修复，同时提供新的GroupAs作为另一种可选的实现方式
由于DeploysInto和UndeploysInto的单向跨类T选拥有层次效果，可结合GroupAs做出注入“第一次T选MTNK选中所有MTNK，第二次T选选中所有MTNK、HTNK、LTNK”的效果
由于原标签自身作用，建筑应当确保不会执行原行为的情况下才适合这样使用，否则仍会正常执行标准操作即反部署成载具
此外这样的转变很多效果无法继承，例如铁幕，Phobos已允许继承其中一部分
特别注意：
这个语句会导致建筑出售时只逆向播放23帧，Phobos已允许定义
Foundation=1x1建筑如果拥有UndeploysInto设定在很多判定中会被视为“载具”，例如可以框选，被维修车维修等，建筑能否框选Ares已给予专门语句允许设定，是否视为载具Phobos已给予专门语句允许设定，此外原本 Artillary、ICBMLauncher、TickTank、SensorArray 四句会让 AI 执行攻击脚本时将其视为载具，但 Phobos 在实现本功能时去除了它们的这一效果。
Unsellable=no并且ConstructionYard=no的的建筑如果拥有UndeploysInto无法正常出售
由于RA2下不再拥有是否按住Alt区分工厂建筑移动(UndeploysInto)与设置集结点的效果，现在总是点击后立即进入反部署并且依然绘制集结线，Phobos下禁用了集结线
Underwater =
是否为水下物体，用于NavalTargeting判定
同时移动不会播放全局Wake=指定的波纹，强制死亡时不会有沉船效果（都已经在水下了）
Unnatural =
是否为非生命体单位
用于Natural与NavalTargeting、LandTargeting的各种判定
UnloadingClass =
Unloading状态引用的图像，是指矿车倒矿、武装直升机部署时所处于的状态
如果原单位Turret=yes那么UnloadingClass会尝试使用自己的炮塔或者一个不存在的空炮塔图像
如果原单位Turret=no那么UnloadingClass会正常使用自己的炮塔，哪怕单位实际上直接使用Body转向目标而Turret单纯同步Body的方向
UnitAbsorb =
载具单位是否能进该生化反应炉入发电
UnitEnterSound =
载具进入该建筑的声音
UnitExitSound =
载具退出该建筑的声音
UnitReload =
该建筑能否补充弹药，原版用于空指部
UnitRepair =
该建筑能否修车，同时也可出售，Ares允许分离设置能否出售，详见说明书
如果同时拥有WeaponsFactory则维修期间将对被维修伤害的物理伤害转移到自己并禁用对被维修单位的特殊伤害类型，哪怕是是超时空抹除和超时空传送，甚至Organic=yes的单位可以抗铁幕，虽然并不能得到效果
如果一个BalloonHover=yes的单位使用抛射体Vertical=yes的武器攻击一个这样的建筑那么即便建筑在武器Range范围外单位也不会尝试接近目标
UnitsCostBonus =
载具建造价格为原来多少倍
UnitsGainSelfHeal =
给单位增加每桢几点的回血，算法类比InfantryGainSelfHeal
Unsellable =
无法被出售，仅影响玩家使用出售光标手动出售，也就是AI和触发强制Selling等可以无视这条进行出售，仅可通过Buildup留空等方式去更上层禁用。Ares下已拓展至非建筑类，用于维修厂等出售方式
Upgrades =
这个建筑能够被加载物加载的次数，见PowersUpBuilding一句下的详细注解
UndeploySound =
反部署时的声音，用于武装直升机类单位
UseOwnName =
YR新增
用于步兵
是否让Gunner载具的名称显示为{([InfantryPassenger] -> UIName=) ([TransportVehicle] -> UIName=)}的形式
在YR中使用该语句有一些不一致之处
IFVMode[2]
武器:机关枪A|Tur[1]
使用者E1、E2、SPY，名为”Machine Gun IFV“
IFVMode[3]
武器:高射炮|Tur[1]
使用者FLAKT，但因为缺少UseOwnName显示为“Machine Gun IFV”
IFVMode[4]
武器:机枪B|Tur[1]
使用者GHOST、TANY、BORIS，因为存在该语句被称为“<Passenger> IFV”
使用者CCOMAND、PTROOP，但因为缺少UseOwnName被称为“Machine Gun IFV”
鬼知道WW写了一手啥玩意……

修复示例
[FLAKT]
UseOwnName=true
[CCOMAND]
UseOwnName=true
[PTROOP]
UseOwnName=true
当然你也可以把BORIS他们三个的这个标签禁用

为什么磁爆步兵明明没有UseOwnName=yes但是正常显示为“磁爆步兵 多功能步兵车”呢？这就要见HasTurretTooltips一条下的另一套更上层的规则了

 -V-
VeteranAbilities =
老兵升级加的能力，具体可用的值类型见EliteAbilities
VHPScan =
用于爱国者，视目标可能受的伤害决定目标选择。
None为
不开启逻辑，即无效果
Normal为
优先VHP<Strength/2的目标，尤其VHP<0者
即攻击预测将要死亡的目标以尽量摧毁更多的目标
Strong为
忽略VHP<0者，也就是尽可能的让杀伤有效，均摊伤害
VHPScan是给每个单位一个“预计血量”（VHP），我们设实际血量为RHP
每当有一个武器射向目标时，无论引爆与否VHP先预计一下被炸后的血量
同时保证VHP>=RHP-30，然后每4帧增加1次直到VHP==RHP
如果目标单位得到修复则把VHP立即写为RHP

VoxelBarrelOffsetToPitchPivotPoint =
建筑VXL炮管垂直方向旋转（X轴，与地面平面的夹角）的基点
VoxelBarrelOffsetToRotatePivotPoint =
建筑VXL炮管水平方向旋转（Y轴，垂直与地面的平面）的基点
VoxelBarrelOffsetToBarrelEnd =
建筑VXL炮管的终点，也就是实际射出炮弹播放开火动画的位置
VoxelBarrelOffsetToBuildingPivotPoint =
建筑VXL炮管相对建筑0,0格子的绝对坐标
其中
第4句会在TurretAnimX、TurretAnimY决定的TurretAnim坐标之后叠加计算，使用XYZ坐标
前3句均在第4句与TurretAnimX和TurretAnimY指定的中心坐标的基础上绘制，使用FLH坐标
不过炮塔朝向依然是根据TurretAnimX和TurretAnimY决定的中心来计算相对方向的
VoxelBarrelFile =
炮管图像，需要BarrelAnimIsVoxel一句来开启。仅用于SHP炮塔使用VXL炮管，无法用于VXL炮塔独立调用其他VXL炮管，VXL炮塔会自动匹配与其命名规则相符的炮管
VoxelBarrelScale =
建筑VXL炮管的缩放倍数，仅限 FS，RA2中无效

VoiceAttack =
接受攻击指令的声音，如果单位为[FV]且造成负值杀伤那么使用[AudioVisual] -> VoiceIFVRepair=指定的音效
非[FV]的情况YR下在使用对应武器时会被下面四句覆盖
VoicePrimaryWeaponAttack =
YR新增，主武器射击的声音
VoicePrimaryEliteWeaponAttack =
YR新增，精英主武器的声音
VoiceSecondaryWeaponAttack =
YR新增，副武攻击声音
VoiceSecondaryEliteWeaponAttack =
YR新增，精英副武器的声音
VoiceCrashing =
被击落的声音
VoiceDeploy =
部署的声音，通过快捷键或底边栏按钮部署不会触发，PhobosBuild47已修复
VoiceUndeploy =
反部署时的声音
VoiceEnter =
进入[TechnoType] -> Dock=的建筑时的声音（非战机）
在步兵身上使用需要Assaulter等语句中的至少一种（不然都没法Enter又何谈Enter的Voice）
VoiceFeedback =
害怕时播放的声音
VoiceHarvest =
采收矿物的声音
VoiceMove =
接受移动指令的声音，包括Aircraft执行吊运，Phobos 下可以为吊运单独指定一个将载具拾取的音效
VoiceSelect =
选中的声音
VoiceSelectDeactivated =
失去控制时候的声音 见遥控坦克
VoiceSelectEnslaved =
奴隶类被解放的声音
VoiceSpecialAttack =
接受特殊攻击指令（例如坐下后攻击）的声音
C4=yes
Harvester=yes
Ivan=yes
Deployer=yes
Parasite=yes
CanDisguise=yes
选中医疗兵并点击下达区域防御命令
仅在满足以上任一条件时启动
VoiceSinking =
沉没喂鱼时的声音
VehicleThief =
是否为偷车贼
这句的效果是该步兵可以在敌方载具上出现“进入”光标
在原版这句加上Thief=yes可以在Ra2/Yr做偷车贼
会让AI寻敌智障，RA2下可以用寄生心控几乎完美的复刻，YR也给搞残了，Ares已复原相关逻辑，详见说明书，如果你获得本文档的同时没有配套这一文件，说明你的文档并非从原正式发布渠道获取，而是已经被第三方未经许可拆分修改过的
VoiceComment =
步兵平时闲聊音效
VoiceFalling =
指定空中单位从天空落下时要发出的声音
VoiceCapture =
占领音效需要有[InfantryType] -> Engineer=yes
VoiceHarvest =
收集矿石时发出的声音
仅应用于设置了[TechnoType] -> ResourceGatherer=yes或[VehicleType] -> Harvester=yes的对象
VoiceDie =
被摧毁时发出的声音

 -W-
Warpable =
填no，则免疫超时空抹消攻击，但是不影响超时空传送超武
甚至这个标签单纯控制效果，让物体不被抹除，但是不影响目标选择和实际开火，也就是只要对方乐意依然可以射个没完，无论主动攻击还是手动攻击
WalkRate =
填数值。单位行走动画播放速率，素材中每帧实际播放多少帧。可用于shp载具和vxl载具
Wall =
是否为围墙，建造时会根据[TechnoType] -> GuardRange=指定的距离与同类型链接，建筑实际放下后会立即变成其在art中通过[BuildingImage] -> ToOverlay=所指定的覆盖物
此外AI尝试放置时会让单元格的单位执行分散指令以让出空位，与全局[General] -> MaximumBuildingPlacementFailures=合用保持1次放置失败后仍会再次尝试（而此时恰好单位已经让出空位）
然而这个逻辑实现的比较质朴，程序并不判定围墙链接的方向，也就是说存在单位向围墙延伸方向移动的情况
原版引擎下苏盟围墙可以在破损的墙上直接修建新墙来修复墙体，但并不支持新增的围墙（包括尤里围墙），在Ares中已经解除了这一限制
于是可能表现为：
AI尝试放下墙 -> 单位向旁边挪了一格，但是移动到了围墙链接所需的另一格子 -> AI放下了墙，但是由于没有完全围住建筑，再次放下另一格墙 -> 返回第一步
也就是走一步放一格再走一步再放一格直到最后一格分散时找空地只能找到不阻碍围墙链接的格子为止，然而此时围墙也已经用不着自动连接了
WantsExtraSpace =
建筑是否需要额外的空间，影响AI建筑间隔，为yes时AI建造该建筑会按全局[AI] -> AIBaseSpacing=值+1来计算，可以更好的防止堵车，但也会降低AI基地建设效率
WaterBound =
是否为水上建筑，实际确定该BuildingType是否只能在构造时放置在其中Float的SpeedType百分比值高于0％的地形图块上
原版是水，你也可以改成公路等等，但仍要求是空地，矿石那种实际是一个覆盖物占据了格子的依旧造不了，形象点说用这个往矿上拍建筑相当于尝试往敌人的围墙上拍个自家兵营
相当于给建筑写了SpeedType=Float，同时这个效果会无视Buildable，原版下在限制建造区域方面和Naval分离控制有部分功能重叠，Phobos把Naval干掉后只吃这句
优先级高于SpeedType，也就是建筑拥有SpeedType=Float与WaterBound中至少一句的三种情况等效，但如果同时拥有SpeedType≠Float与WaterBound则WaterBound覆盖SpeedType回到Float效果
原版下不被DeployToFire考虑，因此无法完成DeployToFire成水上建筑的任务，Phobos已修复
WeaponCount =
武器种类数(IFV 盖特 光棱坦克)配合Weapon1 Weapon2等使用，光棱充能炮塔实际上只使用Weapon1，哪怕你放开了WeaponCount
WeaponStages =
盖特武器有几阶，Stage1 Stage2 等则分别代表盖特计数器多少以内为此阶
如果不满足WeaponCount=WeaponStages*2那么可以得到一个精致的0070DF8A
如果处于SimpleDeployer或使用DeployFire释放武器则不会升档，武直状态虽然用Weapon2但是Report却会去单独升档读Weapon246……当然你也可以用DeployFireWeapon一句指定一下
WeaponX =
由上述多武器逻辑启用，启用多少只看WeaponX，也就是盖特的WeaponStages没有用上的武器也可以通过Ares的NoAmmoWeapon等用起来，例如https://www.bilibili.com/opus/789437335972348039
Weight =
重量，决定应对[Warhead] -> Rocker=yes的弹头时被掀翻的难易度，同时对于Naval=yes且Underwater=no、Organic=no的水上单位若该值大于全局[General] -> ShipSinkingWeight=的值则在水上被摧毁会表现为沉没而不是直接被摧毁（原版海蝎与航母），沉没的声音用SinkingSound指定，沉没的形态根据Locomotor决定是直接下沉（Mech）还是整个船体倾斜后再下沉（Drive和Ship）
WorkingSound =
工作声音
Weeder =
在TiberiumSun中
这是NOD化学飞弹所使用的的逻辑
即Weeder矿车收集了足够的泰伯利亚废矿倒入Weeder储藏舱中
储藏舱满时才可使用化学飞弹超武
相关的还有[SuperWeaponType] -> AuxBuilding=和[SuperWeaponType] -> ManualControl=两个逻辑
个人倒是觉得其实就是一种变相的矿车(Harvester)逻辑，而且同样不能用于步兵233
一个Weeder=yes的建筑可以储存矿石
要用Storage=控制储存数量
一个Weeder=yes的单位
可以收集矿石
不过它还需要Storage=来控制每一个格子代表的矿石数量才能收集
在RedAlert2中
泰伯利亚废矿随着泰伯利亚藤蔓逻辑一起被Westwood砍了
这个单位会到自己的Dock=<Building>旁
这个建筑和矿场一样（废话）要有DockUnload=yes
然后卸下它所装载的任何东西，如果有载员可以放出载员（子机没试）
如果是载员的话则会被卸载到这个建筑旁边，用来做自动运输车似乎不错
有很多类似Refinery的特性，例如会使建筑强制无法将单位生产出来

Phobos已经复原了泰伯利亚藤蔓相关的硬编码逻辑，详见说明书

WeaponsFactory =
该工厂生产的载具是否从车场内开出来
如果否的话虽然仍有集结点但是不集结
而不是直接生成于建筑外
用于船港会出现许多错误
同时会阻断矿车单位倒矿
阻碍医院等建筑单位离开

 -X-
没有收录以X开头的语句

 -Y-
YuriBarracks =
填yes或no，是否为尤里方的兵营，步兵从相对建筑中心位于[2,1]的格子离开建筑，也影响AI。所有南北向长于东西向的兵营都应该使用，否则会导致生产一个飞行步兵后无法继续生产其他步兵等问题

 -Z-
ZFudgeTunnel =
指定载具位于隧道口时的ZAdjust
ZFudgeColumn =
指定载具位于高架桥头后面的ZAdjust
ZFudgeCliff =
指定载具位于悬崖后面的ZAdjust
ZFudgeBridge =
指定载具位于高架桥梁桥体下的ZAdjust

全都是绘制遮挡层级相关的东西，正值向后负值向前，例如ZFudgeBridge=2000会导致载具在桥梁下面时ZAdjust向后2000，直接被地板盖住而显示不出图像
以上四句不影响伪装逻辑的图像
这些实际上是用于单位处理与这些特殊Tile之间Z关系的标签，Z并不用于VehicleType之间的遮挡处理，对于Z的概念详见ART词典ZAdjust条目下方注解
```

最后修订日期20241106By九千天华
如果有错误或者缺漏，请参阅拓展引擎说明书与IDA