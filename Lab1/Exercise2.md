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

![equation](http://www.sciweavers.org/tex2img.php?eq=%5Cfrac%7B%20%20%5Coverline%7BX%7D%20-%20%5Cmu%20%20%7D%7B%20%5Cfrac%7B%20%5Csigma%7D%7B%20%5Csqrt%7Bn%7D%20%7D%20%20&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0%22%20align=%22center%22%20border=%220%22%20alt=%22\frac{%20\overline{X}%20-%20\mu%20}{%20\frac{%20\sigma}{%20\sqrt{n}%20})

 * Assumed the Random Number Generator block had a uniform distribution of [0,1] which gives population mean standard deviation as below
 
![equation 2](http://www.sciweavers.org/tex2img.php?eq=%5Cmu%20%3D%20%20%5Cfrac%7B1%7D%7B2%7D%28a%2Bb%29%20%3D%20%5Cfrac%7B1%7D%7B2%7D%280%2B1%29%20%3D%20%5Cfrac%7B1%7D%7B2%7D&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0)

![equation 3](http://www.sciweavers.org/tex2img.php?eq=%20%5Csigma%20%3D%20%20%5Csqrt%7B%20%5Cfrac%7B1%7D%7B12%7D%20%28b-a%29%5E2%7D%20%3D%20%5Csqrt%7B%20%5Cfrac%7B1%7D%7B12%7D%20%281-0%29%5E2%7D%20%3D%20%5Csqrt%7B%20%5Cfrac%7B1%7D%7B12%7D%20%281%29%5E2%7D%20%3D%20%20%5Csqrt%7B%20%5Cfrac%7B1%7D%7B12%7D%7D%20%20%20%5Capprox%200.28868&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=0)

 * This was implemeneted by subtracting 0.5 from the sample mean, then dividing by the population standard dev. (above) divided by SQRT(n) (where n is 100)
 * The rest of the code was not changed
 
####Ex2.3.PNG when fixed

