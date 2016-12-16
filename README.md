# ECE-287-DES-Project
DES encryption/decryption
Kyle Palmer
Alex Lee

DES Encryption on the DE2-115 Board

The Data Encryption Standard (DES) algorithm is an older encryption standard widely  used in the public and private sectors from 1976 to 1999 to protect data of moderate sensitivity that need to be regularly accessed. As computer technology advanced, it became more and more feasible to break DES in a reasonable time span. It was initially succeeded by triple DES, which extended the algorthim's lifespan into the late 1990's at which point it was fully phased out in favor of AES. DES works by applying a 64-bit key to some message text 64-bits at a time. It converts the inputted text into an encrypted version known as ciphertext. The process can then take the ciphertext and return it to its initial state by applying the keys produced within the system in opposite order. The DES algorithm is composed of three key elements; the key schedule, the S-Box look up tables, and the feistel function used to apply them.
For our project we are implementing DES in hardware, taking in a user inputted key and text to be encrypted and eventually decrypted. The challenge with this project is the complicated algorithm being implemented on the hardware with the timing requirements. There are many steps which all rely on one another to function. We first start the process with taking in the 64-bit text and key. We then take the 64-bit key and remove every 8th bit in the sequence and move around the bits, placing them in a new 56-bit arrangements. With the key now being reduced to 56-bits, we split it into two separate 28-bit parts. A number of left shifts are performed on the two separate keys,  16 times, resulting in 16 new pairs of 28-bit keys. These keys are all then concatenated together in pairs, sent through the same permutation, and then turn the 56-bit total arrangements into new 48-bit arrangements, removing 8 more bits from each. We then begin changing the text inputted by the user, we start by rearranging the bits, maintaining the 64-bit length, unlike the process with the keys. Using this new permutation of the text, we split it into two halves: A and B. A0 and B0 are  This is then XOR’d with the respective keys, . We want to XOR this result with the 32-bit halve of the text which means it must be returned to 32-bits. This is done with what is called S-Boxes. Each box contains 4 rows of 4-bit numbers, 1 through 15 with no repeats. Taking C in 6 bit chunks, we map them to a look-up table to the values in the S-Boxes. This happens with 8 unique S-Boxes which are at the end concatenated making a 32-bit number “ D.” We use each value generated from this, setting A1 equal to A0, and B1 equal to A0 XOR’d with D. This happens 16 times, resulting in one final A and B. We the concatenate these, B and then A. Finally the concatenated product is sent through on more permutation, rearranging the bits. This is the output of our machine, the encrypted message. To decrypt the message we impose the keys onto the system in opposite order, flipping the two halves and then going about the same process as described above. To implement DES encryption/decryption in Verilog we began by breaking it into the smallest of components we could. We broke the process into basic permutations such as Feistel Rounds, S-Boxes, and timers. In Feistel we did the majority of our operations. This was the controller for the key schedule, initial permutation, S-Box operations, and final permutations. In Control we control the actual encryption and decryption process that uses what we get in Feistel. The output from Control is the result of the processes as described above. In image3 this is before the encryption process is began and after the user inputs the key and text. In image2 this is the result of the encryption process. In image1 it displays the result from the decryption process.

Resources: The DES Algorithm Illustrated by J. Orlin Grabbe originally featured in the Laissez Faire City Times Vol.2 Nov 28.
