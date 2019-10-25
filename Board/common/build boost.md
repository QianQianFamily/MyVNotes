# Build Boost

boost的build分为两部：
- 1. Build the Bjam
- 2. Build the boost Libraries

## Building the Bjam
以Windows为例， 运行 <boost_root>/bootstrap.bat即可。

## Building the libraries
这里也分两步， 一个是stage，一个是install：
- stage是build 需要build的library
- install 是将头文件和库文件放到指定目录


[Reference](https://www.codeproject.com/articles/11597/building-boost-libraries-for-visual-studio/)
