#### 统一异常处理@ExceptionHandler

   [本文链接](https://blog.csdn.net/hzz_321/article/details/81280979)
   
   在开发过程中，我们会遇到很多的异常，比方说：500，如果直接返回给用户，则显得很low，此时我们就需要捕获异常
   先举个下例子：
   
   1）简单异常的捕获
   
       public class ErrorController {
        //一般情况下初学者都会用try-catch来进行简单的异常捕获，如下所示
        // 1)一般情况下
        public String testError(int a) {
   		int b = 0 ;
   		try {
   			b=1/a;
   		} catch (Exception e) {
   			return "系统错误";
   		}
   		return "success"+b;
   	    }
    }
    
   注：由于开发过程中有较多的方法，如果按照此方法来捕获异常则较为繁琐，因此引入全局捕获异常
   
   2）全局异常捕获
   
       全局捕获异常的原理：使用AOP切面技术
       用@RequestBody，@ResponseBody，就解决了JSon自动绑定。接着就发现，如果遇到RuntimeException，需要给出一个默认返回JSON。
   
   (1)创建一个utils工具类，来捕获全局异常
   
   @ControllerAdvice是一个Controller增强器，可以对范围内的Controller中被@RequestMapping注解的方法加一些逻辑处理，例如搭配@ExceptionHandler做统一异常处理
   
       package com.demo.utils;
       import java.util.HashMap;
       import java.util.Map;
       import org.springframework.web.bind.annotation.ControllerAdvice;
       import org.springframework.web.bind.annotation.ExceptionHandler;
       import org.springframework.web.bind.annotation.ResponseBody;
       /**
        * 全局捕获异常
        * 原理:使用AOP切面技术
        * 捕捉返回json串
        * @ControllerAdvice(basePackages="com.demo.controller")意指在此包下自动捕获@ExceptionHandler(RuntimeException.class)指定的RuntimeException异常
        */
       @ControllerAdvice(basePackages="com.demo.controller")
       public class ErrorUtil {
        //统一异常处理@ExceptionHandler,主要用于RuntimeException
        @ExceptionHandler(RuntimeException.class)
        @ResponseBody//返回json串
         public Map<String, Object> errorResoult(){
          Map<String, Object> errorMap= new HashMap<String, Object>();
          errorMap.put("errorCode", "500");
          errorMap.put("errorMsg", "系统错误");
          return errorMap;
         }
       }
   
   （2）控制层代码
   
       package com.demo.controller;
       import org.springframework.web.bind.annotation.RequestMapping;
       import org.springframework.web.bind.annotation.RestController;
       /**
        * 全局捕获异常例子
        * @author hzz
        *
        */
       @RestController
       public class ErrorController {
        
        //2)全局捕获异常 
        @RequestMapping("/test-error")
        public String testError(int a) {		
   		int b = 1/a;
   		return "success"+b;
     	}
    }
   自定义异常处理步骤：
   
   1.创建一个自定义异常类并标注注解@RestControllerAdvice（basePackages属性为扫描需要异常处理的包）
   
   2.定义相关异常的方法，方法上加入注解@ExceptionHandler（value属性为异常的类）：
         1）具体异常：@ExceptionHandler(value = MethodArgumentNotValidException.class)
         2）未知异常：@ExceptionHandler(value = Throwable.class)
   
   举个例子：
   
       /*
        *@RestControllerAdvice是上边所说的@ResponseBody + @ControllerAdvice的组合注解
        *basePackages ：表明需要扫描当前包下的所有方法
        */
       @RestControllerAdvice(basePackages = "com.atguigu.gulimall.product.controller")
       public class GulimallExceptionControllerAdvice {
           //自定义校验异常处理方法，一般情况下以json的形式将异常信息返回
           @ExceptionHandler(value = MethodArgumentNotValidException.class)
           public R handleVaildException(MethodArgumentNotValidException e){
               //将错误的信息封装到map中
               HashMap<String, String> errMap = new HashMap<>();
               //log.error("数据校验出现问题{}，异常类型：{}",e.getMessage(),e.getClass());
               BindingResult result = e.getBindingResult();
               result.getFieldErrors().forEach((item) ->{
                   //获取数据校验错误的属性名
                   String errorField = item.getField();
                   //获取数据校验错误的信息
                   String errorMessage = item.getDefaultMessage();
                   errMap.put(errorField,errorMessage);
               });
               return  R.error(BizCodeEnume.VAILD_EXCEPTION.getCode(),BizCodeEnume.VAILD_EXCEPTION.getMessage()).put("data",errMap);
           }
           //自定义未知异常
           @ExceptionHandler(value = Throwable.class)
           public R handleException(Throwable throwable){
               log.error("错误：",throwable);
               return R.error(BizCodeEnume.UNKNOWN_EXCEPTION.getCode(),BizCodeEnume.UNKNOWN_EXCEPTION.getMessage());
           }
       }
   这就是简单的全局捕获异常，实际开发中还需要log日志的打印，后期我将会继续更新，由于博主刚入Java坑不久，难免有些错误，请大家批评，共同提高。‘

