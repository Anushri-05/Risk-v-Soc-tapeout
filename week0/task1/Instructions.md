# 🛠 Week 0 — Task 1: Tool Installation

This task covers the installation of **Yosys**, **Icarus Verilog**, and **GTKWave** on Ubuntu 20.04 inside VirtualBox.

---

## ✅ System Configuration
- Oracle VirtualBox
- Ubuntu 20.04 LTS
- RAM: 6 GB
- HDD: 50 GB
- CPU: 4 vCPUs

---

## 🔹 Install Yosys

Run the following commands:

```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make build-essential clang bison flex \
libreadline-dev gawk tcl-dev libffi-dev git \
graphviz xdot pkg-config python3 libboost-system-dev \
libboost-filesystem-dev zlib1g-dev

git submodule update --init
make config-gcc
make
sudo make install
