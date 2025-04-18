;■HUD设置文件hud/**.txt

;***********************************************************************************



; ★重要

; HUD即使在启动“我的卡夫”的状态下也可以重新读取。

; [乘坐机体→使用R键补给画面→MOD Option→Development→Reload All HUD]

; 纹理的重新读取利用了我的卡夫的默认功能，而不是从直升机MOD。

; [Esc键游戏菜单→设定→资源包→完成]




;************************************************************************************************************

; 顺序只影响HUD的设定文件。

; 按照在设定文件中记载的顺序执行处理，其成为描绘顺序。



;************************************************************************************************************

; 关于公式

; ■DrawString、DrawCenteredString的数据部分以外的数值可以设定计算公式。

; 示例：Color=123+456

; ■可以在公式中设定十六进制数。在数字前面加上#或0x。

; 示例：Color=#123+0x456+789

; ■可以在公式中设定“变量”。

; 示例：Color=hp_rto * 100

; hp_rto的机体耐久值为0.0～1.0。因此，*100为0.0～100.0。

; ■可以在公式中设定条件。

; 格式：条件？条件成立时的值：条件不成立时的值

; 示例：Color=hp_rto>0.2? 0xFFFFFFFF: 0x00000000

; hp_rto超过0.2时为0xFFFFFF，0.2以下时为0x00000000设定为Color

;

; 变量列表

; center_x：画面中央坐标X

; center_y：画面中央坐标Y

; 宽度：屏幕宽度

; height:屏幕高度

; yaw:机体偏航[横向旋转]（-180.0～180.0）

; pitch:机体的俯仰[纵向旋转]（-90.0～90.0）

; roll:机体的角色（-180.0～180.0）

; plyr_yaw:玩家的偏航[横向旋转]（-180.0～180.0）

; plyr_pitch：玩家的间距[纵向旋转]（-90.0～90.0）

; altitude:机体的高度（0～）从机体到下方向的块的距离（不为负值）

; sea_alt：机体高度（0～）海拔。与作为基准的海的高度的距离（不为负）

; hp:机体剩余耐久值（0～）

; max_hp:机体的最大耐久值（0～）

; hp_rto:机体剩余HP的比例（0.0～1.0）

; throttle：机体当前节气门（0.0～1.0）

; pos_x:机体坐标X

; pos_y:机体坐标Y

; pos_z:机体的坐标Z

; motion_x:机体加速度X

; motion_y:机体加速度Y

; motion_z:机体加速度Z

; fuel:机体剩余燃料的比例（0.0～1.0）

; low_燃料：显示燃料下降警告。为了使其闪烁，降低时重复0和1（0=有燃料，1=燃料降低）

; stick_x：操纵杆X方向的量（-1.0～1.0）

; stick_y：操纵杆Y方向的量（-1.0～1.0）

; reloading：武器重装状态（0=未重装。1=重装中）

; reload_time:武器重装剩余时间百分比（0.0～1.0）0.0完成重装

; wpn_武器热量（0.0～1.0）

; is_heat_wpn:是否是热量式武器（0=不是热量式。1=热量式）

; dsp_mt_dist:显示着落距离（0=不显示。1=显示）

; mt_dist:着落距离（小于0.0时不可计算）

; have_radar:是否装备雷达（0=无雷达。1=有雷达）

; radar_rot：雷达的旋转角度。绕一圈后更新实体的位置

; vtol_stat：仅限固定翼飞机。0=通常，1=VTOL切换中，2=VTOL中

; free_look:0=通常，1=FREE LOOK中

; cam_mode:0=通常，1=NIGHT VISION中，2=THERMAL VISION

; cam_zoom:相机倍率。1.0 ~ 10.0

; auto_pilot:0=通常，1=自动pilot中

; have_flare:是否配备了火炬射出装置（0=无。1=有）

; can_flare:是否启用光斑（0=启用；1=准备中禁用）

; sight_type：瞄准类型（0=无，1=移动Sight，2=MissileSight）

; 火箭：导弹锁定状态（0.0到1.0）

; 颜色：当前颜色设置（0x00000000~0xFFFFFF）

; 库存：库存插槽数（0-54）

; hovering:悬停状态（0=不悬停，1=悬停）

; is_uav:是否是UAV（0=非UAV，1=UAV）

; uav_fs:UAV的电波强度。越大越接近UAV站（0.0~1.0）

; gunner_模式：是否为甘纳模式（0=正常模式，1=甘纳模式）

; time:我的一天时间为24000（0-24000），0=上午6点，6000=中午

; test_模式：是否为测试模式（0=正常模式，1=测试模式）




;************************************************************************************************************

; 其他HUD绘图文件调用

; 如果指定HUD的文本文件名，则可以执行该设定文件的描绘处理。

;

; Call = common_对于pilot，common_执行pilot.txt

; 也可以在调用的设定文件内读出其他的文件，但不能双重读出相同的文件。

; 例如，如果在heli.txt内Call=heli，则由于heli.txt已经在执行中，所以不进行处理，被忽略。

; 另外，在heli.txt内记载为Call=plane，在plane.txt内记载为Call=heli情况下

; 因为heli.txt正在执行，所以在这种情况下也不执行。

Call = common_pilot




;************************************************************************************************************

; 结束当前HUD文件的绘制

;

; 如果调用的是Call，则返回调用者

; heli.txt到uav_调用fs.txt，将uav_如果在fs.txt中使用Exit，则uav_fs的绘制结束

; heli.txt中的uav_处理从调用fs.txt的下一行继续。

;

Exit




;************************************************************************************************************

; 条件分支

; 仅在满足指定条件时执行处理

;

; 在条件为0以外情况下，执行处理1处理2处理3

; 条件为0时不执行处理1处理2处理3

; If=条件

; 活动1

; 活动2

; 处理3

; EndIf

; ※嵌套不兼容（不能在If到EndIf之间再加If）

;

; 在以下示例中，is_heat_如果wpn为1，则执行Color和DrawRect。

If = is_heat_wpn==1

Color = 0xFF28d448

DrawRect = -145, 57, 43, 10

EndIf




;************************************************************************************************************

; 颜色设置

; 当进行颜色设定时，以该设定颜色描绘以后的文字颜色或线的颜色

;

; 有两种模式的设定方法。

; 一个参数指定的方法和四个参数指定的方法。

; 单个设置：从顶部到不透明度、红色、绿色和蓝色

; :例）0xAABBCCDD时，不透明度=AA、红色=BB、绿色=CC、蓝色=DD

; 如果设置为四个：从上到下依次为不透明度、红色、绿色、蓝色

; :例）12、34、56、78时，不透明度=12、红色=34、绿色=56、蓝色=78

; 十六进制或四个十进制

; 示例：以下均为有效设置

Color = 0xFFFFFFFF

Color = #FFFFFFFF

Color = 0xFF, 40, 212, 72




;************************************************************************************************************

; 绘制字符串

; DrawString：从指定坐标向右绘制

;
