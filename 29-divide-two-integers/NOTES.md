​Explanation:
	dividend = (quotient) * divisor + remainder
We have to find the quotient in this equation and we are given divisor and dividend.
Any number can be represented in binary form. Same goes for quotient :

Let us have an example: 58/5:
58 = (11) * 5 + 3
Representing the quotient in binary form: (11)10 = (1011)2:

	58 = (2^3 + 2^1 + 2^0) * 5 + 3                // --- (I)
	58 = [(2^3 * 5) + (2^1 * 5) + (2^0 * 5)] + 3  // --- (II)
Since we dont know the quotient and remainder the equation we know is:
58 = (q) * 5 + rem

We get a hint at what we would like to do here. We will first multiply 5 with maximum power of 2 such that the resulting number is still smaller than the dividend (read further if you don't understand why). Since multiplication operator is not allowed, we would use bitwise left shift to achieve this multiplication: each time we shift 5 by 1, we multiply it by 2:

	5 << 0 = 5               // less than dividend
	5 << 1 = 5*2 = 10        // less than dividend
	5 << 2 = 5*2*2 = 20      // less than dividend
	5 << 3 = 5*2*2*2 = 40    // less than dividend
	5 << 4 = 5*2*2*2*2 = 80  // (stop and consider the previous value as the result is greater than dividend
We observe that:
58 = (2^3 * 5) + (something * 5) + rem // --- (III)
You can see we are getting close to the equation we initialy wanted (eqa II).

Since 5 is multiplied with 23, we add 23 to our answer.
Further operating on equation III:

	58 - (2^3 * 5)  =  (something * 5) + rem
	58 - (8 * 5) = something * 5 + rem
	58 - 40 = something * 5 + rem
	18 = something * 5 + rem
What we effectively have done is, subtracted the result we got from our first step from dividend (58 - 40).
We arived at the same question again but with a smaller dividend this time.
dividend = 18, divisor = 5

Therefore let us repeat the process:

	5 << 0 = 5           // less than dividend
	5 << 1 = 5*2 = 10    // less than dividend
	5 << 2 = 5*2*2 = 20  // (stop and consider the previous value as the result is greater than dividend
We add 21 to our answer.
Looking back:

	18  =  (2^1 * 5) + (something * 5) + rem
	58 - (2^3 * 5) = (2^1 * 5) + (something * 5) + rem
	58 =  (2^3 * 5) + (2^1 * 5) + (something * 5) + rem
You can notice we are gradually advancing towards equ II:
Our new dividend is now:

	18 - (2^1 * 5)  =  (something * 5) + rem
	18 - (2 * 5) = something * 5 + rem
	18 - 10 = something * 5 + rem
	8 = something * 5 + rem
dividend = 8, divisor = 5
Repeating the process:

	5 << 0 = 5           // less than dividend
	5 << 1 = 5*2 = 10    // (stop and consider the previous value as the result is greater than dividend
We add 20 to our answer.
New dividend:

	8 = (2^0 * 5) + (something * 5) + rem
	8 - 5 = something * 5 + rem
	3 = something * 5 + rem
dividend = 3, divisor = 5
At this step, we stop iterating as our dividend is less than the divisor (we have also found our remainder = 3, as 5 should be multiplied with 0 and what remains is the remainder).

Looking back again for the last time:

	3 = 0*5 + rem
	8 = (2^0 * 5) + 3
	18  =  (2^0 * 5) + (2^1 * 5) + 3
	58 = (2^3 * 5) + (2^1 * 5) + (2^0 * 5) + 3
In the process, we have finally reached the equation we wanted to, and have got the answer as:
quotient = (2^3 + 2^1 + 2^0)
