# GridView

lesson 84-85
1.GridView:类似于表格方式的视图,用网格方式排列视图，与矩阵类似，当屏幕上有很多元素（文字/图片或者其他元素）需要显示时，可以使用该            组件.还可以用于简单的图片排列视图.主要有以下属性：
  --numColumns:多少列，可以给一个具体的数字，也可以给一个常量auto_fit可以根据每一列的大小和屏幕的大小来自动匹配成多少列,但要配合              其他属性使用(columnWidth,horziontalSpacing);
  --columnWidth:列的宽度,单位dp;
  --verticalSpacing:两行之间的边距，单位dp;
  --horizontalSpacing:两列之间的边距，单位dp;
  --stretMode:缩放与列宽大小同步,设置以什么缩放模式去填充空间，如果是columnWidth则表示将多余的空隙均匀填充到列中;
  --gravity:设置GridView的位置，如center居中;
  
2.setScaleType属性:是控制图片如何调整大小或移动来匹配imageView的size,其相关参数设置如下：
  --CENTER/center:按图片的原来size居中显示，当图片长/宽超过View的长/宽，则截取图片的居中部分显示;
  --CENTER_CROP/centerCrop:按比例扩大图片的size居中显示，使得图片长宽等于或大于View的长宽;
  --CENTER_INSIDE/centerInside:将图片的内容完整居中显示，通过按比例缩小或原来的size使得图片长/宽等于或小于View的长/宽;
  --FIT_CENTER/fitCenter:把图片按比例扩大/缩小到View的宽度，居中显示;
  --FIT_END/fitEnd:把图片按比例扩大/缩小到View的宽，显示在View的下部分位置;
  --FIT_START/fitStart:把图片按比例扩大/缩小到View的宽度，显示在View的上部分位置;
  --FIT_XY/fitXY:把图片不按比例扩大/缩小到View的大小显示.
  
3.实例演示：在res->layout->编辑主要布局activity_main.xml:
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context="com.example.mackerlee.android_84.MainActivity">
  
      <GridView
          android:id="@+id/gridView84"
          android:layout_width="match_parent"
          android:layout_height="match_parent"
          android:numColumns="auto_fit"
          android:columnWidth="90dp"
          android:horizontalSpacing="10dp"
          android:verticalSpacing="10dp"
          android:stretchMode="columnWidth"
          android:gravity="center">
      </GridView>
  </RelativeLayout>
  
  在java->包名->MainActivity.java:
  package com.example.mackerlee.android_84;

  import android.content.Context;
  import android.support.v7.app.AppCompatActivity;
  import android.os.Bundle;
  import android.view.View;
  import android.view.ViewGroup;
  import android.widget.BaseAdapter;
  import android.widget.GridView;
  import android.widget.ImageView;
  
  public class MainActivity extends AppCompatActivity {
  
      private GridView gridView;
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
          gridView = (GridView)findViewById(R.id.gridView84);
          ImageAdapter imageAdapter = new ImageAdapter(this);
          //--用适配器动态填充View视图
          gridView.setAdapter(imageAdapter);
      }
  
      //--自定义适配器,定义静态内部类相当于外部类，上面不能直接调用了，要把上下文传递进来
      static class ImageAdapter extends BaseAdapter{
  
          //--图片数组，要显示的图片资源
          private Integer[] mThumbIds = {
                  R.drawable.s1, R.drawable.s2,
                  R.drawable.s3, R.drawable.s4,
                  R.drawable.s5, R.drawable.s6,
                  R.drawable.s7, R.drawable.s8,
                  R.drawable.s9,R.drawable.s10,
                  R.drawable.s1, R.drawable.s2,
                  R.drawable.s3, R.drawable.s4,
                  R.drawable.s5, R.drawable.s6,
                  R.drawable.s7, R.drawable.s8,
                  R.drawable.s9,R.drawable.s10
          };
  
          private Context mContext;
  
          //--构造方法将调用者的上下文环境传递进来，很多布局加载时都要用到上下文
          public ImageAdapter(Context c) {
              mContext = c;
          }
  
          @Override
          public int getCount() {
              return mThumbIds.length;
          }
  
          @Override
          public Object getItem(int position) {
              return null;
          }
  
          @Override
          public long getItemId(int position) {
              return position;
          }
  
          @Override
          public View getView(int position, View convertView, ViewGroup parent) {
              ImageView imageView;
              if (convertView == null) {  // if it's not recycled, initialize some attributes
                  imageView = new ImageView(mContext);
                  //--设置imageView的宽高，因为要放到GridView里面，用GridView.LayoutParams
                  imageView.setLayoutParams(new GridView.LayoutParams(285, 285));
                  //--设置图片的截取拉伸方式：大了截取，小了拉伸
                  imageView.setScaleType(ImageView.ScaleType.CENTER_CROP);
                  //--设置边距
                  imageView.setPadding(8, 8, 8, 8);
              } else {
                  imageView = (ImageView) convertView;
              }
              //--设置图片
              imageView.setImageResource(mThumbIds[position]);
              return imageView;
          }
      }
  }


