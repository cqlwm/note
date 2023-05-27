# 注解扫描



## AnnotationScanner Class

```kotlin
import org.springframework.context.annotation.ClassPathScanningCandidateComponentProvider
import org.springframework.core.type.filter.AnnotationTypeFilter

object AnnotationScanner {
    fun scan(packageName: String, annotationClass: Class<out Annotation>): List<String> {
        val provider = ClassPathScanningCandidateComponentProvider(false)
        provider.addIncludeFilter(AnnotationTypeFilter(annotationClass))
        val beanDefinitions = provider.findCandidateComponents(packageName)
        val classNames: MutableList<String> = ArrayList()
        for (beanDefinition in beanDefinitions) {
            beanDefinition.beanClassName?.let { classNames.add(it) }
        }
        return classNames
    }
}
```



## AnnotationScanner Case

```kotlin
val templateExecutionMetas = mutableMapOf<String, TemplateExecutionMeta<out InputTemplate<*>, out Any>>().let { map ->
    val packageName = "tech.example.keywords.model.template"
    val templateDefineClasses = AnnotationScanner.scan(packageName, PromptTemplateDefine::class.java)
    for (className in templateDefineClasses) {
        val classz = Class.forName(className)
        val templateDefineAnnotation = classz.getAnnotation(PromptTemplateDefine::class.java)
        val id = templateDefineAnnotation.id
        val outputBodyClass = templateDefineAnnotation.outputBodyClass
        val pres = templateDefineAnnotation.preprocessor.map { preprocessorDefines.getValue(it) }
        val posts = templateDefineAnnotation.postprocessor.map { postprocessorDefines.getValue(it) }
        map[id] = TemplateExecutionMeta(
            inputClass = classz as Class<InputTemplate<*>>,
            outputBodyClass = outputBodyClass.java,
            preprocessor = pres,
            postprocessor = posts
        )
    }
    map.toMap()
}
```

