PUMA
====

Push Unbound Metrics Asynchronously

This is a very simple app that pushes unbound metrics to Solomon. It's written
specifically for SafeDNS. It uses unbound-control to query given instances of
unbound for their stats, makes a diff between current and previous run and pushes that diff to Solomon.
