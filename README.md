# Bootiful Kotlin

## <3

Код из конференции `KotlinConf 2017`. Как кодить на Kotlin и Spring Boot 2 показывает *Josh Long*.

Видео можно посмотреть на [YuoTube](https://www.youtube.com/watch?v=SlBRce-aBOc&t=629s).


* h2database

* gradle

* spring boot 2

* reactive-friendly (`spring reactor-test`)

* exposed library functional _db [`org.jetbrains.exposed`]: Fun => () ->_ to it_ { } >>> :-)   

### Главный класс:

```kotlin   
package ru

@SpringBootApplication
class ReactiveApplication

fun main(args: Array<String>) {
    SpringApplicationBuilder()
        .sources(ReactiveApplication::class.java)
        .initializers(beans {
            bean {
                router {
                    GET("/hi") {
                        ServerResponse.ok().body(Flux.just("Hello, functional reactive"), String::class.java)
                    }
                }
            }
            bean {
                ref<RouteLocatorBuilder>().routes {
                    route {
                        path("/guides")
                        uri("http://spring.io:80/guides")
                    }
                }
            }
        })
        .run(*args)
}
```

### Тест:

```kotlin
package ru

@RunWith(SpringRunner::class)
@SpringBootTest
class ReactiveApplicationTests {

    @Test
    fun contextLoads() {
    }

}
```

