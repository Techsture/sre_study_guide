# SSH Connection Setup and Data Transfer
## Connection Setup
- Client opens a TCP connection ( 3-way handshake is done : SYN->SYN+ACK->ACK )
- Server sends its OpenSSH version and public key
- Client checks its supproted sshd version and confirms the public key:
 - User might get prompt to accept key if its not present in known_hosts ( yes/no )
 - Continue if the protcol matches and client accepts the key
- SSH2_MSG_KEXINIT message is sent/receive ( KEX algorithms negotiation )
 - Client sends its KEX algorithms, host key algorithms, ciphers
 - First match of algorithms on clients side is selected for the session
 - KEX Algorithm: Varient of deffie hellman algorithms
 - Host key Algorithm: Public key crypto algorithm 
 - Cipher: cacha-poly1305 > aes256-gcm > aes128-gcm etc   
