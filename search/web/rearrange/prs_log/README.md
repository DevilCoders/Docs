# PrsLog

Rearrange rule for dumping pred-ranking sets (urls, features, whatever) into prs_log.

## Want to log extra fields (slices) or features?

For logging new features just add them to *search/prs_log/logger/configs/web.config*

For logging extra fields (or slices) ensure you have them in *kernel/prs_log/data_types/web.h*
Then update any existing serializer or make a new one.
If you add new slice, don't forget to update the TestConfigSuite::FactorNamesTest from *ut/test_config_ut.cpp*

**IMPORTANT**: do NOT break the serializers' backward compatibility!
There may already be data logged with the existing serializer, and deserialize results must not differ after your patch.
If in doubts, implement the new serializer.

## The logger config format

Every request maps into one or zero log-configs. That is why the sum of LogConfigs' **LogProbabilities** is not supposed to be > 1.
You are free to change the **SerializerName** at any point: serialized messages are self-descriptive. The main rule is not to break their backward compatibility.

Features slices parsing:
* fill the slice FactorNames you wish to log
* empty slice stands for the whole slice
* no slice stands for no slice :)
