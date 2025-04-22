## JugglerCheckGenerator

```python
import datetime

from crypta.lib.python.spine.juggler import (
    consts,
    juggler_check_generator,
)
from crypta.lib.python.spine.juggler.flap_detector_params import FlapDetectorParams

# Aggregates from this generator will aggregate signals from all of the hosts in the group
juggler = juggler_check_generator.JugglerCheckGenerator(
    tags=["my_tag"],
    child_group="my_nanny_service",
    child_group_type=consts.GroupType.nanny,
    # Add this tag to checks that must trigger phone escalation
    # Create notify rule in juggler with escalation for this tag 
    escalation_tag="my_phone_escalation_tag",
    # By default aggregate host that you will see in the result aggregates equals to child_group
    # Uncomment this to override default aggregate host value
    # host="my_aggregate_host"
)

# Methods return JugglerAggregateCheck, checks can be modified with chaining methods
# Create aggregate for "my_service" and set it to CRIT when half of the hosts from the host group report CRIT
# Hosts should send raw signals to juggler with their FQDN as host and service="my_service"
juggler.some("my_service").set_crit_limit("50%").add_tag("tag")

# The following checks are active and do not require hosts to send anything to juggler
# Check that host is up with ICMP ping
juggler.icmpping()

# Check that response of http handle is 200
juggler.http(
    "api_alive",
    path="/ping",
    port=80,
    # Uncomment this to check response text as well (this is a regexp)
    # substr="OK",
    # By default http and icmpping are used as dependencies for another checks
    # When they CRIT, other checks created from this generator are disabled by forcing them to OK state
    # Uncomment this to disable this behaviour
    # is_unreachable=False,
).add_flap_detector(  # Suppress flaps
    FlapDetectorParams(
        stable_time=datetime.timedelta(minutes=5),
        crit_time=datetime.timedelta(minutes=15),
    )
).add_phone_escalation()  # Adds escalation tag to the check

# Clone generator with additional default parameters
another_juggler = juggler.clone(
    host="another.aggregate.host",
    crit_limit="70%",
)

# Just forward raw signal with host="another.aggregate.host" and service="direct_service" without any aggregation
another_juggler.direct("direct_service")

# Use consts.GroupType.host for aggregating signals from specific hosts
# Useful when you need track signals not related to any specific host
fake_host_juggler = juggler_check_generator.JugglerCheckGenerator(
    host="aggregate_host",
    child_group_type=consts.GroupType.host,
    child_group="fake_raw_host",
)
```
