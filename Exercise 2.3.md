
## Exercise 2.3

Design for a mortgage repayment calculator using principles of OOP.
<br>

Class diagram for the program would look as follows:

## MortgageCalculator
\- principal: double
<br>
\- loanTerm: int

---
+MortageCalculator()
<br>
+setPrincipal(double): void
<br>
+setLoanTerm(int): void
<br>
+monthlyInstallment(): double
<br>
+validateInput(): void
<br>
+main(String[]): void

---
<br>
The class outlined above handles calculating the monthly installment. It has methods for setting principal amount, setting loan term, validating input and finally calculating monthly installment.
<br>
<br>
Specifications:
<br>
<br>
Fields:
<br>

- principal (double) -> principal amount of loan
- loanTerm (int) -> term in months

Methods:
<br>

1. **MortgageCalculator()**
- Constructor
- To initialize MortgageCalculator object
- No parameters
2. **setPrincipal(double principal)**
- To set principal amount
- Must be positive number
- Throws IllegalArgumentException if principal not valid.
3. **setLoanTerm(int loanTerm)**
- To set loan term in months
- Loan term must be in given range 1-300
- Throws IllegalArgumentException if loan term not valid.
4. **validateInput()**
- To validate inputs for principal and loan term.
- Make sure that principal is positive number and loan term is in allowed range.
- Throws IllegalArgumentException if any inputs invalid.
5. **monthlyInstallment()**
- To calculate monthly installment based on given formula.
- Inputs must be validated already.
- Return calculated monthly installment as double.
6. **main(String[] args)**
- Entry point of program for interaction via command line.
- User interaction to get principal amount and loan term.
- Handle user input, invoke necessary methods for calculation and display of result.
<br>
<br>
**Special situations:**

- Program handles invalid inputs by throwing exceptions.
- Loan term zero is invalid as division by zero is not sensible.
- Principal must be positive number.
