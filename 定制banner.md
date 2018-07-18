根据这个网址去生成对应的banner
http://patorjk.com/software/taag/#p=display&f=Graffiti&t=Type%20Something%20

将定制好的banner,加入到项目下的resources/banner.txt文件(如果没有则新建一个)


```
   代码中控制是否开启logo
   public static void main(String[] args) {
        SpringApplication app = new SpringApplication(EtlApplication.class);
        //设置打印logo
        app.setBannerMode(Banner.Mode.OFF);
        app.run(args);
    }
```
