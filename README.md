## dependency

### apt
```bash
apt-get update
apt -y install build-essential bison libtool cmake vim gcc g++ libc6-dev autoconf automake curl wget git make unzip openssh-server gdb
apt -y install pkgconf zlib1g zlib1g-dev libzstd1 meson ninja-build doxygen bzip2 flex
apt -y install graphviz libbz2-dev libssl-dev libncurses5-dev libsqlite3-dev libreadline-dev libtk8.6 libgdm-dev libdb4o-cil-dev libpcap-dev 
```

### build python

```bash
wget https://github.com/python/cpython/archive/refs/tags/v3.11.1.zip
unzip v3.11.1.zip && cd cpython-3.11.1/ && ./configure --enable-optimizations
make -j 32 && make install
```

### build pip

```bash
pip3 install --upgrade pip
pip3 install bz2file pydot graphviz angr iced_x86 pyelftools pyinstrument
```


### libdwarf
need install `libdwarf`, can download from https://github.com/davea42/libdwarf-code/releases
```bash
mkdir /tmp/build && cd /tmp && wget  https://github.com/davea42/libdwarf-code/releases/download/v0.5.0/libdwarf-0.5.0.tar.xz && tar xf libdwarf-0.5.0.tar.xz && rm libdwarf-0.5.0.tar.xz && cd  /tmp/build && meson /tmp/libdwarf-0.5.0  &&ninja && ninja install && ninja test
```
### angr
`pip install angr, z3-solver`

## usage

### extract debug info

1. go into extracter/ and `make extracter`
2. execute `./extracter <binary-to-extract> -o <json-file>`, there are also some debug option(s)
   1. `-r` for print raw dwarf expression, `-nc` for only print complex expressions, `-fde` for print CFA info, and `--no-traverse` for avoidance of fully traversing, and quickly print other info

### analysis

1. `rewrite.py` rewrite a piece from large binary into a seperate binary file. `./rewrite.py <large-binary> <startpc> <endpc>`
2. `variable.py` deal with debuginfo from json 
3. `dwarf_iced_map.py`, `dwarf_vex_map.py` mapping between different framework
