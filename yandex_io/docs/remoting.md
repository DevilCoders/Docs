# Glossary 

**Object** - component that implements some functionality, usually represented by C++ class.

**Host** - unique master replica of `Object`'s state. The only way to execute some method on `Object` is to execute it on `Host`.

**Proxy** - slave replica of `Object`'s state. All method calls are routed to `Host`. There are any number of `Proxy` in the system.

**Channel** - any transport channel connecting `Host` and `Proxy` instances.



# Rules

1. Both `Host` and `Proxy` can listen for child objects of `Object` and proxy them.
2. Replica updates for such proxies must be received only from that `Channel`, from which this child object was received.
3. Method calls for such proxies must be routed through that `Channel`, from which this child object was received.

