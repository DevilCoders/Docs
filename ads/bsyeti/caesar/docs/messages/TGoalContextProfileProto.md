
## Message TGoalContextProfileProto
<p> Reference list of retargeting conditions </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal_context.proto?rev=r9795881#L10">GoalContextID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal_context.proto?rev=r9795881#L13">GoalContext</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L3">TGoalContext</a></i>
<p> See detailed description in NBSYeti.NEvent.TGoalContext </p>

</li>
<details open><summary><b>Message TGoalContext</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L45">Version</a></b>  <i>uint64</i>
<p> In fact the iterId from the original direct-banners-log message </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L57">Expression</a></b>  <i>string</i>
<p>* Logical clause of condition in specific format  <expr> ::= <goal_id_1>':'<fresh_time_1> <operator_1> ... <operator_N> <goal_id_N>':'<fresh_time_N>    <goal_id> ::= unsigned int    <fresh_time> ::= unsigned int  i.e. 1:2 & 3:4 means the banner will be picked if a goal with  id = 1 is achieved not early then two days ago and a goal  with id = 3 achieved not early then 4 days ago </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L58">LastActiveTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L59">ParsedExpression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L8">TGoalExpression</a></i>
</li>
<details open><summary><b>Message TGoalExpression</b></summary>
<p> An expression consists of a chain of logical expressions, including "&", "|", "~" and the brackets "()", whose nodes are the satisfying value of TValue.  There are two types of TValue: TKeyword and TGoal:   * TKeyword checks the equality of the Id key to the Value   * TGoal checks whether the goal Id was completed no earlier than Now() - FreshTime (seconds) </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L41">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L23">TExpression</a></i>
</li>
<details open><summary><b>Message TExpression</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L27">Or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L24">TConjunction</a></i>
</li>
<details open><summary><b>Message TConjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L25">And</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L35">TExpressionImpl</a></i>
</li>
<details open><summary><b>Message TExpressionImpl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L37">ExpressionAtom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L29">TExpressionAtom</a></i>
</li>
<details open><summary><b>Message TExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L31">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L23">TExpression</a></i>
</li>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L32">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L17">TValue</a></i>
</li>
<details open><summary><b>Message TValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L19">Keyword</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L9">TKeyword</a></i>
</li>
<details open><summary><b>Message TKeyword</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L10">Id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L11">Value</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L20">Goal</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L13">TGoal</a></i>
</li>
<details open><summary><b>Message TGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L14">Id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L15">FreshTime</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L38">NotExpressionAtom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L29">TExpressionAtom</a></i>
</li>
<details open><summary><b>Message TExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L31">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L23">TExpression</a></i>
</li>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L32">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L17">TValue</a></i>
</li>
<details open><summary><b>Message TValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L19">Keyword</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L9">TKeyword</a></i>
</li>
<details open><summary><b>Message TKeyword</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L10">Id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L11">Value</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L20">Goal</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L13">TGoal</a></i>
</li>
<details open><summary><b>Message TGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L14">Id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/goal_context.proto?rev=r9795881#L15">FreshTime</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>

</ul></details>

</ul></details>

</ul></details>

</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/goal_context.proto?rev=r9795881#L16">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
