```
$ cat query.yql | ./example             
Declares: 

Name: $x9:
Type: 
  KIND_PRIMITIVE[Utf8]

Name: $x22:
Type: 
  KIND_VOID

Name: $x30:
Type: 
  KIND_VARIANT
    KIND_STRUCT
      KIND_KEY_VALUE[a]
        KIND_PRIMITIVE[String]
      KIND_KEY_VALUE[b]
        KIND_PRIMITIVE[Int64]

Name: $x29:
Type: 
  KIND_VARIANT
    KIND_STRUCT
      KIND_KEY_VALUE[a]
        KIND_PRIMITIVE[String]
      KIND_KEY_VALUE[b]
        KIND_PRIMITIVE[Int64]

Name: $x15:
Type: 
  KIND_PRIMITIVE[Datetime]

Name: $x2:
Type: 
  KIND_PRIMITIVE[Double]

Name: $x23:
Type: 
  KIND_PRIMITIVE[Decimal]
    KIND_ID[30]
    KIND_ID[7]

Name: $x6:
Type: 
  KIND_PRIMITIVE[Int64]

Name: $x7:
Type: 
  KIND_PRIMITIVE[Uint64]

Name: $x16:
Type: 
  KIND_PRIMITIVE[Date]

Name: $x1:
Type: 
  KIND_PRIMITIVE[Int32]

Name: $x14:
Type: 
  KIND_PRIMITIVE[Json]

Name: $x21:
Type: 
  KIND_PRIMITIVE[TzDate]

Name: $x11:
Type: 
  KIND_OPTIONAL
    KIND_PRIMITIVE[String]

Name: $x33:
Type: 
  KIND_EMPTY_LIST

Name: $x34:
Type: 
  KIND_EMPTY_DICT

Name: $x25:
Type: 
  KIND_LIST
    KIND_OPTIONAL
      KIND_PRIMITIVE[String]

Name: $x5:
Type: 
  KIND_PRIMITIVE[String]

Name: $x10:
Type: 
  KIND_PRIMITIVE[Uuid]

Name: $crls:
Type: 
  KIND_LIST
    KIND_STRUCT
      KIND_KEY_VALUE[serial]
        KIND_PRIMITIVE[String]
      KIND_KEY_VALUE[ca]
        KIND_PRIMITIVE[String]
      KIND_KEY_VALUE[updated_at]
        KIND_OPTIONAL
          KIND_PRIMITIVE[Uint64]

Name: $x28:
Type: 
  KIND_VARIANT
    KIND_TUPLE
      KIND_PRIMITIVE[String]
      KIND_PRIMITIVE[Int64]

Name: $x4:
Type: 
  KIND_PRIMITIVE[Float]

Name: $x8:
Type: 
  KIND_PRIMITIVE[String]

Name: $x24:
Type: 
  KIND_STRUCT
    KIND_KEY_VALUE[a]
      KIND_PRIMITIVE[Int64]
    KIND_KEY_VALUE[b]
      KIND_PRIMITIVE[String]

Name: $x27:
Type: 
  KIND_VARIANT
    KIND_TUPLE
      KIND_PRIMITIVE[String]
      KIND_PRIMITIVE[Int64]

Name: $x13:
Type: 
  KIND_PRIMITIVE[Yson]

Name: $x32:
Type: 
  KIND_TUPLE
    KIND_PRIMITIVE[String]
    KIND_OPTIONAL
      KIND_PRIMITIVE[Int64]

Name: $x17:
Type: 
  KIND_PRIMITIVE[Timestamp]

Name: $x20:
Type: 
  KIND_PRIMITIVE[TzTimestamp]

Name: $x19:
Type: 
  KIND_PRIMITIVE[TzDatetime]

Name: $x31:
Type: 
  KIND_TUPLE
    KIND_PRIMITIVE[String]
    KIND_OPTIONAL
      KIND_PRIMITIVE[Int64]

Name: $x3:
Type: 
  KIND_PRIMITIVE[Bool]

Name: $x26:
Type: 
  KIND_DICT
    KIND_PRIMITIVE[String]
    KIND_OPTIONAL
      KIND_PRIMITIVE[Int64]

Name: $x12:
Type: 
  KIND_OPTIONAL
    KIND_PRIMITIVE[String]
```