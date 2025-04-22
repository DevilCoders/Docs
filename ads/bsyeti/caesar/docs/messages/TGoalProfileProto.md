
## Message TGoalProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L48">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L49">GoalType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L24">TGoalType</a></i>
</li>
<details open><summary><b>Message TGoalType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L26">Timestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L27">GoalName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L28">GoalType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/metrika/core/libs/protos/protos/types/goal_type.proto?rev=r9795881#L6">GoalType</a></i>
</li>
<details open><summary><b>Enum GoalType</b></summary>
<ul>
<li><span style="color:#1D7373">GOAL_TYPE_UNKNOWN</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_DEPTH</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_URL</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_ACTION</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_OFFLINE</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_CALL</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_EMAIL</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_PHONE</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_FORM</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_MESSENGER</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_FILE</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_SEARCH</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_BUTTON</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_PAYMENT_SYSTEM</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_SOCIAL_NETWORK</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_CONDITIONAL_CALL</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_USER_PURCHASE</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_USER_CART</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_SOVETNIK_PURCHASE</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_SOVETNIK_CART</span></li>
<li><span style="color:#1D7373">GOAL_TYPE_CONTACT_DATA</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L50">Counter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L31">TCounter</a></i>
</li>
<details open><summary><b>Message TCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L32">CounterID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L33">CounterName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L51">GoalConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L19">TGoalConditions</a></i>
</li>
<details open><summary><b>Message TGoalConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L20">GoalConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L12">TGoalCondition</a></i>
</li>
<details open><summary><b>Message TGoalCondition</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L13">URL</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L16">PatternType</a></b>  <i>int64</i>
<p> enum from https://a.yandex-team.ru/arc/trunk/arcadia/metrika/core/libs/statdaemons/Goal.h?rev=r8503296#L26 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L21">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L52">AffinitiveSites</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L36">TAffinitiveSites</a></i>
</li>
<details open><summary><b>Message TAffinitiveSites</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L37">AffinitiveSites</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L5">AffinitiveSite</a></i>
</li>
<details open><summary><b>Message AffinitiveSite</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L6">Site</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L7">Weight</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L38">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L53">AffinitiveFeatures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L41">TAffinitiveFeatures</a></i>
</li>
<details open><summary><b>Message TAffinitiveFeatures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L42">AffinitiveSites</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L5">AffinitiveSite</a></i>
</li>
<details open><summary><b>Message AffinitiveSite</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L6">Site</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L7">Weight</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L43">AffinitiveApps</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L10">AffinitiveApp</a></i>
</li>
<details open><summary><b>Message AffinitiveApp</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L11">App</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L12">Weight</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L44">AffinitiveWords</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L15">AffinitiveWord</a></i>
</li>
<details open><summary><b>Message AffinitiveWord</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L16">Word</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/affinitive_sites.proto?rev=r9795881#L17">Weight</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L45">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal.proto?rev=r9795881#L56">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
<p> service field, used only for updates queue </p>

</li>
<details open><summary><b>Message TServiceFields</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L23">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L16">EProfileServiceFlags</a></i>
</li>
<details open><summary><b>Enum EProfileServiceFlags</b></summary>
<p> flags for updates queue (which) </p>

<ul>
<li><span style="color:#1D7373">PSF_NONE</span></li>
<li><span style="color:#1D7373">PSF_DELETED</span></li>
<li><span style="color:#1D7373">PSF_FULL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L24">ChangedColumns</a></b>  <i>fixed64</i>
</li>


</ul></details>

</ul>
