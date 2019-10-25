# Chapter11 与系统打交道

## Tip81 列出目录中的文件

```c++
#include <boost\filesystem\operations.hpp>
#include <iostream>
//it may link against boost_system and boost_filesystem

int main()
{
    boost::filesystem::directory_iterator begin("./");
    boost::filesystem::directory_iterator end;
    for( it = begin; it != end; ++it)
    {
        boost::filesystem::file_status fs = it->status();
        switch( fs.type() )
        {
            case boost::filesystem：：regular_file: break;
            case boost::filesystem::symlink_file: break;
            case boost::filesystem::directory_file: break
            default: break;
        }
        //output the file name:
        std::cout<< it->path() << std::endl;
    }
}
```

**Notes:**
- POSIX系统使用斜杠( / )指定路径， Windows默认通过反斜杠( \ ), 但是Windows也能理解斜杠。
- filesystem 已被加入到[C++17 标准库](https://en.cppreference.com/w/cpp/filesystem)中

---

## Tip82  创建及删除文件和目录

```c++
//create directroy and sub directoy
boost::filesystem::error_code error;
boost::filesystem::create_drecctories( "dir/subdir", error);
assert(!error);

std::ofstream ofs("dir/subdir/file.txt");
ofs<< " some text" << std::endl;
ofs.close();

//create symlink
boost::fielsystem::create_directory_symlink("dir/subdir", "symlink_dir", error);

//check if a file exists
if( !error )  
{
    assert( boost::filesystem::exists("symblink/file.text");
}

//delete files
boost::filesystem::remove( "dir/subdir/file.text", error);
```

**Notes:**
- create_directory 不能创建子目录，但是create_directories可以
- 如果不对Boost.FileSystem提供 boost::system_error::error_code的实例，代码可以编译，但运行时如果发送错误会抛出一个异常

---

## Tip83 将数据从一个进程快速传递到另一个进程

不同的计算机之间最常见的是使用Soeket， 同一台计算机的多个进程可用使用Boost.Interproess.
Boost.Interprocess可以使单个内存片段从不同的进程访问。

```c++
#include < boost/interprocess/mamanged_shared_memory.hpp>

//创建/获取一个段
boost::interprocess::mamanged_shared_memory  segment {
boost::interprocess::open_or_create, 
"shm-cache",          //name
1024                       //size
};

//创建/获取一个变量
atomic_t& value = *segment.find_or_construt<atomic_t>("shem-conter") (0);          //type/name/intial value

//销毁变量
segment.destory<atomic_t>("shm-counter");

//销毁段
boost.interprocess.shared_memory_object::remove("shm-cache")
```

** Notes:**  
- 共享内存中需要使用原子变量
- boost::interprocess 还提供以下内容:
-- Shared memory.
-- Memory-mapped files.
-- Semaphores, mutexes, condition variables and upgradable mutex types to place them in shared memory and memory mapped files.
-- Named versions of those synchronization objects, similar to UNIX/Windows sem_open/CreateSemaphore API.
-- File locking.
-- Relative pointers.
-- Message queues.

---

## Tip86 读取文件的最快方式

使用内存映射，是读取文件的最快方式。

- 将文件映射到进程的地址空间，之后进程可以像使用正常内存一样使用这些地址。
- 操作系统处理所有的文件操作，如缓存和预读。
- 建立内存映射时，系统不会立刻从磁盘读取数据，只有映射区域的一部分被请求后，才会从磁盘加载那一部分（不是加载全部部分，所以映射大小不会影响性能）。
- 写入内存映射的区域，操作系统会对写入进行缓存，与ofstream的数据缓存不同，应用程序crash不会导致数据丢失。
- 如果多个进程映射单个文件，且其中一个进程修改了映射区域，其变化对其他进程立即可见。

---

## Tip87 Coroutines

Coroutine, 即允许多个入口点的子程序， 多个入口点使我们能够在 某些地方暂停和恢复程序的执行，以及切换到其他子程序。

```c++

#include <boost\coroutine2\coroutine.hpp>
//need to link libboost_context-vc140-mt-gd-1_63.lib

#include <boost\coroutine2\coroutine.hpp>
//need to link libboost_context-vc140-mt-gd-1_63.lib

#include <iostream>
#include <list>

using COROUT_TYPE = boost::coroutines2::coroutine<int>;

void task1(COROUT_TYPE::push_type& system)
{
    int i = 0;

    system(i);
    while ( i++ < 40 )
    {
        std::cout << "task1  time slice "<< i << std::endl;
        system(i);
    }

}

void task2(COROUT_TYPE::push_type& system)
{
    int i = 0;

    system(i);
    while (i++ < 20)
    {
        std::cout << "task2 time slice " << i << std::endl;
        system(i);
    }
}

int main()
{
    COROUT_TYPE::pull_type t1(task1);
    COROUT_TYPE::pull_type t2(task2);
    std::list<COROUT_TYPE::pull_type> task_list;
    task_list.push_back( std::move(t1));
    task_list.push_back( std::move(t2));

    while (!task_list.empty())
    {
        bool notask = true;
        for (auto it = task_list.begin(); it != task_list.end(); ++it)
        {
            if (*it)
            {
                (*it)().get();

                if (notask)
                    notask = false;
            }
        }

        if (notask)
            break;
    }

    getchar();
    return 0;
}
```