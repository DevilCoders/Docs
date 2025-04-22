
## Message TDomainProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/domain.proto?rev=r9795881#L14">DomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/domain.proto?rev=r9795881#L15">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/domain.proto?rev=r9795881#L10">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/domain.proto?rev=r9795881#L11">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
</li>
<details open><summary><b>Message TCounterPack</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L22">counter_ids</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L23">keys</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L44">values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L36">TValueType</a></i>
</li>
<details open><summary><b>Message TValueType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L38">float_values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L33">TFloatValue</a></i>
</li>
<details open><summary><b>Message TFloatValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L34">value</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L39">double_values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L30">TDoubleValue</a></i>
</li>
<details open><summary><b>Message TDoubleValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L31">value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L40">fixed32_values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L24">TFixed32Value</a></i>
</li>
<details open><summary><b>Message TFixed32Value</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L25">value</a></b>  <i>fixed32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L41">fixed64_values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L27">TFixed64Value</a></i>
</li>
<details open><summary><b>Message TFixed64Value</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L28">value</a></b>  <i>fixed64</i>
</li>


</ul></details>

</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/domain.proto?rev=r9795881#L18">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
