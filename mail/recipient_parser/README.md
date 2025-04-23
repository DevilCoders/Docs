RFC 5322 recipient parser
=========================

Concepts
--------
* This is header-only **C++11** library based on **Boost.Spirit**.
* Only dependencies are STL and Boost.Spirit, plus couple of utility classes from Boost (optional, variant).
* Build system is **CMake**.
* All business logic is implemented as nonterminal Spirit rules.
* Each nontrivial rule is covered with *unit tests* via **googletest**.

How to build
------------
    $ cmake .      # Configure
    $ make check   # Download googletest and build unit tests
    $ make install # Install headers in ${CMAKE_INSTALL_DIR}

`make install` will also install `FindRECIPIENT_PARSER.cmake` file in `${CMAKE_INSTALL_SHAREDIR}/cmake_helpers` directory.
This makes it compliant with bench-based build.

How to use
----------
In CMake:

    find_package(RECIPIENT_PARSER)
    include_directories(${RECIPIENT_PARSER_INCLUDE_DIR})
or, for custom build:

    find_path(RECIPIENT_PARSER_INCLUDE_DIR
        NAMES recipient_parser/addr_spec.hpp 
        HINTS ...) # Your hints here
    include_directories(${RECIPIENT_PARSER_INCLUDE_DIR})


In C++:

    #include <recipient_parser/parse.hpp>
    
    std::string raw_data;         // Can be any symbol range
        
    auto result = rcpt_parser::parse_address(raw_data);
    if( !result ) {
        abort();                  // Parse failed
    } else {
        do_smth( *result );       // *result is variant<Mailbox, MailboxGroup>.
    }

`parse_mailbox()` function is supplied for group-unawared recipient parsing.

If you provide pair of iterators, first iterator will be taken by non-const lvalue reference and will be advanced to the point where parsing stops (just like in Spirit). You can use it for logging fail entries, for instance:

    //...
    std::string raw;
    auto iter = begin(raw);
    
    auto result = parse_address(iter, end(raw));
    if( !result ) {
        log_error(
            "Invalid address: %s, parse stopped here: %s",
            raw,
            std::string(iter, end(raw))
        );
    }
    
Implementation details
----------------------
###Useful links
For parser engine implementation details, visit [Boost.Spirit v2 documentation](http://www.boost.org/doc/libs/1_61_0/libs/spirit/doc/html/index.html) website.

For according RFC 5322 sections, start from [here](https://tools.ietf.org/html/rfc5322#section-3.4).

###Project structure
Project repository consists of folders:
####[include/recipient_parser/](include/recipient_parser)
Contains single header named `parse.hpp`. Interface functions are defined there.
#####[include/recipient_parser/rules](include/recipient_parser/rules)
Collection of parse rules. Parse rules are one-to-one mapped to RFC 5322 entities. and are named after them. One can use any of them to parse some part of recipient.
#####[include/recipient_parser/types](include/recipient_parser/types)
Data structures that are used as output of parse functions. Also named after RFC 5322 entities they represent.

####[share/](share)
Contains `FindRECIPIENT_PARSER.cmake` which allows `find_package(RECIPIENT_PARSER)` for library clients, and `find_recipient_parser_dependencies.cmake` to find library dependencies (currently, only Spirit).

####[tests/](tests)
Unit tests via googletest.