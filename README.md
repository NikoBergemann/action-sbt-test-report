# SBT TEST REPORT

this action will run dedicated tests with the sbt command and gernerate reports for coverage and test-results.

Parameterize the action with the tests you want to run, like this.

```yaml
    # Run Tests
    - name: run tests with coverage and reports
      uses: /NikoBergemann/action-sbt-test-report@v3
      with:
        what-to-test: '*ManagerTests *CourseAccessTests'
```

Note that 
1. The action will only run when the current directory contains the build.sbt that you want to run.
2. The tests referenced need to be specified with their qualified relative path. Or with an asterix to work around that :) 
3. The testReports will be generated to the /target folder a usual.
4. Your scala project need to include the coverage and report utilities.

```sbt
// -- project/plugins.sbt
addSbtPlugin("org.scoverage" % "sbt-scoverage" % "1.6.0")
```
>! note that scoverage version 1.6 is the required minimum version for the coverageAggregate to work

```sbt
// -- build.sbt
// libraries
private val scalaTest = "org.scalatest" %% "scalatest" % "3.2.0" % Test
private val flexmark = "com.vladsch.flexmark" % "flexmark-all" % "0.35.10" % Test

// dependency groups
val scalaTestDependencies = Seq(scalaTest, flexmark)

// reference in project
lazy val myproject = (project in file("."))
.settings(
  libraryDependencies ++= Dependencies.scalaTestDependencies
)
```
