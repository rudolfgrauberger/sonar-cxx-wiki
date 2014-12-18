## Getting ready

When time passes and you get the feeling its time for a new release,
things are usually not in the shape they should be. To actually get to
the point where we can think about a release, make sure that:

* The according
  [milestone](https://github.com/wenns/sonar-cxx/milestones) is
  ready. If necessary, exclude issues which haven't been solved in
  time.
* All issues assigned to the milestone have sound names, sound labels
  ('bugs' are actually bugs, e.g.) are assigned to the developer who
  solved them (this makes sense even after the work is done, just as
  documentation), i.e.: are overall consistent.
* Changes introduced by this release are documented in the Wiki. Especially:
  * All changes on [configuration switches](Supported configuration
    properties) are documented
  * A new row to the [compatibility matrix](SonarQube-compatibility-matrix) is added
* Missing authors are added to to the list of developers in the
  [pom.xml](https://github.com/wenns/sonar-cxx/blob/master/pom.xml)
* Consider extending the tests, especially the
  [integration](https://github.com/wenns/sonar-cxx/tree/master/integration-tests)
  ones, especially having the new features in mind
* The [CI build](https://travis-ci.org/wenns/sonar-cxx) is
  green. Additionally: make sure the integration tests do pass for all
  SQ versions, which are mentioned in the compatibility matrix
* The source code quality of the plugin is acceptable. Use
  SonarQube as a tool for that.
* The [sample project](https://github.com/wenns/sonar-cxx/tree/master/sonar-cxx-plugin/src/samples/SampleProject2)
still works with the latest build
* The <parent>-section in the pom.xml references a recent version of the parent pom.
* Core users did some field testing and didn't found any serious issues

## Release Procedure
* Create and describe the release in Github, use the format of
  previous releases, i.e.
  * compose a list of fixed bugs
  * compose a list of enhancements
  * don't forget to thank to the contributors
* Change the plugin version in the pom.xml, make sure the version
  string contains no 'SNAPSHOT'
* Build and attach the resulting jars to the release on Github.
* Publish the release
* Make a tag in git
* Adjust the 'recent release'-Link in Readme.md
* Tweet/Announce
