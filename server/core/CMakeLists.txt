cmake_minimum_required(VERSION 3.4)
project(core)

set(sources
  include/core/db/sqlite.hpp
  include/core/error.hpp
  include/core/http-body-parser.hpp
  include/core/http-info.hpp
  include/core/http-request-parser.hpp
  include/core/http-server.hpp
  include/core/log.hpp
  include/core/pool.hpp
  include/core/pool-worker.hpp
  include/core/tcp-server.hpp
  include/core/utils.hpp

  src/error.cpp
  src/http-body-parser.cpp
  src/http-info.cpp
  src/http-request-parser.cpp
  src/http-server.cpp
  src/log.cpp
  src/tcp-server.cpp
  src/utils.cpp
  include/core/functor.hpp include/core/ulid.hpp src/ulid.cpp)

add_library(core ${sources})
target_include_directories(core PUBLIC include PRIVATE src)
target_link_libraries(core
  continuable
  llhttp
  sqlite_modern_cpp
  ulid-c
  CONAN_PKG::nlohmann_json
  CONAN_PKG::uvw
  CONAN_PKG::spdlog)
target_compile_definitions(core PUBLIC "$<$<CONFIG:DEBUG>:DEBUG>")
set_target_properties(core PROPERTIES
  CXX_STANDARD 20
  CXX_STANDARD_REQUIRED TRUE
  CXX_EXTENSIONS ON
  LINKER_LANGUAGE CXX)
