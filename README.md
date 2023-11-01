# avail-fullnodeguide
Step by step describing how to setup full node for avail project.

![image](https://github.com/phalchata/avail-fullnodeguide/assets/33813231/92fd0d77-e8c8-42d6-862e-0655befd5037)

# System Requirements

Minimum
- **2 CPU**
- **4GB RAM**
- **20-40GB DISK**
- **Ubuntu 20.04++**

Recommended
- **4 CPU**
- **8GB RAM**
- **200-300GB DISK**
- **Ubuntu 20.04++**

# Important
You need to be syncronized after setup. Check your validator name on Telemetry and if your name is there then go file the form.

**Form and Details:** **https://x.com/AvailProject/status/1715008696835600451?s=20**

**Telemetry:** **https://telemetry.avail.tools/**


```python
sudo apt update && sudo apt upgrade -y
```

```python
sudo apt install make clang pkg-config libssl-dev build-essential git screen protobuf-compiler -y
```

```python
curl https://sh.rustup.rs -sSf | sh
```

```python
source $HOME/.cargo/env
```

```python
rustup update nightly
```

```python
rustup target add wasm32-unknown-unknown --toolchain nightly
```

```python
git clone https://github.com/availproject/avail.git
```

```python
screen -S avail
```
```python
cd avail
```

```python
cargo build --release -p data-avail
```

```python
mkdir -p output
```

```python
git checkout v1.7.2
```

```python
cargo run --locked --release -- --chain kate -d ./output
```

CTRL-C

```python
sudo touch /etc/systemd/system/availd.service
```

```python
sudo nano /etc/systemd/system/availd.service
```
Write down your validator name in (name "validator-name")

```python
[Unit]
Description=Avail Validator
After=network.target
StartLimitIntervalSec=0
[Service]
User=root
ExecStart= /root/avail/target/release/data-avail --base-path `pwd`/data --chain kate --name "validator-name"
Restart=always
RestartSec=120
[Install]
WantedBy=multi-user.target
```
Exit with CTRL X-Y Enter.

```python
sudo systemctl enable availd.service
```

```python
sudo systemctl start availd.service
```

```python
sudo systemctl status availd.service
```


Exit with CTRL-C. 

```python
journalctl -f -u availd
```

Stopping System

```python
sudo systemctl stop availd.service
```

Sencronized Log

![alt text](https://i.hizliresim.com/n8tva63.png)


