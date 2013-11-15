## Extending rules in supported code analysers

If you're using a patched or not-yet-supported version of an integrated code checker (like Cppcheck), you probably want to see those new checks in SonarQube, too. To do this, you have to:

1. Define those rules using the XML format described further below in a file "rules.xml"
2. Place this file in a directory matching the name of the analyzer under _$SONARQUBEHOME\extensions\rules_; e.g. for Cppcheck, the rules file would be expected to be here: 
```BASH
$SONARQUBEHOME\extensions\rules\cppcheck\rules.xml
```

3. Restart the SonarQube server
4. Make sure the newly added rules are visible in the quality profile; enable them
5. Run the analysis

### The format of the rules file
The format of rules file is expected to be the following:

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
