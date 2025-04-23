# YT Persistent Queue

## Synopsis

This is a persistent queue implementation based on ordered YT tables.
It allows building near real time data stream pipelines on top of a YT cluster.

## Introduction

Data streams are organized in a way resembling apache kafka's topics:
  - Each data stream is an ordered YT table
  - Each record is a YT table row
  - The library does not impose any limitations on the table format, table schema is provided by the user.

Basic ideas behind this queue implementation:
  - Elements are appended to the table at the bottom
  - Elements are read from the top of the table
  - Each client maintains the offset at which the data is read from the table

Requirements included the following:
  - The library shall have a very simple and concise API
  - The library shall provide both C++ and Python interfaces
  - A command line interface would be a plus


### Guarantees
This implementation provides "at least once" guarantee.


### Storage
XXX TODO Describe trimming here.
XXX TODO Describe (yet unimplemented) TTL here.


## C++ client
The C++ client uses http YT api internally and provies the following methods:
```
    TYTQueue(NYT::IClientPtr client,
             const TString& tablePath,
             const NYT::TNode& schema,
             ui64 rowsTTL=DefaultRowsTTL);

    void Put(const NYT::TNode& row);
    void PutMultiple(NYT::TNode::TListType rows);
    NYT::TNode::TListType GetMultiple(size_t limit);
    NYT::TNode Get();
    void Seek(i64 offset);
    void Trim(i64 count);
```
XXX TODO: describe methods


## Python interface
Python wrapper is implemented in cython.
The only major difference in the python interface is that the YTQueue class constructor takes a proxy and a token as arguments instead of a client object.

```
class YTQueue(object):
    def __init__(self, proxy, tablePath, schema, token=None)
    def put(self, node)
    def get(self)
    def put_multiple(self, rows)
    def get_multiple(self, limit)
    def seek(self, offset)
    def trim(self, count)
``` 

## Command line interface
The ytq command line tool exposes the libary interface as a set of three commands: put, get and trim.
Input data is read from stdin, output is written to stdout.
Error messages are dumped to stderr.

```
Usage: ./ytq [OPTIONS]

Required parameters:
  {-p|--proxy} VAL     YT proxy
  {-t|--table} VAL     Queue YT table path

Optional parameters:
  --svnrevision        print svn version
  {-?|--help}          print usage
  {-T|--token} FILE    path to YT token file
  --put                put items in the queue (default: 0)
  --get N              get N items from the queue
  --trim N             trim N records from the top the table
  --offset N           get offset (default: 0)
  {-d|--delimiter} VAL items delimiter character, backslash escape sequence are supported, i.e. \n, \t, \0...)
```
