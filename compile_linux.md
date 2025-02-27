根据项目文档，在 Linux 上编译 Akira-obfuscator 的步骤如下：

1. 首先安装必要的依赖：
```bash
apt-get update
apt-get install -y cmake ninja-build build-essential git
```

2. 克隆项目：
```bash
git clone https://github.com/thomasxm/Akira-obfuscator.git
cd Akira-obfuscator
```

3. 创建并进入构建目录：
```bash
mkdir build_ninja
cd build_ninja
```

4. 运行 cmake 配置：
```bash
cmake -DCMAKE_BUILD_TYPE=Release \
      -DLLVM_ENABLE_ASSERTIONS=ON \
      -DLLVM_ENABLE_PROJECTS="clang;clang-tools-extra;lld;lldb" \
      -G "Ninja" ../llvm
```

5. 编译：
```bash
ninja
```

注意事项：
1. 如果遇到 CryptoUtils.cpp 相关错误：
```cpp
/home/kali/akira/llvm/lib/Transforms/Obfuscation/CryptoUtils.cpp:679:26: error: variable 'std::ifstream devrandom' has initializer but incomplete type
```
需要在 `/akira/llvm/lib/Transforms/Obfuscation/CryptoUtils.cpp` 文件开头添加：
```cpp
#include <fstream>
```

2. 编译过程可能需要较长时间，建议确保系统有足够的内存和磁盘空间。

3. 编译完成后，编译产物会在 `build_ninja/bin` 目录下。
