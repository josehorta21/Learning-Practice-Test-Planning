# AD361 – Learning Practice 7: Test Planning

**Application:** North Vacation Booking  
**Document:** Test plan for the next booking release  
**Status:** Proposed plan (testing has not been executed for this assignment)

## 1. Test Context

I am planning the testing for a new version of North Vacation Booking. Users should be able to select a rental, choose check-in and checkout dates, enter the number of guests, create a booking, and view their bookings. I want to make sure the basic booking process works before the release, but also that the form handles incorrect information properly.

### Test objectives

1. **Verify the main booking flow:** Confirm that a user can create a booking with valid information and see the correct rental, dates, and guest count in the bookings list.
2. **Check validation and error handling:** Test the important invalid-input scenarios defined by the approved requirements, including missing fields, incorrect dates, and invalid guest counts. Any unclear rules will be raised with the product owner before deciding whether a result passes or fails.

### Scope

| In scope | Out of scope |
|---|---|
| Rental selection and available rental options | Real payment processing and refunds |
| Check-in and checkout date entry | Account registration and authentication |
| Guest-count input and increase/decrease/reset controls, where provided | Email or SMS notifications |
| Booking creation and display in the bookings list | Third-party services not included in this release |
| Form validation, error messages, and the complete booking flow | Large-scale load testing and unrelated features |
| Basic usability and keyboard navigation of the booking flow | |

**Test basis:** The North Vacation Booking requirements in the assignment, approved user stories and acceptance criteria, available interface designs, and relevant source code when component tests are prepared. Findings from an earlier practice version can help choose risk areas, but they are not proof that a defect exists in this release.

**Assumptions and constraints:** I am assuming that the team will provide a working test environment and sample rentals. I am planning a five-day test window with a small team. The requirements provided here do not state the exact guest maximum, date-range rules, or availability policy, so those expected behaviors need confirmation before related cases are graded as passes or failures.

## 2. Roles and Responsibilities

| Role | Responsibility | When involved | Communication |
|---|---|---|---|
| QA tester | Review requirements, write and run test cases, record results, report defects, and retest fixes | Planning through test completion | Work with developers on bugs and give progress to the product owner |
| Developer | Explain the implementation, provide builds, help set up test data, fix reported defects, and maintain automated tests | Setup, testing, and defect fixes | Respond to GitHub issues and discuss fixes with QA |
| Product owner | Confirm booking rules, approve acceptance criteria, and decide whether remaining risks are acceptable | Planning, requirement questions, and release decision | Clarify requirements with QA and review the final test summary |
| Test coordinator / team lead | Track the schedule, environment access, and high-priority issues | Start of testing and daily check-ins | Share status, blockers, and release readiness with the team |

## 3. Test Approach

I would start with the most important user flow, then focus on cases likely to fail. I would use manual tests for the interface and automated tests for repeated checks when the source code and test tools are available.

| Test area | Level / test type | Technique | Execution | Planned deliverable |
|---|---|---|---|---|
| Date and guest validation | Component / functional | Equivalence partitioning and boundary value analysis | Automated where practical, plus manual checks | Test cases and unit test files |
| Booking rules with multiple inputs | Component or system / functional | Decision table testing | Manual or automated | Decision table and test results |
| Create booking → view booking | Integration and system / functional | State transition testing | Manual, with repeatable checks automated if possible | Flow test cases and results |
| Empty fields, unexpected input, repeated submissions | System / functional | Error guessing and exploratory testing | Manual | Session notes and defect reports |
| Keyboard use, readable errors, mobile layout | System / non-functional usability | Checklist-based testing | Manual | Usability checklist and findings |
| Booking storage and display | Integration / functional | Expected-input/output checks | Automated if a test backend is available | Integration test results |

**Planned deliverables:** Test cases, a requirements-to-tests checklist, automated test files if suitable, a test execution log, coverage results when code-level tests run, defect reports, and a short test completion report.

**Test execution order:** Valid booking first, then missing or invalid values, then save-and-display integration checks, followed by usability and regression testing after fixes. I will use the requirements as the source for expected behavior rather than assuming that the current application is correct.

## 4. Test Requirements

| Requirement | What is needed |
|---|---|
| Environment | A stable local or staging build of North Vacation Booking with a separate test data store and a working booking service |
| Browsers and devices | Current Chrome and Firefox on desktop, plus a mobile-sized browser viewport; a real mobile device if available |
| Tools | Browser developer tools, VS Code, Git/GitHub for defect tracking; Jest and React Testing Library for component tests if the supplied code supports them |
| Test data | At least two rental options; valid dates such as Dec 5–8, 2026; an earlier date such as Dec 1, 2025; blank dates; one guest, zero guests, and a value beyond the confirmed maximum |
| Access | Permission to open the test application, create and inspect test bookings, read the approved requirements, and view relevant logs |
| People and knowledge | A tester who understands the booking flow, a developer who can troubleshoot issues, and a product owner to clarify unclear rules |

All bookings and accounts used in testing should contain fictional data. I would reset or separate the test data where needed so that one test does not affect the result of the next one.

## 5. Risk Register

Likelihood and impact are initial estimates, using **Low / Medium / High**; they should be reviewed with the team before testing starts.

| ID | Risk | Type | Likelihood | Impact | Mitigation |
|---|---|---|---|---|---|
| R01 | A booking may be accepted with a date that should not be allowed. A similar issue was observed in an earlier practice build. | Product | High | High | Confirm the date rules and prioritize past-date and checkout-before-check-in tests; retest after any fix |
| R02 | A booking may save without the intended rental or display incomplete booking details. | Product | Medium | High | Test rental selection and verify every saved field on the bookings page |
| R03 | Guest-count limits or required-field validation may behave incorrectly. | Product | Medium | Medium | Test blank values, zero, minimum, and confirmed maximum with boundary checks |
| R04 | The test server or sample data may be unavailable during the scheduled test period. | Project | Medium | High | Verify the environment on Day 1 and keep a local backup or reusable test fixtures |
| R05 | Unclear requirements about dates, availability, or capacity may delay testing. | Project | Medium | Medium | Review requirements early and get written answers from the product owner |

I would investigate R01 and R02 first because they could lead to incorrect reservations being stored, not just a confusing message on the screen.

## 6. Entry Criteria

Testing can begin when **all four** conditions are met:

1. The current release build opens in the agreed test environment, and the booking form and bookings page are accessible.
2. The rental test data and test storage are available, with at least two known rentals and a way to inspect created bookings.
3. The planned test cases for rental selection, dates, guest counts, booking creation, and booking display have been written and reviewed.
4. The product owner has confirmed the expected rules for date validity, required fields, and guest-count limits, or has recorded any unresolved rule as a blocker for those tests.

Each item can be marked **Met** or **Not met** before execution.

## 7. Exit Criteria

Testing is complete when **all four** conditions are met:

1. **100%** of the planned test cases have been executed and recorded, with at least **95% passing**.
2. **100%** of high-priority booking, date validation, and booking-display test cases have passed.
3. There are **zero open critical or high-severity defects** affecting the features in scope.
4. Regression tests for the main booking flow have passed after the final fixes, and all remaining defects and test results are documented in the completion report.

If the deadline arrives before these criteria are met, I would report what is incomplete and ask the product owner to make the release decision rather than describe testing as fully passed.

## 8. Test Schedule

This is a **proposed five-day testing schedule**, not a log of work already performed.

| Activity | Responsible | When | Dependency |
|---|---|---|---|
| Review requirements and confirm unclear booking rules | QA tester + product owner | Day 1 | Requirements available |
| Prepare environment, test rentals, and access | Developer + QA tester | Day 1 | Test build available |
| Design and review test cases and checklists | QA tester + product owner | Day 2 | Requirements clarified |
| Run component validation and manual booking tests | QA tester + developer | Day 3 | Entry criteria met |
| Test booking persistence, invalid flows, and usability | QA tester | Day 4 | Booking flow and test data working |
| Retest fixes, run regression, and prepare final report | QA tester + developer + product owner | Day 5 | Defects reported and fixes ready |

## 9. Communication Plan

| Information | Audience | Method | When |
|---|---|---|---|
| Testing progress, planned work, and blockers | QA, developers, product owner | Short team stand-up or Slack update | Daily during the test window |
| New defect with steps, expected behavior, and actual behavior | Assigned developer and QA tester | GitHub issue | As soon as the defect is found |
| Questions about booking requirements | Product owner and QA tester | Slack or a documented issue/comment | Whenever an unclear rule blocks testing |
| High-severity risk or release blocker | Team lead and product owner | Direct message plus GitHub issue | Immediately after confirmation |
| Final results, open defects, and exit-criteria status | Product owner and project team | Test completion report shared in GitHub | End of Day 5 |

## Conclusion

I think this plan keeps the testing focused on what users need most: creating a correct reservation and finding it again. It also gives the team a clear way to track progress, report problems, and decide if the release is ready instead of just assuming everything works.

## AI

I used ChatGPT to help organize the test plan and improve the writing.
