#Lab 1

##Exercise 1

 * Learned the basic interface of LabView
 * Made a text to ASCII Byte array (UTF-8) 
 * Interpreted as Temperatures in F, converted to C
 * Got average of whole array (each letter converted to one element of byte array)  
 * Got to understand the UI

**Block diagram and front panel for exercise 1 with my surname as input**
![Exercise 1](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex1.png)

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


###Tasks


**Original block diagram**
![Exercise 2.1](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex2.1.png)



 * Control to stop afer 1000 iterations was added by using a => block comparing the while loop count with a constant of 1000 and feeding that into the stop condition.


**Stop after 1000 iterations block diagram**
![Exercise 2.2](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex2.2.png)

####Revising so output is a standardised normal distribution
 
 * To convert into a standard normal distribution: N(0, 1), the equation below was used

![Equation 1](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/eq1.png)


 * Assumed the Random Number Generator block had a uniform distribution of [0,1] which gives population mean standard deviation as below
 

![Equation 2](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/eq2.jpg)

![Equation 3](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/eq3.jpg)

 * This was implemeneted by subtracting 0.5 from the sample mean, then dividing by the population standard dev. (above) divided by SQRT(n) (where n is 100)
 * The rest of the code was not changed
 
**Block diagram after the change**
![Exercise 2.3](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex2.3.png)



##Exercise 3


 * Wired up three sine waves, and added them up
  * FFT PSD module
  * Two adder blocks, as extending one adder block to do three gave me an error
   *  
  * Filter added with controls
 * Creating graphs from the panel view was a new concept
  * Very useful

###Tasks

**Block Diagram**
![Exercise 3.2](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex3.1.png)
**Front panel with all requested waveforms**
![Exercise 3.2](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex3.2.png)

####Chaging filter parameters 

 * Filter changed to a bandpass filter with cut off frequencies of 25 and 35
 * This let mostly only the sine wave at 30Hz through
 * Along with a transient of course.
 * This works because its both a high pass and low pass filter
 
**Front Panel for bandpass filter**
![Exercise 3.3](https://github.com/JacobKay97/CommsLab/blob/master/Lab1/Ex3.3.png)



#Lab 2

##Exercise 1

 * Created AM signal
 * Obeyed the equation given in the notes
 * PSD of modulated signal had two sidebands
 * Also turned it into a Sub-VI
 
###Tasks

**Block diagram for AM modulation**
![Exercise 1.1](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/Ex1.1.png)
**Front panel for initial test**
![Exercise 1.2](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/ex1.2.png)

####A_c = 2 and changing A_m for varying mu

 * Changing AM to give mu of {.5, 1, 1.5} 
 * Increasing mu changes the AM signal
  * at 1 the modulated signal's lowest point is 0, however going being that leads to the message signal being bigger than the carrier
  * Looks a bit weird, would break envelope detector
  
  
**Mu = 0.5**
![Exercise 1.3a](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/Ex1.3a.png)
**Mu = 1.0+**
![Exercise 1.3b](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/Ex1.3b.PNG)
**Mu = 1.5**
![Exercise 1.3c](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/Ex1.3c.PNG)


####Changing message frequency
 
 * Changing message frequency as {1k, 2k, 5k}
 * Aliasing as message frequency approaches carrier frequency
  * Technically carrier is sampling the message, reaching Nyquist frequency
  * Loss of information - unable to get full information back

**1kHz message**
![Exercise 1.4a](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/ex1.4a.PNG)
**2kHz message**
![Exercise 1.4b](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/ex1.4b.PNG)
**5kHz message**
![Exercise 1.4c](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/ex1.4c.PNG)


##Exercise 2

###Coherant Detection



 * Made coherant Demodulator
 * Scaling issues
 * Have to multiply demodulated signal by 2
  * However input carrier is not normalised, so have to divide by the amplitude of carrier
   * Or normalise carrier, but that was more wiring so opted for passing A_c through

Maths behind coherant detection
![eq1 ](https://github.com/JacobKay97/CommsLab/blob/master/Lab2/eq1.png)

###Enevelope Detector

 * Made envelope detector
 * Hopefully it works
  * Aliasing
 * Needed to pass through all the waveform properties from Waveform Properties to Build Waveform
 

##Exercise 3

 * Had a fuck tonne of issues, look back at exercise 2 for fixes
 
###ex3.png
 
###Changing mu

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
 
