---
formatter: "@formatter:off"
title: "Spring Validation"
subtitle: 
summary: 校验
tags: [spring,validation] 
date: 2023-03-20 09:50:48 +800 
version: 1.0
formatter: "@formatter:on"
---

# Validation

在Spring中，可以通过在方法或参数上添加`@Validated`和`@Valid`注解及配合众多`@Constraint`来实现对参数的校验。

先说结论：

* 如果参数需要值校验，则需要在方法上声明`@Validated`注解同时在参数上声明需要校验的规则。如`@NotNull String name`、`@NotEmpty List<String> list`。
* 如果参数需要嵌套校验，则需要在对应的参数上声明`@Valid`注解。
* 如果需要分组校验，则需要（在方法或参数上）声明`@Validated`或在JavaBean中声明`@GroupSequenceProvider`。



> 从Spring Boot 2.3.0开始，需要显示添加以下依赖：
> ```xml
> <dependency>
>     <groupId>org.springframework.boot</groupId>
>     <artifactId>spring-boot-starter-validation</artifactId>
> </dependency>
> ```

## 校验时机

### 参数校验

**参数校验**指的是对每一个参数进行一对一的校验，参数之间互不影响。

在Spring中，一个参数（Controller方法中的参数）能否被校验，取决于该参数是否有满足校验的注解：

* 注解的名称是否等于`javax.validation.Valid`；
* 注解上是否有`@Validated`元注解
* 注解名称是否以`Valid`开头

```java
public abstract class ValidationAnnotationUtils {

	private static final Object[] EMPTY_OBJECT_ARRAY = new Object[0];

	/**
	 * Determine any validation hints by the given annotation.
	 * <p>This implementation checks for {@code @javax.validation.Valid},
	 * Spring's {@link org.springframework.validation.annotation.Validated},
	 * and custom annotations whose name starts with "Valid".
	 * @param ann the annotation (potentially a validation annotation)
	 * @return the validation hints to apply (possibly an empty array),
	 * or {@code null} if this annotation does not trigger any validation
	 */
	@Nullable
	public static Object[] determineValidationHints(Annotation ann) {
		Class<? extends Annotation> annotationType = ann.annotationType();
		String annotationName = annotationType.getName();
		if ("javax.validation.Valid".equals(annotationName)) {
			return EMPTY_OBJECT_ARRAY;
		}
		Validated validatedAnn = AnnotationUtils.getAnnotation(ann, Validated.class);
		if (validatedAnn != null) {
			Object hints = validatedAnn.value();
			return convertValidationHints(hints);
		}
		if (annotationType.getSimpleName().startsWith("Valid")) {
			Object hints = AnnotationUtils.getValue(ann);
			return convertValidationHints(hints);
		}
		return null;
	}

	private static Object[] convertValidationHints(@Nullable Object hints) {
		if (hints == null) {
			return EMPTY_OBJECT_ARRAY;
		}
		return (hints instanceof Object[] ? (Object[]) hints : new Object[]{hints});
	}

}
```

### 方法校验

**方法校验**也叫**切面校验**，Spring中通过AOP方式在方法被调用之前对参数进行（整体）校验。

一个（Spring Bean对象的）方法是否能被校验，取决于这个方法是否满足以下条件之一：

* **方法**上有`@Validated`注解
* **类**上有`@Validated`注解

```java
public class MethodValidationInterceptor implements MethodInterceptor {
    ...
	protected Class<?>[] determineValidationGroups(MethodInvocation invocation) {
        // 1. 查找方法上声明的 @Validated 注解
		Validated validatedAnn = AnnotationUtils.findAnnotation(invocation.getMethod(), Validated.class);
		if (validatedAnn == null) {
			Object target = invocation.getThis();
			Assert.state(target != null, "Target must not be null");
            // 2. 查找类上声明的 @Validated 注解
			validatedAnn = AnnotationUtils.findAnnotation(target.getClass(), Validated.class);
		}
        // 返回注解中声明的分组或返回空数组。
		return (validatedAnn != null ? validatedAnn.value() : new Class<?>[0]);
	}
    ...
}
```



## 分组校验

* **静态分组**：使用Spring提供的`@Validated`注解。
* **动态分组**：实现Hibernate提供的`@GroupSequenceProvider`注解。

### @Validated

通常来说，通过指定`@Validated`注解的`value()`，就可以实现分组校验，但这种方式只适用于静态分组，对于动态分组，则需要使用`@GroupSequenceProvider`。

```java
@RestController
@RequestMapping("/validated-group")
public class ValidatedGroupController{
    
    @GetMapping("/a")
    public Group a(@Validated(GroupA.class) Group group){
        return group;
    }

    @GetMapping("/b")
    public Group b(@Validated(GroupB.class) Group group){
        return group;
    }
    
    
    public static class Group{
        @NotNull(groups={GroupA.class})
        private String a;
        @NotNull(groups={GroupB.class})
        private String b;
    }
    
    public interface GroupA {}
    public interface GroupB {}
}
```



### @GroupSequenceProvider

一般来讲，通过在被校验的类上声明`@GroupSequenceProvider`注解，并指定分组序列提供者`DefaultGroupSequenceProvider`，就可以实现对某个被校验类实现分组校验。
