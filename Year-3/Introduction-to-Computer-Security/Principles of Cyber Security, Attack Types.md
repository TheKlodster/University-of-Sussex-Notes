# Introduction, Principles of Cyber Security & Attack Types

### Learning Aims
1. Discuss key dimensions of computer security (secrecy, authentication, integrity, anonymity) and their relationship to the main threats and attack techniques.
2. Describe the main building blocks of cryptography.
3. Deploy up-to-date tools and techniques for finding vulnerabilites in computer systems.
4. Design secure computer systems by using established computer security principles.

## Fundamental Security Design Principles
- *Economy of mechanism*
- *Fail-safe defaults*
- *Complete mediation*
- *Open design*
- *Separation of privilege*
- *Least privilege*
- *Least common mechanism*
- *Psychological acceptability*
- *Isolation*
- *Encapsulation*
- *Modularity*
- *Layering*
- *Least astonishment*

### Key Security Concepts
- **Confidentiality**
  - preserving authorised restrictions on information access and disclosure.
- **Integrity**
  - guarding against improper information modification or destruction.
- **Availability**
  - ensuring timely and reliable access to use of information.
  
<center>

<img src="https://images.slideplayer.com/25/8072066/slides/slide_9.jpg">

</center>

### Vulnerabilities, Threats and Attacks
- **Vulnerability Categories**
  - corrupted (loss of integrity).
  - leaky (loss of confidentiality).
  - unavailable or very slow (loss of availability).
- **Threats**
  - capable of exploiting vulnerabilities.
  - represent potential security harm to an asset.
- **Attacks**
  - passive - attempt to learn or make use of information from the system.
  - active - attempt to alter system resources or affect their operation.
  - insider - initiated by an entity inside the security parameter.
  - outsider - intiated from outside the perimeter.

### Countermeasures
- Means used to deal with security attacks:
  - prevent.
  - detect.
  - recover.

### Threat Consequences
1. **Unauthorised Disclosure.**
    - entity gains access to data which they are not authorised.
2. **Deception.**
   - entity receiving false data and believing it to be true.
3. **Disruption.**
   - prevents the correct operation of system services and functions.
4. **Usurpation.**
   - control of system services or functions by an unauthorised entity.

<center>

<img src="https://slideplayer.com/slide/13337350/80/images/11/Computer+and+Network+Assets%2C+with+Examples+of+Threats.jpg">

</center>

## Attack Surfaces
Consists of the reachable and exploitable vulnerabilities in a system. 

Categories:
- Network Attack Surface.
  - vulnerabilities over an enterprise network, WAN or the internet.
- Software Attack Surface.
  - vulnerabilities in application, utility or operation system code.
- Human Attack Surface.
  - vulnerabilities created by personel or outsiders, such as social engineering, human error, and trusted insiders.