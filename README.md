# MobaXterm
**how you fixed the "cannot connect to X server" error with GaussView over SSH using MobaXterm**:

---

### ✅ **Fixing X11 Forwarding for GaussView in MobaXterm**

---

### 🧩 **Problem:**

You were seeing these errors:

```
MoTTY X11 proxy: Unsupported authorisation protocol
gview.exe: cannot connect to X server localhost:10.0
```

This meant **X11 forwarding was enabled**, but **authentication was failing** due to missing or misconfigured `xauth`, and conflicting manual settings.

---

### 🛠 **Steps to Fix It:**

#### ✅ **1. Installed `xauth` on the remote server**

On the Linux machine (via SSH):

```bash
which xauth
```

If it wasn’t found, you installed it:

* On Ubuntu/Debian:

  ```bash
  sudo apt install xauth
  ```

* On CentOS/RHEL:

  ```bash
  sudo yum install xauth
  ```

---

#### ✅ **2. Removed conflicting manual `DISPLAY` and `XAUTHORITY` exports**

You edited your `.bashrc`:

```bash
nano ~/.bashrc
```

You **commented out** lines like:

```bash
# export DISPLAY=localhost:0.0
# export XAUTHORITY=$HOME/.Xauthority
```

Then reloaded the file:

```bash
source ~/.bashrc
```

> ✅ MobaXterm **automatically sets** the correct `DISPLAY` and `XAUTHORITY` variables when X11 forwarding is enabled.

---

#### ✅ **3. Reconnected via MobaXterm with X11 forwarding**

* Closed all existing SSH sessions
* Restarted MobaXterm
* Reconnected to the remote machine using **MobaXterm’s built-in SSH client**
* Verified that `DISPLAY` was automatically set:

  ```bash
  echo $DISPLAY
  ```

  Output should be something like:

  ```
  localhost:10.0
  ```

---

#### ✅ **4. Verified X11 forwarding with a simple app**

Before launching GaussView, you ran:

```bash
xclock
```

🕒 A clock window appeared on your Windows machine — confirming X11 forwarding worked.

---

#### ✅ **5. Launched GaussView successfully**

Finally:

```bash
gview
```

And GaussView opened — mission accomplished! 🎉

---

Let me know if you'd like this turned into a PDF or printable cheat sheet for future reference!
