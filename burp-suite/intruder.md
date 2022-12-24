# Burp Suite: *Intruder*

### [GO BACK](./intro.md)

> Allows request automation. Useful for fuzzy and/or bruteforcing.

> **Note:** It's ***highly rate-limited***. Hence alternatives are more commonly used

- Uses word-lists and fuzzy attacks. Example:
  - Brute-force enumeration
  - Word-list enumerations
- 

### Interface utils

- Positions: Helps us define the placeholders(enclosed within `§`) to where we apply fuzziness. COMMON UTILS: `Add`, `Clear`, `Auto`
- *ATTACK TYPES*
  - **Sniper**(Single set of payload): One field is variable(word-list is enumerated over this single field), rest are kept at constant hard-coded values. 
    - Example: For `username=§pentester§&password=§Expl01ted§` and word-list `[alpha, beta]`, enumerations are: [`username=alpha&password=Expl01ted`, `username=beta&password=Expl01ted`, `username=pentester&password=alpha`, `username=pentester&password=beta`].
  - **Battering ram**(Single payload set): Word-list is enumerated over all fields simultaneosly
    - Example: For `username=§pentester§&password=§Expl01ted§` and word-list `[alpha, beta]`, enumerations are: [`username=alpha&password=alpha`, `username=beta&password=beta`].
  - **Pitchfork**(Multiple payload sets): Similar to operations done in Python's `zip` operation. Multiple word-lists map to indivisual positions, in-order.
    - Example: For `username=§pentester§&password=§Expl01ted§` and word-lists `[alpha, beta]` and `[gamma, delta, omega]`, enumerations are: [`username=alpha&password=gamma`, `username=beta&password=delta`]
  - **Cluster bomb**: (Multiple payload sets): All possible combinations amongst word-lists(applied in order over positions) are enumerated.
    - Example: For `username=§pentester§&password=§Expl01ted§` and      word-lists `[alpha, beta]` and `[gamma, delta, omega]`, enumerations are: [`username=alpha&password=gamma`, `username=alpha&password=delta`,`username=alpha&password=omega`,`username=beta&password=gamma`, `username=beta&password=delta`,`username=beta&password=omega`]
- Payloads: These payloads can be of different types(`Simple list`, `Sequential numbers`, etc.), can be pre-processed/filtered before enumeration and can be encoded in URL in particular patterns.
- Resource pooling: Allocating certain resources(network connection pools, bandwidth, CPU, RAM, etc.) to particular kinds of attacks.

### Performing actual attacks 

- On most auth operations, on success or on failures, re-directs occur(with status code 302). 
  - Determining success or failures isn't trivial as monitoring 200 or 403/401/etc. respectively
  - Using other bulk metrics help though. Example: ***Monitoring response sizes*** can help. Successfull combination returns response with 800B response size, whereas failure returns with 500B.
- ***Need for Macro operations.***
  - If CSRF or Session auth has been applied, their respective tokens have to be passed with each request
  - These are to be different for each session and usage, or else 403(or sth similar) is observed if repeatedly used
  - Macro operations can be mimicked using Burp Suite for the same to mimic human usage before each enumeration

### Further studies

- Idea:: Walkthrough code tutorials on YT for CSec as practice
- Idea:: Start getting into CTFs for learning about it
- IG:: Most common wordLists and their sources

### Tools

- VS Code full walkthrough:: Using it as a pro
- Burp Suite:: Using it as a pro
- Similar tools:: -`ffuf` -`wfuzz`