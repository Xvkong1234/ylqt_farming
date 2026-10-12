# 妖恋奇谭 · 刷本推荐

## 网页版使用
`index.html` 为单文件应用(数据已内嵌),双击用任意手机/电脑浏览器打开即可,无需联网。

## 功能说明
1. **多选角色**:点击角色名片勾选/取消,可任意组合,支持全选/清空。
2. **素材汇总**:自动合并所选角色的进化材料需求(Excel 中冗余的 0 值已剔除,只取「进化材料查询表」的有效数据)。
3. **合成展开**:只能通过天地熔炉合成获得的素材(如混元丹、筑基丹、完美XX石等)会自动递归展开为合成材料,并计入总需求(黄色标签 = 合成展开来的素材)。
4. **副本推荐**:按"覆盖需求素材数"从高到低排序——优先推荐一次能刷到多种需求素材的副本;含 🚩 标记的素材**只能通过委托探索获得**,对应副本带「含远征专属素材」徽章并优先排列。
5. **排除项**:
   - 神秘之地系列(每日限次)不参与推荐;
   - 天地熔炉(合成系统)不参与推荐;
   - 龙王宝窟、黑砖窑、百草植物园、矿盐山、明光冶炼厂、狩猎场、早稻田(时产建筑)单独放在最后一节,优先度最低,仅列出可产出的需求素材。

## 打包为 APK(安卓)

### 方式一:Capacitor(推荐,需 Node.js + Android Studio)
```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init 妖恋刷本推荐 com.yaolian.farm --web-dir www
mkdir www
copy index.html www\
npx cap add android
npx cap sync
```
然后用 Android Studio 打开 `android` 项目 → Build → Build APK(s)。

### 方式二:直接套 WebView 壳(最简单)
新建一个 Android 项目,`MainActivity` 中放一个 WebView 加载 `file:///android_asset/index.html`,把 `index.html` 拷入 `app/src/main/assets/` 即可。关键代码:
```java
WebView wv = new WebView(this);
wv.getSettings().setJavaScriptEnabled(true);
setContentView(wv);
wv.loadUrl("file:///android_asset/index.html");
```

### 方式三:在线免编译
把 index.html 上传到任意静态托管(如 GitHub Pages),再用 "Web into APP" 类在线打包服务生成 APK。

## 数据更新
Excel 表更新后,重新运行根目录 `_dump.py` 与 `_inject.py` 可重新生成并嵌入数据(需 Python + openpyxl)。
