### wykobi的使用

wykobi是一个模板库

- 函数模板的定义放到头文件

  原始的wykobi代码使用将**函数模板的定义放到头文件**的方法进行模板组织不适合做lib，需要把所有源文件单独放在 /usr/local/include/wykobi下面，然后通过`include "wykobi/*.hpp"`进行库的调用，这样一旦调用它的代码修改，编译会比较耗时，应该是要把整个wykobi的源文件重新编译；

  好处是不会出现inline的warning

- 显式实例化模板

  参考资料：[函数模板、类模板生成静态库](https://blog.csdn.net/abcdefg0h/article/details/78180765)

  我现使用显示实例化模板组织，在调用库的项目的makefile中加入wykobi，同样通过`include "wykobi/*.hpp"`进行库的调用，但由于函数为lnline，编译时会发出warning: 

  ```sh
  warning: inline function ‘...’ used but never defined
  ```

  看不到inline的定义，会warning，但程序运行没问题

### 模板如何分离编译？

显示实例化或export关键字（基本所有的编译器都不支持）

当做成模板库的时候，如果库中有inline函数并被外部调用就会造成warning，使用编译选项`-fno-inline`也没有用；没有inline的时候不会warning