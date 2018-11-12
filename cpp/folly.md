# FOLLY

[folly](https://github.com/facebook/folly)

## 编译

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

boost 最好是通过libboost-all-dev安装, 如果是自己编译的, cmake可能会对高版本的boost报错

mkdir _build && cd _build
  cmake ..
  make -j $(nproc)
  make install

默认生成为静态库
```

## 使用

### 链接

以下是必备的

```
-std=c++14  -lfolly -pthread -lglog -lunwind   -levent -ldouble-conversion -lboost_context   -ldl  -liberty
```