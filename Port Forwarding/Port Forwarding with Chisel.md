### Chisel: Fast TCP/UDP Tunnel Over HTTP

Chisel is a fast TCP/UDP tunnel over HTTP. It can be used for port forwarding.

#### Transfer Chisel Binary to Remote Machine

If the remote machine does not have the Chisel binary, transfer it from the local machine (if the local machine has the binary).

_On the local machine:_

```bash
python3 -m http.server --directory /path/to/chisel/directory
```

_On the remote machine:_

```bash
wget http://<local-ip>:8000/chisel
chmod +x chisel
./chisel -h
```

#### Port Forwarding

_On the remote machine:_

```bash
chisel server -p <listen-port>
```

_On the local machine:_

```bash
chisel client <listen-ip>:<listen-port> <local-port>:<target-ip>:<target-port>
```

#### Reverse Port Forwarding

It is useful when we want to access a host and port that cannot be directly accessible from the local machine.

_On the local machine:_

```bash
chisel server -p 9999 --reverse
```

_On the remote machine:_

Replace `10.0.0.1` with your local IP:

```bash
chisel client 10.0.0.1:9999 R:8090:172.16.22.2:8000
```

After that, we can access `http://localhost:8090/` on the local machine. In short, we can access `http://172.16.22.2:8000/` via `localhost:8090`. Try using `curl` to confirm:

```bash
curl http://localhost:8090
```

_The result is the content of `http://172.16.22.2:8000/`._

#### Example (SSH)

Assume we want to connect to an SSH server (`ssh://172.17.0.1:22`) that cannot be directly accessed from the local machine.

_On the local machine:_

```bash
chisel server -p 9999 --reverse
```

_On the remote machine (assuming we want to connect to `ssh://172.17.0.1:22`):_

```bash
chisel client <local-ip>:9999 R:2222:172.17.0.1:22
```

After that, we can connect to the SSH server from the local machine. Run the following command on the local machine:

```bash
ssh user@localhost -p 2222
```

#### Forward Multiple Ports

_On the local machine:_

```bash
chisel server -p 9999 --reverse
```

_On the remote machine:_

```bash
chisel client 10.0.0.1:9999 R:3000:127.0.0.1:3000 R:8000:127.0.0.1:8000
```

After that, we can access `http://localhost:3000` and `http://localhost:8000` on the local machine.

#### Forward Dynamic SOCKS Proxy

_On the remote machine:_

```bash
chisel server -p 9999 --socks5
```

_On the local machine:_

```bash
chisel client 10.0.0.1:9999 8000:socks
```

Then, modify `/etc/proxychains.conf` on the local machine. Comment out the line of `socks4` and add `socks5 127.0.0.1 8000`:

```bash
# /etc/proxychains.conf
...
socks5 127.0.0.1 8000
```

#### Reverse Dynamic SOCKS Proxy

It is useful when we want to access a host and multiple ports that cannot be directly accessible from the local machine.

_On the local machine:_

```bash
chisel server -p 9999 --reverse --socks5
```

_On the remote machine:_

```bash
chisel client 10.0.0.1:9999 R:socks
```

After connecting, see the Chisel server log:

```
2024/09/01 00:00:00 server: session#3: tun: proxy#R:127.0.0.1:1080=>socks: Listening
```

Note the `127.0.0.1:1080` and paste it for SOCKS proxy settings such as Proxychains and Burp.

Modify `/etc/proxychains.conf` on the local machine. Comment out the line of `socks4`:

```bash
# /etc/proxychains.conf
...
socks5 127.0.0.1 1080
```

To confirm if we can reach the desired host and port, run `nmap` with Proxychains:

```bash
proxychains nmap localhost
```

#### Enable Proxychains Bash

It allows us to execute programs without adding the `proxychains` command before the main command.

```bash
proxychains bash

# Run some command without "proxychains" command.
nmap localhost
```

#### Burp Suite Settings for Proxy

If we want to use Burp Suite with Proxychains, we can add the SOCKS proxy in the Proxy settings. For details, please see the SOCKS Proxy in Burp Suite.

#### References

- [Chisel GitHub Repository](https://github.com/jpillora/chisel)

---

Hope this helps! If you need further assistance, feel free to ask. 🚀
