# Android ![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)
## Circular shape (mostly for background)
Required files:
- <a href="circle.xml" target="_blank">drawable/circle.xml</a>

Usage:
```
<RelativeLayout
            android:layout_gravity="center_vertical"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">

            <ImageView
                android:background="@drawable/call_background_circle"
                android:layout_width="48dp"
                android:padding="5dp"
                android:src="@drawable/ic_action_phone_in_talk"
                android:layout_height="48dp"/>


</RelativeLayout>
```
Output: <br />
![](img/circle-1.png)

## Programmatically change colors in StateListDrawable
Ref: [Stack Overflow- How can I change colors in my StateListDrawable?](https://stackoverflow.com/questions/19864337/how-can-i-change-colors-in-my-statelistdrawable) <br />
button_main.xml (main layout)
```
<RelativeLayout

            android:layout_marginEnd="10dp"
            android:layout_gravity="center_vertical"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">

            <ImageView
                android:id="@+id/make_call"
                android:background="@drawable/call_background_circle"
                android:layout_width="48dp"
                android:padding="5dp"
                android:src="@drawable/ic_action_phone_in_talk"
                android:layout_height="48dp"/>


        </RelativeLayout>
```
background_circle.xml (drawable)
```
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <shape android:shape="oval">
            <solid android:color="#00FF00"/> # this is what we want to change
            <size

                android:height="120dp"
                android:width="120dp"/>
        </shape>
    </item>

</selector>
```
Code for changing background color
```
ImageView callImageView = (ImageView) convertView.findViewById(R.id.make_call);
        StateListDrawable backgroundDrawable = (StateListDrawable) callImageView.getBackground();
        DrawableContainer.DrawableContainerState drawableContainerState = (DrawableContainer.DrawableContainerState) backgroundDrawable.getConstantState();
        Drawable[] children = drawableContainerState.getChildren();
        GradientDrawable firstItem =  (GradientDrawable) children[0];
        firstItem.getDrawable(0);
        firstItem.setColor(magnitudeColor); // magnitudeColor is int 
```