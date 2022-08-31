# CMake < 3.19 JSON parse

CMake 3.19 added [string(JSON)](https://cmake.org/cmake/help/latest/command/string.html#json).
This [JsonParse.cmake](./JsonParse.cmake) greedily parses the JSON string input and uses `macro()` to populate a variable structure.
Instead of upgrading this code to be non-greedy, it's better to use CMake > 3.19. For the meantime, this code makes a workaround for older CMake < 3.19.
