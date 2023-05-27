# Build Spring Native Application

> https://docs.spring.io/spring-native/docs/current/reference/htmlsingle/#getting-started-native-image-system-requirements

## build lightweight container image

```shell
$ ./mvnw spring-boot:build-image
```

## jar to executable file

```
pack build --builder paketobuildpacks/builder:tiny \
    --path target/my-app-0.0.1-SNAPSHOT.jar --env 'BP_NATIVE_IMAGE=true' my-app:0.0.1
```


## build tools

### install sdk
```shell
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk version
```

### download graalvm

https://www.oracle.com/downloads/graalvm-downloads.html


### install java

**注: 版本与graalvm保持一致**

```shell
sdk install java 22.1.r11-nik
```

### use or default
```shell
sdk use java 22.1.r11-nik

# or
sdk default java 22.1.r11-nik
```

