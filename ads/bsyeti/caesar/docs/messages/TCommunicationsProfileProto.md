
## Message TCommunicationsProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications.proto?rev=r9795881#L9">UserID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications.proto?rev=r9795881#L10">Settings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L165">TProfileSettings</a></i>
</li>
<details open><summary><b>Message TProfileSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L166">Version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L167">DirectWebUIChannelSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L151">TDirectWebUIChannelSettings</a></i>
</li>
<details open><summary><b>Message TDirectWebUIChannelSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L152">Disabled</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L168">MailChannelSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L155">TMailChannelSettings</a></i>
</li>
<details open><summary><b>Message TMailChannelSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L156">Disabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L157">Emails</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L169">SmsChannelSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L160">TSmsChannelSettings</a></i>
</li>
<details open><summary><b>Message TSmsChannelSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L161">Disabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L162">Phones</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications.proto?rev=r9795881#L11">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L172">TProfileState</a></i>
</li>
<details open><summary><b>Message TProfileState</b></summary>
<p>Данные по запланированным сообщениям, чтобы при появлении новых не нарушать лимиты </p>

<ul>
<span>empty</span>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications.proto?rev=r9795881#L13">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
