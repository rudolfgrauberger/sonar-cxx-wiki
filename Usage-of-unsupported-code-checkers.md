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

3. Set the property **sonar.cxx.externalrules.reportPath** to point to the location of transformed report (relative to project root). 

4. Run the analysis

Importing the violation report for the external tool

The property sonar.cxx.externalrules.reportPath is used to point to the location of the report (relative to project root). The following table describes the format of the report

Xml Description - RNG-Schema

Example
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
<?xml version="1.0"?>
<results>
<error file="sources/utils/code_chunks.cpp" line="1" id="cxxexternal-unusedFunction" msg="The function 'foo' is never used"/>
<error file="sources/utils/utils.cpp" line="1" id="cxxexternal-unusedFunction" msg="The function 'utils' is never used"/>
</results>
Attribute	
Description
file	source file, relative to project path
line	line of the violation
id	id of the rule, mapped a rule in SonarQube. See "Enable the rules in SonarQube server" below
msg	description of the violation
List of third party tools and their profiles
Tool
Source
Usage
Rules Profile / Needed scripts
cpplint	
Home Page
Download Tool
Create the rules profile and the modified cpplint python script as follow:
python cpplint_createrules.py cpplint.py
This will generate the following files:
cpplint.xml that should installed in extensions/rules/cxxexternal
cpplint_mod.py that should be used to check the code
After this you can run the cpplint_mod.py against any source file like this:
python cpplint_mod.py source.cpp 2> report.txt
The output file report.txt needs to be converted to xml format described above. For convenience a perl script is available here and can be run as follow:
perl cpplintReport2checkstyleReport.perl report.txt cpplint-result-0.xml
Create Rules Script
CppLint Report Converter Script
intel inspector XE 2013	Product Home Page	
Using the intelInspectorReport_2_cppcheckReport
Install the profile under [SonarQube Server]/extension/rules/cxxexternal and restart the server
Modify the in use quality profile in SonarQube Server to accommodate the newly added rules

Run your test/application using intel inspector and generate a csv report. Refer to product manual to on how to do it.
Run the convert of the csv file as follow:
python intelInspectorReport_2_cppcheckReport.py report.csv convertedfile.xml /path/to/root/of/project testexecutable.exe
The convertedfile.xml can be than used during the analysis to populate intel inspector results into sonar.
Using MSbuild for windows users
See wiki on MSBuild-SonarQube-CXX
Profile
Csv Convert Tool
Icon
This is maintained by the community, so if you want to share additional rules profiles or tool do so by using the user mailing list
Icon
The list above is provided without any warranty, therefore you may need to debug the scripts or tools in order to make them work