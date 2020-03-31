---
title: HexoEditor之快捷键教程
date: 2020-03-31 20:07:21
tags:

---

标题  
代码块  
粗体  
斜体  
删除线  
链接  
图片  
引用  
有序列表  
无序列表  
段落  
表格  
<!--more-->
**标题**
> Key:
> 升级：Ctrl - \[
> 降级：Ctrl - \]

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
####### 不支持六级以上标题
```
*效果*


# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
####### 不支持六级以上标题

**代码块**
> Key:
> 无

```java
<Button
    android:id="@+id/test_btn"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_below="@id/captcha_layout"
    android:text="隐藏"/>
<!--测试child visibility属性-->
<LinearLayout
    android:id="@+id/test_layout"
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_below="@id/test_btn"
    android:orientation="vertical"
    android:visibility="gone">
    <TextView
        android:id="@+id/test_child"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="测试child visibility属性"/>
</LinearLayout>

boolean display = false;
private void testChildVisibility() {
    final Button btn = findViewById(R.id.test_btn);
    final LinearLayout layout = findViewById(R.id.test_layout);
    final TextView child = findViewById(R.id.test_child);

    btn.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View v) {
            display = !display;
            btn.setText(display ? "显示" : "隐藏");
            layout.setVisibility(display ? View.VISIBLE : View.GONE);
            Log.e("dawei", "child is display == " + (child.getVisibility() == View.VISIBLE));
        }
    });
}
```

**粗体**
> Key:
> Ctrl - B

```
**粗体**
```
*效果*
**粗体**

**斜体**
> Key:
> Ctrl - I

```
*斜体*
```
*效果*
*斜体*

**删除线**
> Key:
> Ctrl - D
> 删除当前行，已空格为分隔

```
~~我是被删除的内容1~~ ~~我是被删除的内容2~~
```
*效果*
~~我是被删除的内容1~~ ~~我是被删除的内容2~~

**链接**
> Key:
> Ctrl - U

```
[HexoEditor开源地址](https://github.com/zhuzhuyule/HexoEditor)
```
*效果*
[HexoEditor开源地址](https://github.com/zhuzhuyule/HexoEditor)

**图片**
> Key:
> Ctrl - Alt - U

```
![百度](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_ca79a146.png)
```
*效果*
![百度](https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/superman/img/logo_top_ca79a146.png)

**引用**
> Key:
> 增加：Ctrl - =
> 减少：Ctrl - -

```
> 我是一条引用语句
>> 我是一条引用语句
>>> 我是一条引用语句
```
*效果*
> 我是一条引用语句
>> 我是一条引用语句
>>> 我是一条引用语句

**有序列表(非正式)**
> Key:
> 切换有序列表：Ctrl - Alt - L
> 在HexoEditor有序列表里，只要列表第1项为数字(0或任意正数开头)符号，无论后面项目是任意数字符号|横线-符号|星\*符号，均以1开头顺序的有序列表

```
0. 发都发
- 发
1. dfa
* dfaf
```
*效果*
0. 发都发
- 发
1. dfa
* dfaf

**有序列表（正式）**
> Key:
> 切换有序列表：Ctrl - Alt - L

```
1. 看过
2. 打了
3. 房东
4. 赶快来
5. 力嘎
```
*效果*

1. 看过
2. 打了
3. 房东
4. 赶快来
5. 力嘎

**段落**
```
普通段落文字-普通段落文字 - 
```
普通段落文字-普通段落文字 - 

**无序列表**
> Key:
> 切换无序列表：Ctrl - L
> 横线- 星号* 均可

```
* A
* B
* C
* D
* E
* F
```
```
- A
- B
- C
- D
- E
- F
```
*效果*
* A
* B
* C
* D
* E
* F

**表格**
> Key:
> 添加表格：Ctrl - T
> 注意：表格表头行前面需要有换行，否则渲染失效
> 表格行高随内容自动展开
> 格式化表格：Alt - F
> 将不整齐的md表格内容，格式化为整齐的表格形式

```
| Head1 | Head2 | Head3  |
| :---: | :---: | :----: |
| row1  | 中国  | 亚洲   |
| row2  | 英国  | 欧洲   |
| row3  | 美国  | 北美洲 |

| Head1 | Head2 | Head3                               |
| :---: | :---: | :---------------------------------: |
| row1  | 中国  | 亚洲                                |
| row2  | 英国  | 欧洲-欧洲-欧洲-欧洲-欧洲-欧洲-欧洲- |
| row3  | 美国  | 北美洲                              |
```
*效果*

| Head1 | Head2 | Head3  |
| :---: | :---: | :----: |
| row1  | 中国  | 亚洲   |
| row2  | 英国  | 欧洲   |
| row3  | 美国  | 北美洲 |

| Head1 | Head2   | Head3                               |
| :---: | :-----: | :---------------------------------: |
| row1  | 中国    | 亚洲                                |
| row2  | 英   国 | 欧洲-欧洲-欧洲-欧洲-欧洲-欧洲-欧洲- |
| row3  | 美国    | 北美洲   