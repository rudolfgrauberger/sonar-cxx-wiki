## Extending rules in supported code analysers

If you're using a patched or not-yet-supported version of an integrated code checker (like Cppcheck), you probably want to see those new checks in SonarQube, too. To do this, you have to:

1. Define those rules using the XML format described further below in a file "rules.xml"
2. Paste the content of file into the relevant configuration property in the SonarQube server.
   ![Ui Settings](images/custom-rules-configuation.png)
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


## Usage of unsupported code checkers
If you're using a code checker which is **not** supported by the plugin, this feature is for you. It allows to feed violatios into SonarQube in a code checker agnostic way. To do this follow the steps below:

1. Create a XML file describing the rules and place it in global setting in the SonarQube server under sonar.cxx.customRules.cxxexternal
   ![Ui Settings](images/external-custom-rules-configuation.png)
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
4. Set the property **sonar.cxx.externalrules.reportPath** to point to the location of transformed report (relative to project root) and run one analysis.


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
<b>cpplint.xml</b>: that should be copied to $SONARQUBEHOME/extensions/rules/cxxexternal
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
to $SONARQUBEHOME/extension/rules/cxxexternal and restart the server
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