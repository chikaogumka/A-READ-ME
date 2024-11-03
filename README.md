## Test automation for big bank
During solving this test task, playwright with typescript was used. To run this project:
- Unpacking the files enclosed in the zip to your pc.
- open the project in your IDE or navigate into the project in your command line and run npm install or npm ci
- After the installation run tests using any for these commands
   ```bash
   - npm run test //to run all the tests in this project in headless mode
   - npm run test --headed //to run all test in headed mods
   - npm run test-ui //to run only UI tests 
   - npm run test-ui-headed //to run only UI tests whille the browser is visible
   - npm run test-api // to run only api tests
   ```
- The test results and reports are automatically displayed at the end of every test run in the browser.
- The test result analysis and report is discussed below

## Objective
The objective of this test strategy is to ensure the loan calculator modal operates as intended, allowing users to input values, visualize outcomes, and navigate seamlessly through the application. We aim to validate input fields, slider functionality, the visualizer, and the navigation elements (continue and close buttons). The automated testing method used to acheieve this goal was created to ensure:
- A reasonable test structure
- Reusable utility functions
- Create reports and loggs data in terminal
- Scalable and written independent of each test
- Configurable and parametized
- Error handling for necessary tests
- Data validation
- Multiple browsers tested

## Scope of Test
  ### In-Scope:
-	Calculator Modal functionality
-	Calculator Input fields (numerical validation, min/max constraints)
-	Calculator Slider behavior
-	Final loan payback amount Visualizer accuracy
-	Navigation (continue and close buttons)
  ### Out-of-Scope:
- Backend calculations logic
- Performance testing of the underlying framework
- Loan amount displayed accuracy

## Test Plan for Loan Calculator
1.	Validate calculator Modal Pop-Up
2.	Text Input Validation
3.	Validate Slider Functionality (Manual Test)
4.	Validate Loan payback amount Display
5.	Validate Button Functionality (Continue and Close)

## Features to Test
1.	Modal pop-up display
2.	Text input fields:
   - Numeric input validation
   - Minimum and maximum value constraints
4.	Slider functionality (synchronization with input fields)
5.	Visualizer displaying the calculated amount
6.	Continue button navigation
7.	Close button functionality

## Test Environment
- Browsers: Chrome, Firefox, Safari, Edge
- Devices: Desktop and mobile (responsive testing)
- Operating Systems: Windows, macOS, iOS, Android

## Testing Approach
  ###	Functional Testing:
- Verify modal pop-up behavior
- Validate input constraints on both text fields
- Ensure sliders adjust values correctly and update visualizer (Manual test case)
- Confirm accuracy of the visualizer
- Verifies the amount received as input in the loan amount section on the modal is equal to the amount displayed in the application after the modal is closed
- Test button functionalities
  ###	Usability Testing:
- Assess the user experience for modal, inputs, sliders, and buttons
- Check for accessibility compliance
  ###	Boundary Testing:
- Test minimum and maximum input values
- Validate slider behaviour at boundary limits
  ###	Negative Testing:
-	Input invalid data to check error handling
-	Test behaviour when modal is closed with unsaved data
  ###	Cross-browser Testing:
-	Ensure consistent functionality across different browsers and devices

## Test Cases for Loan Calculator
The test cases has been divided into 3 parts: automated UI test, automated api test and manual test cases

### Automated UI test cases:
#### Test Case 1: Modal Pop-Up
- Objective: should verify the calculator modal is visible after redirecting to link
- Steps:
  1. Trigger the loan calculator modal by clicking Laenusumma button on the text fill page or loading the url in this test task
  2. Expected Result: The modal should appear, displaying the input fields, sliders, final amount visualizer, and buttons.
#### Test Case 2: Text Input Validation for valid data input (Amount and Month feild)
- Objective: should allow the input of valid data in amount and period text field
- Steps:
  1. Enter a valid number in amount input field (range 500 - 30000)
  2. Enter a valid number in months input field (range 6 - 120)
- Expected Results: Input should be accepted without errors.
#### Test Case 3: Text Input Validation for invalid data input (Amount and Month feild)
- Objective: should not allow or throw error on the input of invalid data in amount and period text field
- Steps:
  1. Enter an invalid number in amount input field (outside the range 500 - 30000) e.g "abc" or "-1"
  2. Enter a valid number in months input field (outside the range 6 - 120) e.g "abc" or "-1"
- Expected Results: Input should not be accepted and an error should be displayed.
#### Test Case 4: Loan amount input validation.
- Objective: should use the same value used during loan calculation on the application page after closing the modal.
- Steps:
  1. Trigger the loan calculator modal by clicking Laenusumma button on the text fill page or loading the url in this test task
  2. Enter a valid number in the amount textbox feild
  3. Enter a valid number in the months textbox feild
  4. click "Jakta" button
- Expected results: The value filled into the amount textbox is equal to the amount in the laenusumma section on the datafill page
#### Test Case 5: Continue Button Functionality
- Objective: Verify that the continue button redirects correctly
- Steps:
  1.	Enter valid values in both input fields
  2.	Click the continue "Jakta" button
- Expected Result: The modal should close and the user should see the "Saame tuttavaks" page
#### Test Case 6: Close Button Functionality
- Objective: Verify that the close "x" button closes the modal
- Steps:
  1.	Click the close button in the modal
- Expected Result: The modal should close and the user should return to the data fill page without errors.
#### Test Case 7: Unsaved Data Closure
- Objective: Test modal closure with unsaved data
- Steps:
  1.	Enter valid values in both fields but do not click continue.
  2.	Click the close button.
- Expected Result: The user should see a prompt warning them about unsaved changes, if applicable and verifying if the user really want to close the web page.

#### Automated API test cases:
All steps were iterated in the automated script over different value inputs. All requests were made using the post method. Each test case has a range of expected values in each response received after sending a request.

#### Test Case 1: should calculate loan with randomized amount and maturity sent in payload
- Objective: Verify that the api accepts values dynamically and returns a valid response
#### Test Case 2: should calculate loan with boundary value amount and maturity sent in payload
- Objective: Verify that the api accepts values on the boundary and still in range and rejects boundary values that are not in range

Manual Test Cases
#### Test Case 1: Slider Functionality for Amount (Manual test case)
- Objective: Validate slider adjustment for amount input
- Steps:
  1.	Use the slider to set the value to any amount in range
  2.	Use the slider to set the value to any amount in range
- Expected Results: The slider should reflect the correct values and update the text input accordingly with visibly figure movement in amount in "Kuumakse" section.
#### Test Case 2: Slider Functionality for Months (Manual test case)
- Objective: Validate slider adjustment for months input
- Steps:
  1.	Use the slider to set the value to any number of months
  2.	Use the slider to set the value to any number of months
- Expected Results:
- The slider should reflect the correct values and update the text input accordingly with visibly figure movement in amount in "Kuumakse" section.

## Test results and analysis
- The boundary value tests for the amount and month input, were failing as seen in the test result. The API did not reject or throw error for the POST of out of bound numbers being parsed in the request feilds for maturity and amount. Same was observed for maximum and minimum boundary values.
- Closing the calculator modal by clicking any area outside the calculator app closes the calculator without any warning or prompt to assert the user wants to close the application. This doesn't validate the data was being saved.
- Caluculator app dose not have any text inbox validation that prevents users from filling in wrong input values
- Calculator UI did not accepts invalid inputs e.g values outside the boundary of the amount input which is 500 to 30000 and 6 to 120 for the months input or values that were not numbers.
- Slider functionality was quite dificult to automate so a click and drag method was implemented to check the slider functionallity

## Conclusion
This test strategy, plan, and detailed test cases ensure comprehensive validation of the loan calculator's features, including input validation, slider functionality, and the navigation experience which worked mostly as expected on the app. The calculator application can be improved by adding data validation in the amount input and the months input, ensuring there is a prompt or safety net for user's data to be saved on the calculator before the application is closed.
