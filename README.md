# nomin https://github.com/dobrynya/nomin
Estudar alternativa para Groove 


## Estudar Forma de adicionar o número em cima do icone Android

public static void setBadge(Context context, int count) {
    String launcherClassName = getLauncherClassName(context);
    if (launcherClassName == null) {
        return;
    }
    Intent intent = new Intent("android.intent.action.BADGE_COUNT_UPDATE");
    intent.putExtra("badge_count", count);
    intent.putExtra("badge_count_package_name", context.getPackageName());
    intent.putExtra("badge_count_class_name", launcherClassName);
    context.sendBroadcast(intent);
}

public static String getLauncherClassName(Context context) {

    PackageManager pm = context.getPackageManager();

    Intent intent = new Intent(Intent.ACTION_MAIN);
    intent.addCategory(Intent.CATEGORY_LAUNCHER);

    List<ResolveInfo> resolveInfos = pm.queryIntentActivities(intent, 0);
    for (ResolveInfo resolveInfo : resolveInfos) {
        String pkgName = resolveInfo.activityInfo.applicationInfo.packageName;
        if (pkgName.equalsIgnoreCase(context.getPackageName())) {
            String className = resolveInfo.activityInfo.name;
            return className;
        }
    }
    return null;
}
