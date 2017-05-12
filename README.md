"""
================================
常见的画图操作
================================

本函数主要是一些常见的画图操作，如设置画图颜色，字体，坐标轴，标题，legend,在画好的图上写文字等

"""
#color:'b'	blue; 'g'	green; 'r'	red; 'c'青色; 'm'品红; 'y'	yellow; 'k'	black; 'w'	white
#linestyle:'-'	solid line style;  '--'	dashed line style;  '-.'	dash-dot line style
#':'	dotted line style;  '.'	point marker;  ','	pixel marker;  'o'	;  'v';'^'	 '<'; '>';'1'	tri_down marker
#'2'	tri_up marker;  '3'	tri_left marker;  '4'	tri_right marker;  's';'p'	pentagon marker;'*';
#'h'	hexagon1 marker;  'H'	hexagon2 marker; '+';'x'	x marker;  'D'	diamond marker;  'd'	thin_diamond marker; 
#'|'	vline marker;  '_'	hline marker
#画图操作
import numpy as np
from matplotlib import pyplot as plt#导入pyplot模块并用别名plt表示
from matplotlib.font_manager import FontProperties    #导入管理字体的模块
#from matplotlib.widgets import Cursor   #导入鼠标的模块
x = np.linspace(0, 10, 10)   #在0-10的范围取100个点
y = np.sin(x)
z = np.cos(x**2)
w=2*np.cos(x+2)
plt.close('all')
#plt.plot的属性
#Property:  alpha:表示透明度(0-1之间);animated	是否显示动画[True|False]
#antialiased(aa):是否使用抗锯齿渲染画图[True | False];axes:一个Axes实例;clip_box:一个matplotlib.transforms.Bbox实例
#clip_on:设置是否剪辑图片[True | False];clip_path:设置剪辑的方式;color：设置线条颜色
#dash_capstyle	:设置虚线的封面样式[‘butt’ | ‘round’ | ‘projecting’]
#dash_joinstyle:设置虚线的连接样式[‘miter’ | ‘round’ | ‘bevel’]
#drawstyle:设置绘制样式[‘default’ | ‘steps’ | ‘steps-pre’ | ‘steps-mid’ | ‘steps-post’]
#figure:一个matplotlib.figure.Figure实例;fillstyle：设置标记的填充方式[‘full’|‘left’|‘right’|‘bottom’ | ‘top’ | ‘none’]
#gid:设置组的ID;label：为legend设置标签
#linestyle(ls) 设置线条的样式	[‘solid’ | ‘dashed’, ‘dashdot’, ‘dotted’ | (offset, on-off-dash-seq) |
#'-' | '--' | '-.' | ':' | 'None' | ' ' | '']
#linewidth(lw)：设置线条的宽度;marker:设置标记的形状;markeredgecolor(mec)设置标记边缘的颜色
#markeredgewidth(mew):设置标记的边缘宽度;markerfacecolor(mfc):设置标记的填充颜色
#markerfacecoloralt(mfcalt):设置标记的备用填充颜色;markersize(ms):设置标记的大小
#markevery=n:每隔n个点将被使用marker进行绘制;picker:设置线条的事件选择器详细信息。
#pickradius	Sets the pick radius used for containment tests;rasterized:在向量后端输出强制使用栅格化(位图)绘制。
#solid_capstyle:设置实线的封面样式[‘butt’ | ‘round’ | ‘projecting’];solid_joinstyle:设置实线的封面
#样式[‘miter’ | ‘round’ | ‘bevel’]
#transform:一个matplotlib.transforms.Transform实例;url:设置url;visible:图是否可见[True | False]
plt.plot(x,y,linestyle='dotted',marker="v",color="r",linewidth=2)
#在y+-0.3范围内画填充阴影，alpha表示透明度
plt.fill_between(x, y - 0.3,y + 0.3, alpha=0.1,color="r") 
#markersize可以控制所画圆圈的大小，而linewidth控制所画图形线的宽度
plt.plot(x,z,linestyle='-',marker='o',markerfacecolor='k',markersize=10,linewidth=1.5)
#MarkerEdgeColor用于设置方框边缘颜色，%MarkerfaceColor用于设置方框填充颜色
plt.plot(x,w,'s-',markeredgecolor='m',markerfacecolor='g',markersize=8,linewidth=1.5)

ax=plt.gca() 
#设置坐标轴顶端边缘线为蓝色，线宽度为2
ax.spines['top'].set_color('b')
ax.spines['top'].set_linewidth('2')
ax.yaxis.set_ticks_position('right')   #设置y坐标轴位置为右侧
plt.xlim(-1,10)   #x轴范围
ax.set_xticks(np.linspace(0,10,11))  #设置xticks为刻度线为0-10,共十一个点
#设置xticklabel刻度注释为，'zero','One','Two','Three','Four','five'等，并将刻度旋转30度
ax.set_xticklabels( ('zero','One','Two','Three','Four','five','six','seven','eight','nine','ten'),
                   fontsize=16,fontname='Times New Roman',rotation=15)  
plt.xlabel("x(s)",fontsize=16,color='m',horizontalalignment='center',
           fontname='Times New Roman')    #中间对齐
ax.set_ylabel("$f(x)$",fontsize=16,color='r',fontname='Times New Roman')
#图标题 weight表示颜色的浓浅
#微软雅黑:msyh.ttc;楷体:simkai.ttf;黑体：simhei.ttf;宋体:simsun.ttc;仿宋：simfang.ttf更多字体见
#C:\Windows\Fonts\下的文件
fontSet = FontProperties(fname=r"C:\Windows\Fonts\simsun.ttc", size=16) 
plt.title(u"第一幅图",color='k',fontproperties=fontSet,weight='heavy')  
#ax.set_xticks([])   #设置x坐标轴刻度为空
#ax.set_yticks([])   #设置y坐标轴刻度为空
plt.ylim(-3,3)   #y轴范围
#'r'表示自然字符串，和一般字符串相比，自然字符串里的\不再具有特殊含义
plt.text(6, 2.1,r'$\mu=100,\sigma=15$', color='b',fontsize=20)   
plt.text(3, -2,r'$\alpha_i > \beta_i$', fontsize=20)
plt.text(0.7, -0.6, r'$\sum_{i=0}^\infty x_i$', fontsize=20)
plt.text(0.7,2.4,r'$sin(\omega+\alpha)=\lim_{n\rightarrow-8}$',color='r',fontsize=20)
#plt.grid(True)
#设置网格线颜色为黑色,线型为虚线,alpha表示网格的清晰度;用'major'|'minor'|'both' to set the grid 
#for major or minor ticks.
plt.grid(b='major',color='k',linestyle='--', linewidth=1.5,alpha=0.7) 
#shadow=True设置阴影为真;标题title='legend',设置lengend列数：ncol=3(默认为1)
#legend.Legend(parent, handles, labels, loc=None, numpoints=None,markerscale=None,markerfirst=True,
#scatterpoints=None,scatteryoffsets=None,prop=None,fontsize=None,borderpad=None,labelspacing=None,
#handlelength=None, handleheight=None, handletextpad=None, borderaxespad=None, columnspacing=None,
#ncol=1, mode=None, fancybox=None, shadow=None, title=None, framealpha=None, edgecolor=None, 
#facecolor=None, bbox_to_anchor=None, bbox_transform=None, frameon=None, handler_map=None)parent表示
#包含legend的图例;handles表示要添加到legend上的图例列表;labels表示用于标记图例的字符串列表;loc表示
#legend的放置位置，参数可为'upper right';'upper left';'lower right';'lower left';'center right';
#'center left';'center';'lower center';'upper center';numpoints表示在plt所画的图中legend上marker符号的点
#数;markerscale表示legend的符号相对于坐标原点的大小;markerfirst为bool型，True表示marker在标签的左侧。
#scatterpoints表示在散点图中legend上marker符号的点数;scatteryoffsets表示legend中散点符号的yoffsets列
#表;prop表示字体属性;fontsize字体大小;borderpad表示legend边界内的小数空格;labelspacing表示legend条目
#之间的垂直空间;handlelength表示legend手柄的长度;handleheight表示legend手柄的高度;handletextpad表示
#legend手柄和文字之间的pad;borderaxespad表示legend手柄和坐标轴之间的pad;columnspacing表示列之间的间距;
#ncol表示列的个数;mode  ；fancybox为bool型,True表示画一个圆形花式框;shadow为bool型，表示画legend后是
#否有倒影;titleb表示legend的标题;framealpha表示框的透明度;edgecolor表示框的边缘颜色;facecolor表示框的
#填充颜色;bbox_to_anchor用于控制legend的位置，bbox_to_anchor=(x,y)x,y值均在0-1之间，其值越大表示
#legend越向右和向上移动;bbox_transform=ax.transAxes表示坐标是相对于坐标轴;frameon为bool型，True表示
#在框上画legend;handler_map？？
ax.legend(("$sin(x)$", "$cos(x^2)$","$2cos(x+2)$"),loc='lower right',title='legend',bbox_transform
          =ax.transAxes,numpoints=1)#numpoints=1表示legend上表示线的点数为1
ax.get_legend().get_title().set_color("red")
#legend另一种画法，legend位置更加自由 bbox_to_anchor=(x,y).当x,y有一个参数大于1，则legend位于图的外面
#如bbox_to_anchor=(0.99, 1.27)：在图形的右上角;bbox_to_anchor=(0.99, 0.3)：在图形的右下角
#bbox_to_anchor=(0.14, 1.27)：在图形的左上角;bbox_to_anchor=(0.14, 0.3)：在图形的左下角
ax.legend(("$sin(x)$", "$cos(x^2)$","$2cos(x+2)$"),bbox_to_anchor=(0.99, 0.3),title='legend')
ax.get_legend().get_title().set_color("red")
box = ax.get_position()
ax.set_position([box.x0, box.y0, box.width , box.height* 0.8])
#plt.tight_layout()    #以紧凑形式显示图片
#plt.savefig('fig1.png')   #保存图片
plt.show()

