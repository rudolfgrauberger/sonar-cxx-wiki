If you're using a code checker which is **not** supported by the plugin, this feature is for you. It allows to feed violatios into Sonar in a code checker agnostic way. To do this follow the steps below:

1. Create and install a rule set
Create a XML file describing the rules and copy it to the directory 
_$SONARQUBEHOME\extensions\rules\cxxexternal_. Use the format described in [[Extending rules in code analysers]].

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

4. Set the property **sonar.cxx.externalrules.reportPath** to point to the location of transformed report (relative to project root). 

5. Run the analysis


## Resources

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