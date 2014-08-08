TRX to XML Parser
==========

A parser for converting .trx files generated by the execution of Unit Tests for .NET projects by MSTest, to maven-surefire compatible .xml file.

Sample TRX input :
---

    <?xml version="1.0" encoding="UTF-8" ?>
    <TestRun id="" name="" runUser="" xmlns="http://microsoft.com/schemas/VisualStudio/TeamTest/2010">
        ...
        <Times creation="2014-08-06T18:13:44.9423872+05:30" queuing="2014-08-06T18:13:45.4050385+05:30" start="2014-08-06T18:13:45.4760768+05:30" finish="2014-08-06T18:13:46.4626810+05:30" />
        <ResultSummary outcome="Failed">
            <Counters total="132" executed="132" passed="112" error="1" failed="15" timeout="0" aborted="0" inconclusive="4" passedButRunAborted="0" notRunnable="0" notExecuted="0" disconnected="0" warning="0" completed="0" inProgress="0" pending="0" />
        </ResultSummary>
        <TestDefinitions>
            <UnitTest name="sampleTest" storage="sample.test.dll" id="">
                <Execution id="" />
                <TestMethod codeBase="path/to/sample.test.dll" adapterTypeName="" className="Sample.Test.SampleTest, Sample.Test, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" name="sampleTest" />
            </UnitTest>
            <UnitTest name="testMethod" storage="sample.test.dll" id="">
                <Execution id="" />
                <TestMethod codeBase="path/to/sample.test.dll" adapterTypeName="" className="Sample.Test.SampleTest, Sample.Test, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" name="testMethod" />
            </UnitTest>
            ...
        </TestDefinitions>
        ...
        <Results>
            <UnitTestResult executionId="" testId="" testName="SampleTest" computerName="" duration="00:00:00.0541128" startTime="2014-08-06T18:13:45.5001065+05:30" endTime="2014-08-06T18:13:45.7012120+05:30" testType="" outcome="Inconclusive" testListId="" relativeResultsDirectory="">
                <Output>
                    <ErrorInfo>
                        <Message>Assert.Inconclusive failed. TODO: Implement code to verify target</Message>
                        <StackTrace>at Sample.Test.SampleTest.SampleTest() in path\to\SampleTest.cs:line 82</StackTrace>
                    </ErrorInfo>
                </Output>
            </UnitTestResult>
            <UnitTestResult executionId="" testId="" testName="TestMethod" computerName="" duration="00:00:00.0001557" startTime="2014-08-06T18:13:46.3355910+05:30" endTime="2014-08-06T18:13:46.3365922+05:30" testType="" outcome="Passed" testListId="" relativeResultsDirectory="">
            </UnitTestResult>
        </Results>
    </TestRun>

Sample XML output :
---
```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<testsuite errors="1" failures="15" name="TestSuite" skipped="4" tests="132" time="0.986">
    <testcase classname="Sample.Test.SampleTest" name="SampleTest" time="201">
        <failure type="Inconclusive">Assert.Inconclusive failed. TODO: Implement code to verify target</failure>
    </testcase>
    <testcase classname="Sample.Test.SampleTest" name="TestMethod" time="88"/>
</testsuite>
```
