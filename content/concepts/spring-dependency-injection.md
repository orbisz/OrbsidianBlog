---
title: Spring 依赖注入使用技巧
category: concepts
tags: [Spring, DI, Java, backend]
sources: ["F:/blog/my-blog/blogs/backend/DI.md"]
summary: Spring 依赖注入高级技巧，涵盖构造注入 List/Map 收集、条件注入、原型对象、Profile 环境配置、@Primary 首选 Bean 等实用模式。
created: 2026-05-20
updated: 2026-05-20
base_confidence: 0.75
lifecycle: draft
lifecycle_changed: 2026-05-20
tier: supporting
provenance:
  extracted: 0.85
  inferred: 0.10
  ambiguous: 0.05
---

# Spring 依赖注入使用技巧

## 构造注入：List 和 Map 收集

当接口有多个实现类时，Spring 可按类型自动注入为 `List` 或 `Map<String, Interface>`。

```java
private final Map<String, IAwardService> awardServiceMap;

public AwardController(Map<String, IAwardService> awardServiceMap) {
    this.awardServiceMap = awardServiceMap;
}
```

**使用场景**: 将 Bean 名称设为业务 key（如奖品 awardKey），运行时根据 key 直接获取对应实现，消除 if-else 分支。

## 空注入判断

`@Autowired(required = false)` 允许注入的 Bean 不存在时不抛异常。适合支付/外部接口对接测试阶段关闭某些服务时使用。

## 首选 Bean：@Primary

多实现类时，`@Primary` 标记首选注入对象，避免 `NoUniqueBeanDefinitionException`。

## 条件注入控制

- **@ConditionalOnMissingBean**: 上下文中已存在时不重复创建，常用于组件库开发避免冲突
- **@ConditionalOnProperty**: 通过配置 `enabled` 值控制是否实例化，无需注掉 pom 依赖
- **自定义 Condition**: 实现 `Condition` 接口的 `matches` 方法，完全自定义实例化逻辑

## 环境配置：@Profile

`@Profile({"prod", "test"})` 指定特定环境才实例化（如生产支付服务），配合 `@Autowired(required = false)` 使用。

## 其他实用注解

- **@Scope("prototype")**: 每次获取都是新实例，适合动态责任链
- **@DependsOn**: 声明 Bean 实例化依赖顺序
- **@Async**: 异步方法执行，适合数据导出等场景
- **@EnableScheduling**: 开启定时任务

## 相关页面
- 数据库: [[concepts/mvcc]] | [[concepts/redis-persistence]]
