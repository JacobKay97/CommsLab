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

Remember to add things to this


![equation](http://www.sciweavers.org/tex2img.php?eq=%5Cfrac%7B%20%20%5Coverline%7BX%7D%20-%20%5Cmu%20%20%7D%7B%20%5Cfrac%7B%20%5Csigma%7D%7B%20%5Csqrt%7Bn%7D%20%7D%20%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0%22%20align=%22center%22%20border=%220%22%20alt=%22\frac{%20\overline{X}%20-%20\mu%20}{%20\frac{%20\sigma}{%20\sqrt{n}%20})
Explain why standard deviation block
