cmake_minimum_required(VERSION 3.13)

project("main")

SET(NOT_CACHE "some not cache value")
get_property(testIsNotCache CACHE NOT_CACHE PROPERTY TYPE)
message("testIsNotCache: " ${testIsNotCache})

if(testIsNotCache)
    message("NOT_CACHE is cache")
else()
    message("NOT_CACHE is not cache")
endif()

SET(DEFINITELY_CACHE "dummy value" CACHE STRING "This variable is definitely cache")
get_property(testIsCache CACHE DEFINITELY_CACHE PROPERTY TYPE)
message("testIsCache: " ${testIsCache})

if(testIsCache)
    message("DEFINITELY_CACHE is cache")
else()
    message("DEFINITELY_CACHE is not cache")
endif()

# If you use ${} on the variable it will be considered "never cache"
get_property(wrongSyntaxA CACHE ${DEFINITELY_CACHE} PROPERTY TYPE)
message("wrongSyntaxA: " ${wrongSyntaxA})

get_property(wrongSyntaxB CACHE ${NOT_CACHE} PROPERTY TYPE)
message("wrongSyntaxB: " ${wrongSyntaxA})
