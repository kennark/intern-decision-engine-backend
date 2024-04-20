# Ticket-101 conclusion

### What the intern did well

* Exception handling  
I see that new exceptions were created for different scenarios, making debugging and finding faults easier. 
* Code readability  
The intern has written meaningful variable and method names, and added comments for where it is needed. 
* Method usage  
All methods serve one purpose for easier maintainability and readability.
* Use of constants  
All needed constants are defined in a separate config-class, making requirement changes simpler.
* Tests added  
The intern created tests for the implementation cover most important methods


### What the intern could have done better

* Short comments in methods  
While the code is written with understandable variables and methods, I got lost in the method calculateApprovedLoan() with what the method was processing.
* Unneccesary complication  
In method verifyInputs(): 
```
if (!(DecisionEngineConstants.MINIMUM_LOAN_AMOUNT <= loanAmount)
                || !(loanAmount <= DecisionEngineConstants.MAXIMUM_LOAN_AMOUNT)) {
            throw new InvalidLoanAmountException("Invalid loan amount!");
        }
```
The above code is made a little hard to read using ! for a simple check. I would have written the if statement as:
```
if (DecisionEngineConstants.MINIMUM_LOAN_AMOUNT > loanAmount
                || loanAmount > DecisionEngineConstants.MAXIMUM_LOAN_AMOUNT) 
```
This way the condition would be easier to understand for readers. The same issue goes for the loadPeriod check.
* Possible infinite loop  
In method calculateApprovedLoan():  
```
while (highestValidLoanAmount(loanPeriod) < DecisionEngineConstants.MINIMUM_LOAN_AMOUNT) {
            loanPeriod++;
        }
```
If highestValidLoanAmount() is modified in any way, this could then result in a loop.  
I would replace this with a for loop or include a safety check to avoid an infinite loop.

* SOLID principles  
The implementation is correct, but is lacking in "Single responsibility" principle. I would have split the DecisionEngine class methods into separate classes DecisionEngine, InputValidation, and CreditCalculation.
* Front-end design choices  
The "Loan period" slider has the left end starting at 6 months, while the ticket is asking for 12 months minimum loans. The slider itself is programmed correctly, just the text under it is wrong.
* Tests do not 100% cover back end  
The created test cases are missing a few exception lines in DecisionEngine, and InbankBackendApplicationTests does not have any test cases in it.
* Returned loan amount is wrong  
The ticket asked for the program to return the maximum amount the bank can offer. For loans amounts under the maximum (the bank could offer with the terms), it returns the requested amount, not the maximum available. 

### Highlight the most important shortcoming

The most important shortcoming is that the ticket asked for a credit score algorithm, the intern did not implement this.   
``Scoring algorithm. For calculating credit score, a really primitive algorithm should be implemented.
You need to divide the credit modifier with the loan amount and multiply the result with the loan
period in months.``

