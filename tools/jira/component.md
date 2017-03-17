## jira模块
#### 命令行查看模块种类
```
atlas-create-jira-plugin-module
```
> 通过命令可以看到，jira提供了34种模块类型

#### 模块描述
1.  **Component Import**
> Component Import plugin modules allow you to access Java components shared by other plugins, even if the component is upgraded at runtime.
2.  **Component**
> Component plugin modules enable you to share Java components between other modules in your plugin and optionally with other plugins in the application. You can use it to make any type of class instance available to other plugins or modules. It's in effect a Spring bean declaration (with greatly simplified syntax, since only autowiring is supported) plus an OSGi export.

*The typical uses of a component are:*
* To define a singleton class that's used internally by your plugin, which the framework instantiates for you and passes to your other classes via autowiring; or
* To expose an API to other plugin modules.
3.  Component Tab Panel
> Adds new tabs to the Browse Component page.
4.  Custom Field
> Defines a custom field and its type.
5.  Custom Field Searcher
> Defines a search method for indexing a custom field.
6.  Downloadable Plugin Resource
7.  Gadget Plugin Module
> Defines an Atlassian gadget provided by this plugin.
8.  Issue Tab Panel
> Adds new tabs to the View Issue panel.
9.  Keyboard Shortcut
10. JQL Function
> Defines new functions for use in the JIRA Query Language (JQL).
11. Licensing API Support
12. Module Type
13. Project Tab Panel
> Adds new tabs to the Browse Projects page.
14. REST Plugin Module
> Exposes data and services as REST resources.
15. RPC Endpoint Plugin
16. Report
> Defines a report in JIRA.
17. Search Request View
> Allows display of search results in the issue navigator in custom formats (such as XML or MS Excel format).
18. **Servlet Context Listener**
> Servlet Context Listener plugin modules allow you to deploy Java Servlet context listeners as a part of your plugin. This helps you to integrate easily with frameworks that use context listeners for initialisation.
19. **Servlet Context Parameter**
> Servlet Context Parameter plugin modules allow you to set parameters in the Java Servlet context shared by your plugin's servlets, filters, and listeners.
20. **Servlet Filter**
> Servlet Filter plugin modules allow you to deploy Java Servlet filters as a part of your plugin, specifying the location and ordering of your filter. This allows you to build filters that can tackle tasks like profiling and monitoring as well as content generation.
21. **Servlet**
> Servlet plugin modules enable you to deploy Java servlets as a part of your plugins.
22. **Template Context Item**
> This module type allows you to put arbitrary context items into the context of any Using the Atlassian Template Renderer. This is useful to ensure plugin developers don't have to repeatedly create the same context each time they need to render content.

*This module type is similar to the Confluence velocity-context-item module type. However, it is more powerful in the following ways:*
* It can be used with any template rendering technology, not just velocity
* It allows items to be scoped in the context of the plugin that declares it, or to be in the global context of all plugins
* It allows referencing of arbitrary components, not just classes. This means you don't need to create wrapper classes if you want to put a general component (such as the SAL I18nResolver) in your context. It also means you can use Spring prototype beans if you want to use some per context stateful bean
23. User Format
24. Version Tab Panel
> Adds new tabs to the Browse Version page.
25. **Web Item**
> Web Item plugin modules allow plugins to define new links in application menus.
26. **Web Panel**
> Web Panel plugin modules allow plugins to define panels, or sections, on an HTML page. A panel is a set of HTML that will be inserted into a page.
27. Web Panel Renderer
> Defines a custom rendering engine for a <web-panel>.
28. Web Resource
> Defines downloadable resources (files) for a plugin, such as CSS or JavaScript files.
29. Web Resource Transformer
> Defines transformers which allow changing web resources before being served to the browser.
30. Web Section
> Defines a new section in an application menu.
31. Webwork Plugin
32. Workflow Condition
> Checks whether a user can perform a workflow transition.
33. Workflow Post Function
> Performs actions after a workflow transition has executed.
34. Workflow Validator
> Checks that the data supplied to a workflow transition is valid.
