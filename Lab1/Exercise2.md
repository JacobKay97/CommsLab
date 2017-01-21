#Exercise 2

##Implementation of CLT 

 * Nested for Loop, inside while loop
 * Inner for loop generates a random number which is summed up
 * This is done n1*n2 times (product of iterations of both for loops)
 * Average is taken to get 'sample mean' via Add Array Elements + divide 
 * Insert into Array block is used
  * Average is fed into New element
  * Index is the while loop iteration counter (so to increment array)
  * Array output is taken 'through the right wall' of the while loop using a shift register
  * Then fed back in from the left side into the Array terminal
  * This ensures the data is transferred from one iteration to the other and the array grows
 * Tested with 10 milliseconds to wait, and 100 bins

Ex2.1.PNG

###Tasks

 * Control to stop afer 1000 iterations was added by using a => block comparing the while loop count with a constant of 1000 and feeding that into the stop condition.

####EX2.2.PNG

 * To convert into a standard normal distribution: N(0, 1), the equation below was used

####Eq1


 * Assumed the Random Number Generator block had a uniform distribution of [0,1] which gives population mean standard deviation as below
 
####Eq2

####Eq3


 * This was implemeneted by subtracting 0.5 from the sample mean, then dividing by the population standard dev. (above) divided by SQRT(n) (where n is 100)
 * The rest of the code was not changed
 
####Ex2.3.PNG when fixed

