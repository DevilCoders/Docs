
# Rope

Rope is a microframework originally designed to bind sandbox task parameters
with invoking executable binaries with command line interface.
It is achieved by describing task parameters with class inherited from rope.parameters.TaskParams.
This class allows:
* transform its parameter declaration to declaration with sandbox.sdk2.Parameters specification,
* parse parameters from sandbox.sdk2.Parameters class during sandbox execution,
* transform parsed parameters to environment variables dict,
* parse parameters from command line arguments or environment variables.

As a result you don't have to duplicate parameters declaration.

It also helps to create a common sandbox runner task
for a set of executable binaries. You can choose which one to run with a radio button.
It also un-hiding parameters you need to specify for this task.
