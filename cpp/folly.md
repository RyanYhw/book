# FOLLY

[folly](https://github.com/facebook/folly)

## compile

```
gcc 4.9+
cmake_minimum_required(VERSION 3.0.2 FATAL_ERROR)

sudo apt-get install \
    g++ \
    cmake \
    libboost-all-dev \
    libevent-dev \
    libdouble-conversion-dev \
    libgoogle-glog-dev \
    libgflags-dev \
    libiberty-dev \
    liblz4-dev \
    liblzma-dev \
    libsnappy-dev \
    make \
    zlib1g-dev \
    binutils-dev \
    libjemalloc-dev \
    libssl-dev \
    pkg-config

sudo apt-get install \
    libunwind8-dev \
    libelf-dev \
    libdwarf-dev

mkdir _build && cd _build
  cmake ..
  make -j $(nproc)
  make install

```

## USE

### LINK

```
-std=c++14  -lfolly -pthread -lglog -lunwind   -levent -ldouble-conversion -lboost_context   -ldl  -liberty
```