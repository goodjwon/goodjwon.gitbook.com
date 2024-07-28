---
layout: single
title: "Servlet 2.5 를 사용하는 경우 Spring에서 파일 업로드 제한 설정"
---


## Servlet 2.5 를 사용하는 경우
>  web.xml 에 servlet 태그 내부에 추가는 불가능 하고 Bean 요소에 설정 해야 함.

### 파일 사이즈 제한과 최대 요청 크기를 설정
 - Spring의 설정 파일에 MultipartResolver 빈을 정의할 때, 이러한 제한을 지정. 

 - 일반적으로 사용되는 MultipartResolver 구현체인 CommonsMultipartResolver를 사용

 - 파일 사이즈 제한과 최대 요청 크기를 설정하는 방법을 보여주는 Spring 설정 파일 (dispatcher-config.xml 또는 root-context.xml) 내의 빈 설정 예시
 
```xml
    <!-- Spring configuration file (dispatcher-config.xml or root-context.xml) -->
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- Multipart Resolver -->
    <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
        <!-- 한 파일 최대 크기 (예: 5MB) -->
        <property name="maxUploadSizePerFile" value="5242880"/> <!-- 5 * 1024 * 1024 -->

        <!-- 전체 요청 최대 크기 (예: 20MB) -->
        <property name="maxUploadSize" value="20971520"/> <!-- 20 * 1024 * 1024 -->
    </bean>

</beans>

 ```

 - 설명
   - 위 설정에서 maxUploadSizePerFile 속성은 개별 파일의 최대 크기를 바이트 단위로 지정. 
   - 예를 들어, 5242880은 약 5MB를 의미. 
   - maxUploadSize 속성은 전체 요청의 최대 크기를 지정, 
   - 예제에서는 20971520으로 설정하여 약 20MB의 제한


- 기타
  - MaxUploadSizeExceededException 발생  됨으로  이 예외를 처리하기 위한 예외 핸들러를 컨트롤러에 추가하여 사용자에게 적절한 에러 메시지를 제공 필요


# 참고
## Servlet 3.0 이상을 사용하는 경우
>  web.xml에 multipart-config 요소를 servlet 태그 내부에 추가 가능

```xml
  <servlet>
    <servlet-name>dispatcher</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <multipart-config>
        <!-- 최대 파일 크기 (예: 5MB) -->
        <max-file-size>5242880</max-file-size> <!-- 5 * 1024 * 1024 -->

        <!-- 최대 요청 크기 (예: 20MB) -->
        <max-request-size>20971520</max-request-size> <!-- 20 * 1024 * 1024 -->

        <!-- 파일 데이터를 디스크에 저장하기 전에 메모리에 저장할 수 있는 최대 크기 -->
        <file-size-threshold>0</file-size-threshold>
    </multipart-config>
    <load-on-startup>1</load-on-startup>
</servlet>
```