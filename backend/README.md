### 说明

创建功能
    
    [java]
    edit com/kingland/neusoft/course/controller/UserController.java
    add com/kingland/neusoft/course/util/tools.java

    [angular]
    add src/app/admin/edit-user/edit-user.component.ts

用户账户信息可修改
```java
@PostMapping("/users/edit/{id}")
 try {
     userData.put("DateBirthday", new SimpleDateFormat("yyyy-MM-dd").parse((String)userData.get("birthday")));
 } catch (ParseException e) {
     return tools.responseJson(false, null, e.getMessage());
 }
 if(userData.get("password") != ""){
     if(userData.get("password").toString().length() <6){
         return tools.responseJson(false, null, "密码必须大于6位数");
     }else if(!userData.get("password").equals(userData.get("confirmPassword"))){
         return tools.responseJson(false, null, "两次密码不相同");
     }
     userData.replace("password", this.passwordEncoder.encode(userData.get("password").toString()));
 }else{
     userData.replace("password",null);
 }
 if(userService.updateUserModel(tools.toUserModel(userData)) ==0)
     //全局调用 tools.responseJson 输出
     return tools.responseJson(false, null, "新增用户数据失败");
 else 
     return tools.responseJson(true, null, "成功新增用户数据");
```



修改功能

[page=UserController.java;edit-user.component.ts] 查看用户时 日期不显示 两次密码验证
```ts
this.registerForm.controls['birthday'].setValue(new Date(user.birthday));
```
```java
if(userData.get("password") != ""){
    if(userData.get("password").toString().length() <6){
        return tools.responseJson(false, null, "密码必须大于6位数");
    }else if(!userData.get("password").equals(userData.get("confirmPassword"))){
        return tools.responseJson(false, null, "两次密码不相同");
    }
    userData.replace("password", this.passwordEncoder.encode(userData.get("password").toString()));
}else{
    return tools.responseJson(false, null, "密码不能为空"); 
}
```

+ 数据库

无

    