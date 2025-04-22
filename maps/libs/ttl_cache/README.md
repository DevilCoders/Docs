Cache with a limited storage duration
===

`TTLCache` implements a key-value dictionary with a limited storage duration using explicitly set Clock.
`Clock` is either a function or a type with defined `operator()()`.
Keep in mind that cache uses a copy of what you pass, so share your state in case of non-temporary object.
You can pass `SharedClock` that is already implemented for you.
It allows you to set current time via its methods.
Or just use a standart time function `StdClock` to use system clock.

Public interface
====
**Types:**
* `Key` – dictionary key type
* `Value` – dictionary value type
* `Clock` – clock implementation (see above), `std::function<time_t()>` by default

**Constructors:**
* `TTLCache(time_t ttl, Clock clock = StdClock)` – initializes empty cache with a given time-to-live param value (in seconds) and a clock object

**Methods:**
* `Value* get(const Key& key)` – get value by key to update it, promotes element; returns `nullptr` if no such key
* `Value& getOrCreate(const Key& key, auto&& create)` – get element or create it with a given functor
* `template<typename... Args> Value& getOrEmplace(const Key& key, Args&&... args)` – get element or construct it with given args
* `const Value* peek(const Key& key) const` – peek value, doesn't promote element; returns `nullptr` if no such key
