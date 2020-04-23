# Chapter-5

第五讲 网络 Json Gson Retrofit

添加了post接口

```Java
@FormUrlEncoded
@POST("user/register")
Call<UserResponse> register (@Field("username") String userName,
                             @Field("password") String password,
                             @Field("repassword") String repassword);
```

用Retrofit做网络请求：

```java
apiService.register(name, password, repassword).enqueue(new Callback<UserResponse>() {
    @Override
    public void onResponse(Call<UserResponse> call, Response<UserResponse> response) {
        if (response.body().errorCode == 0){
            Toast.makeText(RegisterActivity.this, "注册成功！" + response.body().user.nickname,
                    Toast.LENGTH_SHORT).show();
        }
        else{
            Toast.makeText(RegisterActivity.this, "注册失败：" + response.body().errorMsg,
                    Toast.LENGTH_SHORT).show();
        }
    }

    @Override
    public void onFailure(Call<UserResponse> call, Throwable t) {
        Toast.makeText(RegisterActivity.this, "网络错误：" + t.getMessage(), Toast.LENGTH_SHORT).show();
    }
});
```

