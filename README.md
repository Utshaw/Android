# Android ![Contributions welcome](https://img.shields.io/badge/contributions-welcome-orange.svg)
## Overlay loading/progress dialog
![](https://camo.githubusercontent.com/d8108413298d70047f52cff9ac05603a5fd51988/687474703a2f2f332e62702e626c6f6773706f742e636f6d2f2d6c3155765657694d5341672f564c61355a6657346444492f41414141414141414e54632f7273576f755f71623042632f733332302f593648615453772e676966) <br />
Link: https://github.com/dybarsky/spots-dialog

## Bitmap from filepath
Ref: https://stackoverflow.com/questions/16804404/create-a-bitmap-drawable-from-file-path
<br /> Code:
```
String filepath = "/storage/emulated/0/DCIM/Screenshots/Screenshot_20200516-164037_Some_App.jpg";
Bitmap bitmap = BitmapFactory.decodeFile(filePath);
```


## Adding svg file(s) in Android Studio
Ref: https://stackoverflow.com/questions/30923205/easiest-way-to-use-svg-in-android

## Reverse ListView (like in messenger)
Ref: https://stackoverflow.com/questions/16318034/android-reverse-listview-as-message-display
```
android:stackFromBottom="true"
android:transcriptMode="normal"
```

## Add header in ListView
Ref: https://android--code.blogspot.com/2015/08/android-listview-header.html
```
// Get reference of widgets from XML layout
final ListView lv = (ListView) findViewById(R.id.lv);

// Initializing a new String Array
String[] fruits = new String[] {
        "Abiu",
        "Batuan",
        "Black Mulberry",
        "Cape Gooseberry",
        "Desert banana",
        "Eastern May Hawthorn",
        "Fibrous Satinash",
        "Gooseberry",
        "Hairless rambutan",
        "Illawarra Plum",
        "Jelly Palm"
};

// Create a List from String Array elements
final List<String> fruits_list = new ArrayList<String>(Arrays.asList(fruits));

// Create an ArrayAdapter from List
final ArrayAdapter<String> arrayAdapter = new ArrayAdapter<String>
        (this, android.R.layout.simple_list_item_1, fruits_list);

// Add a header to the ListView
LayoutInflater inflater = getLayoutInflater();
ViewGroup header = (ViewGroup)inflater.inflate(R.layout.listview_header,lv,false);
lv.addHeaderView(header);

// DataBind ListView with items from ArrayAdapter
lv.setAdapter(arrayAdapter);
```


## Image click to preview in bigger size
Ref: https://stackoverflow.com/questions/12089485/how-to-show-a-fullsize-image-after-clicking-the-thumbnail-image-in-android#answer-12089733
<br /> **Better approach is mentioned after this code**
<br /> My code:
<br /> Method inside the adapter class:
```
private void showImagePreview(String imageLink) {

    final Dialog nagDialog = new Dialog(context,android.R.style.Theme_Black_NoTitleBar_Fullscreen);
    nagDialog.requestWindowFeature(Window.FEATURE_NO_TITLE);
    nagDialog.setCancelable(false);
    nagDialog.setContentView(R.layout.preview_image);
    Button btnClose = (Button)nagDialog.findViewById(R.id.btnIvClose);
    final ImageView ivPreview = (ImageView)nagDialog.findViewById(R.id.iv_preview_image);


    Glide.with(context)
            .load(imageLink)
            .transition(DrawableTransitionOptions.withCrossFade())
            .into(ivPreview);

    btnClose.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View arg0) {

            nagDialog.dismiss();
        }
    });
    nagDialog.show();
}

```
<br /> preview_image.xml:
```
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

<ImageView
    android:layout_width="match_parent"
    android:layout_height="fill_parent"
    android:id="@+id/iv_preview_image" />


<Button
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:background="@drawable/ic_close_white_24dp"
    android:id="@+id/btnIvClose"
    android:layout_alignParentRight="true"
    android:layout_alignParentTop="true" />

</RelativeLayout>
```
<br /> Inside getView of adapter:
```
ivImageAttachment.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {

        showImagePreview(comment.getCommmentAttachmentLink());
    }
});
```
**Important: better approach is using stfalcon library** <br />
Link: https://github.com/stfalcon-studio/StfalconImageViewer <br />
- [ImageView with fullscreen zoom using stfalcon](https://stackoverflow.com/questions/47510992/imageview-with-fullscreen-zoom#answer-53849943)
- [Usage of StfalconImageViewer in Java only Project](https://github.com/stfalcon-studio/StfalconImageViewer/issues/4)


## Glide Image loading from low res to full res transition
Ref: https://medium.com/@elye.project/glide-image-loader-the-basic-798db220bb44


## Fit multiple image size into list item view (ImageView)
Ref: https://stackoverflow.com/questions/8232608/fit-image-into-imageview-keep-aspect-ratio-and-then-resize-imageview-to-image-d#answer-20488327
<br /> List item view:
```
<ImageView
    android:scaleType="centerInside"
    android:adjustViewBounds="true"
    android:id="@+id/ivImageAttachment"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="10dp"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:maxWidth="250dp"
    android:maxHeight="250dp"/>
```
Load using Picasso from adapter:
```
Picasso.with(context).load(comment.getCommmentAttachmentLink()).into(ivImageAttachment);
```

## ListView onItemClickListener not working
Ref: https://stackoverflow.com/questions/5551042/onitemclicklistener-not-working-in-listview
<br />
Add this on the child item element's container view
```
android:focusable="false"
android:descendantFocusability="blocksDescendants"
```

## Hide keyboard programmatically
Ref: https://stackoverflow.com/questions/1109022/close-hide-android-soft-keyboard
```
public void hideKeyboard() {
try {
    InputMethodManager inputmanager = (InputMethodManager)context.getSystemService(Context.INPUT_METHOD_SERVICE);
    if (inputmanager != null) {
        inputmanager.hideSoftInputFromWindow(context.getCurrentFocus().getWindowToken(), 0);
    }
} catch (Exception var2) {
}

}
```

## OnClickListener not working
Reasons:
- The view you are trying to click may have a "transparent" view above it
- This type of scenario will arise when ListView is defined after Empty View. You need to define listview first then empty view for letting the empty view to handle the click event.


## Button click ripple effect on TextView/ImageView
Ref: https://stackoverflow.com/questions/33477025/how-to-set-a-ripple-effect-on-textview-or-imageview-on-android
<br />**For rectangle ripple effect**
```
android:background="?attr/selectableItemBackground"
android:clickable="true"
```
<br />**For circular ripple effect(did't work properly in my usage)**
```
android:background="?attr/selectableItemBackgroundBorderless"
android:clickable="true"
```

## Comment popup like Facebook
Ref: https://stackoverflow.com/questions/26795263/how-to-build-a-facebook-comment-like-popup-in-android

## ListView scrolls to bottom when keyboard opens
Ref (not working for me though): https://stackoverflow.com/questions/3606530/listview-scroll-to-the-end-of-the-list-after-updating-the-list
<br />
Used this (works)

For ListView:
```
android:transcriptMode="alwaysScroll"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:layout_above="@id/comment_section"
```
For comment section:
```
<LinearLayout

    android:id="@+id/comment_section"
    android:layout_alignParentBottom="true"
    android:layout_marginBottom="5dp"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <include
        android:id="@+id/llCommentPreview"
        layout="@layout/comment_image_preview" />

    <include
        android:id="@+id/llCommentSendLayout"
        layout="@layout/comment_send_box" />

</LinearLayout>
```

## ListView inside ScrollView showing one item only
Ref: [StackOverflow](https://stackoverflow.com/questions/18411494/android-listview-show-only-one-item#answer-45629226)
```
public class NonScrollListView extends ListView {

public NonScrollListView(Context context) {
    super(context);
}
public NonScrollListView(Context context, AttributeSet attrs) {
    super(context, attrs);
}
public NonScrollListView(Context context, AttributeSet attrs, int defStyle) {
    super(context, attrs, defStyle);
}
@Override
public void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        int heightMeasureSpec_custom = MeasureSpec.makeMeasureSpec(
                Integer.MAX_VALUE >> 2, MeasureSpec.AT_MOST);
        super.onMeasure(widthMeasureSpec, heightMeasureSpec_custom);
        ViewGroup.LayoutParams params = getLayoutParams();
        params.height = getMeasuredHeight();    
}

}
```
```
<xx.xx.NonScrollListView
    android:id="@+id/lv_nonscroll_list"
    android:layout_width="match_parent"
    android:layout_height="wrap_content" >
</xx.xx.NonScrollListView>
```



## RelativeLayout inside ScrollView not taking full height
Ref: https://stackoverflow.com/questions/10962602/cant-resize-a-relativelayout-inside-a-scrollview-to-fill-the-whole-screen
<br />
`android:fillViewport="true"`
```
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/scrollView1"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
         android:fillViewport="true" >

```
## TextView ending with ellipsize
Three lines are important:
```
android:maxLines="1"
android:ellipsize="end"
android:maxEms="15"
```
Example:
```
<TextView
    android:maxLines="1"
    android:ellipsize="end"
    android:maxEms="15"
    android:id="@+id/problemDesc"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    tools:text="Problem desc"
    android:textColor="#000000"
    android:textSize="14sp"
    android:typeface="sans" />
```

## ListView nested inside ScrollView showing only one item
Call this method with the listview as parameter after setting the adapter. 
```
public static void setListViewHeightBasedOnChildren(ListView listView) {
        BaseAdapter listAdapter = (BaseAdapter) listView.getAdapter();
        if (listAdapter == null) {
            // pre-condition
            return;
        }

        int totalHeight = 0;
        Log.d("UIU-965", listAdapter.getCount() + "");
        for (int i = 0; i < listAdapter.getCount(); i++) {
            View listItem = listAdapter.getView(i, null, listView);
            listItem.measure(0, 0);
            totalHeight += listItem.getMeasuredHeight();
        }

        ViewGroup.LayoutParams params = listView.getLayoutParams();
        params.height = totalHeight + (listView.getDividerHeight() * (listAdapter.getCount() - 1));
        listView.setLayoutParams(params);
        listView.requestLayout();
    }
```

## ALertDialog with curved edge
![](img/feedback.png)
XML file:
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@drawable/cornered_white_bg"
    android:orientation="vertical"
    android:padding="10dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_marginStart="5dp"
        android:text="Give Feedback"
        android:textColor="@color/black"
        android:textSize="18sp"
        android:textStyle="bold" />



    <TextView
        android:id="@+id/warning"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_marginStart="5dp"
        android:layout_marginTop="25dp"
        android:textColor="@color/ABpos"
        android:textSize="12sp"
        android:textStyle="normal" />

    <android.support.v7.widget.AppCompatEditText
        android:id="@+id/et_feedback"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginStart="5dp"
        android:layout_marginEnd="10dp"
        android:layout_marginBottom="10dp"
        android:gravity="bottom"
        android:hint="Write something here......."
        android:padding="12dp"
        android:singleLine="true"
        android:textSize="14sp"
        app:backgroundTint="@color/colorPrimary" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:layout_marginBottom="12dp"
        android:orientation="horizontal">

        <TextView
            android:id="@+id/btn_feedback"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginStart="5dp"
            android:layout_weight="1"
            android:text="SUBMIT"
            android:textColor="@color/colorPrimary"
            android:textSize="14sp"
            android:textStyle="bold" />

        <TextView
            android:id="@+id/btnCancel"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginStart="5dp"
            android:layout_marginEnd="5dp"
            android:text="CANCEL"
            android:textColor="@color/colorPrimary"
            android:textSize="14sp"
            android:textStyle="bold" />
    </LinearLayout>
</LinearLayout>

```
Activity.java
```
AlertDialog.Builder mBuilder = new AlertDialog.Builder(MainActivity.this);
View mView = getLayoutInflater().inflate(R.layout.feedback_dialog, null);
mBuilder.setView(mView);
final AlertDialog dialog = mBuilder.create();
dialog.getWindow().setBackgroundDrawable(new ColorDrawable(Color.TRANSPARENT));
dialog.show();
```


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

## Programmatically change colors of StateListDrawable
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

## Properly showing CardView inside a ListView
ListView code fragment
```
<ListView
    android:id="@+id/list"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:divider="@android:color/transparent"
    android:dividerHeight="10.0sp"/>
```
List item
```
<android.support.v7.widget.CardView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    xmlns:card_view="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    card_view:cardBackgroundColor="#E6E6E6"
    card_view:cardCornerRadius="8dp"
    card_view:cardElevation="8dp">

<LinearLayout
    android:background="#F3EEEE"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">

            .....
            .....
            .....
</LinearLayout>
</android.support.v7.widget.CardView>
```


## Volley
Latest release: https://github.com/google/volley/releases <br />

## Awesome Android Resource
- [awesome-android-ui](https://github.com/wasabeef/awesome-android-ui)
