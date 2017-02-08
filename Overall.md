#Lab 1

##Exercise 1

 * Learned the basic interface of LabView
 * Made a text to ASCII Byte array (UTF-8) 
 * Interpreted as Temperatures in F, converted to C
 * Got average of whole array (each letter converted to one element of byte array)  
 * Got to understand the UI
 
 
###Include EX1.PNG

![Exercise 1](https://github.com/JacobKay97/CommsLab/blob/master/pics/Ex1.png)

##Exercise 2

###Implementation of CLT 

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

####Ex2.1.PNG

####Tasks

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

##Exercise 3


 * Wired up three sine waves, and added them up
  * FFT PSD module
  * Two adder blocks, as extending one adder block to do three gave me an error
  * Filter added

####EX3.1 and .2 images


 * Filter changed to a bandpass filter with cut off frequencies of 25 and 35
 * This let mostly only the sine wave at 30Hz through
 
####Ex3.3.png


#Lab 2

##Exercise 1

 * Created AM signal
 * Obeyed the equation given in the notes
 * PSD of modulated signal had two sidebands


###Ex1.1.png block diagram
###ex1.2 png plot

 * Changing AM to give mu of {.5, 1, 1.5} 
 * Increasing mu changes the AM signal
  * at 1 the modulated signal's lowest point is 0, however going being that leads to the message signal being bigger than the carrier and losing some of the data 
  * Aliasing

###ex1.3a/b/c - think harder too

 * Changing message frequency as {1k, 2k, 5k}
 * Aliasing as message frequency approaches carrier frequency
  * Technically carrier is sampling the message, reaching Nyquist frequency

###ex1.4a/b/c - make some more notes twat


##Exercise 2

###Insert maths here + ex2a.png

 * Made coherant Demodulator
 * Hopefully it works
 * Scaling issues
 * Have to multiply demodulated signal by 2
  * However input carrier is not normalised, so have to divide by the amplitude of carrier
   * Or normalise carrier, but that was more wiring



###Insert maths here and ex2B.pNg

 * Made envelope detector
 * Hopefully it works
 * Needed to pass through all the waveform properties from Waveform Properties to Build Waveform
 

##Exercise 3

 * Had a fuck tonne of issues, look back at exercise 2 for fixes
 
###ex3.png
 
### Changing mu

 * Coherant detection worked for all values 
 * Envelope detection breaks when A_m > A_c
 * Which occurs because the envelope detector relies on the signal being on 'top' of the carrier, so it appears after rectification


### ex31/b/c/d.png


##Exercise 4


####Recieving and Transmitting

#####Transmission

 * Opens up the Tx session with the correct device
 * Sets device signal parameters from the input parameters (Gain, F_c, IQ rate)
 * While loop
  * Generates sine wave, sends it to Write Tx Data
  * Write Tx Data sends the baseband signal to the USRP for transmission
  
#####Recieving

 * Opens Rx session
 * Configures signal paramaters, (Gain, F_c, IQ rate)
 * Does coherant demodulation
 
