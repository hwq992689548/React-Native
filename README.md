# React-Native
React-Native 调用原生方法

用xcode创建Object类 MHNSLog

##
MHNSLog.h文件： 

#import <Foundation/Foundation.h>

//引入两个头文件
#import <React/RCTBridge.h>
#import <React/RCTEventDispatcher.h>

@interface MHNSLog : NSObject<RCTBridgeModule>

@end

##
MHNSLog.m文件：

#import "MHNSLog.h"
@implementation MHNSLog


RCT_EXPORT_MODULE();

//自定义方法名：callNativeIosMethodParam 带一个参数

RCT_EXPORT_METHOD(callNativeIosMethodParam:(NSString *)name){
  NSLog(@"%@",name);
}

//自定义方法名：RCTResponseSenderBlock 带回调

RCT_EXPORT_METHOD(callNativeIosBack:(RCTResponseSenderBlock)callBack) {
  callBack(@[@"first",@"second"]);//注意：这里用的是数组返回
}

@end


//在js文件中先引入创建好的类：

var MyLog = require('react-native').NativeModules.MHNSLog  //MHNSLog为类名

在方法中调用：

MyLog.callNativeIosMethodParam('abc'); //调用原生自定义好的方法

//调用原生还有回调的方法

MyLog.callNativeIosBack((param1, param2) => {
  alert(param1);
  alert(param2);
});





