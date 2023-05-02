Download Link: https://assignmentchef.com/product/solved-cpe202-project2-evaluating-expressions-using-stacks
<br>
1. Background  (https://en.wikipedia.org/wiki/Exponentiation)

For this project, you will implement a program to convert infix to postfix and evaluate a <a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">postfix (Reverse Polish</a> <a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">or RPN) expression</a><a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">.</a> To make the program more versatile, you’ll also provide code to convert infix expressions (the kind used in standard arithmetic) and <a href="https://en.wikipedia.org/wiki/Polish_notation">prefix (Polish or PN) expressions</a> to postfix expressions.  In this way, your program will be able to evaluate prefix, infix and postfix expressions.

For this assignment, you will use an implementation of the Abstract Data Type Stack. Make use of a stack_array you implemented.  Many language translators (e.g. compiler) do something similar to convert expressions into code that is easy to execute on a computer.

Section 3.9 of the text has a detailed discussion of this material that you should read carefully before building your implementation.  You program must use your own implementations of the Abstract Data Type Stack. See the text and Lab 2 for further information on the ADT Stack.

<strong>Notes</strong>:

<ul>

 <li>Expression will only consist of numbers (integers, reals, positive or negative) and the five operators separated by spaces. You may assume a capacity of 30 will be sufficient for any expression that your programs will be required to handle.</li>

 <li>The text discusses an easier version of this problem in detail. You should read it carefully before proceeding.  In addition to the <strong>operators (+,-,*,/)</strong> shown in the text, your programs should handle the exponentiation operator.  In this assignment, the exponential operator will be denoted <strong>by ^</strong>.  For example, 2^38 and 3^2</li>

 <li>The exponentiation operator has higher precedence than the * or /. For example, 2*3^2 = 2*9 = 18 <strong>not</strong> 6^2=36</li>

 <li>Also, the exponentiation operator associates from right to left. The other operators (+,-,*,/) associate left to right. Think carefully about what this means.  For example: 2^3^2 = 2^(3^2) = 2^9 = 512 <strong>not</strong> (2^3)^2= 8^2=64</li>

 <li><strong>Every class and function must come with a brief purpose statement in its docstring. In separate comments you should explain the arguments and what is returned by the function or method. </strong></li>

 <li>You must provide test cases for all functions.</li>

 <li>Use descriptive names for data structures and helper functions. You must name your files and functions (methods) as specified below.</li>

 <li>You will not get full credit if you use built-in functions beyond the basic built in operations unless they are explicitly stated as being allowed. If you are in doubt ask me or one of the student assistants.</li>

</ul>

<h1>2. Functions</h1>

The following bullet points provide a guide to implement some of the data structures and individual functions of your program.  Start by downloading templates to be used. You can use your stack_array from previous project. (Note if you didn’t get full credit for stack_array, contact me!)

<ul>

 <li>py</li>

 <li>py (contains infix_to_postfix(infix_expr) and postfix_eval(postfix_expr)</li>

 <li>py</li>

</ul>







from PolyLearn and use these are starting points for your project. <strong> </strong>

<strong> def </strong>infix_to_postfix(infix_expr):

<em>“””Converts an infix expression to an equivalent postfix expression”””  </em>

<em>“””Input argument:  a string containing an infix expression where tokens are     space separated.  Tokens are either operators {+ – * / ^} or numbers </em>

<em>   Returns a string containing a postfix expression “”” </em>




Use the split function to convert the input to a list of tokens




<strong>def </strong>postfix_eval(postfix_expr):

<em>“””Evaluates a postfix expression””” </em>

<em> </em>

<em>“””Input argument:  a string containing a postfix expression where tokens     are space separated.  Tokens are either operators {+ – * / ^} or numbers””” </em>

<strong> </strong>

<h1>3. Modifications</h1>

<ol>

 <li>Write a separate function postfix_valid (string) to test for an invalid postfix expression. As above you may assume that what is passed in a string that only contains numbers and operators. These are separated into valid tokens by spaces so you can use split and join as necessary. The focus is on whether the string had the correct number and position of operators and operands. This function should return true if the expression is valid and False if it is not valid.</li>

 <li>You may now assume that the postfix_eval() function will always be called with a valid expression. The empty string will be considered invalid.</li>

 <li>There is now a Stack class posted using an array implementation. The graders will use this in testing your program. Make sure that your program imports the file and the StackArray class appropriately.</li>

 <li>Note that when your program creates a stack the syntax should be <strong>name_of_stack = StackArray(30)</strong></li>

 <li>There is now a template file posted for your testcases. Use this and submit your tests in a file with the same name.</li>

</ol>

<h1>4.  Algorithms</h1>




<h2>Evaluating a Postfix (RPN) Expression</h2>




While RPN will look strange until you are familiar with it, here you can begin to see some of its advantages for programmers. One such advantage of RPN is that it removes the need for parentheses. Infix notation supports operator precedence ( and ∕ have higher precedence than + and −) and thus needs parentheses to override this precedence. This makes parsing such expressions much more difficult. RPN has no notion of precedence, the operators are processed in the order they are encountered. This makes evaluating RPN expressions fairly straightforward and is a perfect application for a stack data structure, just follow these steps:




<ul>

 <li>Process the expression from left-to-right  When a value is encountered: o             Push the value onto the stack           When an operator is encountered:

  <ul>

   <li>Pop the required number of values from the stack o Perform the operation</li>

   <li>Push the result back onto the stack</li>

  </ul></li>

 <li>Return the last value remaining on the stack</li>

</ul>

For example, given the expression <strong>5 1 2 + 4 ^ + 3 –</strong> :




<table width="719">

 <tbody>

  <tr>

   <td width="58"><strong>Input </strong></td>

   <td width="77"><strong>Type </strong></td>

   <td width="58"><strong>Stack </strong></td>

   <td width="526"><strong>Notes </strong></td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="77">Value</td>

   <td width="58">5</td>

   <td width="526">Push 5 onto stack</td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="77">Value</td>

   <td width="58">1 5</td>

   <td width="526">Push 1 onto stack</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="77">Value</td>

   <td width="58">2 1 5</td>

   <td width="526">Push 2 onto stack</td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="77">Operator</td>

   <td width="58">3 5</td>

   <td width="526">Pop two operands (1, 2), perform operation (1+2=3), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="77">Value</td>

   <td width="58">4 3 5</td>

   <td width="526">Push 4 onto stack</td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="77">Operator</td>

   <td width="58">81 5</td>

   <td width="526">Pop two operands (3, 4), perform operation (3<strong>^</strong>4=81), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="77">Operator</td>

   <td width="58">86</td>

   <td width="526">Pop two operands (5, 81), perform operation (5+81=86), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="77">Value</td>

   <td width="58">3 86</td>

   <td width="526">Push 3 onto stack</td>

  </tr>

  <tr>

   <td width="58">−</td>

   <td width="77">Operator</td>

   <td width="58">83</td>

   <td width="526">Pop two operands (86, 3), perform operator (86−3=83), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58"> </td>

   <td width="77">Result</td>

   <td width="58">83</td>

   <td width="526"> </td>

  </tr>

 </tbody>

</table>




<h2>Converting Infix Expressions to Postfix (RPN)</h2>




You can also use a stack to convert an infix expression to an RPN expression via the <a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">Shunting</a><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">–</a><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">yard algorithm</a><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">.</a> The steps are shown below. Note that the algorithm is more complex that what was shown in class, because the project will include a power operator.

<ul>

 <li>Process the expression from left-to-right  When you encounter a value:

  <ul>

   <li>Append the value to the RPN expression  When you encounter an opening parenthesis: o         Push it onto the stack</li>

  </ul></li>

 <li>When you encounter a closing parenthesis: o Until the top of stack is an opening parenthesis, pop operators off the stack and append them to the RPN expression

  <ul>

   <li>Pop the opening parenthesis from the stack (but don’t put it into the RPN expression)  When you encounter an operator, o<sub>1</sub>: o    While there is an operator, o<sub>2</sub>, at the top of the stack and either</li>

  </ul></li>

</ul>

o<sub>1</sub>is left-associative and its precedence is <em>less than or equal to</em> that of o<sub>2</sub>, or o<sub>1</sub> is right-associative, and has precedence <em>less than</em> that of o<sub>2</sub>

<ul>

 <li>Pop o<sub>2</sub> from the stack and append it to the RPN expression o Finally, push o<sub>1</sub> onto the stack</li>

 <li>When you get to the end of the infix expression, pop (and append to the RPN expression) all remaining operators</li>

</ul>

For example, given the expression <strong>3 + 4 * 2 / ( 1 – 5 ) ^ 2 ^ 3</strong>:

<table width="280">

 <tbody>

  <tr>

   <td width="80"><strong>operator </strong></td>

   <td width="96"><strong>precedence </strong></td>

   <td width="104"><strong>associativity </strong></td>

  </tr>

  <tr>

   <td width="80">^</td>

   <td width="96">high</td>

   <td width="104">Right</td>

  </tr>

  <tr>

   <td width="80">*</td>

   <td width="96">medium</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">/</td>

   <td width="96">medium</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">+</td>

   <td width="96">low</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">−</td>

   <td width="96">low</td>

   <td width="104">Left</td>

  </tr>

 </tbody>

</table>




<table width="719">

 <tbody>

  <tr>

   <td width="58"><strong>Input </strong></td>

   <td width="162"><strong>Action </strong></td>

   <td width="141"><strong>RPN </strong></td>

   <td width="60"><strong>Stack </strong></td>

   <td width="298"><strong>Notes </strong></td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="162">Append 3 to expression</td>

   <td width="141">3</td>

   <td width="60"> </td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="162">Push + onto stack</td>

   <td width="141">3</td>

   <td width="60">+</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="162">Append 4 to expression</td>

   <td width="141">3 4</td>

   <td width="60">+</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">*</td>

   <td width="162">Push * onto stack</td>

   <td width="141">3 4</td>

   <td width="60">* +</td>

   <td width="298">* has higher precedence than +</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="162">Append 2 to expression</td>

   <td width="141">3 4 2</td>

   <td width="60">* +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="162">Pop *, push /</td>

   <td width="141">3 4 2 *</td>

   <td width="60">/ +</td>

   <td width="298">/ and * have same precedence/ has higher precedence than +</td>

  </tr>

  <tr>

   <td width="58">(</td>

   <td width="162">Push ( to stack</td>

   <td width="141">3 4 2 *</td>

   <td width="60">( / +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="162">Append 1 to expression</td>

   <td width="141">3 4 2 * 1</td>

   <td width="60">( / +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="162">Push – to stack</td>

   <td width="141">3 4 2 * 1</td>

   <td width="60">– ( / +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="162">Append 5 to expression</td>

   <td width="141">3 4 2 * 1 5</td>

   <td width="60">– ( / +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">)</td>

   <td width="162">Pop stack</td>

   <td width="141">3 4 2 * 1 5 –</td>

   <td width="60">/ +</td>

   <td width="298">Pop and append operators until opening parenthesis;then pop opening parenthesis</td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="162">Push ^ to stack</td>

   <td width="141">3 4 2 * 1 5 –</td>

   <td width="60">^ / +</td>

   <td width="298">^ has higher precedence than /</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="162">Append 2 to expression</td>

   <td width="141">3 4 2 * 1 5 – 2</td>

   <td width="60">^ / +</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="162">Push ^ to stack</td>

   <td width="141">3 4 2 * 1 5 – 2</td>

   <td width="60">^ ^ /+</td>

   <td width="298">^ is evaluated right-to-left</td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="162">Append 3 to expression</td>

   <td width="141">3 4 2 * 1 5 – 2 3</td>

   <td width="60">^ ^ /+</td>

   <td width="298"> </td>

  </tr>

  <tr>

   <td width="58"><em>end</em></td>

   <td width="162">Pop entire stack to output</td>

   <td width="141">3 4 2 * 1 5 – 2 3 ^^ / +</td>

   <td width="60"> </td>

   <td width="298"> </td>

  </tr>

 </tbody>

</table>

<h2>Converting Prefix Expressions (PN) to Postfix (RPN)</h2>




<ul>

 <li>Read the Prefix expression in reverse order (from right to left)</li>

 <li>When an operand is encountered, push it onto the stack</li>

 <li>When an operator is encountered:

  <ul>

   <li>Pop two operands/strings from the stack: op1 = pop(), op2 = pop()</li>

   <li>Create a string by concatenating the two operands/strings and the operator after them: string = op1 + op2 + operator (remember space separation)</li>

   <li>Push the resultant string back to the stack</li>

  </ul></li>

 <li>Repeat the above steps until end of Prefix expression</li>

 <li>The one string remaining on the Stack is the resultant Postfix expression</li>

</ul>

For example, given the Prefix expression: * – 3 / 2 1 – / 4 5 6




<table width="719">

 <tbody>

  <tr>

   <td width="58"><strong>Input</strong></td>

   <td width="342"><strong>Action</strong></td>

   <td width="133"><strong>Stack</strong></td>

   <td width="185"><strong>Notes</strong></td>

  </tr>

  <tr>

   <td width="58">6</td>

   <td width="342">Push ‘6’ onto stack</td>

   <td width="133">‘6’</td>

   <td width="185">Read from right to left</td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="342">Push ‘5’ onto stack</td>

   <td width="133">‘5’ ‘6’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="342">Push ‘4’ onto stack</td>

   <td width="133">‘4’ ‘5’ ‘6’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="342">Pop ‘4’, ‘5’, combine with /, push onto stack</td>

   <td width="133">‘4 5 /’ ‘6’</td>

   <td width="185">Keep tokens space separated</td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="342">Pop ‘4 5 /’, ‘6’, combine with -, push onto stack</td>

   <td width="133">‘4 5 / 6 -’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="342">Push 1 onto stack</td>

   <td width="133">‘1’ ‘4 5 / 6 -’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="342">Push 2 onto stack</td>

   <td width="133">‘2’ ‘1’ ‘4 5 / 6 -’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="342">Pop ‘2’,’1’, combine with /, push onto stack</td>

   <td width="133">‘2 1 /’ ‘4 5 / 6 -’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="342">Push 3 onto stack</td>

   <td width="133">‘3’ ‘2 1 /’ ‘4 5 / 6-’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="342">Pop ‘3’,‘2 1 /’, combine with -, push onto stack</td>

   <td width="133">‘3 2 1 / -’ ‘4 5 / 6-’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58">*</td>

   <td width="342">Pop ‘3 2 1 / -’,‘4 5 / 6 -’, combine with *, push onto stack</td>

   <td width="133">‘3 2 1 / – 4 5 / 6 –*’</td>

   <td width="185"> </td>

  </tr>

  <tr>

   <td width="58"><em>end</em></td>

   <td width="342">Pop entire stack to output</td>

   <td width="133"> </td>

   <td width="185">Result: ‘3 2 1 / – 4 5 / 6 – *’</td>

  </tr>

 </tbody>

</table>







<h1>3. Tests</h1>

<ul>

 <li>Write sufficient tests using unittest to ensure full functionality and correctness of your program. <strong>Do not provide test cases for you stack since you did that for Lab 2</strong>.</li>

 <li>Make sure that your tests test each branch of your program and any edge conditions. You do not need to test for correct input in the assignment, other than what is specified above.</li>

 <li>You may assume that when infix_to_postfix(input_str) is called that input_str is a well formatted, correct infix expression containing only numbers and the specified operators and the tokens are space separated. You may use the python string functions .split and .join</li>

 <li>You may assume that when prefix_to_postfix(input_str) is called that input_str is a well formatted, correct prefix expression containing only numbers, the specified operators, and that the tokens are space separated. You may use the Python functions split and join.</li>

 <li>Examples of invalid expression would be “3 5”  or “ 3 * +” or “” . The expression will be invalid due to the number or position of the operators or the numbers.  <strong>It will not be due to including some other </strong></li>

</ul>

<h2>token, say “X”</h2>

<ul>

 <li>postfix_eval() should raise a ValueError if a divisor is 0.</li>

 <li>postfix_eval(input_str) should raise a PostfixFormatException if the input is not well-formed.</li>

</ul>

Specifically, it should raise this exception with the following messages in the following conditions:

<ul>

 <li>“Invalid token” if one of the tokens is neither a valid operand nor a valid operator.</li>

 <li>“Insufficient operands” if the expression does not contain sufficient operands. o “Too many operands” if the expression contains too many operands.</li>

 <li>Note: to raise an exception with a message: rasie PostfixFormatException(“Here is a message”)</li>

</ul>





