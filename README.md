# LSposed-
对Hyper OS 3系统进行修改
// 核心Hook代码，修改状态栏运营商文字
class MainHook : IXposedHookLoadPackage {
    override fun handleLoadPackage(lpparam: XC_LoadPackage.LoadPackageParam) {
        // 只Hook系统框架进程
        if (lpparam.packageName == "android") {
            // 找到系统状态栏相关类
            XposedHelpers.findAndHookMethod(
                "com.android.systemui.statusbar.policy.CarrierTextController",
                lpparam.classLoader,
                "getCarrierText",
                object : XC_MethodHook() {
                    // 替换返回值，修改状态栏文字
                    override fun afterHookedMethod(param: MethodHookParam) {
                        param.result = "Hyper OS 定制版"
                    }
                }
            )
        }
    }
}
