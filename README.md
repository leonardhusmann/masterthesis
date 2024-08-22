# DEGREE PROJECT PROPOSAL

## NAME AND E-MAIL ADDRESS OF THE STUDENT
Leonard Sebastian Husmann
(husmann@kth.se)


## THESIS TITLE
Detecting Semantic Changes in Dependency Updates Using Dynamic Analysis


## BACKGROUND
External dependencies are an inevitable part of modern software projects.
With these external dependencies and their own release cycles comes the necessity for quick assessment of dependency updates.
On the one hand, developers want the new features, performance improvements and security fixes of the new versions.
On the other hand, they need to assess quickly if the new version introduces breaking changes and could therefore lead to a regression of their own package.

While there are approaches focusing on breaking changes manifesting as compile errors, there are no tools/techniques focusing on effectively detecting semantic changes.
Tools like dependabot or renovate rely on the client's test suite to determine if an update is safe or not.
But this depends heavily on the quality of the client's test suite.
Hejderup & Gousious (2022) have shown that the median coverage of external dependencies is 58% (mean: 55%) and therefore significantly lower than the typical coverage of own code.
David et al. (2022) have shown that dynamic approaches are of interest as they can improve the accuracy of detecting semantic changes.
This brings rise to the question if test cases of the dependencies can be used to detect possible semantic changes affecting client packages.


## PROBLEM STATEMENT
Every new release of an external dependency comes with changes.
It is the developer's responsibility to assess if the introduced changes of the dependency can lead to a degradation of their own package.
Current and well known approaches like dependabot and renovate rely on the test suite of a package and can therefore only detect changes covered by tests.
Test coverage of external dependencies is usually low (Hejderup & Gousious).

This thesis aims to implement and evaluate an approach which detects semantic changes of external dependencies beyond the coverage of the package's test suite.
Such a technique gives developers a better understanding if their own package is affected by changes which would not have been discovered by previous approaches.
This allows developers to update dependencies quicker and with more confidence.

## RESEARCH QUESTIONS

### RQ1
How can dependency test cases be used to detect semantic changes in dependency updates using dynamic analysis?

This includes the implementation of the tool.
Open questions are if source code of dependencies is always and easily available and if it includes a test suite.
The next step is to determine which of the functionality of the dependency is actually used by the package, the test cases of these functions must then be located in the dependency's test suite.
As a last step these test cases are then analyzed for semantic changes using dynamic analysis techniques.
Possible techniques are checking for return values or assessing the state of objects for each version but further assessed in RQ2.

### RQ2
Which dynamic analysis techniques can be used to detect semantic changes?

Different dynamic analysis techniques must be evaluated how applicable they are in this context.
In this context there are always two results of the dynamic analysis (one for the old and one for the new version of the dependency).
To answer this question, it is necessary to evaluate how well semantic changes can be recognized from this diff of the output.

### RQ3
How effective is said tool in detecting semantic changes and what are the most predominant groups of semantic changes?

BUMP can be used to measure the effectiveness of the tool.
Especially the dependency updates which are failing because of failed test assertions are of interest.
The dependency updates which are known to cause a failed test assertion are executed using the tool.
If the tool detects semantic changes, we call this a true positive.
If it fails to detect changes, we call this a false negative.
This allows for measuring the effectiveness of the tool based on precision and recall.

### RQ4
To what extent does automatic test suite augmentation help if dependencies' test suites are missing?

If an external dependency does not offer a test suite (or one of low quality), this must be generated or augmented.
There are several approaches to generating/augmenting test cases automatically ([dspot](https://github.com/STAMP-project/dspot), [unit-test-generator](https://github.com/audreycj/unit-test-generator)).
To answer the question, dependencies without test suites (or low quality test suites) must be found.
Test cases can then be generated for them and the tool is executed again with the newly generated test cases.
The effectiveness can then be evaluated according to RQ3.


## RESEARCH METHOD
The core of this project is a tool which needs to be developed.
This tool is given two versions of a specific maven dependency and returns if a semantic change occurred and therefore classifies the update as either 'safe' or 'unsafe'.

The tool will execute all the test cases of the dependency for each respective version.
Comparing the return values of the methods of each respective version allows to determine if the dependency behaves differently after the update.
Structural changes must be filtered out.

The classified dependency updates (classified as either 'safe' or 'unsafe') can then be evaluated using BUMP.
BUMP serves as ground truth for the evaluation.
Important to note is that only the test cases failing because of a failed assertion are of interest here.
Failed test cases because of compilation errors cannot be used.
A dependency update is correctly marked as 'unsafe' if the build fails after the update because of a failed assertion in BUMP.


## SUGGESTED EXAMINER AT KTH
Martin Monperrus


## SUGGESTED SUPERVISOR AT KTH
- Frank Reyes García
- César Soto Valero


## RESOURCES
- BUMP for benchmarking (Reyes, F., Gamage, Y., Skoglund, G., Baudry, B., & Monperrus, M. (2024). BUMP: A Benchmark of Reproducible Breaking Dependency Updates. https://doi.org/10.1109/SANER60148.2024.00024)
- Hejderup, J., & Gousios, G. (2022). Can we trust tests to automate dependency updates? A case study of Java Projects. Journal of Systems and Software, 183, 111097. https://doi.org/10.1016/J.JSS.2021.111097
- David, Y., Sun, X., Sofaer, R. J., Senthilnathan, A., Yang, J., Zuo, Z., Xu, G. H., Nieh, J., & Gu, R. (2022). UPGRADVISOR: Early Adopting Dependency Updates Using Hybrid Program Analysis and Hardware Tracing. http://upgradvisor.github.io.


## ELIGIBILITY
I have completed all courses prior to the degree project.
This includes more than 60 credits at second cycle level as well as a course in theory of knowledge and research methodology (DA2210).


## STUDY PLANNING
I have completed all other courses. My degree project will be the last element of my education.
