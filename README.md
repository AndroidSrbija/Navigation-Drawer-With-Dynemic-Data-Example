# Navigation Drawer With Dynemic Data Example

###Add dependencies

```xml
compile 'com.android.support:recyclerview-v7:23.1.0'
```

###Add DrawerLayout to main.xml

```xml
<android.support.v4.widget.DrawerLayout
        android:id="@+id/drawerLayout"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        tools:context="com.example.android_srbija.navigationdrawerwithdynemicdataexample.MainActivity">
    </FrameLayout>
    <fragment
        android:id="@+id/navigation_drawer_fragment"
        android:name="com.example.android_srbija.navigationdrawerwithdynemicdataexample.NavigationDrawerFragment"
        android:layout_width="@dimen/navigationDrawerWidth"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        app:layout="@layout/fragment_navigation_drawer"
        tools:layout="@layout/fragment_navigation_drawer"/>
</android.support.v4.widget.DrawerLayout>
```

### Create Fragment for navigation drawer and set it up

```java
public void setUp(DrawerLayout drawerLayout, Toolbar toolbar) {       
   RecyclerView mRecyclerView = (RecyclerView) getActivity().findViewById(R.id.recycler_view);
   mRecyclerView.setHasFixedSize(true);
   LinearLayoutManager mLayoutManager = new LinearLayoutManager(getContext());
   mRecyclerView.setLayoutManager(mLayoutManager);
   ArrayList<String> data = new ArrayList<>();
   for (int i = 0; i < 10; i++) {
       data.add("Android Srbija item " + i + 1);
   }
   RecyclerViewAdapter mAdapter = new RecyclerViewAdapter(data);
   mRecyclerView.setAdapter(mAdapter);
   mDrawerLayout = drawerLayout;
   mDrawerToggle = new ActionBarDrawerToggle(getActivity(), drawerLayout, toolbar, R.string.drawer_open, R.string.drawer_close) {
       @Override
       public void onDrawerOpened(View drawerView) {
           super.onDrawerOpened(drawerView);
           getActivity().invalidateOptionsMenu();
       }
       @Override
       public void onDrawerClosed(View drawerView) {
           super.onDrawerClosed(drawerView);
           getActivity().invalidateOptionsMenu();
       }
   };
   mDrawerLayout.setDrawerListener(mDrawerToggle);
   mDrawerLayout.post(new Runnable() {
       @Override
       public void run() {
           mDrawerToggle.syncState();
       }
   });
}
```

### Create xml file for recycler view item

### Set up RecyclerView Adapter
