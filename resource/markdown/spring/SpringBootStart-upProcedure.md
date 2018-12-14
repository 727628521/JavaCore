<h3 style="padding-bottom:6px; padding-left:20px; color:#ffffff; background-color:#E74C3C;">SpringBoot启动过程</h3>

> 一个Application被注解为 `@SpringBootApplication`，通过 `main` 方法开始、SpringApplication.run(Object source, String... args)运行。
>
> 本文是基于 `SpringBoot 2.0.6.RELEASE` 进行解析

#### Application初始化过程：

不同于 `1.5.6` 版本的使用 `initialize(sources)` 初始化方法进行初始化资源，`2.0.6` 使用构造方法进行初始化资源。

```java
/**
 * 创建一个新的 SpringApplication 实例。此 application context 将从指定的基础资源 SpringApplication类级文件加载 beans 详情。实例可以在调用 run(String... args) 方法前定制化。
 * @param resourceLoader 使用的资源加载器
 * @param primarySources 基础 bean 资源
 * @see #run(Class, String[])
 * @see #setSources(Set)
 */
@SuppressWarnings({ "unchecked", "rawtypes" })
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
	this.resourceLoader = resourceLoader;
    // 如果为 primarySources == null，那么直接停止运行(run方法一定要填**Application.class)
	Assert.notNull(primarySources, "PrimarySources must not be null");
    // 将 **Application.class 添加到 LinkedHashSet<Class<?>> (1.5.6是Object泛型)
	this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
    // 推导web应用的类型
	this.webApplicationType = WebApplicationType.deduceFromClasspath();
    // 设置初始化器
	setInitializers((Collection) getSpringFactoriesInstances(
			ApplicationContextInitializer.class));
    // 设置监听器
	setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
    // 推导主函数的类
	this.mainApplicationClass = deduceMainApplicationClass();
}
```

##### 1、将 `Application` 添加到到 `Set` 容器

容器是 **LinkedHashSet<Class<?>>**

```java
private Set<Class<?>> primarySources;
this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
```

##### 2、根据类路径推导Web应用

```java
static WebApplicationType deduceFromClasspath() {
	if (ClassUtils.isPresent(WEBFLUX_INDICATOR_CLASS, null)
			&& !ClassUtils.isPresent(WEBMVC_INDICATOR_CLASS, null)
			&& !ClassUtils.isPresent(JERSEY_INDICATOR_CLASS, null)) {
        // Spring 5.x 新特性之一就是reactive响应式编程，此处推导出响应式reactive web server
		return WebApplicationType.REACTIVE;
	}
	for (String className : SERVLET_INDICATOR_CLASSES) {
		if (!ClassUtils.isPresent(className, null)) {
            /* 
             * 如果存在Servlet或Spring ConfigurableWebApplicationContext
             * 推导出是一般的 web server
			 */return WebApplicationType.NONE;
		}
	}
    // 否则就认为是 Servlet 服务
	return WebApplicationType.SERVLET;
}
```

#####  3、设置/添加初始化器（将初始化器添加到ArrayList）

设置/添加 `ApplicationContextInitializer.class` 为初始化器

```java
setInitializers((Collection) getSpringFactoriesInstances(
			ApplicationContextInitializer.class));
// --------------------------------------------------
private <T> Collection<T> getSpringFactoriesInstances(Class<T> type) {
	return getSpringFactoriesInstances(type, new Class<?>[] {});
}
// --------------------------------------------------
private <T> Collection<T> getSpringFactoriesInstances(Class<T> type,
		Class<?>[] parameterTypes, Object... args) {
    // 类加载器是当前线程的上下文类加载器
	ClassLoader classLoader = Thread.currentThread().getContextClassLoader();
	// 使用名称并确保唯一性以防止重复
	Set<String> names = new LinkedHashSet<>(
			SpringFactoriesLoader.loadFactoryNames(type, classLoader));
    // 将创建后的实例放入 List
	List<T> instances = createSpringFactoriesInstances(type, parameterTypes,
			classLoader, args, names);
	AnnotationAwareOrderComparator.sort(instances);
	return instances;
}
```

##### 4、设置/添加监听器

设置/添加 `ApplicationListener.class` 为监听器（同上）

```java
setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
```

##### 5、推断main方法所在的Application应用类

虚拟机栈是方法的执行模型，从栈信息查找 `mian`  方法所在的类

```java
private Class<?> deduceMainApplicationClass() {
	try {
		StackTraceElement[] stackTrace = new RuntimeException().getStackTrace();
		for (StackTraceElement stackTraceElement : stackTrace) {
            // 判断栈追踪元素的方法是否等于 main 方法
			if ("main".equals(stackTraceElement.getMethodName())) {
                // 则根据此实例的类名称获取类，并返回
				return Class.forName(stackTraceElement.getClassName());
			}
		}
	}
	catch (ClassNotFoundException ex) {
		// 啥也不处理，并继续
	}
	return null;
}
```

