# BannerView


### 第一步 添加依赖
在项目的build.gradle中
```
allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
  ```
  在module的build.gradle中
  ```
  dependencies {
	        compile 'com.github.Yuyang1257312385:BannerView:v1.0.0'
	}
  ```
 ### 第二步 在布局中添加控件,可以使用默认的，也可以自定义样式
 ```
 <?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    <!--命名空间-->
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <com.lyj.bannerlib.Banner.BannerView
        android:id="@+id/banner_view"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:layout_marginTop="50dp"
        <!--指示点的位置-->
        app:dotGrivity="right"
        <!--指示点的大小-->
        app:dotSize="4dp"
        <!--指示点的距离-->
        app:dotDistance="9dp"
        <!--选中的知识点的颜色-->
        app:dotIndicatorFocus="#00ff00"
        <!--未选中的指示点的颜色    -->
        app:dotIndicatorNormal="#ffffff"
        <!--底部的背景色-->
        app:bottomColor="#99e1e1e1"
        <!--高度的比例-->
        app:heightPercent="16"
        <!--宽度的比例-->
        app:widthPercent="25"
        <!--多久切换一张图片 单位毫秒-->
        app:intervalTime="3000"
        <!--切换的时候用多长时间 单位毫秒-->
        app:switchTime="500"
        >
    </com.lyj.bannerlib.Banner.BannerView>

</RelativeLayout>
 ```
 ### 第三步 代码中实现需要定制的功能
 
 首先你要添加项目中需要的权限和依赖，例子中用的是glide,需网络权限，这些根据自己的项目定制
 ```
 private void initData() {
        mBannerBeanList = new ArrayList<>();
        //bannerBean替换成项目中需要的javabean
        mBannerBeanList.add(new BannerBean("http://pic.baike.soso.com/p/20090711/20090711100446-226055609.jpg","军人"));
        mBannerBeanList.add(new BannerBean("http://pic.baike.soso.com/p/20090711/20090711101754-314944703.jpg","顺溜"));
        mBannerBeanList.add(new BannerBean("http://www.jikedaohang.com/images/first_code.jpg","第一行代码"));

        mBannerView.setAdapter(new BannerAdapter() {
            @Override
            public View getView(final int position,View convertView) {
                ImageView imageView = null;
                if(convertView != null){
                    imageView = (ImageView) convertView;
                    Log.d("BannerLog","reuse == " +imageView);
                }else {
                    imageView = new ImageView(MainActivity.this);
                    imageView.setScaleType(ImageView.ScaleType.FIT_XY);
                    Log.d("BannerLog","create == " +imageView);
                }
                BannerBean bannerBean = mBannerBeanList.get(position);
                Glide.with(MainActivity.this).load(bannerBean.getUrl()).into(imageView);
                //若需要点击，直接添加监听即可
                imageView.setOnClickListener(new View.OnClickListener() {
                    @Override
                    public void onClick(View v) {
                        Toast.makeText(MainActivity.this,"第"+(position+1)+"张",Toast.LENGTH_SHORT).show();
                    }
                });
                return imageView;
            }

            @Override
            public int getCount() {
                return mBannerBeanList.size();
            }

            //若不需要显示title的时候，不重写此方法
            @Override
            public String getDesc(int position) {
                return mBannerBeanList.get(position).getTitle();
            }
        });
        //开始滚动
        mBannerView.startRoll();

    }
    ```
    
    若有疑问，可联系qq:1257312385
 
 
  
