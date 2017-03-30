## 自定义字段
#### jira版本：7.2
> 后端：由于spring scanner技术，低版本引入component-import的方式无法使用，需要使用``` @sanner ```和``` @component-import ```

``` Java
@Scanned
public class emtcField extends TextCFType {
    private static final Logger log = LoggerFactory.getLogger(emtcField.class);

    public emtcField(@ComponentImport CustomFieldValuePersister customFieldValuePersister,@ComponentImport GenericConfigManager genericConfigManager) {
        super(customFieldValuePersister,genericConfigManager);
    }

    @Override
    public Map<String, Object> getVelocityParameters(final Issue issue,
                                                     final CustomField field,
                                                     final FieldLayoutItem fieldLayoutItem) {
        final Map<String, Object> map = super.getVelocityParameters(issue, field, fieldLayoutItem);

        if (issue == null) {
            return map;
        }

         FieldConfig fieldConfig = field.getRelevantConfig(issue);
         //add what you need to the map here

        return map;
    }
}
```
