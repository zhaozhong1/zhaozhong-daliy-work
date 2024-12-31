# MyBatis 源码阅读

## 大体路线

### 扫描Mapper

SqlSessionFactoryBuilder#build(Reader reader, String environment, Properties properties) 

-> XMLConfigBuilder#parse() 开始解析xml文件

-> XMLConfigBuilder.parseConfiguration(XNode root) 解析配置文件，加载Mapper

-> XMLConfigBuilder#mappersElement(XNode context)  根据mapper标签中的resource/url/mapperClass 来获取mapper类并加载

### 使用Mapper进行查询



