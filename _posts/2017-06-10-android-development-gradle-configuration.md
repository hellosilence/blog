---
layout:     post
title:      "Android 开发 Gradle 配置"
date:       2017-06-10 12:00:00
author:     "Samuel"
tags:
    - Android
    - Gradle
---
# Android 开发 Gradle 配置
Android 开发中经常需要打包测试，配置好 Gradle 后可以尽可能自动化，先看代码。

````gradle
def releaseTime() {
    return new Date().format("yyyyMMddHHmm")
}

def cmd = 'git rev-list HEAD --count'
def initVersionName = '1.0.0'
def gitVersionCode = cmd.execute().text.trim().toInteger()
def gitVersionName = initVersionName + '.' + gitVersionCode


android {
    signingConfigs {
        releaseconfig {
            keyAlias 'abc'
            keyPassword 'abc123456'
            storeFile file('./abc.jks')
            storePassword 'abc123456'
        }
    }
    compileSdkVersion 25
    buildToolsVersion "25.0.1"
    defaultConfig {
        applicationId "com.xyz.abc"
        minSdkVersion 16
        targetSdkVersion 22
        versionCode gitVersionCode
        versionName gitVersionName
        multiDexEnabled true
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }

    productFlavors {
        Xiaomi {}
        Baidu {}
        Ali {}
        Yingyongbao {}
        Market360 {}
        Huawei {}
    }

    productFlavors.all {
        flavor ->
            flavor.manifestPlaceholders = [UMENG_CHANNEL_VALUE: name]
    }

    buildTypes {
        debug {

            versionNameSuffix "-debug"
            minifyEnabled false
            zipAlignEnabled false
            shrinkResources false
            signingConfig signingConfigs.debug
        }

        release {
            minifyEnabled false
            signingConfig signingConfigs.releaseconfig
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
            
            zipAlignEnabled true
            // 移除无用的resource文件
            shrinkResources false

            applicationVariants.all { variant ->

                variant.outputs.each { output ->
                    def outputFile = output.outputFile
                    if (outputFile != null && outputFile.name.endsWith('.apk')) {
                        def fileName = "abc-${variant.buildType.name}-v${defaultConfig.versionName}-${variant.productFlavors[0].name}-${releaseTime()}.apk"
                        output.outputFile = new File(outputFile.parent, fileName)
                    }
                }
            }

        }
    }

}
```

先定义了几个变量：`releaseTime`代表时间，`cmd` 代表 git 提交次数，加上友盟的多渠道打包，最后生成的 apk 就会像这样：`abc-release-v1.0.0.18-Yingyongbao-201603161510.apk`

再配合蒲公英和 Jenkins 自动化部署，非常方便项目打包和测试。



