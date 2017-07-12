# 侧边滑动框架使用

* [引用](#引用)
* [使用](#使用)
* [参考地址](#参考地址)


## 引用
build.gradle中添加：
```
dependencies {
    compile('com.mikepenz:materialdrawer:5.9.1@aar') {
        transitive = true
    }
}
```


## 使用
使用DrawerBuilder来添加侧边滑动  
链式创建DrawerBuilder对象
* withActivity添加到当前页面
* withToolbar 添加当前页面toolBar
* withHeader 添加侧边栏头部
* addDrawerItems 添加侧边栏选项
* withOnDrawerItemClickListener 添加侧边栏选项的点击事件
* build 对象创建，最后调用

new DrawerBuilder()返回Drawer类型
通过drawer可以对侧边栏进行相应的调整，例如openDrawer，closeDrawer等。

代码如下：
```
PrimaryDrawerItem item1 = new PrimaryDrawerItem().withIdentifier(1).withName("Home").withIcon(R.mipmap.ic_launcher_round);
PrimaryDrawerItem item2 = new PrimaryDrawerItem().withIdentifier(2).withName("Permissions");

Drawer drawer = new DrawerBuilder()
        .withActivity(this)
        .withHeader(R.layout.util_drawer_hdr)
        .withToolbar(tb)
        .addDrawerItems(
                item1,
                item2
        )
        .withOnDrawerItemClickListener(new Drawer.OnDrawerItemClickListener() {
            @Override
            public boolean onItemClick(View view, int position, IDrawerItem drawerItem) {

                if (drawerItem != null) {
                    Fragment fragment = null;
                    FragmentManager fragmentManager = getFragmentManager();

                    switch ((int) drawerItem.getIdentifier()) {
                        case 1:
                            fragment = new MainFragment();
                            break;
                        case 2:
                            fragment = new SecondFragment();
                            break;
                    }

                    if (fragment != null) {
                        fragmentManager.beginTransaction().replace(R.id.frame_container, fragment).commit();
                    }

                    if (drawerItem instanceof Nameable) {
                        setTitle(((Nameable) drawerItem).getName().getText(getApplicationContext()));
                    }
                }

                return false;
            }
        })
        .withShowDrawerOnFirstLaunch(true)
        .withFireOnInitialOnClick(true)
        .withSavedInstance(savedInstanceState)
        .build();
drawer.openDrawer();
```


## 参考地址

[https://github.com/mikepenz/MaterialDrawer](https://github.com/mikepenz/MaterialDrawer "参考地址")