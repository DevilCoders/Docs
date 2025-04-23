# Конечный автомат статусов для Order

```
digraph A {

    draft -> ready [label="Customer"]
    ready -> accepted [label="Supplier"]
    ready  -> rejected [label="Supplier"]
    rejected -> draft [label="Customer"]

}
```

# Конечный автомат статусов для MosaicSource

```
digraph A {
    broken -> fixed [label="supplier"]
    parsed -> new [label="auto"]
    parsed -> processing_failed [label="auto"]
    processing_failed -> parsed [label="developer"]
    new -> accepted [label="customer"]
    new -> rejected [label="customer"]
    rejected -> rejected_approved [label="supplier"]
    rejected -> rejected_declined [label="supplier"]
    new -> extend_boundary [label="customer"]
    extend_boundary -> extend_boundary_approved [label="supplier"]
    extend_boundary -> extend_boundary_declined [label="supplier"]
    rejected_approved -> fixed [label="supplier"]
    extend_boundary_approved -> fixed [label="supplier"]
    fixed -> parsed [label="auto"]
    extend_boundary_declined -> extend_boundary_approved [label="supplier"]
    extend_boundary_declined -> accepted [label="customer"]
    rejected_declined -> rejected_approved [label="supplier"]
    rejected_declined -> accepted [label="customer"]
}
```
