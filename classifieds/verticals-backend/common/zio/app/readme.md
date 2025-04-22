
info: generic information about runtime
 * service name
 * datacenter
 

base: <: info
 * + config
 * + ops server
 * + prometheus
 * + tracer
 * - sentry
 * + logging
 ? - common features (zookeeper?)
 
 
akka-http: <: base 
 * akka-http
 * tracing
 * access logging
 * metrics
 * /ping
 * open/close signal handler
 
 