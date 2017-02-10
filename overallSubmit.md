# Jacob Kay
# Comms Lab
# Ay-05-10
# Logbook
# Link to github, it looks nicer there (check commit time)
# https://github.com/JacobKay97/CommsLab/blob/master/overallSubmit.md
# .
# .
# .
# .
# .
# .
# .
# .
# .
# .
# .
# .



_______

# Lab 1
## Exercise 1

 * Learned the basic interface of LabView
 * Made a text to ASCII Byte array (UTF-8)
 * Interpreted as Temperatures in F, converted to C
 * Got average of whole array (each letter converted to one element of byte array)  
 * Got to understand the UI

**Block diagram and front panel for exercise 1 with my surname as input**

![Exercise 1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex1.png)

## Exercise 2

### Implementation of CLT

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


### Tasks


**Original block diagram**

![Exercise 2.1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex2.1.png)



 * Control to stop afer 1000 iterations was added by using a => block comparing the while loop count with a constant of 1000 and feeding that into the stop condition.


**Stop after 1000 iterations block diagram**

![Exercise 2.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex2.2.png)

#### Revising so output is a standardised normal distribution

 * To convert into a standard normal distribution: N(0, 1), the equation below was used


![Equation 1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/eq1.png)


 * Assumed the Random Number Generator block had a uniform distribution of [0,1] which gives population mean standard deviation as below



![Equation 2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/eq2.jpg)


![Equation 3](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/eq3.jpg)

 * This was implemeneted by subtracting 0.5 from the sample mean, then dividing by the population standard dev. (above) divided by SQRT(n) (where n is 100)
 * The rest of the code was not changed

**Block diagram after the change**

![Exercise 2.3](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex2.3.png)



## Exercise 3


 * Wired up three sine waves, and added them up
  * FFT PSD module
  * Two adder blocks, as extending one adder block to do three gave me an error
  * Filter added with controls
 * Creating graphs from the panel view was a new concept
  * Very useful

### Tasks

**Block Diagram**

![Exercise 3.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex3.1.png)

**Front panel with all requested waveforms**

![Exercise 3.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex3.2.png)

#### Changing filter parameters

 * Filter changed to a bandpass filter with cut off frequencies of 25 and 35
 * This let mostly only the sine wave at 30Hz through
 * Along with a transient of course.
 * This works because its both a high pass and low pass filter

**Front Panel for bandpass filter**

![Exercise 3.3](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab1/Ex3.3.png)


_______

# Lab 2

## Exercise 1

 * Created AM signal
 * Obeyed the equation given in the notes
 * PSD of modulated signal had two sidebands
 * Also turned it into a Sub-VI

### Tasks

**Block diagram for AM modulation**

![Exercise 1.1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/Ex1.1.png)
**Front panel for initial test**

![Exercise 1.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex1.2.png)

#### A_c = 2 and changing A_m for varying mu

 * Changing AM to give mu of {.5, 1, 1.5}
 * Increasing mu changes the AM signal
  * at 1 the modulated signal's lowest point is 0, however going being that leads to the message signal being bigger than the carrier
  * Looks a bit weird, would break envelope detector


**Mu = 0.5**

![Exercise 1.3a](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/Ex1.3a.png)
**Mu = 1.0**

![Exercise 1.3b](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/Ex1.3b.PNG)
**Mu = 1.5**

![Exercise 1.3c](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/Ex1.3c.PNG)


#### Changing message frequency

 * Changing message frequency as {1k, 2k, 5k}
 * Aliasing as message frequency approaches carrier frequency
  * Technically carrier is sampling the message, reaching Nyquist frequency
  * Loss of information - unable to get full information back

**1kHz message**

![Exercise 1.4a](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex1.4a.PNG)

**2kHz message**

![Exercise 1.4b](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex1.4b.PNG)

**5kHz message**

![Exercise 1.4c](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex1.4c.PNG)


## Exercise 2

### Coherant Detection



 * Made coherant Demodulator
 * Scaling issues
 * Made into subVI
 * Have to multiply demodulated signal by 2
  * However input carrier is not normalised, so have to divide by the amplitude of carrier
  * Or normalise carrier, but that was more wiring so opted for passing A_c through
 * Remove DC value as it is the 0.5(A_c^2) term

**Maths behind coherent detection**


![eq1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/eq1.png)


**Coherent detector block diagram**

![ex2a](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex2a.PNG)


### Envelope Detector

 * Made envelope detector
 * Aliasing issues when mu => 1
 * Needed to pass through all the waveform properties from Waveform Properties to Build Waveform
  * Forgot so had issues building waveform
 * Made into subVI

#### Maths behind it

 * Multiply by pi because rectifier scales it down by pi
 * Turn waveform into an array
 * Rectify using a loop and case statement
 * This gives just the top half of the modulated signal which has the message riding on it
 * Low pass filter will get rid of the carrier frequency (mathematically) as message has a lower frequency
  * In actual physical implementation, RC filter is used, so capacitor basically 'traces' (for lack of a better word) and 'fills in the gaps' to recover the message signal
 * DC term has to then be removed, and message signal is recovered

**Block diagram for envelope detector**

![ex2b](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex2b.PNG)




## Exercise 3

* Connected together the modulator  with both coherent and envelope detectors
* Worked on first attempt

**Block diagram for AM**

![ex3](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex3.PNG)

### Changing mu

 * Coherent detection worked for all values
 * Envelope detection breaks when A_m > A_c
 * Which occurs because the envelope detector relies on the signal being on 'top' of the carrier, so it appears after rectification
  * get loss of information
  * Envelope is only the positive half of the wave, so when A_m > A_c; (A_c + A_m) < 0  so the modulated signal no longer 'rides' on top of the carrier... (Unable to explain in better words..)


**mu=0.5**

![ex3a](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex3a.PNG)

**mu=1**

![ex3b](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex3b.PNG)

**mu=1.5**

![ex3c](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex3c.PNG)
**mu=2**

![ex3d](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex3d.PNG)



## Exercise 4


#### Receiving and Transmitting

##### Transmission

 * Opens up the Tx session with the correct device
 * Sets device signal parameters from the input parameters (Gain, F_c, IQ rate)
 * While loop
  * Generates sine wave, sends it to Write Tx Data
  * Write Tx Data sends the baseband signal to the USRP for transmission

##### Receiving

 * Opens Rx session
 * Configures signal parameters, (Gain, F_c, IQ rate)
 * Does coherent demodulation


#### Transmission of 5kHz signal

**Transmit panel**

![ex4a-tx](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4a-tx.PNG)

**Receive panel**

![ex4a-rx](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4a-rx.PNG)


#### Noise

 * Changed modulation index

**Modulation index = 0.1 - signal very noisy**

![ex4b-rx-mu0.1-noise](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4b-rx-mu0.1-noise.PNG)

**Modulation index = 0.75 - quite noisy**

![ex4b mu0.75](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4b-rx-mu0.75-noise-zoomed.PNG)
**Modulation index = 1.5 - not noisy**

![ex4b mu 1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4b-rx-mu1-noise.PNG)

**Modulation index = 5 - noisy??**

![ex4b mu 5](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab2/ex4b-rx-mu5-noise.PNG)



_______

# Lab 3

## Exercise 1

 * Created FM modulator
 * Basically implemented the s(t) equivalent equation directly with the blocks
 * Didn't have any issues

**Block Diagram for FM modulator**

![ex1 block](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex1%20Block%20Diagram.PNG)

 * Increased k_f (deltaf = k_f * max|m(t)| and max|m(t)| = 1) from 500 to 2000 to 5000

**k_f = 500**

![k_f=500](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex1%20Block%20Diagram.PNG)

**k_f = 2000**

![k_f=2000](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex1%20kf%20%3D%202000.PNG)

**k_f = 5000**

![k_f=5000](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex1%20kf%20%3D%205000.PNG)


 * increasing k_f increases how much the instantaneous frequency changes with m(t)
 * So FM is very visible when k_f = 5000
  * at m(t)= -1, f_i = 10k-5k =5kHz
  * at m(t)= 1, f_i = 10k+5k = 15kHz
 * Becomes wideband
 * PSD shows the bandwidth taken up by the FM
 * modulation index, mu decides if narrow or wide band if mu << 1
 * kf = 500, mu = 0.5
  * Narrowband FM, Bandwidth approximately 2 x message bandwidth
 * kf = 2000, 5000 mu = 2, 5
  * Wideband FM
  * Bandwidth approximated by 2 x delta_f (kf in this case)
  * B approximately = 4000, 10000
 * Can see from PSD that this is relatively accurate


## Exercise 2

 * Copied envelope detector blocks
 * Just had to change the scaling factor
 * Maths below

**Maths explaining derivation of demodulator**

![eq2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/png.png)


**Block Diagram**

![ex2.1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex%202%20block%20diagram.PNG)


## Exercise 3

 * Created FM simulation
 * Wired up modulator with demodulator
 * Worked well

**Block Diagram**

![ex3.a](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/Ex%203%20block%20diagram.PNG)

**Front panel with required input**

![ex3.1](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/EX3%20graphs%201.PNG)

**Front panel zoomed in on demodulated(t) graph**

![ex3.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/EX3%20graphs%202.PNG)

 * Scaling was done correctly, FM worked

## Exercise 4


 * Verified carsons rule worked well

**Frequency deviation of 5kHz**

![ex3.2](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab3/ex4 kf5k.PNG)

 * Bandwidth as predicted ~ 12kHz


 _______


# Lab 4

## Exercise 1

 * Made BPSK transmitter
 * Generate random sequence of bits
 * Scale so 0 --> -1, 1 --> +1
  * Multiply by 2, take 1 away
 * Add frame header
 * Upsample
 * Convolute with filter coefficients
 * Scale, insert pilots, add frame header again
 * Needs to be complex valued for USRP

### Tasks

 * L = 20


**Block Diagram**

![Block diagram for BPSK transmitter](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab4/EX1%20block%20%20diagaram%20of%20my%20addition.PNG)

**Root Raised cosine**

![Root raised cosine](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab4/Ex1.1%20root%20raised%20cosine.PNG)

**Rectangular pulses**

![Rectangular pulses](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab4/Ex1.1%20none%20in%20pulse%20shaping%20filter.PNG)


 * Root raised cosine rolls off a lot quicker
 * Main lobe bandwidth ~2E-7
 * Rectangular pulses rolls off slower
 * More lobes present
 * Main lobe has very similar bandwidth



## Exercise 2

 * Made receiver
 * Basically followed the instructions in the notes
 * number of samples into receiver = message bits * L * arbitrary number because receiver doesn't always start at correct point
 * Getting BER of 0 - very good

**Block diagram of receiver**

![EX2 block](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab4/Ex2%20block.PNG)

**Picture of front panel for rx=tx=0**

![EX2 panel](https://raw.githubusercontent.com/JacobKay97/CommsLab/master/Lab4/EX2%20normal.PNG)


 * Ran 5 times and got BER average for various rx tx

| Tx Gain (dB) | Rx Gain (dB) | Average BER |
| --- | --- | --- |
| 0 | 0 | 0 |
| -35 | -15 | 0.172711|
| -37 | -15 | 0.231933 |
| -40 | -15 | 0.312612 |


## Exercise 3

 * used basic ECC
 * Tripled bits using build array
 * FEC


| Tx Gain (dB) | Rx Gain (dB) | Average BER |
| --- | --- | --- |
| 0 | 0 | 0 |
| -35 | -15 | 0.134 |
| -37 | -15 | 0.1998 |
| -40 | -15 | 0.4346 |


 * Some improvement in BER
 * Issues out of my control
 * I don't think its syncing the frame correctly
 * Issues with the receiver triggering at the correct time
 * Hence I don't think my BER values are reliable
 * Would have preferred to build decoder for this
 * Disadvantage is that 3 bits transmitted = 1 bit of data
 * so have to spend 3 times as long Transmitting
 * 3 times as much power used


## Exercise 4

 * Kind of ran out of time to do it
 * I have ideas of how to implement it
