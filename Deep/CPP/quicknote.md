# quicknote

## 清空 stringstream
```c++

#include <sstream>

std::stringstream ss;
ss  << "hello sun" ；

ss.clear();  //it doesn't work, it only clear the error flag

ss.str(""); //works

```

[Ref](https://stackoverflow.com/questions/20731/how-do-you-clear-a-stringstream-variable)




