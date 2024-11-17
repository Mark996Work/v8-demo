cmake_minimum_required(VERSION 3.28)
project(v8_demo)

# 项目名称和版本号
project(v8_demo VERSION 1.0)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_OSX_ARCHITECTURES "x86_64")

# 包含头文件目录
include_directories(xxx/v8/v8/include)
include_directories(xxx/v8/v8)

# 链接库目录
link_directories(xxx/v8/v8/out.gn/x64.release.sample/obj)

# 查找源文件
set(SOURCES ./hello-world.cc)
set(CALC_SOURCE
        ./shell/shell.cpp
        ./shell/interceptor.cpp
        ./shell/exposeToJsFuncs.cpp
        ./shell/exposeToJsVar.cpp
        ./shell/shell_util.cpp
)


# 添加可执行文件
add_executable(hello_world ${SOURCES})
add_executable(shell ${CALC_SOURCE})

# 为目标添加编译选项
target_compile_options(hello_world PRIVATE -pthread -DV8_COMPRESS_POINTERS -DV8_ENABLE_SANDBOX)
target_compile_options(shell PRIVATE -pthread -DV8_COMPRESS_POINTERS -DV8_ENABLE_SANDBOX)

# 链接库
target_link_libraries(hello_world PRIVATE v8_monolith dl pthread)
target_link_libraries(shell PRIVATE v8_monolith dl pthread)

