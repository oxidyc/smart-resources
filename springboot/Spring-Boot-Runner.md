# Spring Boot 之 CommandLineRunner和ApplicationRunner

## Overview
1. 使用场景

	需要在容器启动的时候执行一些内容，例如：读取配置文件信息，数据库连接，删除临时文件，清除缓存信息。在Spring框架下通过`ApplicationListener`监听器来实现的，在Spring Boot中提供了两个接口来帮助我们实现这样的需求。这两个接口就是 `CommandLineRunner` 和 `ApplicationRunner`，他们的执行时机为容器启动完成的时候

2. 共同点和区别

    **共同点**
    - 执行时机都是在容器启动完成的时候进行执行
    - 接口中都有一个`run()`方法

    **不同点**
    - ApplicationRunner接口中的run()方法的参数是`ApplicationArguments`, 是对原始参数做了进一步的封装。可以解析--name=value的，可以通过name来获取value。
	  - String[] getSourceArgs()
	  - boolean containsOption(String name)
	  - Set<String> getOptionNames()
	  - List<String> getOptionValues(String name)
    - CommandLineRunner接口中的run()方法的参数是`String数组`，是原始的参数，没有做任何处理。

3. 使用例子
```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.ApplicationListener;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.event.ContextRefreshedEvent;

@Configuration
public class SpringDoneDataInit implements ApplicationListener<ContextRefreshedEvent> {
    @Autowired
    private UserService userService;
    @Override
    public void onApplicationEvent(ContextRefreshedEvent contextRefreshedEvent) {
        int result = userService.count();
        System.out.println("----------SpringDoneDataInit---------"+result);
    }
}
/*
    - ContextRefreshedEvent：ApplicationContext容器初始化或者刷新时触发该事件。 
    - ContextStartedEvent：当使用ConfigurableApplicationContext接口的start()方法启动ApplicationContext容器时触发该事件。
    - ContextClosedEvent：当使用ConfigurableApplicationContext接口的close()方法关闭ApplicationContext容器时触发该事件。
    - ContextStopedEvent:  当使用ConfigurableApplicationContext接口的stop()方法停止ApplicationContext容器时触发该事件。
*/

//============================================================================================

import org.springframework.stereotype.Component;
import org.springframework.boot.CommandLineRunner;
import org.springframework.core.Ordered;

@Component
//@Order(1)
public class MyStartupRunner1 implements CommandLineRunner,Ordered{
    @Override
    public void run(String... args) throws Exception {
        String strArgs = Arrays.stream(args).collect(Collectors.joining("|"));
        if(null != args){
            for(String s : args){
                System.out.println(s);
            }
        }
        System.out.println("<<<<<<<<<<<<这个是测试CommandLineRunner接口>>>>>>>>>>>>>>");
    }

    @Override
    public int getOrder() {
        return 1;
    }
}

import org.springframework.boot.ApplicationRunner;
import org.springframework.boot.ApplicationArguments;
import org.springframework.core.annotation.Order;
/**
 *  参数格式为Key-Value格式，类似 --foo=bar --developer.name=jackson
 *
 */
@Component
@Order(2)
public class MyStartupRunner2 implements ApplicationRunner{
    @Override
    public void run(ApplicationArguments args) throws Exception {
        String strArgs = Arrays.stream(args.getSourceArgs()).collect(Collectors.joining("|"));
        String[] sourceArgs = args.getSourceArgs();
        if(null != sourceArgs){
            for(String s : sourceArgs){
                System.out.println(s);
            }
        }
        System.out.println("<<<<<<<<<<<<这个是测试ApplicationRunner接口>>>>>>>>>>>>>>");
    }
}
```
4. 执行顺序

    使用Ordered接口或者@Order注解修改执行顺序，注解中数字越小，优先级越高。

5. 执行流程源码分析
- (1).`SpringApplication.run(args)`
```java
public ConfigurableApplicationContext run(String... args) {
		StopWatch stopWatch = new StopWatch();
		stopWatch.start();
		ConfigurableApplicationContext context = null;
		FailureAnalyzers analyzers = null;
		configureHeadlessProperty();
		SpringApplicationRunListeners listeners = getRunListeners(args);
		listeners.started();
		try {
            // 对用户在Arguments输入的参数进行封装
			ApplicationArguments applicationArguments = new DefaultApplicationArguments(
					args);
			ConfigurableEnvironment environment = prepareEnvironment(listeners,
					applicationArguments);
			Banner printedBanner = printBanner(environment);
			context = createApplicationContext();
			analyzers = new FailureAnalyzers(context);
			prepareContext(context, environment, listeners, applicationArguments,
					printedBanner);
			refreshContext(context);
            
            // 在更新完ApplicationContext之后，进行操作，run方法的调用就在这里被执行
			afterRefresh(context, applicationArguments);
			listeners.finished(context, null);
			stopWatch.stop();
			if (this.logStartupInfo) {
				new StartupInfoLogger(this.mainApplicationClass)
						.logStarted(getApplicationLog(), stopWatch);
			}
			return context;
		}
		catch (Throwable ex) {
			handleRunFailure(context, listeners, analyzers, ex);
			throw new IllegalStateException(ex);
		}
	}
```
- (2).跟踪`afterRefresh(ConfigurableApplicationContext context,ApplicationArguments args) `方法
```java
protected void afterRefresh(ConfigurableApplicationContext context,
			ApplicationArguments args) {
		callRunners(context, args);
	}
 
	private void callRunners(ApplicationContext context, ApplicationArguments args) {
		List<Object> runners = new ArrayList<Object>();
        // 1.获取所有实现ApplicationRunner接口的类
		runners.addAll(context.getBeansOfType(ApplicationRunner.class).values());
        // 2.获取所有实现CommandLineRunner的类
		runners.addAll(context.getBeansOfType(CommandLineRunner.class).values());
        // 3.根据其@Order进行排序
		AnnotationAwareOrderComparator.sort(runners);
		for (Object runner : new LinkedHashSet<Object>(runners)) {
            // 4.调用ApplicationRunner其run方法
			if (runner instanceof ApplicationRunner) {
				callRunner((ApplicationRunner) runner, args);
			}
            // 5.调用CommandLineRunner其run方法
			if (runner instanceof CommandLineRunner) {
				callRunner((CommandLineRunner) runner, args);
			}
		}
	}
```
- (3).跟踪`context.getBeansOfType()`方法，具体实现如下（在类`DefaultListableBeanFactory`中）：
```java
public <T> Map<String, T> getBeansOfType(Class<T> type, boolean includeNonSingletons, boolean allowEagerInit)
			throws BeansException {
        // 根据类型获取beanName
		String[] beanNames = getBeanNamesForType(type, includeNonSingletons, allowEagerInit);
		Map<String, T> result = new LinkedHashMap<String, T>(beanNames.length);
		for (String beanName : beanNames) {
			try {
				result.put(beanName, getBean(beanName, type));
			}
			...
		}
		return result;
	}
 
	private String[] doGetBeanNamesForType(ResolvableType type, boolean includeNonSingletons, boolean allowEagerInit) {
		List<String> result = new ArrayList<String>();
 
		// 检查容器中所有的bean
		for (String beanName : this.beanDefinitionNames) {
			// Only consider bean as eligible if the bean name
			// is not defined as alias for some other bean.
			if (!isAlias(beanName)) {
				try {
					RootBeanDefinition mbd = getMergedLocalBeanDefinition(beanName);
					// Only check bean definition if it is complete.
					if (!mbd.isAbstract() && (allowEagerInit ||
							((mbd.hasBeanClass() || !mbd.isLazyInit() || isAllowEagerClassLoading())) &&
									!requiresEagerInitForType(mbd.getFactoryBeanName()))) {
						// In case of FactoryBean, match object created by FactoryBean.
						boolean isFactoryBean = isFactoryBean(beanName, mbd);
						BeanDefinitionHolder dbd = mbd.getDecoratedDefinition();
						boolean matchFound =
								(allowEagerInit || !isFactoryBean ||
										(dbd != null && !mbd.isLazyInit()) || containsSingleton(beanName)) &&
								(includeNonSingletons ||
										(dbd != null ? mbd.isSingleton() : isSingleton(beanName))) &&
								isTypeMatch(beanName, type);
						if (!matchFound && isFactoryBean) {
							// In case of FactoryBean, try to match FactoryBean instance itself next.
							beanName = FACTORY_BEAN_PREFIX + beanName;
							matchFound = (includeNonSingletons || mbd.isSingleton()) && isTypeMatch(beanName, type);
						}
                        // 对于符合类型的，添加到result中
						if (matchFound) {
							result.add(beanName);
						}
					}
				}
				...
			}
            return StringUtils.toStringArray(result);
		}
```

 ## Resource
 - https://blog.csdn.net/qq360694660/article/details/79354508
 - https://blog.csdn.net/qq_26323323/article/details/80856973   
 - https://www.jianshu.com/p/5d4ffe267596