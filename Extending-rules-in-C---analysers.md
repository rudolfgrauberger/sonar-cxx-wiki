From version 0.2, its possible to extend the rules available in quality profiles for any tool. To do this a directory matching the tool name and a XML with the description of the rules within this directory should be provided. For example, in case of Cppcheck the path would be:

_$SONARQUBEHOME\extensions\rules\cppcheck\rules.xml_

The format of the XML file is expected to be the following:

```XML
<rules> 
<rule key="RULE_ID">
<name><![CDATA[ ... put here the human readable name of this rule ... ]]></name>
<configKey><![CDATA[RULE_ID@$(EXTERNALSENSORCLASS)]]></configKey>
<category name=" ... category type ... " />
<description><![CDATA[ ... put here the human readable description of this rule ... ]]></description>
</rule>
</rules>
```

Where the fields have the following semantics:

<table>
<tr>
<td><b>Tag/Attribute</b></td>
<td><b>Semantic</b></td>
</tr>

<tr>
<td>key [RULE_ID]</td>
<td>Id of the rule, should match the ID in the external reports</td>
</tr>

<tr>
<td>name</td>
<td>Can be really anything, in the quality profile in SonarQube its the first name that is displayed per rule</td>
</tr>

<tr>
<td>configKey</td>
<td>This key is used later by the sensor to configure the code analyzer ([Extending+Coding+Rules] (http://docs.codehaus.org/display/SONAR/Extending+Coding+Rules)) </td>
</tr>

<tr>
<td>category name</td>
<td>Can be anything, examples include Maintainability Style Usability etc</td>
</tr>

<tr>
<td>description</td>
<td>In the quality profile in SonarQube UI, the description will be show after expanding each rule</td>
</tr>

</table>

Example:

```XML
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<rules>
<rule key="Te0001DataContextCannotBeSet">
<name><![CDATA[Te0001DataContextCannotBeSet]]></name>
<configKey>
<![CDATA[Te0001DataContextCannotBeSet@PC_LINT]]>
</configKey>
<category name="Maintainability" />
<description>
<![CDATA[ Data Context Should no be set, please use another approach ]]>
</description>
</rule>
</rules>
```

**_Important: Once rules have been added to extensions/rules, they should be enabled in the relevant quality profile in SonarQube. Only after this has been done, the analysis can be performed_**