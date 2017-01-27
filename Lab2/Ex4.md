#Exercise 4


### Recieving and Transmitting

####Transmission

 * Opens up the Tx session with the correct device
 * Sets device signal parameters from the input parameters (Gain, F_c, IQ rate)
 * While loop
  * Generates sine wave, sends it to Write Tx Data
  * Write Tx Data sends the baseband signal to the USRP for transmission
  
####Recieving

 * Opens Rx session
 * Configures signal paramaters, (Gain, F_c, IQ rate)
 * Does coherant demodulation
 
 
