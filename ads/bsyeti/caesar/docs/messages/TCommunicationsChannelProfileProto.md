
## Message TCommunicationsChannelProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L12">Channel</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L13">MessageId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L14">EventId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L15">Uid</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L16">Source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L93">TEventSource</a></i>
</li>
<details open><summary><b>Message TEventSource</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L94">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L55">ESourceType</a></i>
</li>
<details open><summary><b>Enum ESourceType</b></summary>
<ul>
<li><span style="color:#1D7373">DIRECT_ADMIN</span></li>
<li><span style="color:#1D7373">DIRECT_WEB</span></li>
<li><span style="color:#1D7373">DIRECT_OFFLINE_REGULAR</span></li>
<li><span style="color:#1D7373">RECCOMENDATION_RUNTIME_SERVICE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L95">Id</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L17">Created</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L18">Expired</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L19">Data</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L28">TMessageData</a></i>
</li>
<details open><summary><b>Message TMessageData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L29">Status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L30">EMessageStatus</a></i>
<p>Может быть несколько статусов </p>

</li>
<details open><summary><b>Enum EMessageStatus</b></summary>
<ul>
<li><span style="color:#1D7373">NEW</span></li>
<li><span style="color:#1D7373">CANCEL</span></li>
<li><span style="color:#1D7373">DELIVERED</span></li>
<li><span style="color:#1D7373">ANSWERED</span></li>
<li><span style="color:#1D7373">MUTE</span></li>
<li><span style="color:#1D7373">APPLY</span></li>
<li><span style="color:#1D7373">REJECT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L30">CommunicationType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L23">ECommunicationType</a></i>
</li>
<details open><summary><b>Enum ECommunicationType</b></summary>
<ul>
<li><span style="color:#1D7373">MARKETING</span></li>
<li><span style="color:#1D7373">INFORMATION</span></li>
<li><span style="color:#1D7373">TRIGGER</span></li>
<li><span style="color:#1D7373">UNRESTRICTED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L32">DirectWebData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L108">TDirectWebUIData</a></i>
</li>
<details open><summary><b>Message TDirectWebUIData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L121">MessageText</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L122">ShowAfter</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L123">Priority</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L124">MessageFormat</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L116">EMessageFormat</a></i>
</li>
<details open><summary><b>Enum EMessageFormat</b></summary>
<ul>
<li><span style="color:#1D7373">SIMPLE</span></li>
<li><span style="color:#1D7373">RICH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L125">MessageType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L109">EWebUIMessageType</a></i>
</li>
<details open><summary><b>Enum EWebUIMessageType</b></summary>
<ul>
<li><span style="color:#1D7373">ALERT</span></li>
<li><span style="color:#1D7373">INFO</span></li>
<li><span style="color:#1D7373">POLL</span></li>
<li><span style="color:#1D7373">RECOMMENDATION</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L126">Slot</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L40">ESlot</a></i>
</li>
<details open><summary><b>Enum ESlot</b></summary>
<ul>
<li><span style="color:#1D7373">TOP</span></li>
<li><span style="color:#1D7373">TOP_LEFT</span></li>
<li><span style="color:#1D7373">TOP_RIGHT</span></li>
<li><span style="color:#1D7373">LEFT_SIDE_TOP</span></li>
<li><span style="color:#1D7373">LEFT_SIDE_MIDDLE</span></li>
<li><span style="color:#1D7373">LEFT_SIDE_BOTTOM</span></li>
<li><span style="color:#1D7373">RIGHT_SIDE_TOP</span></li>
<li><span style="color:#1D7373">RIGHT_SIDE_MIDDLE</span></li>
<li><span style="color:#1D7373">RIGHT_SIDE_BOTTOM</span></li>
<li><span style="color:#1D7373">BOTTOM</span></li>
<li><span style="color:#1D7373">BOTTOM_LEFT</span></li>
<li><span style="color:#1D7373">BOTTOM_RIGHT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L127">DisableControls</a></b>  <i>string</i>
<p>идентификаторы контролов, которые нужно заблокировать </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L128">OnlyForPages</a></b>  <i>string</i>
<p>показать только на этих страницах </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L129">SlotTypes</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L130">MajorViewDataVersion</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L131">MinorViewDataVersion</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L132">ViewData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L98">TKeyValues</a></i>
</li>
<details open><summary><b>Message TKeyValues</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L99">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L100">ListValue</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L101">MapValue</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L98">TKeyValues</a></i>
</li>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L33">MailData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L135">TMailData</a></i>
</li>
<details open><summary><b>Message TMailData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L136">MessageText</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L137">SendAfter</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L138">Priority</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L139">RecipientEmails</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L140">ProcessorId</a></b>  <i>string</i>
<p>идентификатор рассылятора </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L141">TemplateId</a></b>  <i>uint32</i>
<p>идентификатор шаблона </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L34">SmsData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L144">TSmsData</a></i>
</li>
<details open><summary><b>Message TSmsData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L145">MessageText</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L146">SendAfter</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L147">Priority</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/communications/proto/common.proto?rev=r9795881#L148">RecipientPhones</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L20">TargetEntityId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L21">NextShowTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L22">StatusBits</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L23">SlotTypeBits</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/communications_channel.proto?rev=r9795881#L25">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
