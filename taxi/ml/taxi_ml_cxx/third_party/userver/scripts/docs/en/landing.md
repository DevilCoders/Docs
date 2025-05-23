
<div class="landing-description">Userver -- C++ Asynchronous Framework</div>


<img src='logo.svg' class='landing-logo' alt='Userver logo big'/>

---

<div class="landing-text">
Userver is an open source asynchronous framework with a rich set of abstractions
for fast and comfortable creation of C++ microservices, services and utilities.
The problem of efficient I/O interactions is solved transparently for the
developers:</div>

<div class="landing-text">
<pre style="padding: 20px; color: silver;white-space: pre-wrap; word-wrap: break-word;">
std::size_t InsertKey(storages::postgres::ClusterPtr pg, std::string_view key) {
    <span style="color: darkgoldenrod">// Asynchronous execution of the SQL query. Current thread handles other</span>
    <span style="color: darkgoldenrod">// requests while the response from the DB is being received:</span>
    <span style="color: #008000">auto</span> res = pg->Execute(storages::postgres::ClusterHostType::kMaster,
                           <span style="color: darkgreen">"INSERT INTO key_table (key) VALUES ($1)"</span>, key);
    <span style="color: #008000">return</span> res.RowsAffected();
}
</pre>
</div>

<!--@snippet postgresql/src/storages/postgres/tests/landing_test.cpp  Landing sample1 -->

<!--div class="landing-text"><div class="landing-motto">Fast. Reliable. Yours!</div></div-->

---

<div class="landing-container">
  <div class="landing-intro-center">
      Userver based micro-services served more than a billion requests while
      you were reading this sentence.
  </div>
</div>

---

<div class="landing-container">
  <div class="landing-intro-left">
      Technologies for debugging and memory profiling a running production
      service.
  </div>
  <div class="landing-intro-right">
      Write @ref md_en_userver_tutorial_hello_service "your first toy C++ service",
      evolve it into a @ref md_en_userver_tutorial_production_service "production ready service".
  </div>
</div>

<div class="landing-container">
  <div class="landing-intro-left">
      Efficient asynchronous drivers for databases (MongoDB, PostgreSQL, Redis,
      ...) and data transfer protocols (HTTP, GRPC, TCP, ...), tasks
      construction and cancellation.
  </div>
  <div class="landing-intro-right">
      Functionality to @ref md_en_schemas_dynamic_configs "change the service configuration"
      on-the-fly. Adjust options of the deadline propagation, timeouts,
      congestion-control without a restart.
  </div>
</div>

<div class="landing-container">
  <div class="landing-intro-left">
      Rich set of high-level components for caches, tasks, distributed locking,
      logging, tracing, statistics, metrics, @ref md_en_userver_formats "JSON/YAML/BSON".
  </div>
  <div class="landing-intro-right">
      Comprehensive set of asynchronous low-level synchronization primitives
      and OS abstractions.
  </div>
</div>


---

<div class="landing-container">
  <div class="landing-intro-center">
      Speed of C++, simplicity of Python, coroutine model of Go.
  </div>
  <div class="landing-intro-center">
      Dive @ref md_en_index "into docs" for more details.
  </div>
</div>
