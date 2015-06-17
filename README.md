# nuxeo-dynamic-renderer-widgets-plugin
This plugin creates some widget types to be used in other Nuxeo plugins. This widget types updates the current tab when it's value is changed.

## Installation

Just download & compile the pom.xml using Maven and deploy the plugin in 
```{r, engine='bash', count_lines}
cd nuxeo-dynamic-renderer-widgets-plugin
mvn clean install
cp target/dynamicRendererWidgets-*.jar $NUXEO_HOME/nxserver/plugins
```

## Use
In your custom plugin, when defining your widgets, use the new widgetTypes available.

```xml
			<widget name="myCheckboxRenderer" type="dynamicRendererWidget_checkbox">
				<labels>
					<label mode="any">label.myCheckboxRenderer</label>
				</labels>
				<translated>true</translated>
				<fields>
					<field>MyType:myCheckboxRenderer</field>
				</fields>
			</widget>
```

Then, restart your nuxeo server. When you change the value of your widget/field, the tab will be re-rendered to show the changes in the layout. This is specially useful when you have some widgets hidden depending on your special field's value. 
For example:
```xml
			<widget name="maybeHiddenField" type="datetime">
				<labels>
					<label mode="any">label.maybeHiddenField</label>
				</labels>
				<translated>true</translated>
				<fields>
					<field>MyType:maybeHiddenField</field>
				</fields>
				<widgetModes>
          			<mode value="create">#{layoutValue.MyType:myCheckboxRenderer?'hidden':'edit'}</mode>
          			<mode value="edit">#{layoutValue.MyType:myCheckboxRenderer?'hidden':'edit'}</mode>
          			<mode value="view">#{layoutValue.MyType:myCheckboxRenderer?'hidden':'view'}</mode>
        		</widgetModes>
			</widget>
```
## Widget Types
When you deploy this plugin in Nuxeo, all these new widget types will be available:
- dynamicRendererWidget_checkbox
