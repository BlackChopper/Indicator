# Indicator
[![](https://img.shields.io/badge/platform-android-orange.svg)](https://github.com/hacknife) [![](https://img.shields.io/badge/language-java-yellow.svg)](https://github.com/hacknife) [![](https://img.shields.io/badge/JCenter-1.0.3-brightgreen.svg)](http://jcenter.bintray.com/com/hacknife/indicator/) [![](https://img.shields.io/badge/build-passing-brightgreen.svg)](https://github.com/hacknife) [![](https://img.shields.io/badge/license-MIT-green.svg)](https://github.com/hacknife) [![](https://img.shields.io/badge/api-19+-green.svg)](https://github.com/hacknife)<br/><br/>

![magicindicaotor.gif](https://github.com/hacknife/Indicator/blob/master/magicindicator.gif)

# Usage

Simple steps, you can integrate **MagicIndicator**:

1. checkout out **MagicIndicator**, which contains source code and demo
2. import module **magicindicator** and add dependency:

  ```groovy
  compile project(':magicindicator')
  ```
  
  **or**
  
  ```groovy

  dependencies {
      ...
      compile 'com.hacknife:indicator:1.0.3'
  }
  ```
  
3. add **MagicIndicator** to your layout xml:

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:orientation="vertical"
      tools:context="net.lucode.hackware.magicindicatordemo.MainActivity">
  
      <net.lucode.hackware.magicindicator.MagicIndicator
          android:id="@+id/magic_indicator"
          android:layout_width="match_parent"
          android:layout_height="40dp" />
  
      <android.support.v4.view.ViewPager
          android:id="@+id/view_pager"
          android:layout_width="match_parent"
          android:layout_height="0dp"
          android:layout_weight="1" />
  
  </LinearLayout>
  ```

4. find **MagicIndicator** through code, initialize it:

  ```java
  MagicIndicator magicIndicator = (MagicIndicator) findViewById(R.id.magic_indicator);
  CommonNavigator commonNavigator = new CommonNavigator(this);
  commonNavigator.setAdapter(new CommonNavigatorAdapter() {
  
      @Override
      public int getCount() {
          return mTitleDataList == null ? 0 : mTitleDataList.size();
      }
  
      @Override
      public IPagerTitleView getTitleView(Context context, final int index) {
          ColorTransitionPagerTitleView colorTransitionPagerTitleView = new ColorTransitionPagerTitleView(context);
          colorTransitionPagerTitleView.setNormalColor(Color.GRAY);
          colorTransitionPagerTitleView.setSelectedColor(Color.BLACK);
          colorTransitionPagerTitleView.setText(mTitleDataList.get(index));
          colorTransitionPagerTitleView.setOnClickListener(new View.OnClickListener() {
              @Override
              public void onClick(View view) {
                  mViewPager.setCurrentItem(index);
              }
          });
          return colorTransitionPagerTitleView;
      }
  
      @Override
      public IPagerIndicator getIndicator(Context context) {
          LinePagerIndicator indicator = new LinePagerIndicator(context);
          indicator.setMode(LinePagerIndicator.MODE_WRAP_CONTENT);
          return indicator;
      }
  });
  magicIndicator.setNavigator(commonNavigator);
  ```
  
5. work with ViewPager:

  ```java
  ViewPagerHelper.bind(magicIndicator, mViewPager);
  ```

  **or**
  
  work with Fragment Container(switch Fragment by hide()、show()):
  ```java
  mFramentContainerHelper = new FragmentContainerHelper(magicIndicator);
  
  // ...
  
  mFragmentContainerHelper.handlePageSelected(pageIndex);   // invoke when switch Fragment
  ```
  
# Extend

**MagicIndicator** can be easily extended:

1. implement **IPagerTitleView** to customize tab:

  ```java
  public class MyPagerTitleView extends View implements IPagerTitleView {
  
      public MyPagerTitleView(Context context) {
          super(context);
      }
  
      @Override
      public void onLeave(int index, int totalCount, float leavePercent, boolean leftToRight) {
      }
  
      @Override
      public void onEnter(int index, int totalCount, float enterPercent, boolean leftToRight) {
      }
  
      @Override
      public void onSelected(int index, int totalCount) {
      }
  
      @Override
      public void onDeselected(int index, int totalCount) {
      }
  }
  ```

2. implement **IPagerIndicator** to customize indicator:

  ```java
  public class MyPagerIndicator extends View implements IPagerIndicator {
  
      public MyPagerIndicator(Context context) {
          super(context);
      }
  
      @Override
      public void onPageSelected(int position) {
      }
  
      @Override
      public void onPageScrolled(int position, float positionOffset, int positionOffsetPixels) {
      }
  
      @Override
      public void onPageScrollStateChanged(int state) {
      }
  
      @Override
      public void onPositionDataProvide(List<PositionData> dataList) {
      }
  }
  ```

3. use **CommonPagerTitleView** to load custom layout xml.

Now, enjoy yourself!

See extensions in [*app/src/main/java/net/lucode/hackware/magicindicatordemo/ext*](https://github.com/hackware1993/MagicIndicator/tree/master/app/src/main/java/net/lucode/hackware/magicindicatordemo/ext)，more extensions adding...

# Who developed?

hackware1993@gmail.com

cfb1993@163.com

Q&A <a target="_blank" href="http://shang.qq.com/wpa/qunwpa?idkey=7ac5bef0321c7afa7e9fc4e94175fa36f413e3330c82e828b1743274af8a64d7"><img border="0" src="http://pub.idqqimg.com/wpa/images/group.png" alt="MagicIndicator交流群" title="MagicIndicator交流群"></a>

An intermittent perfectionist.

Visit [My Blog](http://hackware.lucode.net) for more articles about MagicIndicator.

# License

  ```
  MIT License
  
  Copyright (c) 2016 hackware1993
  
  Permission is hereby granted, free of charge, to any person obtaining a copy
  of this software and associated documentation files (the "Software"), to deal
  in the Software without restriction, including without limitation the rights
  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
  copies of the Software, and to permit persons to whom the Software is
  furnished to do so, subject to the following conditions:
  
  The above copyright notice and this permission notice shall be included in all
  copies or substantial portions of the Software.
  
  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
  SOFTWARE.
  ```

# More

Have seen here, give a star?（都看到这儿了，何不给个...，哎，别走啊，star还没...）
