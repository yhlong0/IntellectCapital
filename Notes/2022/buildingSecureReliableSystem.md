# Building Secure & Reliable Systems

1. Reliability and security are both crucial components of a system, the Google password manager's failure was triggered by a reliability problem--poor load-balancing and its recovery was later complicated by multiple measures designed to increase the security of the system. 
2. When designing for reliability, you assume that something will go wrong at some point. When designing for security, you must assume that an adversary could be trying to make things go wrong at any point. 
3. In the absence of an adversary, systems often fail safe (or open): An electronic lock is designed to remain open in case of power failure, however this can lead to obvious security vulnerabilities. 
4. In designing for reliability, you often need to add redundancy to systems, while redundancy increases reliability, it also increases the attack surface. An adversary need only find a vulnerability in one path to be successful. 
5. Least Privilege: grants the least privilege necessary for any given task or action path to ensure that users don't have *ambient authority*.
6. Zero Touch: Zero Touch Networking reduce outages by removing direct human access to production roles. Instead, human have indirect access to production through tooling and automation that make predictable and controlled changes to production infrastructure. 
7. If your dependencies are up to date, it's likely you can apply a critical patch directly instead of needing to merge with a backlog of changes or apply multiple patches. 
8. 


