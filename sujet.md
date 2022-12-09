# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers
1. Indeed, ships, planes, missiles and space vehicles are equipped with an inertial guidance system composed of several tools such as the internal computer, gyroscopes and accelerators, all of which allow the measurement of some of the vehicle's movements: its position, speed, inclination, etc. .... It was this inertial guidance system that caused the crash and explosion of the Ariane 5 rocket.
Indeed, the Ariane 4 rocket had been used as a programming model for the construction of Ariane 5. A copy and paste operation was used to duplicate volumetric data (the source of the bug, so local), but Ariane 5 was much larger and heavier.
The rocket pressure obeyed the basic codes of the programming system, causing a computer failure because of the unfairly duplicated volumetric values. A pressure measurement output not suitable for take-off, fatally causing the explosion. An error that cost a lot of money, in terms of human resources and work.
The incident, due to an integer overflow in the memory registers of the electronic computers used by the autopilot, caused the failure of the rocket's navigation system, effectively destroying it and the payload.
There were no casualties from the rocket's fallout, no humans were on board the flight. However, $500,000 million went up in smoke.
ESA immediately tried to find the cause of this spectacular crash. Experts from all countries met and a report was drawn up, only one month after the crash.
Yes, by doing unit tests on different scenarios with a good set of data provided, we think this could have avoided the crash as the programmer would have realised and fixed it.

2. Bug: SetUniqueList.createSetBasedOnList does not add list items to return the value as specified in the documentation until version 4.2.
This is a local bug as a method call was accidentally removed.
In the documentation, the createSetBasedOnList method should provide a new set with the same type as the provided set and fill it with all the list elements. However, this method does not add any more list elements to the return list.
Indeed during a commit it removed the addAll method ... So to fix this bug they just had to add it.
The reading of the various comments did not allow us to determine if they had put measures in place to avoid this kind of problem in the future.

3. They take action by assuming that a region has been taken offline: then they redirect customer requests to other
Amazon regions, and observe the effects.
They use various real-world events
One obvious choice is to look at historical data to see what types of inputs have been involved in previous system outages, to ensure that the types of problems that occurred previously cannot happen again.
However, any input that you think might disrupt the system's steady-state behaviour is a good candidate for an experiment
Some examples of inputs that Netflix uses in these experiments:
● terminating virtual machine instances
● inject latency into requests between services
● fail requests between services
● fail an internal service
● make an entire Amazon region unavailable

4. The main advantages of having a formal specification for WebAssembly are the following:
●security: the behaviour of the language is well deterministic since it has been proven since its construction
●fast: verification checks are automatic since the language specification is formal
However, all these advantages do not exclude testing of WebAssembly language implementations. Indeed the design is proven but not the implementation, the tests will allow to check and validate the implementations

5. The main advantages of the mechanical specifications:
	**
		*concrete and exhaustive verification
		* verification by checking 
	**
		*this mechanised specification has allowed to improve the formal specification. Indeed it has allowed to detect and correct the errors of the formal specification
	**
		*by successfully passing all the tests of the formal specification with its implementation of the specification
	**
		*This new specification does not eliminate the need for testing as testing still has its place in the validation of a given implementation.
