To create production metrics nirvana graph, build this folder (ya make .) and then create a draft
```
ya make .
./graph_adjustment draft daily_adjustment_counting
```

You can also create testing graph. It is equal to production but with different
settings and different input tables
```
./graph_adjustment draft daily_adjustment_counting_testing
```
