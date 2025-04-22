TF controls summary
===================

Applicator requires Dossier node in the graph. The `Dossier.Env` field
lists "environment" variables controlling the execution of the graph.
For details of the controls see `library/cpp/tf/mkldnn`.

The Dossier.Env variables `TF_ENABLE_MKLDNN` and `MKDLNN_USE_WEIGHTS_AS_GIVEN`
are set per-session, so graphs with different settings of these variables
may be executed concurrently.

If `MKLDNN_USE_WEIGHTS_AS_GIVEN` is set, but the host does not support AVX (which
is necessary to use MKLDNN) the applicator aborts the application.

The Dossier.Env variable `DANET_STYLE_PADDING` is *obligatory*, 
set per process rather than per session, so the applicator cannot execute
graphs with different settings of this variable in parallel.
