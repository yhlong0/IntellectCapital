# Building Secure & Reliable Systems

1. Reliability and security are both crucial components of a system, the Google password manager's failure was triggered by a reliability problem--poor load-balancing and its recovery was later complicated by multiple measures designed to increase the security of the system. 
2. When designing for reliability, you assume that something will go wrong at some point. When designing for security, you must assume that an adversary could be trying to make things go wrong at any point. 
3. In the absence of an adversary, systems often fail safe (or open): An electronic lock is designed to remain open in case of power failure, however this can lead to obvious security vulnerabilities. 
4. In designing for reliability, you often need to add redundancy to systems, while redundancy increases reliability, it also increases the attack surface. An adversary need only find a vulnerability in one path to be successful. 


