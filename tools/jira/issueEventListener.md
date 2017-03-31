## issueEventListener（jira:7.2）
#### 官方资料
* [issueEventListener文档](https://developer.atlassian.com/jiradev/jira-platform/guides/other/tutorial-writing-jira-event-listeners-with-the-atlassian-event-library)
* [demo](https://bitbucket.org/atlassian_tutorial/jira-event-listener/overview)
* [Class API](https://docs.atlassian.com/software/jira/docs/api/latest/com/atlassian/jira/event/issue/IssueEventListener.html)

#### 参考资料

* https://answers.atlassian.com/questions/39155501/event-listener-plugin-is-not-logging-issue-events

#### demo
* pom.xml

``` xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>${spring.core.version}</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>${spirng.security.core.version}</version>
    <scope>provided</scope>
</dependency>
```
---
``` xml
<properties>
    <jira.version>7.2.2</jira.version>
    <amps.version>6.2.11</amps.version>
    <plugin.testrunner.version>1.2.3</plugin.testrunner.version>
    <atlassian.spring.scanner.version>1.2.13</atlassian.spring.scanner.version>
    <spring.core.version>2.5.6.SEC01</spring.core.version>
    <spirng.security.core.version>3.1.0.RELEASE</spirng.security.core.version>
    <!-- This key is used to keep the consistency between the key in atlassian-plugin.xml and the key to generate bundle. -->
    <atlassian.plugin.key>${project.groupId}.${project.artifactId}</atlassian.plugin.key>
    <!-- TestKit version 6.x for JIRA 6.x -->
    <testkit.version>6.3.11</testkit.version>
</properties>
```

* module

``` Java
@ExportAsService
@Component
@Named("eventListener")
public class IssueCreatedResolvedListener implements InitializingBean, DisposableBean {

    private static final Logger log = LoggerFactory.getLogger(IssueCreatedResolvedListener.class);
    @ComponentImport
    private final EventPublisher eventPublisher;

    /**
     * Constructor.
     * @param eventPublisher injected {@code EventPublisher} implementation.
     */
    @Inject
    public IssueCreatedResolvedListener(EventPublisher eventPublisher) {
        System.out.println("IssueCreatedResolvedListener");
        this.eventPublisher = eventPublisher;
    }



    /**
     * Called when the plugin has been enabled.
     * @throws Exception
     */
    public void afterPropertiesSet() throws Exception {
        // register ourselves with the EventPublisher
        eventPublisher.register(this);
    }

    /**
     * Called when the plugin is being disabled or removed.
     * @throws Exception
     */
    public void destroy() throws Exception {
        // unregister ourselves with the EventPublisher
        eventPublisher.unregister(this);
    }

    /**
     * Receives any {@code IssueEvent}s sent by JIRA.
     * @param issueEvent the IssueEvent passed to us
     */
    @EventListener
    public void onIssueEvent(IssueEvent issueEvent) {
        System.out.println("onIssueEvent function");
        Long eventTypeId = issueEvent.getEventTypeId();
        System.out.println("eventTypeId:"+eventTypeId);
        Issue issue = issueEvent.getIssue();
        // if it's an event we're interested in, log it

        if (eventTypeId.equals(EventType.ISSUE_CREATED_ID)) {
            //新增bug
            System.out.println("ISSUE_CREATED_ID");
            log.info("Issue {} has been created at {}.", issue.getKey(), issue.getCreated());
        } else if (eventTypeId.equals(EventType.ISSUE_RESOLVED_ID)) {
            System.out.println("ISSUE_RESOLVED_ID");
            log.info("Issue {} has been resolved at {}.", issue.getKey(), issue.getResolutionDate());
        } else if (eventTypeId.equals(EventType.ISSUE_CLOSED_ID)) {
            System.out.println("ISSUE_CLOSED_ID");
            log.info("Issue {} has been closed at {}.", issue.getKey(), issue.getUpdated());
        } else if (eventTypeId.equals(EventType.ISSUE_UPDATED_ID)){
            //修改bug
            System.out.println("ISSUE_UPDATED_ID");
        } else if ( eventTypeId.equals( EventType.ISSUE_COMMENT_DELETED_ID ) ){
            //删除bug
        }else if (eventTypeId.equals(EventType.ISSUE_ASSIGNED_ID)){
            //修改指派人
            System.out.println("ISSUE_ASSIGNED_ID");
        } else if (eventTypeId.equals(EventType.ISSUE_GENERICEVENT_ID)){
            //修改bug状态
            System.out.println("ISSUE_GENERICEVENT_ID");
        } else if (eventTypeId.equals(EventType.ISSUE_COMMENTED_ID)){
            //新增comment
        } else if ( eventTypeId.equals( EventType.ISSUE_COMMENT_EDITED_ID ) ){
            //编辑comment
        } else if ( eventTypeId.equals( EventType.ISSUE_COMMENT_DELETED_ID ) ){
            //删除comment
        }
    }
}
```
