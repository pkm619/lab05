# lab05

TO: Mark A. Yoder
From: Pushpendra Kumar
Date: 11/09/2015

Sub: Readme file for Lab05

Team 11: Pushpendra Kumar(B13132)
         Ankur Sardar (B13108)
         
In Lab 05 we use a ULTRA 4-pin Range finder, which we used for finding the time b/w signal sent and signal recieved 
from any obstacle.

So in this lab  basically first we designed a circuit digram for range finding sensor using fritzing software and then 
we write a code for finding the time b/w sending and receving the signal.

It was an intresting lab and alo find one more thing that can be used with the help of beagelbone.

Code:

var b = require('bonescript');
var trigger = 'P9_16', // Pin to trigger the ultrasonic pulse
echo = 'P9_41', // Pin to measure to pulse width related to the distance
ms = 2500; // Trigger period in ms
var startTime, pulseTime;
b.pinMode(echo, b.INPUT, 7, 'pulldown', 'fast', doAttach);
function doAttach(x) {
if(x.err) {
console.log('x.err = ' + x.err);
return;
}
// Call pingEnd when the pulse ends
b.attachInterrupt(echo, true, b.FALLING, pingEnd);
}
b.pinMode(trigger, b.OUTPUT);
b.digitalWrite(trigger, 1); // Unit triggers on a falling edge.
// Set trigger to high so we call pull it low later
// Pull the trigger low at a regular interval.
setInterval(ping, ms);
// Pull trigger low and start timing.
function ping() {
// console.log('ping');
b.digitalWrite(trigger, 0);
startTime = process.hrtime();
}
// Compute the total time and get ready to trigger again.
function pingEnd(x) {
if(x.attached) {
console.log("Interrupt handler attached");
return;
}
if(startTime) {
pulseTime = process.hrtime(startTime);
b.digitalWrite(trigger, 1);
console.log('pulseTime = ' + (pulseTime[1]/1000000-0.8).toFixed(3));

    
}
}

