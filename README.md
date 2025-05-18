# CSNotes
computer science a level 9618 notes

# Data types

###  User defined Type:
A datatype type based on an existing data type or data types that have been defined by a programmer
###  Non-composite Type:
a datatype that doesn't reference any other data type (primitive defined by the language)
  -  enumerated: A user defined non-composite data type with an ordered list of possible values
  -  pointer: a user-defined non-composite data type used to reference a memory location
###  Composite Type:
  -  set: a given list of unique an unordered elements on which mathematical set operations can be performed, such as union and intersection
  -  record: a composite data type consisting of several related data items that may be of different data types
  -  class: a template defining the templates and data of a certain kind of object
  -  object: an instance of a class that is self-contained and includes data and methods that interact with one another.

---

### File Organization

###  Serial Organization:
    - Stored in chronological order 
    - new records are added in the next available space, i.e. records are appended to the file
    - when access time doesn't really matter?
###  Sequential Organization:
    - Stored with ordered records and in the order of the key-field
    - new records are inserted in the correct position based on the order of the key field
###  Random Organization:
    - records stored physically in any available position 
    - hashing algo applied to keyfield of the record
###  Hashing
    - mathematical function that transforms input to a unique value
  ####  open hash
    - record added to next available space if no collision
    - if collision, record stored in next free space. makes lookup slower.
  ####  closed hash 
    - record added to next available space if no collision
    - overflow area set up for duplicate key-fields
    - if collision, record stored in next free space in overflow area
    - overflow area searched so slightly faster than open
###  Sequential file access
    - for serial organization, all records need to be checked UNTIL 
      record is found 
    - for sequential organization, records are checked until key-field is greater than current record or until record found. faster.
    - good if all records need to be processed
###  Direct file access
    - allows record lookup
    - uses key-field for sequential and hash for random

# Floating Point and Number Representation

###  why normalisation:
    - prevents multiple representations of the same number - standardization
    - removes leading and trailing zeroes
    - two MSB always different
###  Changing size of exponent:
    - changes range
###  Changing size of mantissa:
    - changes precision
###  Underflow:
    - when the result is too small to be precisely represented in the available system. mantissa size too small
###  Overflow:
    - result too big to be represented. exponent too small
###  Rounding Errors:
    - limited memory to represent numbers

---

# Networking and Protocols
###  overview: 
    - app, transport, internet, link
    - good for encapsulating data and functionality
###  Why use a protocol:
    - set a standard for communcation 
    - Protocols enable communication/compatibility between devices from different manufacturers 
    - If two devices were sending messages to each other using different protocols, they would not be able to communcate properly
##  Layers:
  ###  Application:
   - top-level
   - contains all programs that exchange data
  ### Transport:
    - receives data from the application layer
    - Breaks data into manageable *packets* - performs segmentation 
    - sequences the packets, adds data to packet header
    - sends the packets to the internet layer
    - handles packet loss or corruption - acknowledges receipt of complete error free packets
    - automatically resends packets if positive acknowledgment not received
#### host-to-host
        - three-way-handshake
        - host 'alice' sends packet to host 'bob'
        - bob checks packet containing sync bits
        - bob sends his own packet containing sync bits
        - if bits match, protocol is established
  ###  Internet
    - recieves packets from transport layer
    - wraps packet around its own header containing src & dst IP
    - Identifies intended network and host
    - transmits datagrams to link layer
    - routes packets indepedently through an optimum route - routing table used 
    - addresses the packets with their src and dst IP addr
    - then uses IP addr and port number to form a socket
  ###  Link:
    - direct access to hardware
###  Protocols
  ###  HTTP
    - for sending and receiving webpages/hypertext documents
  ###  FTP
    - Server: central computer where files to be downloaded are stored
    - Command: user can send action/instruction that is carried out on server
    - Anonymous: allows user to access files without the need to identify itself to the server

  ###  POP3
    - for receiving and downloading emails - pull protocol
    - used by email clients to retrieve email messages from a mail server
    - pull protocol 
    - keeps server and client in sync by not deleting original email
    - allows a copy of the email to be downloaded from the server
    
  ### IMAP
    - for receiving and downloading emails - pull protocol 
    - use by email clients to retrieve emails 
    - from a mail server
    - keeps server and clients (MULTIPLE!!) in sync by not deleting the original email (ocopy still exists)
  ###  SMTP
    - for sending and uploading emails - push protocol
  ###  BitTorrent
#### Tracker
        - central server that stores details of other computers that have parts of the file to be downloaded
        - has data on those peers downloading and uploading file
        - shares IP addr with other clients in the swarm allowing them to connect
#### Seed: 
        - a peer computer that has 100% of the file and is uploading the downloaded content

#### Swarm:
        - all connect pure computers that have all or part of the file to be downloaded. 
        • BitTorrent client software made available
        • One computer must keep a complete copy of the torrent/file to be shared
        • Torrent/file is split into small pieces
        • A computer joins (a swarm) by using the BitTorrent software to load a torrent descriptor file
        • The computer can now download a piece of the file
        • Once a computer has a piece it can become a seed and upload (to other members of the swarm)
        • Pieces of the torrent are both downloaded and uploaded (by each member of the of the swarm)
        • A server called a tracker keeps records of all the computers in the swarm
        • The tracker shares their IP addresses allowing them to connect to each other
---

# Network Communication Models

##  Circuit switching
  - a dedicated circuit is established before transmission starts and released after transmission ends
  - bidirectional
  - required where a dedicated path needs to be sustained
  - used in real-time communication, such as voice communication and private data networks
  ####  Benefits
    - data frames arrive in order and don't need to be reassembled
  ####  Drawbacks
    - A dedicated circuit is required
    - Data is transferred using the whole bandwidth
    - Nobody else can use the same circuit even if it is idle
    - Less secure as only one route is used, so packet sniffers can make more sense of a continuous stream of packets
###  Packet switching
  - data is split into packets and each packet is given its own optimal route, which depends upon congestion
  - used to send large files over the internet
  - when it isn't necessary to use the entire bandwidth
  - email, text messages, VOIP
  ####  Benefits
    - packets can be rerouted if there are problems
    - more secure as it is harder to intercept messages
  ####  Drawbacks
    - time taken to reassemble packets at destination
    - packets may not arrive in order
###  function of a router during packet switching:
    - router examines packet header for dst IP
    - router has access to routing table
    - looks up information about available hops, netmask, gateways used, and status of the routes along the route, such as network congestion 
    - decides on next best hop 
    - sends packet to the next best hop

---

# Processor Architecture
##  Pipelining: 
    - allows several instructions to be processed simultaneously
    - without having to wait for the previous instruction to be completed.
    - cycle goes like
        1. instruction fetch
        2. instruction decode
        3. operand fetch 
        4. instruction execute
        5. writeback

## RISC
  ###  Description: 
    - Fixed len instr 
    - Simple intr
    - uses pipelining
    - many registers registers
    - limited addressing modes
    - Hardwired and micro-coded control unit
    - instr require 1 clock cycle
    - cache is split between data and instr
###  CISC
    - Many instr formats 
    - Many different addressing modes 
    - Variable length instr 
    - Uses fewer registers
    - requires complex circuits
    - instructions may require many clock cycles 
    - Control unit is programmable as opposed to hardwired
###  Differences
    - RISC has fewer instructions // CISC has more instructions
    - RISC has many registers // CISC has few registers
    - RISC’s instructions are simpler // CISC’s instructions are more complex
    - RISC has a few instruction formats / CISC has many instruction formats
    - RISC usually uses single-cycle instructions// CISC uses multi-cycle instructions
    - RISC uses fixed-length instructions // CISC uses variable-length instructions
    - RISC has better pipelineability // CISC has poorer pipelineability
    - RISC requires less complex circuits// CISC requires more complex circuits
    - RISC has fewer addressing modes // CISC has more addressing modes
    - RISC makes more use of RAM// CISC makes more use of cache/less use of RAM
    - RISC has a hard-wired control unit // CISC has a programmable control unit
    - RISC only uses load and store instructions to address memory // CISC has many types of instructions to address
memor

####  SISD:
Single processor executes the a single instruction stream on the the same dataset
####  SIMD:
Many processors execute the same instruction on mulitple data sets
####  MISD:
Many processors, using different instructions, use the same data set
####  MIMD:
many processors, using different instructions, use different data sets

###  Massively parallel computers: 
    - Large number of processors working collaboratively AND simultaneously on the same program 
    - communicating via a messaging interface

---

## Virtualization

###  Virtual Machines:
  an emulated environment of a computer system that provides a layer of compatibility between software running on the guest OS and host OS
####  benefits
    - Multiple guest VMs/OSs can be used on the same computer allowing multiple OSs/VMs to coexist on a single computer
    - VM can crash without affecting host machine
    - security benefits such as malicious software only affects the virtual machine
    - Cost savings due to not needing to purchase extra hardware
    - Can run legacy applications that are currently incompatible
    - Different instruction set architectures can be emulated on a single computer
####  drawbacks
    - Less efficient / has poorer performance on real machines because of the extra load on the host computer 
    - Performance of the guest system cannot be adequately measured 
    - may be affected by any weaknesses of the host machine
    - increases maintenance overheads because both host system and vm(s) need to be maintained
    - cannot emulate some hardware because this hardware may have been developed since the virtual machine was developed

---

# Digital Logic

###  SR flip-flop
    - NAND
        1. S = R = 1 prints same state
        2. when s is 1 q is 1
        3. when r is 1 q is 0
        4. when s = r = 0 INVALID STATE Q = Q' = 1
###  JK flip-flop
    - when j = k = 1, sets output to logical complement
---

# Operating Systems

###  Functions of an OS 
  - multi-tasking
  - managing processes running on the CPU 
  - process scheduling 
  - paging
  - Interrupt handling
###  Process management
  -  multi-tasking
  -  process: dynamic version of a program being executed (task)
  ####  Process states
    -  Running: CPU resources currently being expended on the process
    -  Ready: still in queue awaiting cpu resources
    -  Blocked: due to interrupts. state restored after ISR is done.
  ####  Scheduling
#####  How an OS manages interrupts in low-level scheduling
        - cpu resources finite
        - all processes can't be executed at the same time. 
        - starvation is also a factor
        - uses the following algos to schedule processes
#####  Preemptive
        - a process may be interrupted by the scheduler (taken away from the CPU) by putting it in a blocked state if a another process with a higher priority arrives, or if the current process' time quantum expires. 
        - more responsive but complex
        - RR, SRTF
#####  Nonpreemptive
        - once a process starts, it has to finish
        - terrible interactivity, but more simple
        - jobs with a higher priority can't be executed until the current job is running
        - FCFS, SJF
#####  Round Robin 
      - each process is served for a fixed time slice
      -  Benefits
        - starvation doesn't occur because all processes are given equal priority and attention
      -  Drawbacks
        - starvation may occur
        - not suitable 
    -  Shortest job first
      -  Benefits
        - increased throughput as more processes can be executed in a smaller amount of time
      -  Drawbacks
        - longer jobs may be starved
    -  First come first served
      -  Benefits
      -  Drawbacks
    -  Shortest remaining time
      -  Benefits
      -  Drawbacks

###  Virtual memory
    - uses secondary storage to simulate additional main memory
    - so cpu appears to be able to access more memory space than the available RAM
    - only data in use needs to be in main memory so data can be swapped between RAM and virtual memory as necessary 
###  Paging 
  - allows memory to be divided into fixed size blocks (pages)
  - program given fixed-size chunks of logical memory (frames)
  - logical memory maps to physical memory (via frame number)
  - access times are faster 
  - replacement easier 
  - not necessarily contiguous
  -  Page replacement
    - LRU 
    - FIFO
    - LU
###  Segmentation 
  - divides memory into variable size blocks
  - access times are slower
###  Disk thrashing
    - overreliance on pages in virtual memory 
    - pages loaded from vm to main memory constantly 
    - more processing time goes to swapping than actual stuff
    - swapping has overhead, so execution slowed down

---

# Encryption
### concerns
CAIN (confidentiality, authenticity, integrity, non-repudiation)
###  Public key
    - key available to everyone
###  Private key
    - secret key for the sender
    - generated as a pair of public and private
###  Symmetric encryption
  ####  how
    - plaintext -> ciphertext
    - encryption algorithm used alongside a key 
    - same key used to decrypt cipher text 
    - key distribution problem
  ####  benefits
    - less computationally intesive
    - fine for already secure channels (TLS)
  ####  drawbacks
    - key distribution problem
    - anyone with the key can decrypt
###  Asymmetric encryption
####  how
    - alice's public and private key pair generated
    - bob uses alice's public key to encrypt plaintext
    - alice uses her private key to decrypt the doc
    - only alice can decrypt it. 
    
#### signature algo
    - practically used alongside digital signatures to satisfy CAIN
    - alice's plaintext -> hash function -> digest
    - digest -> encryption (using priv key) -> signature
    - plaintext + signature sent to bob
    
    - bob decrypts signature to get the digest 
    - passes plaintext through digest 
    - if digest1 = digest2 then integrity!
    - authenticity because digest couldn't have been encrypted without alice's private key
    - non-repudiation because alice signed it
    - NO confidentiality, double encryption solves this

#### double encyrption
    - alice's plaintext -> hashing function -> digest 
    - digest -> encryption (via alice's private key) -> signature
    - signature AND plaintext -> encryption (bob's public key) -> ciphertext

    - bob decrypts ciphertext using his private key -> plaintext
    - decrypts signature with alice's public key -> digest
    - plaintext -> hashing algo -> digest_new
    - if digest_new = digest then integrity!
    - non-repudiation because alice signed it duh
    - authenticity because decrypted using senders public key
    - confidentiality because plaintext was encrypted
###  Quantum cryptography 
####  benefits
    - leverages laws of physics - virtually unhackable
    - keys can be longer (??)
    - eavesdropping can be detected - because it uses photons
    - continuously improving so better security
####  drawbacks 
    - expensive as fuck
    - used by terrorists and criminals (IBM, Google)
    - susceptible to interference (error corrrection not sophisticated enough) - sunshine
###  SSL & TLS
####  Why?
    - Provide communcations security over a network via encryption 
    - enable two parties to identify and authenticate each other and communicate with confidentiality and integrity
####  explanation of each
    - An SSL/TSL connection is initiated by an application which becomes the client
    - The application receiving connection becomes the server 
    - Every new session begins with a handshake as defined by the SSL/TSL protocols
    - The client requests a digital certificate from the server 
    - Server sends digital certificate to client
    - Client verifies digital certificate and obtains server's public key
    - Encryption algorithms are agreed upon and session keys are generated
###  Digital certificate
  ####  What 
    - contains serial number, digital signature, version, algoirthm used, public key, vendor ID
  ####  how is it acquired
    - client asks web-server for certificate 
    - web-server - enquiry made to certificate authority (CA)
    - enquirer details checked by CA 
    - if enquirer details verified by CA then public key is agreed upon
    - CA issues ceritificate that includes the enquirers public key
    - encrypting data sent to/by CA with the CA's public/private key
  ####  digital signature 
    - Is used to validate the authenticity of an electronic message 
    - in order to produce a digital signature, a digital certificate is needed

---

# AI (Artificial Intelligence)

###  Purpose and structure of a graph in AI
    - Artificial neural networks can be represented using graphs
    - Graphs provice structures for relationships between nodes
    - AI problems can be definied as finding a path in a graph  
    - Graphs may be analysed by a range of algorithms, i.e. A*, used in machine learning

###  Artificial neural networks
  - ANN are intended to replicate the way human brains work 
  - weights are assigned to each connection between neurons
  - data is input at the input layer and passed into the system 
  - data is analysed at each subsequent layer where the characteristics are extracted and calculuated
  - this is repeated many times to achieve optimimum outputs
  - decisions can be made without explicit programming
  - the deep-learning net will have created complex feature detectors
  - output layer provides the result
   Back propagation of errors - used to adjust the weights of a neural network
###  Deep learning
    - specialised form of machine learning
    - uses many layers to progressively extract higher level features from raw input. 
    - makes good use of unstructured data 
    - outperforms other methods if the data size is large
    - DL systems enable machines to process data in a non-linear fashion
    - is effective at identifying hidden patterns that humans might not be able to see
    - more accurate outcome with higher number of hidden layers
###  Machine learning
  ####  Regression methods
  ####  Supervised Learning 
    - allows data output to be prodcues from previous experience. 
    - known input and output pairs are given, i.e. uses labeled data
    - able to predict future outcomes based on past data
  ####  Unsupervised Learning
    - helps all kinds of unknown patenrs in data to be found 
    - only requires input data to be given, i.e. unlabeled input data
###  Reinforcement learning 
    - enables learning in an interactive environment by trial and error using its own experieces. 
    - desired outcomes are rewarded and undesirable outcomes are punished

---

# Algorithms

###  Conditions for binary search 
    - data needs to be sorted 
###  linear vs binary
    - Linear search O(n) and Binary search O(log2n) / O(Log n)
    - time to search increases linearly in relation to the number of items in the list for a linear search and logarithmically for a Binary search
    - time to search increases less rapidly for a binary search and time to search increases more rapidly for a linear search
### Performance of sorting depends on initial order and number of items

###  What is a graph?
    - data structure used in pathfinding algorithms
    - nodes connected with weighted edges
---

### Recursion

###  recursion
   - a recursive function contains a self-referential call.
   - function calls pushed onto a call stack until base case encountered - winding
   - once basecase encountered, function calls are evaluated - unwinding 
   - trick: for iteration, add another argument to function
---

### Programming Paradigms

###  Low level 
  - Programs using the instruction set of a processor
  -  Addressing-
    -  Immediate
    -  Direct
    -  Indirect
    -  Indexed
###  Imperative
###  OOP
###  Declarative
  -  Facts
  -  Rules



### [TODO] class relation diagrams OOP definitions
### declarative programming
### scheduling diagrams
### recursion diagrams and translations


# pseudocode practice

```pascal
FUNCTION getCustomer(customerID) RETURNS customer
    DECLARE customerRec : customer
    filename = "customerRecords.dat"
    OPENFILE filename FOR RANDOM
    SEEK filename, getRecordLocation(customerID)
    GETRECORD filename, customerRec
    CLOSEFILE filename
    RETURN customerRec
ENDFUNCTION 
```

```pascal
TYPE enum_day = (MONDAY, TUESDAY, WEDNESDAY)
TYPE Ptr = ^INTEGER
DECLARE primes = SET OF INTEGER
TYPE User
    DECLARE ID : STRING 
    DECLARE Age (1, 2, 3) : primes
ENDTYPE

DECLARE Cursor : INTEGER
DECLARE Name : User
DECLARE InputRecord : User
OPENFILE "records.dat" FOR RANDOM
FOR Cursor <- 100 to 1 STEP -1
    SEEK "records.dat", STEP
    GETRECORD "records.dat", User.ID
    SEEK "records.dat", STEP + 1
    PUTRECORD "records.dat", User.ID
NEXT Cursor

SEEK "records.dat", 1
CALL GetInput(BYREF InputRecord)
PUTRECORD "records.dat", InputRecord


CLASS UserClass
    PRIVATE user : User
    PUBLIC PROCEDURE New(ID : STRING, AGE : primes) 
        user.ID <- ID
        user.Age <- AGE
    ENDPROCUECURE
    PUBLIC FUNCTION Getter() RETURNS User
        RETURN user
    ENDFUNCTION
ENDCLASS

DECLARE UserObject : UserClass
UserObject <- NEW UserClass("AE037", 1000)

TYPE species_type = (Cat, Dog, Cow)
CLASS Animal
    PRIVATE species : species_type
    PUBLIC PROCEDURE New(pspecies : species_type)
        species <- pspecies
    ENDPROCEDURE

    PUBLIC FUNCTION GetSpecies() RETURNS species_type
        RETURN species
    ENDPROCEDURE
ENDCLASS

CLASS Dog INHERITS Animal
    PRIVATE Sound : STRING
    PUBLIC PROCEDURE New(pspecies : species_type, psound : STRING)
        SUPER.NEW(pspecies)
        Sound <- psound
    ENDPROCEDURE

    PUBLIC FUNCTION Noise() RETURNS STRING
        RETURN "The Dog Goes " &  & "!"
    ENDFUNCTION
ENDCLASS


CLASS Chiwawa INHERITS Dog
    PUBLIC PROCEDURE New() 
        SUPER.NEW(Dog, "Woof")
    ENDPROCEDURE

    PUBLIC FUNCTION Noise() RETURNS STRING
        RETURN "The Chiwawa Goes " & Sound & "!"
    ENDFUNCTION
ENDCLASS

new_dog = NEW Chiwawa()
OUTPUT new_dog.Noise()

TYPE token = (cat, grep, awk)
TYPE Answer
    DECLARE FullForm : STRING
    DECLARE Description : STRING
ENDTYPE

CLASS HashMap
    PUBLIC name : STRING
    PRIVATE ans : Answer
    PUBLIC PROCEDURE New(name : string)
        name <- name
    ENDPROCEDURE
    FUNCTION find(cursor : token) RETURNS Answer
        OPENFILE filename FOR RANDOM
        SEEK filename, cursor
        GETRECORD filename, ans
        CLOSEFILE filename
        RETURN ans
    ENDPROCEDURE
ENDPROCEDURE

PROCEDURE GracefulExit()
   OUTPUT "Error encountered" 
   EXIT
ENDPROCEDURE

CLASS Program
    PRIVATE prompt : STRING
    PRIVATE answer : Answer
    PRIVATE Map : HashMap
    PUBLIC PROCEDURE New(prompt : STRING, hashmap_name : STRING) 
        prompt <- prompt
        Map <- NEW HashMap(hashmap_name)
    ENDPROCEDURE
    ENDPROCEDURE
    PRIVATE PROCDURE process_answer()
        CASE OF prompt 
            "cat": answer <- Map.find(cat)
            "grep": answer <- Map.find(grep)
            "awk": answer <- Map.find(awk)
            OTHERWISE: CALL GracefulExit()
        ENDCASE
    ENDPROCEDURE 
    PUBLIC PROCEDURE ProvideDescription()
        CALL process_answer()
        OUTPUT Answer.FullForm
        OUTPUT Answer.Description
    ENDPROCEDURE
ENDCLASS

Program <- new Program("cat", "descriptions.dat")
CALL Program.ProvideDescription()
```
![image](https://github.com/user-attachments/assets/33d3983c-2d0a-4f37-b343-e37defc7e550)
