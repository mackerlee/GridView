# GridView

lesson 84
1.GridView:类似于表格方式的视图,用网格方式排列视图，与矩阵类似，当屏幕上有很多元素（文字/图片或者其他元素）需要显示时，可以使用该            组件.还可以用于简单的图片排列视图.主要有以下属性：
  --numColumns:多少列，可以给一个具体的数字，也可以给一个常量auto_fit可以根据每一列的大小和屏幕的大小来自动匹配成多少列,但要配合              其他属性使用(columnWidth,horziontalSpacing);
  --columnWidth:列的宽度,单位dp;
  --verticalSpacing:两行之间的边距，单位dp;
  --horizontalSpacing:两列之间的边距，单位dp;
  --stretMode:缩放与列宽大小同步,设置以什么缩放模式去填充空间，如果是columnWidth则表示将多余的空隙均匀填充到列中;
  --gravity:设置GridView的位置，如center居中;
