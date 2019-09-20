# springboot启动配置原理（启动原理、运行流程、自动配置原理 ）

## 1.几个重要的事件回调机制牵扯到的接口

(1)、ApplicationContextInitializer.initialize()

(2)、SpringApplicationRunListener

(3)、ApplicationRunner

(4)、CommandLineRunner

## 2.启动流程

#### （1）创建SpringApplication对象

此过程分为两步：

​	a.创建SpringApplication 对象，b.执行run方法

```java
    public static ConfigurableApplicationContext run(Class<?> primarySource, String... args) {
        return run(new Class[]{primarySource}, args);
    }

    public static ConfigurableApplicationContext run(Class<?>[] primarySources, String[] args) {
        return (new SpringApplication(primarySources)).run(args);
    }
```



#### （2）启动应用

```java
	/**
	 * Run the Spring application, creating and refreshing a new
	 * {@link ApplicationContext}.
	 * @param args the application arguments (usually passed from a Java main method)
	 * @return a running {@link ApplicationContext}
	 */
	public ConfigurableApplicationContext run(String... args) {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		ConfigurableApplicationContext context = null;
		Collection<SpringBootExceptionReporter> exceptionReporters = new ArrayList<>();
		configureHeadlessProperty();
        //获取SpringApplicationRunListeners；从类路径下的MATA-INFO/spring.factories
		SpringApplicationRunListeners listeners = getRunListeners(args);
        //回调所有的获取SpringApplicationRunListeners.starting();
		listeners.starting();
		try {
            //封装命令
			ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
            //准备环境
			ConfigurableEnvironment environment = prepareEnvironment(listeners, applicationArguments);
			configureIgnoreBeanInfo(environment);
            //打印图标
			Banner printedBanner = printBanner(environment);
            //创建ApplicationContext
			context = createApplicationContext();
			exceptionReporters = getSpringFactoriesInstances(SpringBootExceptionReporter.class,
					new Class[] { ConfigurableApplicationContext.class }, context);
            //准备上下文环境（ApplicationContextInitializer）
			prepareContext(context, environment, listeners, applicationArguments, printedBanner);
            //刷新容器，ioc容器初始化
			refreshContext(context);
            //从ioc容器中获取所有的ApplicationRunner和CommandLineRunner进行回调（ApplicationRunner先回调，CommandLineRunner再回调）
			afterRefresh(context, applicationArguments);
            
			stopWatch.stop();
			if (this.logStartupInfo) {
				new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
			}
			listeners.started(context);
			callRunners(context, applicationArguments);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, exceptionReporters, listeners);
			throw new IllegalStateException(ex);
		}

		try {
			listeners.running(context);
		}
		catch (Throwable ex) {
			handleRunFailure(context, ex, exceptionReporters, null);
			throw new IllegalStateException(ex);
		}
        //整个springboot应用启动完成后返回启动的ioc容器
		return context;
	}
```

