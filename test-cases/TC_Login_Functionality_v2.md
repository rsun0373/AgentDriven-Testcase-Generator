# Test Case Documentation: SauceDemo Login Functionality (v2)
**Issue ID:** #1  
**Title:** Verify login functionality for ecomm website  
**Application:** SauceDemo (https://www.saucedemo.com/)  
**Test Type:** Functional, Security, Validation  
**Date:** 2026-08-13  
**Version:** 2.0 (Updated with Skills v1)

---

## Executive Summary
Comprehensive test cases for SauceDemo login functionality based on explicitly provided acceptance criteria and test data. This version follows updated skills guidelines with explicit test data handling and assumption documentation.

### Key Metrics
- **Total Test Cases:** 9
- **Acceptance Criteria Coverage:** 100% (10/10 AC)
- **Explicitly Provided Test Data:** ✅ Used
- **Assumed Test Data:** ⚠️ Clearly labeled
- **Test Categories:** Functional (3), Negative (3), Boundary (3), Edge (0)

---

## Test Data Repository (From Issue #1)

### Explicitly Provided Test Credentials
| User Type | Username | Password | Source | Status |
|-----------|----------|----------|--------|--------|
| Valid | standard_user | secret_sauce | ✅ Provided in AC | Confirmed |
| Invalid | invalid_user | invalid_password | ✅ Provided in AC | Confirmed |
| Locked Out | locked_out_user | secret_sauce | ✅ Provided in AC | Confirmed |

### Explicitly Provided URLs
| URL Type | Value | Source | Status |
|----------|-------|--------|--------|
| Application Root | https://www.saucedemo.com/ | ✅ Provided in AC | Confirmed |
| Inventory Page | https://www.saucedemo.com/inventory.html | ⚠️ ASSUMPTION | Inferred from AC#9 |

### Explicitly Provided Error Messages
| Scenario | Error Message | Source | Status |
|----------|---------------|--------|--------|
| Invalid credentials | "Epic sadface: Username and password do not match any user in this service" | ⚠️ ASSUMPTION | Inferred from AC#3 & #4 |
| Empty username | "Epic sadface: Username is required" | ⚠️ ASSUMPTION | Inferred from AC#5 |
| Empty password | "Epic sadface: Password is required" | ⚠️ ASSUMPTION | Inferred from AC#6 |
| Both fields empty | [Same as username required] | ⚠️ ASSUMPTION | Inferred from AC#7 |
| Locked out user | "Epic sadface: Sorry, this user has been locked out" | ✅ Provided in AC#10 | Confirmed |

### Missing Test Data (Identified)
| Missing Element | Impact | Placeholder |
|-----------------|--------|-------------|
| Expected page title | AC#9 verification | [TITLE_PLACEHOLDER] |
| Inventory page elements | Visual verification | [INVENTORY_ITEMS_PLACEHOLDER] |
| Response time SLA | Performance acceptance | [RESPONSE_TIME_MS] |
| Session token format | Security verification | [SESSION_TOKEN_PLACEHOLDER] |
| Cookie/storage requirements | Session handling | [SESSION_STORAGE_TYPE] |

---

# TEST CASES - TRADITIONAL/MANUAL FORMAT

## TC#001-M: Successful Login with Valid Credentials
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Functional - Happy Path

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity to https://www.saucedemo.com/ is available
- [ASSUMPTION] JavaScript is enabled in browser

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** standard_user ✅ (Provided)
- **Password:** secret_sauce ✅ (Provided)
- **Expected Page Title:** [TITLE_PLACEHOLDER] ⚠️ (Missing - inferred: "Swag Labs")
- **Expected URL:** https://www.saucedemo.com/inventory.html ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed with username and password input fields
3. ? Enter "standard_user" in username field
4. ? Enter "secret_sauce" in password field
5. ? Click Login button
6. ? Wait for page response
7. ? Verify URL in address bar
8. ? Verify page title/header
9. ? Verify inventory items are displayed

### Expected Results
- ✅ Login succeeds without error message
- ✅ User is redirected to inventory page
- ✅ URL changes to https://www.saucedemo.com/inventory.html
- ✅ Page title displays [TITLE_PLACEHOLDER]
- ✅ Inventory page content is visible

### Postconditions
- User session is established
- User can access authenticated pages
- Logout functionality is available

### Related References
- AC#1, AC#2, AC#9
- Test Data: Valid user (Provided)

---

## TC#002-M: Login Fails with Incorrect Password
**Status:** Manual  
**Priority:** P1 (High)  
**Severity:** Major  
**Automation Feasibility:** High  
**Category:** Negative - Authentication Failure

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] Application validates against stored password hash

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** standard_user ✅ (Provided)
- **Password:** wrong_password ⚠️ (Test value - not provided in AC)
- **Expected Error:** "Epic sadface: Username and password do not match any user in this service" ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Enter "standard_user" in username field
4. ? Enter "wrong_password" in password field
5. ? Click Login button
6. ? Observe response message

### Expected Results
- ✅ Login fails
- ✅ Error message is displayed
- ✅ User remains on login page
- ✅ URL does not change to inventory page

### Postconditions
- No user session created
- User can retry login

### Related References
- AC#3
- Test Data: Valid username with incorrect password

---

## TC#003-M: Login Fails with Unregistered Username
**Status:** Manual  
**Priority:** P1 (High)  
**Severity:** Major  
**Automation Feasibility:** High  
**Category:** Negative - User Not Found

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] invalid_user does not exist in system

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** invalid_user ✅ (Provided)
- **Password:** invalid_password ✅ (Provided)
- **Expected Error:** "Epic sadface: Username and password do not match any user in this service" ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Enter "invalid_user" in username field
4. ? Enter "invalid_password" in password field
5. ? Click Login button
6. ? Observe response message

### Expected Results
- ✅ Login fails
- ✅ Error message is displayed
- ✅ User remains on login page
- ✅ No authentication occurs

### Postconditions
- No user session created
- User can attempt login with registered credentials

### Related References
- AC#4
- Test Data: Unregistered user (Provided)

---

## TC#004-M: Login Fails with Empty Username
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Boundary - Required Field Validation

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] Empty username field triggers validation

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** (empty) ⚠️ (Test value)
- **Password:** secret_sauce ✅ (Provided)
- **Expected Error:** "Epic sadface: Username is required" ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Leave username field empty
4. ? Enter "secret_sauce" in password field
5. ? Click Login button
6. ? Observe validation message

### Expected Results
- ✅ Login fails
- ✅ Validation message is displayed
- ✅ User remains on login page
- ✅ Password field content is preserved or cleared (behavior unspecified)

### Postconditions
- No user session created
- User can enter username and retry

### Related References
- AC#5
- Missing Information: Expected message text

---

## TC#005-M: Login Fails with Empty Password
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Boundary - Required Field Validation

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] Empty password field triggers validation

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** standard_user ✅ (Provided)
- **Password:** (empty) ⚠️ (Test value)
- **Expected Error:** "Epic sadface: Password is required" ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Enter "standard_user" in username field
4. ? Leave password field empty
5. ? Click Login button
6. ? Observe validation message

### Expected Results
- ✅ Login fails
- ✅ Validation message is displayed
- ✅ User remains on login page
- ✅ Username field content is preserved or cleared (behavior unspecified)

### Postconditions
- No user session created
- User can enter password and retry

### Related References
- AC#6
- Missing Information: Expected message text

---

## TC#006-M: Login Fails with Both Username and Password Empty
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Boundary - Multiple Required Fields Validation

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] Empty fields trigger validation

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** (empty) ⚠️ (Test value)
- **Password:** (empty) ⚠️ (Test value)
- **Expected Behavior:** Validation occurs ⚠️ (Inferred)
- **Expected Error:** [VALIDATION_MESSAGE_PLACEHOLDER] ⚠️ (Missing - assumed username required first)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Leave username field empty
4. ? Leave password field empty
5. ? Click Login button
6. ? Observe validation message(s)

### Expected Results
- ✅ Login fails
- ✅ Validation message is displayed (field priority unknown)
- ✅ User remains on login page
- ✅ Both fields are empty

### Postconditions
- No user session created
- User can enter credentials and retry

### Related References
- AC#7
- Missing Information: Which field is validated first, error message text

---

## TC#007-M: Locked Out User Receives Specific Error Message
**Status:** Manual  
**Priority:** P1 (High)  
**Severity:** Major  
**Automation Feasibility:** High  
**Category:** Negative - Account Locked

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available
- [ASSUMPTION] locked_out_user account status is maintained

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** locked_out_user ✅ (Provided)
- **Password:** secret_sauce ✅ (Provided)
- **Expected Error:** "Epic sadface: Sorry, this user has been locked out" ✅ (Provided)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Enter "locked_out_user" in username field
4. ? Enter "secret_sauce" in password field
5. ? Click Login button
6. ? Wait for response
7. ? Verify error message

### Expected Results
- ✅ Login fails
- ✅ Specific error message is displayed: "Epic sadface: Sorry, this user has been locked out"
- ✅ User remains on login page
- ✅ URL does not change

### Postconditions
- No user session created
- User is informed of account lockout
- User may need to contact support

### Related References
- AC#10
- Test Data: Locked out user (Provided)

---

## TC#008-M: User Remains on Login Page After Authentication Failure
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Functional - Error Handling

### Preconditions
- Browser is open at login page
- User enters invalid credentials
- Login button is clicked

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** invalid_user ✅ (Provided)
- **Password:** invalid_password ✅ (Provided)
- **Expected Result:** Page does not redirect ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Enter "invalid_user" in username field
3. ? Enter "invalid_password" in password field
4. ? Click Login button
5. ? Wait for response
6. ? Check URL in address bar
7. ? Verify login form is still visible

### Expected Results
- ✅ Error message is displayed
- ✅ URL remains: https://www.saucedemo.com/
- ✅ Login form is still present and accessible
- ✅ No redirect to inventory or other page occurs

### Postconditions
- User can modify credentials and retry login
- Page state remains on login page

### Related References
- AC#8
- Test Data: Invalid credentials

---

## TC#009-M: Successful Login Displays Inventory Page with Expected Title
**Status:** Manual  
**Priority:** P0 (Critical)  
**Severity:** Blocker  
**Automation Feasibility:** High  
**Category:** Functional - Post-Login Verification

### Preconditions
- Browser is open and functional
- User is not logged into SauceDemo
- Network connectivity is available

### Test Data
- **URL:** https://www.saucedemo.com/ ✅ (Provided)
- **Username:** standard_user ✅ (Provided)
- **Password:** secret_sauce ✅ (Provided)
- **Expected URL:** https://www.saucedemo.com/inventory.html ⚠️ (Inferred)
- **Expected Page Title:** [TITLE_PLACEHOLDER] ⚠️ (Missing - inferred: "Swag Labs")
- **Expected Content:** Inventory items displayed ⚠️ (Inferred)

### Steps
1. ? Navigate to https://www.saucedemo.com/
2. ? Verify login form is displayed
3. ? Enter "standard_user" in username field
4. ? Enter "secret_sauce" in password field
5. ? Click Login button
6. ? Wait for redirect (2-3 seconds assumed)
7. ? Check URL in address bar
8. ? Check page title/header
9. ? Verify inventory content is displayed

### Expected Results
- ✅ Login succeeds
- ✅ User is redirected to inventory page
- ✅ URL is: https://www.saucedemo.com/inventory.html
- ✅ Page title is: [TITLE_PLACEHOLDER]
- ✅ Inventory items are visible and accessible

### Postconditions
- User is authenticated and logged in
- User can browse products and proceed to checkout
- User session is active

### Related References
- AC#9
- Test Data: Valid user (Provided)
- Missing Information: Exact page title, expected inventory items list

---

# TEST CASE SUMMARY

## Coverage Analysis

### Acceptance Criteria Mapping
| AC # | Description | Test Cases | Coverage |
|------|-------------|-----------|----------|
| #1 | Valid credentials required | TC#001-M | ✅ Direct |
| #2 | Valid login redirects | TC#001-M, TC#009-M | ✅ Direct |
| #3 | Incorrect password error | TC#002-M | ✅ Direct |
| #4 | Unregistered username error | TC#003-M | ✅ Direct |
| #5 | Empty username validation | TC#004-M | ✅ Direct |
| #6 | Empty password validation | TC#005-M | ✅ Direct |
| #7 | Both fields empty validation | TC#006-M | ✅ Direct |
| #8 | User remains on login page | TC#008-M | ✅ Direct |
| #9 | Inventory page displays | TC#009-M | ✅ Direct |
| #10 | Locked out user message | TC#007-M | ✅ Direct |

**Total Coverage:** 10/10 (100%) ✅

## Test Data Inventory

### Provided Test Data (Source: AC)
- ✅ Valid user: standard_user / secret_sauce
- ✅ Invalid user: invalid_user / invalid_password
- ✅ Locked out user: locked_out_user / secret_sauce
- ✅ Application URL: https://www.saucedemo.com/
- ✅ Locked out error message (exact text)

### Inferred Test Data (Source: AC inference)
- ⚠️ Inventory page URL: https://www.saucedemo.com/inventory.html
- ⚠️ Invalid credentials error message (inferred wording)
- ⚠️ Empty field error messages (inferred wording)
- ⚠️ Page title: [TITLE_PLACEHOLDER]

### Missing Test Data (Not provided in AC)
- ❌ Page title value
- ❌ Expected response time
- ❌ Session management details
- ❌ Inventory page content list
- ❌ Error message exact format for AC#5, #6, #7
- ❌ Field validation order (when both empty)

## Assumptions Documented
1. JavaScript is required and enabled
2. invalid_user account does not exist
3. locked_out_user account maintains locked status
4. Empty fields trigger client-side or server-side validation
5. Validation failure keeps user on login page
6. Session token is created upon successful login
7. Inventory page URL follows pattern: /inventory.html
8. Page title includes application name or "Swag Labs"

---

## Notes for Test Execution
- Replace [PLACEHOLDER] values with actual data from application
- Verify error message text exactly matches expected (case-sensitive)
- Document any deviations from expected behavior
- Confirm inventory page elements before considering test passed
- Session handling should be verified across browser reload (future enhancement)

---

**End of Test Case Documentation v2.0**
