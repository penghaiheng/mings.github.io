PHP JavaScript 农历公历干支历互转,万年历,四柱,六十甲子,属相,十二星座,二十四节气<br />
支持从-1000年至3000年间的八字排盘及大运推算,真太阳时排盘,分析刑冲合害关系<br />
支持从-104年至2300年间的农历公历互转<br />
-721年至2300年的公历农历与寿星万年历一致<br />

算法原理和JS源码完全来自: http://www.bieyu.com/<br />
结果比对及农历修正来自寿星万年历: http://www.nongli.net/sxwnl/<br />

此工具类包含:<br />
1,儒略日历<br />
以公元前4713年1月1日12时为起点,每天(每廿四小时)加一的历法;<br />
比如2020年1月1日12点的儒略日为2458850,2020年1月1日0点的儒略日为(2458850 - 0.5);<br />
这种历法方便各种计算,比如已知起点日为周一可求得任一日期的星期,已知起点日的干支可求得任一日期的干支<br />

2,公历(阳历,格里历,西历)<br />
以地球绕太阳公转计算的历法;<br />
用公式可直接求得两分两至(春分秋分夏至冬至);<br />
公转是椭圆轨道,把这个椭圆均分为24等分,可求得中国的二十四节气;12等分则为西方的十二星座;<br />
此工具计算出的时间点误差在20秒内;<br />
已知2020年春分点为3月20日11点49分57秒,则算法认为57秒前是双鱼座,57秒后是白羊座,是否按此计算请自行斟酌;<br />
每月两节不变更,最多相差一两天.上半年来六廿一,下半年是八廿三 这里的六廿一和八廿三说的是公历;<br />

3,阴阳历(农历,民间称阴历)<br />
严格地说,以月球绕地一周为一个月计算的历法为阴历;<br />
如果这样,阴历跟二十四节气的时间差就越来越大,我们可能要在夏季过大年初一;<br />
也许人们为了能固定在立春前后吃上年夜饭(May be...),引入闰月的概念,使之与公转齐平,所以农历考虑了月亮又考虑了太阳,为阴阳历;<br />
陰曆正月與置閏这一段很难理解,请参看 http://www.bieyu.com/<br />

4,干支历<br />
这种历法现在可能多用于命理学和历史研究领域,与二十四节气相关;<br />
由于一年只有12个月而不是60个月,一天只有12小时而不是60小时,所以合法的四柱并不是简单的排列组合;<br />
年柱跟月柱有固定的关系:甲己之年丙作首,乙庚之歲戊為頭,丙辛歲首尋庚起,丁壬壬位順行流,若言戊癸何方發,甲寅之上好追求.<br />
日柱跟时柱也有固定关系:甲己還加甲,乙庚丙作初,丙辛從戊起,丁壬庚子屬,戊癸何方發,壬子是真途;<br />
所以不存在甲子年甲子月甲子日甲子时这么个时间.<br />
八字组合共有518400种(不分早晚子时),且一個八字出現後,至少要60年後才会再出現,最多要240年後才又出現;<br />
已知2020立春点为2月4日17时3分44秒,44秒前为己亥年,44秒后为庚子年;<br />
已知2020驚蟄为3月5日10时57分22秒,22秒前为戊寅月,22秒后为己卯月;<br />
是否按此计算请自行斟酌,尤其是要用在命理学上的时候;<br />

5,真太阳时<br />
粗略理解: 我们用的东八区时间(北京标准时间),是东经120度线的理论时间(平太阳时,平均太阳时)<br />
按照地球自转一圈严格为24小时计算,正好每经度4分钟(24小时*60/360度 = 4分钟),我国跨越五个时区,已知经度和北京标准时间可以计算出地方理论时间(地方平太阳时,(J-120)*4).<br />
实际上地球自转速度有快有慢,而且太阳并不总是从正东方升起,考虑这个快慢和倾角而计算出的时间为真太阳时,真太阳时的正午12点,正好当地的(如日晷)影子最短.<br />
地方平太阳时与真太阳时有相对固定的差值,各地都一样,每年1月1日大约相差3分钟,12月1日大约相差11分钟,可以通过"真平太阳时差换算表"查得,本项目采用天文方法计算.<br />
有说古人用日晷计时,没有北京时间的说法,所以排八字要用真太阳时,请自行斟酌<br />

6,精确度问题<br />
当前项目与寿星万年历(源码在 sxwnl 目录)进行过逐时比对[js/diff.js],结果如下:<br />
公历儒略历部分完全匹配<br />
节气及月相部分相差不超过20秒(均为天文科学上的算法)<br />
真太阳时部分相差在20秒内,本项目考虑了纬度(均为天文科学上的算法)<br />
PHP中的date_sun_info($timestamp, $W, $J)也能实现真太阳时的计算,与本项目的真太阳时模块有几分钟误差<br />
农历-721年至2300年完全匹配(古代农历是完全从寿星万年历搬过来的)<br />
四柱八字算法上,寿星不考虑年柱月柱的真太阳时,导致少量对不上<br />
星座算法上,寿星精确到日,本项目精确到秒,导致节气交接日星座对不上<br />

7,需要解释的<br />
采取真太阳时排盘,由于年柱以立春为界,月柱以节令为界,那么廿四节气是否也要转为真太阳时?<br />
真太阳时排盘有几种方案,请自行斟酌:<br />
a.仅对日柱时柱做调整,年柱月柱不动(寿星万年历,常用方案)<br />
b.年月日时柱均做调整,节气时刻不动(本项目方案)<br />
c.年月日时柱均做调整,节气时刻均转为真太阳时(科学地说应该用此方案)<br />
廿四节气是针对北半球而言的,南半球的干支历排盘以及星座等要如何处理呢?<br />

PHP与Javascript的方法是一致的,如下:<br />

公历转儒略日:<br />
p.Jdays(yy, mm, dd, hh, mt, ss);<br />

儒略日转公历:<br />
p.Jtime(jd);<br />

公历转农历:<br />
p.Solar2Lunar(yy, mm, dd);<br />

农历转公历:<br />
p.Lunar2Solar(yy, mm, dd, ry); //传yy年1月1日ry=false,返回中有闰月及各月日数信息<br />

公历转干支历:<br />
p.GetGZ(yy, mm, dd, hh, mt, ss);<br />

干支历转(搜索)公历:<br />
p.gz2gl(ygz, mgz, dgz, hgz, yeai, mx);<br />

根据公历进行八字真太阳时排盘<br />
p.fatemaps(xb, yy, mm, dd, hh, mt, ss, J, W); //J为经度W为纬度,东经80度27分表示: 80+27/60<br />

//引申出来的方法<br />
p.ValidDate(yy, mm, dd);<br />
p.GetWeek(yy, mm, dd); //计算公历的某天是星期几<br />
p.GetSolarDays(yy, mm); //获取公历某个月有多少天<br />
p.GetXZ(yy, mm, dd, hh, mt, ss); //根据公历年月日精确计算星座下标<br />
p.GetAdjustedJQ(yy, false); //求出含某公历年春分點開始的24节气的儒略日历时间<br />
p.MGZ(ygz); //根据年干支计算所有合法的月干支: 甲己之年丙作首...<br />
p.HGZ(dgz); //根据日干支计算所有合法的时干支: 甲己還加甲...<br />
p.GZ(tg, dz); //天干地支计算甲子编号<br />
p.risenset(jd, J, W, LX); //根据经纬度计算日出日落或月出月落时刻<br />

//分析刑冲合害关系<br />
GetGX(tg, dz); //参看demo.html 及 docs/make_gx.php