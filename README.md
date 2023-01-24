* Project to demo a circularity issue when using hibernate

Dependencies between entities:
A -> B -> C -> A


On startup of the spring application the following error is produced:


```

2023-01-24T13:44:13.537+01:00 ERROR 1020 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: [PersistenceUnit: default] Unable to build Hibernate SessionFactory; nested exception is org.hibernate.sql.ast.tree.from.UnknownTableReferenceException: Unable to determine TableReference (`demo.a_class`) for `com.example.demo.db.B.cClasses.{fk-target}`
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1751) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:599) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:521) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:326) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:234) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:324) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:200) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.context.support.AbstractApplicationContext.getBean(AbstractApplicationContext.java:1130) ~[spring-context-6.0.4.jar:6.0.4]
	at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:905) ~[spring-context-6.0.4.jar:6.0.4]
	at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:584) ~[spring-context-6.0.4.jar:6.0.4]
	at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:146) ~[spring-boot-3.0.2.jar:3.0.2]
	at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:730) ~[spring-boot-3.0.2.jar:3.0.2]
	at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:432) ~[spring-boot-3.0.2.jar:3.0.2]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:308) ~[spring-boot-3.0.2.jar:3.0.2]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1302) ~[spring-boot-3.0.2.jar:3.0.2]
	at org.springframework.boot.SpringApplication.run(SpringApplication.java:1291) ~[spring-boot-3.0.2.jar:3.0.2]
	at com.example.demo.DemoApplication.main(DemoApplication.java:10) ~[classes/:na]
Caused by: jakarta.persistence.PersistenceException: [PersistenceUnit: default] Unable to build Hibernate SessionFactory; nested exception is org.hibernate.sql.ast.tree.from.UnknownTableReferenceException: Unable to determine TableReference (`demo.a_class`) for `com.example.demo.db.B.cClasses.{fk-target}`
	at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:421) ~[spring-orm-6.0.4.jar:6.0.4]
	at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.afterPropertiesSet(AbstractEntityManagerFactoryBean.java:396) ~[spring-orm-6.0.4.jar:6.0.4]
	at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.afterPropertiesSet(LocalContainerEntityManagerFactoryBean.java:352) ~[spring-orm-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.invokeInitMethods(AbstractAutowireCapableBeanFactory.java:1797) ~[spring-beans-6.0.4.jar:6.0.4]
	at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1747) ~[spring-beans-6.0.4.jar:6.0.4]
	... 16 common frames omitted
Caused by: org.hibernate.sql.ast.tree.from.UnknownTableReferenceException: Unable to determine TableReference (`demo.a_class`) for `com.example.demo.db.B.cClasses.{fk-target}`
	at org.hibernate.sql.ast.tree.from.AbstractColumnReferenceQualifier.resolveTableReference(AbstractColumnReferenceQualifier.java:45) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.sql.ast.tree.from.ColumnReferenceQualifier.resolveTableReference(ColumnReferenceQualifier.java:16) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.mapping.internal.SimpleForeignKeyDescriptor.createDomainResult(SimpleForeignKeyDescriptor.java:246) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.mapping.internal.SimpleForeignKeyDescriptor.createTargetDomainResult(SimpleForeignKeyDescriptor.java:179) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.mapping.internal.PluralAttributeMappingImpl.createDelayedCollectionFetch(PluralAttributeMappingImpl.java:518) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.mapping.internal.PluralAttributeMappingImpl.generateFetch(PluralAttributeMappingImpl.java:422) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.sql.results.graph.FetchParent.generateFetchableFetch(FetchParent.java:105) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.LoaderSelectBuilder.lambda$createFetchableBiConsumer$7(LoaderSelectBuilder.java:846) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.LoaderSelectBuilder.visitFetches(LoaderSelectBuilder.java:684) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.LoaderSqlAstCreationState.visitFetches(LoaderSqlAstCreationState.java:118) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.sql.results.graph.AbstractFetchParent.afterInitialize(AbstractFetchParent.java:32) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.sql.results.graph.entity.AbstractEntityResultGraphNode.afterInitialize(AbstractEntityResultGraphNode.java:100) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.persister.entity.AbstractEntityPersister.createDomainResult(AbstractEntityPersister.java:1300) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.LoaderSelectBuilder.generateSelect(LoaderSelectBuilder.java:450) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.LoaderSelectBuilder.createSelect(LoaderSelectBuilder.java:177) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.SingleIdEntityLoaderStandardImpl.createLoadPlan(SingleIdEntityLoaderStandardImpl.java:180) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.loader.ast.internal.SingleIdEntityLoaderStandardImpl.prepare(SingleIdEntityLoaderStandardImpl.java:54) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.persister.entity.AbstractEntityPersister.prepareLoader(AbstractEntityPersister.java:4361) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.persister.entity.AbstractEntityPersister.postInstantiate(AbstractEntityPersister.java:4353) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.model.domain.internal.MappingMetamodelImpl.finishInitialization(MappingMetamodelImpl.java:236) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.metamodel.internal.RuntimeMetamodelsImpl.finishInitialization(RuntimeMetamodelsImpl.java:60) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.internal.SessionFactoryImpl.<init>(SessionFactoryImpl.java:311) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.boot.internal.SessionFactoryBuilderImpl.build(SessionFactoryBuilderImpl.java:415) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1425) ~[hibernate-core-6.1.6.Final.jar:6.1.6.Final]
	at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:66) ~[spring-orm-6.0.4.jar:6.0.4]
	at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:376) ~[spring-orm-6.0.4.jar:6.0.4]
	at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:409) ~[spring-orm-6.0.4.jar:6.0.4]
	... 20 common frames omitted
```