# pic-rng
## A USB True Random Number Generator Using a PIC16F1455

There are a number of existing true hardware random number generators
out there with cryptographic applications, but some of them use quite
sophisticated hardware and it is as such harder to verify them for
integrity as one would wish. I wanted to make a RNG circuit that is
easy enough for anyone with a little hardware skill to be able to
build. I wanted as well to remove as far as possible all proprietary
components and make it reasonably fast.

## Circuit Design

The gEDA schematics, as well as an image of the schematic, are in the
hw directory. The circuit design is based upon a reverse biased
semiconductor junction similar to the ChaosKey, and is largely based
on the design given [here](https://web.jfet.org/hw-rng.html), except I
have used 74LS14 Schmitt trigger inverters instead of a 74ALS04
which I have been unable to get. As suggested in the link I have used
a MAX232 to provide the 16V reverse bias required to get the 2N3904's
semiconductor junction to produce noise.  The MAX232 is not used in
the circuit for anything else, though it could conceivably be used to
build an alternative RS-232 interface if one were so inclined.

I originally wired up the random number generator circuit to an
Arduino Nano, and in that way was able to put the 2N3904-based random
bit generator circuit through its paces. It passes the [ENT test
suite](http://www.fourmilab.ch/random/), FIPS 140-2 via the rng-tools
package's rngtest command, and the
[Dieharder](http://www.phy.duke.edu/~rgb/General/dieharder.php) suite
of random number tests. The latter though still comes up with some
'weak' results but the vast majority of tests do pass. I think this
might partially be due to some further bias in the circuit, but it is
hard to investigate given how slow the Arduino has been in interfacing
with my PC.  I would have stuck with the Arduino version but alas I
have been unable to get the Arduino version to send random data to my
PC at a rate higher than 115200 bits per second. The Dieharder tests
use an awful amount of random bits to come up with meaningful
results. And so I had to look at a different approach.

I chose a PIC16F1455 as it seems to be one of the cheapest
microcontrollers available capable of interfacing via USB.

There is no PCB design available. I have not made an actual PCB of the
circuit and have no plans of doing so myself in the near future.  I
have simply taken a pre-made prototyping circuit board, and soldered
everything on with wires to link them all together.  My current
hardware set up, including the Arduino-based in-circuit programming
system I am using (based on [this
project](https://github.com/jaromir-sukuba/a-p-prog)) looks like
[this](http://imgur.com/a/3ct9s).

## Firmware

I haven't even started with this yet.  Currently doing research and
initial coding.  Not yet sure if this is going to look like a USB HID
or a USB CDC class device once it's done.  We will see how it works.

