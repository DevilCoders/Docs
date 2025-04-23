# Extensible YT operations

Build extensible YT operations using composition. 

Authors: stys@, osado@, mihajlova@

## Motivation

The goal of this library is to achieve modularity and extensibility in YT operations. We would like to build complex
operations by combining smaller injectable components. By the basic principle of dependency injection [1] we want to declare 
dependencies as abstract interfaces and provide a constructor for injecting implementations. Derived applications 
provide entry points where components are explicitly assembled via constructors.

To be able to apply this pattern for YT operations we need to support serialization and deserialization of injected
components. This library provides a poor man's reflection for compatibility with `Y_SAVELOAD_JOB` macro.

## Usage

Create an interface for a component with serialization methods `Save` and `Load` for compatibility with `Y_SAVELOAD_JOB` macro:
```
class IFoo : public TThrRefBase {
public:
    IFoo() = default;
    virtual TNode Foo(const TNode& node) const = 0;
    virtual void Save(IOutputStream& stream) const { Y_UNUSED(stream); };
    virtual void Load(IInputStream& stream) { Y_UNUSED(stream); };
};
```

Declare corresponding pointer type
```
using IFooPtr = TIntrusivePtr<IFoo>;
```

Declare template specialization (must be placed in global scope) for pointer serializer
```
template<>
class TSerializer<IFooPtr> : public TPtrSerializer<IFoo, IFooPtr> {};
```

Create a specific implementation. It must provide a default constructor and implement serialization methods. The `Y_SAVELOAD_JOB` macro
may be used to easily provide implementations for inner components which are already supported by this macro, such as 
basic types and other components comforming to this pattern. 
```
public MyFoo : public IFoo {
private:
    int Param;
public:
    MyFoo(): { Param = 0; };
    MyFoo(int param): Param(param) {};   
    
    Y_SAVELOAD_JOB(Param);  // provides 
}
```

Register implementation using special macro provided by the library
```
REGISTER_SUBCLASS(IFoo, MyFoo);
```

Now we can build an YT operation using our component
```
public MyMapper: public IMapper<TTableReader<TNode>, TTableWriter<TNode>> {
private:
    IFooPtr Foo;
    
public:
    MyMapper() = default;
    MyMapper(const IFooPtr& foo): Foo(foo) {};
    
    Y_SAVELOAD_JOB(Foo);
    
    void Do(TTableReader<TNode>* input, TTableWriter<TNode>* output) override {
        TNode inputRow = input->GetRow();
        TNode outputRow = Foo.Foo(node);
        output->AddRow(outputRow);
    }    
}

```
