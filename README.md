## kkkSpring
나의 스프링 연습 (부트기반)

## GitHub 연결
  + GitHub에서 생성한 리파짓을 인텔리제이에서 불러오고 (로컬 위치에 연결)
  + Spring Intializr 에서 스프링부트 프로젝트를 생성하고, 로컬 위치에 저장
  + 그래들로 프로젝트를 생성했으므로, "build.gradle"에서 gradle프로젝트 링크를 클릭해서, 그래들 구성

## 스프링부트 소스의 빌드/실행/배포
  + 빌드를 수행 : build -x test --> 오류가 나는데, JDK버전문제 (17버전을 사용해라!!)
  + 실행을 수행 : Application실행을 추가하고 실행하면, main 클래스를 못찾는다고 나오는데, 그래들 업데이트 후에 기다리면 바로 찾아줌
  + 실행시 오류가 발생
    1) ..java.exe'' finished with non-zero exit value 1 (아래 해결안 참고)
      . 인텔리제이에서 초기에 프로젝트 생성후 빌드/실행할때는, "just invalidate the caches and restart"
      . 그래들 설정에서, 그래들을 인텔리제이로 변경해야함
    2) Logging system failed to initialize using configuration from 'classpath:logback.xml'
      .classpath 밑에, logback.xml 이 없으므로, 추가해주면 됨
    3) Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured. 
      . Reason: Failed to determine a suitable driver class
      . 그래들에서 mysql을 추가했기 때문에, 아래와 같이 데이터소스 기존 설정을 넣어줘야함
        datasource:
          driver-class-name: com.mysql.cj.jdbc.Driver
          url: jdbc:mysql://localhost:3306/mystocks?autoReconnection=true&useSSL=false&allowMultiQueries=true&zeroDateTimeBehavior=convertToNull
          username: root
          password: welcome
+ 배포를 위한 jar파일 생성  
  . 빌드/실행/배포는 모두 그래들 기반으로 수행하므로, 배포도 그래들의 bootJar를 수행하면 됨
  . 빌드는 build, 실행은 java, 배포는 bootJar 로 수행

   