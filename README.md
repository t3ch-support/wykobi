

## wykobi的使用

### 模板

wykobi是一个模板库，所以其编译要考虑模板的编译模型，参考cpp_study.md

- 包含编译模型

  原始的wykobi代码使用将**函数模板的定义放到头文件**的方法进行模板组织不适合做lib，因为需要把所有源文件单独放在 /usr/local/include/wykobi下面，然后通过`include "wykobi/*.hpp"`进行库的调用，这样一旦调用它的代码修改，编译会比较耗时，应该是要把整个wykobi的源文件重新编译；

  好处是不会出现inline的warning

- 显式实例化分离编译模型

  我现使用显示实例化模板组织，在调用库的项目的makefile中加入wykobi，同样通过`include "wykobi/*.hpp"`进行库的调用，但由于函数为lnline，编译时会发出warning: 

  ```sh
  warning: inline function ‘...’ used but never defined
  ```

  看不到inline的定义，会warning，但程序运行没问题

### inline

发现在大多hpp和inl中，函数都加了inline，而wykobi_instantiate.cpp中的显示实例化中却，没有，尝试添加，编译报错：

`error: explicit instantiation shall not use ‘inline’ specifier [-fpermissive]`

采用显式实例化分离编译模型，其它项目使用libwykobi时，会warning，所以实际应该是把它们当做普通函数处理了，没有inline，所以干脆把hpp中的inline去掉，那样外部项目使用时就不会warning.

## Installation

### seperate complication

```sh
mkdir build && cd build
cmake ..
make -j8
# install
sudo make install
sudo ldconfig
```



