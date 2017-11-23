
****Note: Defining rules in extensions/rules folder in SonarQube server is no longer supported by this plugin****

## Extending rules in supported code analysers

If you're using a patched or not-yet-supported version of an integrated code checker (like Cppcheck), you probably want to see those new checks in SonarQube, too. To do this, you have 2 different approachs available.

### Using a xml definition ###

1. Define those rules using the XML format described further below in a temporary file.
2. Paste the content of file into the relevant configuration property in the SonarQube server. For example for cppcheck.
   ![UI Settings](images/custom-rules-configuation.png)
3. Restart the SonarQube server (This is the drawback of this method).
4. Make sure the newly added rules are visible in the quality profile; enable them
5. Run the analysis

####  Properties ####
  <table>
  <tr>
  <td><b>Property</b></td>
  <td><b>Description</b></td>
  </tr>
  <tr>
  <td>sonar.cxx.cppcheck.customRules</td>
  <td>Cppcheck Custom Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.valgrind.customRules</td>
  <td>Valgrind Custom Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.pclint.customRules</td>
  <td>PClint Custom Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.rats.customRules</td>
  <td>RATS Custom Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.vera.customRules</td>
  <td>Vera++ Custom Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.drmemory.customRules</td>
  <td>Dr Memory Analysis Rules</td>
  </tr>
  <tr>
  <td>sonar.cxx.other.rules</td>
  <td>Unsupported Code Checker Custom Rules, see below</td>
  </tr>
  <table>

### The format of the rules file
The format of rules file is expected to be the following ([RulesDefinitionXmlLoader](https://github.com/SonarSource/sonarqube/blob/master/sonar-plugin-api/src/main/java/org/sonar/api/server/rule/RulesDefinitionXmlLoader.java)):

V0.9.6 and later:
```XML
<rules>
  <rule>
    <!-- Required key. Max length is 200 characters. -->
    <key>the-rule-key</key>

    <!-- Required name. Max length is 200 characters. -->
    <name>The purpose of the rule</name>

    <!-- Required description. No max length. -->
    <description>
      <![CDATA[The description]]>
    </description>
    <!-- Optional format of description. Supported values are HTML (default) and MARKDOWN. -->
    <descriptionFormat>HTML</descriptionFormat>

    <!-- Optional key for configuration of some rule engines -->
    <internalKey>Checker/TreeWalker/LocalVariableName</internalKey>

    <!-- Default severity when enabling the rule in a Quality profile.  -->
    <!-- Possible values are INFO, MINOR, MAJOR (default), CRITICAL, BLOCKER. -->
    <severity>BLOCKER</severity>

    <!-- Possible values are SINGLE (default) and MULTIPLE for template rules -->
    <cardinality>SINGLE</cardinality>

    <!-- Status displayed in rules console. Possible values are BETA, READY (default), DEPRECATED. -->
    <status>BETA</status>

    <!-- Type as defined by the SonarQube Quality Model. Possible values are CODE_SMELL (default), BUG and VULNERABILITY.-->
    <type>BUG</type>

    <!-- Optional tags. See org.sonar.api.server.rule.RuleTagFormat. The maximal length of all tags is 4000 characters. -->
    <tag>misra</tag>
    <tag>multi-threading</tag>

    <!-- Optional parameters -->
    <param>
      <!-- Required key. Max length is 128 characters. -->
      <key>the-param-key</key>
      <description>
        <![CDATA[the optional description, in HTML format. Max length is 4000 characters.]]>
      </description>
      <!-- Optional default value, used when enabling the rule in a Quality profile. Max length is 4000 characters. -->
      <defaultValue>42</defaultValue>
    </param>
    <param>
      <key>another-param</key>
    </param>

    <!-- Quality Model - type of debt remediation function -->
    <!-- See enum {@link org.sonar.api.server.debt.DebtRemediationFunction.Type} for supported values -->
    <!-- It was previously named 'debtRemediationFunction' which is still supported but deprecated since 5.5 -->
    <!-- Since 5.5 -->
    <remediationFunction>LINEAR_OFFSET</remediationFunction>

    <!-- Quality Model - raw description of the "gap", used for some types of remediation functions. -->
    <!-- See {@link org.sonar.api.server.rule.RulesDefinition.NewRule#setGapDescription(String)} -->
    <!-- It was previously named 'effortToFixDescription' which is still supported but deprecated since 5.5 -->
    <!-- Since 5.5 -->
    <gapDescription>Effort to test one uncovered condition</gapFixDescription>

    <!-- Quality Model - gap multiplier of debt remediation function. Must be defined only for some function types. -->
    <!-- See {@link org.sonar.api.server.rule.RulesDefinition.DebtRemediationFunctions} -->
    <!-- It was previously named 'debtRemediationFunctionCoefficient' which is still supported but deprecated since 5.5 -->
    <!-- Since 5.5 -->
    <remediationFunctionGapMultiplier>10min</remediationFunctionGapMultiplier>

    <!-- Quality Model - base effort of debt remediation function. Must be defined only for some function types. -->
    <!-- See {@link org.sonar.api.server.rule.RulesDefinition.DebtRemediationFunctions} -->
    <!-- It was previously named 'debtRemediationFunctionOffset' which is still supported but deprecated since 5.5 -->
    <!-- Since 5.5 -->
    <remediationFunctionBaseEffort>2min</remediationFunctionBaseEffort>

    <!-- Deprecated field, replaced by "internalKey" -->
    <configKey>Checker/TreeWalker/LocalVariableName</configKey>

    <!-- Deprecated field, replaced by "severity" -->
    <priority>BLOCKER</priority>

  </rule>
</rules>
```

Example:
```XML
<rules>
  <rule>
    <key>S1442</key>
    <name>"alert(...)" should not be used</name>
    <description>alert(...) can be useful for debugging during development, but ...</description>
    <tag>cwe</tag>
    <tag>security</tag>
    <tag>user-experience</tag>
    <debtRemediationFunction>CONSTANT_ISSUE</debtRemediationFunction>
    <debtRemediationFunctionBaseOffset>10min</debtRemediationFunctionBaseOffset>
  </rule>

  <!-- another rules... -->
</rules>
```

It is also possible to add hyperlinks to the description, use ```<a>``` tags.
```HTML
<description>
  <![CDATA[<a href="http://example.com/xyz.html">Link</a>]]>
</description>
```

Deprecated but still supported:
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

### Deprecated: SQALE characteristics (only V0.9.4, V0.9.5) ###
Starting with the version 0.9.4 it is also possible to define SQALE characteristics for other rules. To define the SQALE characteristics an extra XML file has to be defined and assigned to ```sonar.cxx.other.sqales```. Assign the XML file on server side to the configuration property on the page 'C++ settings / (2) Code analysis' and restart the server to enable it (same as with rule definitions). The XML file must fit the [XML schema for SQALE characteristics](https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/main/resources/com/sonar/sqale/cxx-model-project.xsd). For more complex examples have a look to the folder [SQALE](https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/main/resources/com/sonar/sqale/).

Example:

```XML
<sqale>
  <chc>
    <key>PORTABILITY</key>
    <name>Portability</name>
    <chc>
      <key>COMPILER_RELATED_PORTABILITY</key>
      <name>Compiler related portability</name>
      <chc>
        <rule-repo>other</rule-repo>
        <rule-key>key</rule-key>
        <prop>
          <key>remediationFunction</key>
          <txt>linear_offset</txt>
        </prop>
        <prop>
          <key>remediationFactor</key>
          <val>5</val>
          <txt>mn</txt>
        </prop>
        <prop>
          <key>offset</key>
          <val>10</val>
          <txt>mn</txt>
        </prop>
      </chc>
    </chc>
  </chc>
</sqale>
```

Example of Levels 1 and 2 of a [SQALE Quality Model](http://www.sqale.org/wp-content/uploads/2010/08/SQALE-Method-EN-V1-0.pdf):

### Using Template Rules ###
This method allows the creation of rules on the fly, no need to for server restart. To do this follow these steps.

1. Locate the relevant custom rule for the code checker you want to extend.
![Custom Rules Settings](images/create-custom-rule.png)
2. Press create and fill in the details 
![Custom Rules Settings](images/customrule.png)
3. Enable the rule and run a new analysis 

*These rules can be created using the rest api, see [https://github.com/jmecsoftware/QualityProfileEditorPlugin](https://github.com/jmecsoftware/QualityProfileEditorPlugin "Quality Editor Plugin") as an example*

## Usage of unsupported code checkers ##
If you're using a code checker which is **not** supported by the plugin, this feature is for you. It allows to feed violations into SonarQube in a code checker agnostic way. To do this follow the steps below:

1. Create a XML file describing the rules and place it in code analysis settings of the plugin in the SonarQube server under the property sonar.cxx.other.rules
   ![UI Settings](images/external-custom-rules-configuation.png)
   Use the format described above. You can import multiple custom rules by clicking the Add value and save the settings

2. Run your checker and create a report

3. Transform the report such that it conform to the following RNG schema:
   ```XML
   <element name="results" xmlns="http://relaxng.org/ns/structure/1.0">
     <zeroOrMore>
       <element name="error">
         <attribute name="file"/>
         <attribute name="msg"/>
         <attribute name="id"/>
         <attribute name="line">
           <data type="integer" datatypeLibrary="http://www.w3.org/2001/XMLSchema-datatypes" />
         </attribute>
         <text/>
       </element>
     </zeroOrMore>
   </element>
   ```

  Where the fields have the following semantics:

  <table>
  <tr>
  <td><b>Tag/Attribute</b></td>
  <td><b>Semantic</b></td>
  </tr>

  <tr>
  <td>file</td>
  <td>Source file, relative to project path</td>
  </tr>

  <tr>
  <td>line</td>
  <td>Line number where the violation occurres</td>
  </tr>

  <tr>
  <td>id</td>
  <td>The ID of the violated SonarQube rule</td>
  </tr>

  <tr>
  <td>msg</td>
  <td>Description of the violation</td>
  </tr>
  <table>
4. Set the property **sonar.cxx.other.reportPath** to point to the location of transformed report (relative to project root) and run one analysis.


### Resources

Below you find a list of code analyzers which have already been integrated using this feature and according resources. The setups have been proven to work in one particular environment; you may need to adapt it to make work in yours.


<table>
<tr>
<td>Tool</td>
<td>Usage</td>
</tr>

<tr>
<td><a href="http://google-styleguide.googlecode.com/svn/trunk/cpplint/cpplint.py">cpplint</a></td>
<td>
<ol>
<li>Create the rules profile using the <a href="https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/tools/cpplint_createrules.py">profile creator script</a>:
<br>
<code>python cpplint_createrules.py cpplint.py</code>
<br>
This will generate the following files:
<ul>
<li>
<b>cpplint.xml</b>: that should be copied to web ui as per above and server restarted after save
</li>
<li>
<b>cpplint_mod.py</b>: that should be used to check the code
</li>
<br>
</li>
<li>
After this you can run the cpplint_mod.py against any source file like this:
<br>
<code>python cpplint_mod.py source.cpp 2> report.txt</code>
<br>
The output file report.txt needs to be converted to the XML format described above. For convenience a Perl script is available
<a href="https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/tools/cpplintReport2checkstyleReport.perl">here</a>
and can be run as follows:
<code>perl cpplintReport2checkstyleReport.perl report.txt splint-result-0.xml</code>
</li>
</td>
</tr>

<tr>
<td><a href="http://software.intel.com/en-us/intel-inspector-xe">Intel Inspector XE 2013</a></td>
<td>

<ol>
<li>Copy the
<a href="https://github.com/wenns/sonar-cxx/blob/master/sonar-cxx-plugin/src/main/resources/external/intel_inspector_rules.xml">Intel Inspector rules</a>
to sonar web ui, as per above and restart server.
</li>
<li>Modify the used SonarQube quality profile to accommodate the newly added rules</li>
<li>Run your test/application using the Intel Inspector and generate a CSV report</li>
<li>Convert the report with:
<code>python <a href="">intelInspectorReport_2_cppcheckReport.py</a>
in.csv out.xml <path to project> <test executable></code>
The out.xml can be then used during the analysis to feed the Intel Inspector results into
SonarQube.
</li>
</td>
</tr>
</table>


## Writing your own rules using SSLR, aka custom cxx-rules

You can write custom rules based in SSLR and in Cxx Api, to do this you need to create your own plugin and create a dependency in you pom.xml to the Cxx Plugin version you are using. And extend your checks with CustomCxxRulesDefinition

```
    <dependency>
      <groupId>org.codehaus.sonar-plugins.cxx</groupId>
      <artifactId>sonar-cxx-plugin</artifactId>
      <type>sonar-plugin</type>
      <version>0.9.5-SNAPSHOT</version>
      <scope>provided</scope>
    </dependency>
```

### Example of a rule
```
public class MyCustomRulesDefinition extends CustomCxxRulesDefinition {

  @Override
  public String repositoryName() {
    return "Repository";
  }

  @Override
  public String repositoryKey() {
    return "repo";
  }

  @SuppressWarnings("rawtypes")
  @Override
  public Class[] checkClasses() {
    return new Class[] { UsingNamespaceCheck.class };
  }
}
```

### Installation and usage
Follows a normal procedure for any Sonar plugin, drop in extensions/plugins in you Sonar server and restart. After this enable the rules and run a new analysis.

### Sample code
You can use the https://github.com/SonarOpenCommunity/cxx-custom-checks-example-plugin as a base for your rules, kudos @felipebz
