# Hide-LinearLayout-in-Android
Hide LinearLayout in Android

In xml :
```
 <LinearLayout
        android:id="@+id/ll_chat_log_search"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginLeft="15dp"
        android:layout_marginRight="15dp"
        android:layout_marginTop="70dp"
        android:orientation="horizontal"
        android:focusable="true"
        android:focusableInTouchMode="true">

        <EditText
            android:id="@+id/edt_calllog_search"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/rounded_edittext"
            android:padding="5dip"
            android:hint="Search..."/>
    </LinearLayout>
```
In Activity :

```
EditText callContactSearch;
LinearLayout navigationBottomContactLayout;

On onCreate :
navigationBottomContactLayout=(LinearLayout)this.findViewById(R.id.ll_bottom_callcontact);
callContactSearch = (EditText) findViewById(R.id.edt_calllog_search);
navigationBottomContactLayout.setVisibility(LinearLayout.VISIBLE);
callContactSearch.setOnFocusChangeListener(new View.OnFocusChangeListener() {
    @Override
    public void onFocusChange(View v, boolean hasFocus) {
        if (hasFocus){
            navigationBottomContactLayout.setVisibility(LinearLayout.INVISIBLE);
        } else {
            navigationBottomContactLayout.setVisibility(LinearLayout.VISIBLE);
        }
    }
});
 
 @Override
    public boolean dispatchTouchEvent(MotionEvent event) {
        if (event.getAction() == MotionEvent.ACTION_DOWN) {
            View v = getCurrentFocus();
            if ( v instanceof EditText) {
                Rect outRect = new Rect();
                v.getGlobalVisibleRect(outRect);
                if (!outRect.contains((int)event.getRawX(), (int)event.getRawY())) {
                    Log.d("focus", "touchevent");
                    v.clearFocus();
                    InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
                    imm.hideSoftInputFromWindow(v.getWindowToken(), 0);
                }
            }
        }
        return super.dispatchTouchEvent(event);
    }       
```
