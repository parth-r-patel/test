Distributed System
===
## Final Exam Question Preperation
*Created based on questions outlined by professor*

---

<style>
.question {
	color: #009688;
}
.answer {
	color: #727272;
}
.index {
	color: #B2DFDB;
}
</style>

<div class="question">
**1. How can UDP be made reliable? (messages are received + in the right order)**
<p class="answer">
<span class="index">
*Chapter 5 - Remote Invocation* <br>
</span>
UDP can be made more reliable through the **Request-Reply(RR)** exchange protocol <br>
Reliability ensures: <br>
**validity** - messages sent are delivered <br>
**integrity** - messages are received as they are sent <br>
Validity can be addressed by using timeouts and treating server replies as acknowledgements.
If a reply is not received before the timeout, retransmit request. If retransmit causes a
duplicate request, the server can ignore subsequent requests by filtering out requests with
the same request ID. If operations are not idempotent, then using a history for recent
requests would allow for replies for requests with the same request ID to produce the correct
reply. The request ID is a part of the RR exchange protocol, a simple incremental integer.
</p>

**2. Multithreading with Blocking vs. Non-blocking I/O**
<p class="answer">
<span class="index">
*Assignment 3 | Solman 6.8 | Chapter 7 - OS Support (slide 21)* <br>
</span>
Blocking I/O is synchronized and non-blocking is asynchronized, like counter example
Assignment 3
</p>

**3. Vector Clock Diagram**
<p class="answer">
<span class="index">
*Assignment 3 | Solman 10 | Chapter 14 - Time and Global States (slide 36+)* <br>
</span>
A vector clock of N processess is an array of N integers, each process keeps its own vector clock <br>
V = vector i,j = processes <br><br>

VC1. Vi[j] = 0 for i,j = 1...N <br>
VC2. Just before Pi timestamps event, Vi[i] = Vi[i] + 1 <br>
VC3. Pi includes the value t = Vi in every message
VC4. When Pi receives a timestamp t it merges, it sets Vi[j] = max(Vi[j], t[j] for j = 1...N <br>
4.5 After merge before next event, add 1 to its own element using VC2 <br><br>

V = V' iff V[j] = V'[j] for j = 1...N <br>
V <= V' iff V[j] <= V'[j] for j = 1...N <br>
V < V' iff V <= V' && V != V' <br>
</p>

**10. Idempotent vs. Nonidempotent Operations**
<p class="answer">
<span class="index">
*Solman 4* <br>
</span>
**Idempotent** - multiple invocations of the same method produce the same result <br>
**Nonidempotent** - each invocation of a method has unique results <br>
Pressing an elevator request button is idempotent <br>
Writing data to a file is idempotent if write is done using location sequences, will always write to locations<br>
Writing data to a file using a pointer is not idempotent because each time the pointer will progress and consequent calls will be affected <br>
Appending data to a file is not idempotent <br>
It is necessary for the operation to be state independant for idempotence
</p>

**11. Clock Correction**
<p class="answer">
<span class="index">
*Solman 10 | Chapter 14 - Time and Global States (slide 13+)* <br>
</span>
Cannot just set the time back becasue processess may be running in a time dependant manner, i.e. waiting
</p>

**12. Group Multicast, Ordering (Total, FIFO, Causal)**
<p class="answer">
<span class="index">
*Solman 4,11,16 | Chapter 6 - Indirect Communication (slide 8+) possibly Chapter 4 - Inter Process Communication* <br>
</span>
**Correct Process** - is a proccess that isnt in a fault or isnt faulty <br>
Causal - if p1 sends m1 to p2 causing p2 to send m2 then m1 must receive before m2 everywhere (causal relationships) <br>
FIFO - if p1 sends m1 then m2 m1 and m2 received in that order everywhere, does not apply cross process <br>
Total - screw the sending, arbitrarly order messages across all processes (standardize-ish)
</p>

**13. Logical Clocks**
<p class="answer">
<span class="index">
*Solman 10 | Chapter 14 - Time and Global States (slide 31+)* <br>
</span>
- short fall is that L(e) < L(e') does not imply e happened before e'
- (Ti, i) < (Tj, j) if Ti< Tj or (Ti = Tj and i < j) this is total ordering to solve identical timestanps
</p>

**14. Consistent and Inconsistent Cuts**
<p class="answer">
<span class="index">
*Solman 10 | Chapter 14 - Time and Global States (slide 52+)* <br>
</span>
Inconsistent cuts are effects without cause, else cut is consistent
</p>

**16. Chandy Lamport Snapshot Algorithm**
<p class="answer">
<span class="index">
*Solman 10 | Chapter 14 - Time and Global States (slide 56+)* <br>
</span>
Follow slides and hope for the best
</p>

**19. Global State Lattice**
<p class="answer">
<span class="index">
*Solman 10 | Chapter 14 - Time and Global States (slide 67+)* <br>
</span>
For the lattice State i increases to the left, and j increases to the right. <br>
The level = i + j in Sij <br>
Initial state 00 is level 0, dont label final level <br><br>

Distributed Debugging can be done using the lattice structure linearization (traverse). <br>
**Possibly True** - when a predicate is ture for some state S, which is a part of a linearization <br>
**Definitely True** - when a predicate is true at some state in all linearizations <br>
possibly true follows existential property and definitely true follows universal property
</p>
</div>