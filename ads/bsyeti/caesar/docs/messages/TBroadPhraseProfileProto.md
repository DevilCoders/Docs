
## Message TBroadPhraseProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L17">BroadPhraseID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L18">PhraseContent</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L10">TPhraseContent</a></i>
<p> Additional BroadPhrase info </p>

</li>
<details open><summary><b>Message TPhraseContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L11">Sources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L5">ESource</a></i>
<p> if multiple - last one is the last update. </p>

</li>
<details open><summary><b>Enum ESource</b></summary>
<ul>
<li><span style="color:#1D7373">BANNERLAND</span></li>
<li><span style="color:#1D7373">BMYT</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L19">NormType</a></b>  <i>int32</i>
<p> NBannerLand.ENormType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L20">PhraseData</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L21">UpdateTime</a></b>  <i>fixed64</i>
<p> DEPRECATED FIELD </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L22">DeltaTimestamp</a></b>  <i>fixed64</i>
<p> actual timestamp of update (DeltaTimestamp in BL or creation_time of delta table for BMYT) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/broad_phrase.proto?rev=r9795881#L25">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
