```
<?xml version="1.0" encoding="UTF-8" ?>
<configuration debug="true">
    <property name="name" value="etl"/>
    <contextName>${name}</contextName>
    <appender name="console" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    <appender name="rollingFile" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>logs/${name}.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <fileNamePattern>logs/${name}.%d{yyyy-MM-dd}.log</fileNamePattern>
        </rollingPolicy>
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    <!-- project default level -->
    <logger name="cn.etl" level="info"/>
    <!-- 定义根日志级别 -->
    <root level="info">
        <appender-ref ref="rollingFile"/>
        <appender-ref ref="console"/>
    </root>
    <!--
        logger	description	since
        jdbc.sqlonly	Logs only SQL. SQL executed within a prepared statement is automatically shown with it's bind arguments replaced with the data bound at that position, for greatly increased readability.	1.0
        jdbc.sqltiming	Logs the SQL, post-execution, including timing statistics on how long the SQL took to execute.	1.0
        jdbc.audit	Logs ALL JDBC calls except for ResultSets. This is a very voluminous output, and is not normally needed unless tracking down a specific JDBC problem.	1.0
        jdbc.resultset	Even more voluminous, because all calls to ResultSet objects are logged.	1.0
        jdbc.connection	Logs connection open and close events as well as dumping all open connection numbers. This is very useful for hunting down connection leak problems.	1.2alpha1
     -->
    <logger name="jdbc.sqlonly" level="ERROR"/>
    <logger name="jdbc.sqltiming" level="INFO"/>
    <logger name="jdbc.audit" level="ERROR"/>
    <logger name="jdbc.resultset" level="ERROR"/>
    <logger name-"jdbc.resultsettable" level="INFO">
</configuration>
```
```
如果要打印sql日志,则需要加入一下配置
＃将驱动设置为log4jdbc的虚拟驱动
spring.datasource.driver-class-name=net.sf.log4jdbc.sql.jdbcapi.DriverSpy
＃url开头改为jdbc:log4jdbc
spring.datasource.url=jdbc:log4jdbc:mysql://127.0.0.1/etl?useUnicode=true&characterEncoding=utf-8&useSSL=true
#将log4jdbc的spylogdelegator改为Slf4jSpyLogDelegator接口，默认为Log4j2SpyLogDelegator
log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
```
