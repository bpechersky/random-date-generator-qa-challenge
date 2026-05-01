# Random Date Generator QA Challenge

This repository contains my testing approach, test report, and bug reports for:
https://codebeautify.org/generate-random-date

## Technology Stack
- Java, TestNG, Rest Assured
- Selenium WebDriver / Selenide
- Postman
- GitHub Actions
- Manual + API + UI Testing

  ## Test Approach
- Functional testing
- Boundary value testing
- Input validation testing
- UI/UX validation
- Negative testing


## Test Scenarios

1. Verify page loads successfully
2. Verify default generation produces 10 dates
3. Verify generated dates follow selected format
4. Verify dates fall within start/end range
5. Verify custom format works correctly
6. Verify invalid inputs are handled
7. Verify copy functionality


## Test Results

| Scenario | Result |
|--------|--------|
| Default generation | Pass |
| Date format validation | Pass |
| Custom format | Fail |
| Input validation | Fail |



## Bug Report 1: Custom Date Format Corrupts Month Names

**Title:**  
Custom date format `month DD YYYY` generates corrupted month names in output.

**Environment:**  
- Windows 10
- Google Chrome
- URL: https://codebeautify.org/generate-random-date

**Steps to Reproduce:**
1. Open the random date generator.
2. Select `Custom date format` from Date Output Format.
3. Enter custom format: `month DD YYYY`
4. Enter start date: `12/12/2010`
5. Enter end date: `12/10/2023`
6. Click `Generate Random Date`.

**Expected Result:**  
The generated dates should display full month names correctly, for example:

```text
December 02 2015
August 24 2016
March 08 2016


Actual Result:
Some generated dates contain corrupted month names with random numbers inserted, for example:

Dece59ber 02 2015
Augu46t 24 2016
Dece45ber 27 2010
Marc16 08 2016
Aug31t 03 2014


Severity: Medium
Priority: High

Impact:
Users cannot rely on the custom date format output because generated dates may be invalid and unreadable.

Recommendation:
Fix custom format parsing so the token month is treated as one complete month-name token and is not partially overwritten by day/month numeric values.




## Bug Report 2: Invalid Date Inputs Are Accepted Without Validation

**Title:**  
Application accepts invalid dates (e.g., month = 13) without validation or error message.

**Environment:**  
- Windows 10  
- Google Chrome  
- URL: https://codebeautify.org/generate-random-date  

**Steps to Reproduce:**
1. Open the random date generator.
2. Enter an invalid start date: `2020-13-01`
3. Enter an invalid end date: `2099-13-31`
4. Click `Generate Random Date`.

**Expected Result:**  
The application should validate input and display an error message such as:
- "Invalid date format"
- "Month must be between 01 and 12"

Date generation should be blocked until valid input is provided.

**Actual Result:**  
The application accepts invalid dates and still generates output without any validation or error message.

**Severity:** High  
**Priority:** High  

**Impact:**  
- Users can input impossible dates  
- Results may be incorrect or misleading  
- Reduces trust in the tool and data integrity  

**Recommendation:**  
Implement strict input validation:
- Validate month range (01–12)  
- Validate day range based on month (including leap years)  
- Prevent generation when input is invalid  
- Display clear and user-friendly error messages  

