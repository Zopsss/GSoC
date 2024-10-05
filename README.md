
# Google Summer of Code 2024 Final Report



### **Project**: [Refine Google Style Guide Implementation](https://github.com/checkstyle/checkstyle/wiki/Checkstyle-GSoC-2024-Project-Ideas#project-name-refine-google-style-guide-implementation)



### **Student**: [Mauryan Kansara](https://github.com/Zopsss)



### **Organisation**: [Checkstyle](https://github.com/checkstyle)



### **Mentors**: [Roman Ivanov](https://github.com/romani), [Ruslan Diachenko](https://github.com/rdiachenko)



---

### Project Goals

The project aims to update the implement of [google java style guide](https://google.github.io/styleguide/javaguide.html) to latest version. The [google_checks.xml](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml) is the xml file where google style guide is implemented. The previous version we supported was [May 23 2018](https://github.com/google/styleguide/commit/f9347e1e9d79aee9cde0802fe178d72c8f87926c). After that there was a major update of style guide released on [Feb 03 2022](https://github.com/google/styleguide/commit/49488412b2f59843fce2433bd834a3fd9700604e). The project's main goal was to implement this newer version of style guide and update to [coverage page](https://checkstyle.org/google_style.html#Google.27s_Java_Style_Checkstyle_Coverage) according to it. The other goals were transitioning our google style tests from per-module approach to whole-config approach, solving bugs in existing implementation and we also updated the coverage page's style.



---



### What I Did During GSoC



1.  **Researched about updated sections of style guide**: I began my research about finding out what parts of style guide was updated in the latest version by creating a [diff PR](https://github.com/checkstyle/checkstyle/pull/14901/files). The PR contained diff between the older version of style guide and newer version. It helped us to identify what sections were changed and which modules needs to be updated to follow the new rules. It served as foundation to open new issues and discuss the approach to implement the new rules.

2.  **Updating Coverage Table**: In first week, we discussed the updated parts in the diff PR and separate issues were opened to indicate the defects in our implementation. [Coverage table](https://checkstyle.org/google_style.html#Google_Coverage_table) was updated for each sections which were changed with a message & its corresponding issue,  specifying that the section's implementation is based on the previous version and it will be updated to the latest version as part of its referenced issue.

3.  **Migrating Google Style Guide Tests**: Google style guide implementation's tests were implemented based on per-module approach. All tests needed to be transitioned to whole-config testing for better coverage of the style guide. We decided to migrate tests to chapter-wise testing first and then to whole-config testing to ease the migration process. All tests were migrated to chapter-wise testing approach as part of issue [#14937](https://github.com/checkstyle/checkstyle/issues/14937). After this, support for testing the input file against whole [google_checks.xml](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml) was added at [#15026](https://github.com/checkstyle/checkstyle/issues/15026), later all tests were migrated to whole-config testing approach as part of [#14937](https://github.com/checkstyle/checkstyle/issues/14937).

4. **Comparing Input Files against google-java-format**: We added support to compare google style guide input files against [google-java-format](https://github.com/google/google-java-format) in CI. This helps us to find any false-negatives/positives easily. Support for google-java-format was added at [#15237](https://github.com/checkstyle/checkstyle/pull/15237/files). Separate `InputFormattedXxxxx` files were created as part of [#15340](https://github.com/checkstyle/checkstyle/issues/15340) to be compared against google-java-format. During this, we also found some bugs in google-java-format which were reported to them.

5. **Standardizing Content of Coverage Table**:
  - **Fixing Inconsistent Spacing**: Previously, coverage table had inconsistent spacing and didn't had a proper way to display configs of the different Checks used and their input files, it was resolved as part of [#14930](https://github.com/checkstyle/checkstyle/issues/14930).
  - **Removing Closed Referenced Issues**: All the closed referenced issues were removed from each sections as part of [#15442](https://github.com/checkstyle/checkstyle/issues/15442).
  - **Updating Validation Tests of Coverage Table**: Content of coverage table was simplified and it's validation tests were updated as part of [#14968](https://github.com/checkstyle/checkstyle/issues/14968).

6. **Implementation of new rules**:
  - **Adding missing or new sections**: Missing or newly introduced sections in the latest version were added to the coverage table.
  - **Updating implementation of Style Guide**: Based on the new requirements, google_checks.xml and required Checks were updated. Different issues were opened to discuss the approach for updating implementation. Many bugs/defect were found & solved during this process.
  - **Handling Lack of Coverage**: Some new rules were not able to be fully implemented by us due to [limitations](https://checkstyle.org/writingchecks.html#Limitations) of Checkstyle. For such sections, coverage table was updated with a message explaining the reason behind lack of coverage.


---



### Current Status and Future Work
The project is currently in stable state, with majority of successful implementation of new rules and extending style guide tests by implementing whole-config testing approach. The new coverage table has a more simple way of referencing configs of different modules used and their input files.

However, there are several areas for future enhancements:



-  **google-style Issues**: Solve [google-style](https://github.com/checkstyle/checkstyle/issues?q=is:open%20is:issue%20label:%22google%20style%22) labeled issues, these issues shows pending bugs/features to be solved. Closing such issues would help us to improve our coverage of the style guide.

-  **false-negatives**: Some modules in google_checks.xml have false-negatives, if the code does not follow style guide's rules, module is not able to detect such incorrect code. Explore such modules and find a way to detect false-negatives.

-  **Reduce Blue Ticks**: Blue Tick ( ![](https://checkstyle.org/images/ok_blue.png) ) beside modules in coverage table indicates that module is not able to fully implement the rule, reduce such Blue Ticks by improving the implementation of the rule.

---



### Code Contributions

- All PRs/Issues related to the project can be found in [GitHub project board](https://github.com/orgs/checkstyle/projects/7).

- All PRs related to migrating towards chapter-wise testing can be found [here](https://github.com/checkstyle/checkstyle/pulls?q=is%3Apr+%2214937%22+in%3Atitle+).

- All PRs related to migrating towards whole-config testing can be found [here](https://github.com/checkstyle/checkstyle/pulls?q=is%3Apr+%2215214%22+in%3Atitle+).

- All PRs related to creating `InputFormattedXxxxx` input files can be found [here](https://github.com/checkstyle/checkstyle/pulls?q=is%3Apr+%2215218%22+in%3Atitle+).

- My work on this project is part of Checkstyle 10.18.0, 10.18.1, 10.18.2 release.

The release notes can be found here: [10.18.0](https://checkstyle.org/releasenotes.html#Release_10.18.0), [10.18.1](https://checkstyle.org/releasenotes.html#Release_10.18.1), [10.18.2](https://checkstyle.org/releasenotes.html#Release_10.18.2).

- All my contributions to checkstyle can be found [here](https://github.com/checkstyle/checkstyle/pulls/Zopsss).
- All issues opened by me can be found [here](https://github.com/checkstyle/checkstyle/issues/created_by/Zopsss).


---



### What I Learned During GSoC



#### Technical Skills:

- **Implementing new Checks/Features**: While working on this project, based on new rules I had implement new Checks and Features to extend our coverage. Implementing such features have helped me to improve my problem solving ability, it forced me to find a way to solve the problem in an effective and efficient way. Implementing new Checks & Features helped to understand how Checkstyle works at it core and how the Checkstyle API works under the hood.

-  **Bug Solving**: I have developed a good skill of bug solving by finding and solving many bugs in Checkstyle Checks. I required to work on many Checks as part of this project, I had to go through different types of Check's implementation written by someone else in the past and find a way to fix the Check's implementation to reduce the number of false-positives/negatives. This has helped me to understand code written by other contributors and improve the code quality.

-  **BDD Testing**: The new BDD Testing approach of Google tests helped me to extend my software testing abilities. I participated in test improvement process by implementing different types of testing approach like chapter-wise testing, whole-config testing and I wrote many new test cases to improve the implementation of style guide.

-  **Code Quality**: Working on Checkstyle has improved my ability to write clean and optimized code by enforcing high coding standards. Checkstyle uses JaCoCo for code coverage metrics, it follows a strict policy of 100% code coverage. Checkstyle uses PIT for mutation testing, following such standards have helped me to develop a habit of writing more efficient and maintainable code while following a good coding style.


#### Non-Technical Skills:



-  **Project Management**: We dedicated starting few weeks to structure and organize the project to efficiently implement new rules and extend our coverage of the style guide. We discussed about how we should approach migrating our google tests and came up with an efficient way to achieve it. While implementing new rules, we found many defects in our style guide. All mentors and I, discussed and organized such defects into smaller tasks and decided to solve them priority wise. We decided to solve false-positives first as they would give unnecessary errors to users, we then moved towards tackling false-negatives. This has helped me understand how big projects are managed and how all people collaborates to achieve a single goal.

-  **Effective Communication**: Though English is my second language I got to communicate with my experienced mentors and it has improved my communication skills by a great factor. I learnt how to effectively communicate with mentors and handle disagreements. By communicating with them, I learnt a lot about how we can solve a complex problem by collaborating with other team members, how to ask good questions and understand other person's opinion. I also got to interact with google-java-format's community members as we found and submitted few bugs to them.

- **Teamwork and Collaboration**: Working with my mentors taught me the value of teamwork. We often brainstormed ideas, discussed potential solutions to problems, and shared feedback on each other's work. I learned to appreciate the different perspectives each team member brought to the table and how to work efficiently in a team, especially when dealing with a large codebase and complex issues. This experience has significantly enhanced my ability to work in collaborative environments and be more adaptable in future projects.

Overall, This experience has been incredibly enriching, both technically and personally. I’ve gained valuable skills in project management, communication, and teamwork, along with a deeper understanding of how large open-source projects are maintained. These lessons have boosted my confidence and will serve as a strong foundation for my future career in software development.

---



### Acknowledgements

I would like to express my deepest gratitude to my mentors, [Roman Ivanov](https://github.com/romani) and [Ruslan Diachenko](https://github.com/rdiachenko), for their unwavering support and guidance throughout this project. Their calm and understanding nature made it easy for me to ask questions, I got to learn so much from their experience. I also want to thank [Richard Veach](https://github.com/rnveach), who was always willing to help and provided detailed explanations to clear my doubts. This project would not have been possible without their invaluable mentorship and assistance. I am looking forward to keep contributing to Checkstyle and help other new comers to get their open-source journey started.

