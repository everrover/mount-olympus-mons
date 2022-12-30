# Active recon

> Active recon: Info gained via ***direct engagement*** with target. Can be made to look like regular client activity(eg: web browsing while connected to 100s and 1000s of users).

Social engg is done at times.(eg: visiting the premises, making phone calls, etc.).

### Common tools

- Web browsers(with their inspectors and debug tools)
- Search engines(with advanced search options)

### `ping` tool: Check weather remote system is online

- Validates that network is connecting to remote system in question
  - Blockages
    - Firewalls
    - Faulty network devices along the route
    - System unplugged from n/w
- Uses ICMP(Internet Control Message Protocol) protocol
  - ICMP Echo packet sent
  - ICMP Echo reply rcv

```shell
ping <M/C_IP/HOSTNAME>
ping google.com -c 5 # send 5 packets
ping google.com -s 24 # header byte: 8 Bytes, Payload bytes: 24 Bytes
```

### `traceroute`

> Finds **hops**(IP addresses of routers) and router **count** along the path towards network host. 

Following are to be notes while evaluating the response of `traceroute`
- Three ICMP packets are sent with incrementing TTL after getting a response. 
  - Some req may return response and some may not 
- Routers may drop req if TTL expires
- Routes extracted might be different on each run
  - For hops may come and go depending on the time and circumstances
- Public IP addresses might be returned via routers

How it works: Notes on the image

### Telnet: `telnet`

- Uses TELNET protocol
- Communicates in *plaintext*
- Default port: `23`
- Secure alternativeL: `ssh` Used already
- Used for remote connection to a server and issuing shell based commands over it.
  - Similar to shell operations we do on AWS EC2

### Netcat: `nc`

- Can serve both as **server** and **client**
- Supports both TCP AND UDP protocols

```shell
nc HOST PORT # server ops
nc 10.10.37.114 23 # for connecting to server

nc -vlnp PORT # start server with PORT
nc -vlnp 23
```