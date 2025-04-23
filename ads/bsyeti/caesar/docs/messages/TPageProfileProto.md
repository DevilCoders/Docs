
## Message TPageProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L20">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L21">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L16">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L17">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L22">PartnerPage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L3">TPartnerPage</a></i>
</li>
<details open><summary><b>Message TPartnerPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L4">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L6">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L7">PageCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L8">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L9">Domain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L10">PartnerID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L17">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L12">EState</a></i>
</li>
<details open><summary><b>Enum EState</b></summary>
<ul>
<li><span style="color:#1D7373">DISABLED</span></li>
<li><span style="color:#1D7373">TESTING</span></li>
<li><span style="color:#1D7373">ENABLED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L18">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L19">Login</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L20">Mirrors</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L21">ProductID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L22">ProductType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L23">BannerLang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L24">CPA</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L25">CreateDate</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L26">TargetType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L27">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L28">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L29">DisabledFlags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L30">MobileAppMode</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L31">PPCTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L32">AppID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L33">CookieMatchTag</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L35">IsRegularUpdate</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L36">IsTesting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L37">MobileApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L38">OnlyPicture</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L80">RtbVideo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L40">TRtbVideo</a></i>
</li>
<details open><summary><b>Message TRtbVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L41">BufferEmptyLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L42">BufferFullTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L49">Categories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L44">TCategory</a></i>
</li>
<details open><summary><b>Message TCategory</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L45">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L46">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L47">Archive</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L55">Contents</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L51">TContent</a></i>
</li>
<details open><summary><b>Message TContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L52">ContentID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L53">CPM</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L57">Platform</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L58">Skin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L59">SkinTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L60">SkipDelay</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L61">SkipTimeLeftShow</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L62">TimeLeftShow</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L63">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L64">VASTTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L65">VPAIDEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L66">VPAIDTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L67">VideoTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L75">VmapIDs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L69">TVmap</a></i>
</li>
<details open><summary><b>Message TVmap</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L70">VmapID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L71">SingleVideoSession</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L72">SingleVideoSessionInterval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L73">UseInterestingPoints</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L77">WrapperMaxCount</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L78">WrapperTimeout</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L81">SSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L82">SSPPageToken</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L83">Store</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L84">Sad</a></b>  <i>bool</i>
<p> src sad </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L90">Options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L86">TOption</a></i>
<p> E.g. "dontshowbehavior=1;BlockTitle=Реклама;ReloadTimeout=30" </p>

</li>
<details open><summary><b>Message TOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L87">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L88">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L96">PageOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L117">Places</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L99">TPlace</a></i>
</li>
<details open><summary><b>Message TPlace</b></summary>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/partner_interface_object/page.h?rev=r8404394#L52 </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L100">PlaceID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L106">MediaSize</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L102">TMediaSize</a></i>
</li>
<details open><summary><b>Message TMediaSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L103">Width</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L104">Height</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L114">StripeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L108">EStripeType</a></i>
</li>
<details open><summary><b>Enum EStripeType</b></summary>
<ul>
<li><span style="color:#1D7373">FLOATING</span></li>
<li><span style="color:#1D7373">SHIFTING</span></li>
<li><span style="color:#1D7373">BOTTOM</span></li>
<li><span style="color:#1D7373">SCROLL_ON</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L115">StripeAnimation</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L118">ExcludedDomains</a></b>  <i>string</i>
<p> src excludeddomains </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L120">FastContext</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L121">BusinessUnit</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L122">IsGraySite</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L123">IsYandexPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L124">IsPi2</a></b>  <i>bool</i>
<p> src isPi2 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L125">PicturesEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L127">UpdateTime</a></b>  <i>int64</i>
<p> src UpdateTimePI </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L128">EditTime</a></b>  <i>int64</i>
<p> src PIEditTime </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L299">RtbBlocks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L130">TBlock</a></i>
</li>
<details open><summary><b>Message TBlock</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L131">BlockID</a></b>  <i>uint64</i>
<p> ImpID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L133">AdBlockBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L134">AdFoxBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L153">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L148">TAdType</a></i>
</li>
<details open><summary><b>Message TAdType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L149">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L150">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L151">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L159">AdTypeSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L155">TAdTypeSet</a></i>
</li>
<details open><summary><b>Message TAdTypeSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L156">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L157">Value</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L160">AllowedImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L161">AltHeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L162">AltWidth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L163">AlternativeCode</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L164">AlternativeTraffPart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L171">Article</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L166">TArticle</a></i>
</li>
<details open><summary><b>Message TArticle</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L167">ArticleID</a></b>  <i>int64</i>
<p> NOTE: may be negative </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L168">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L169">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L172">BlindLevel</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L173">BlockCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L174">BlockModel</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L175">BlockType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L182">Brand</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L177">TBrand</a></i>
</li>
<details open><summary><b>Message TBrand</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L178">BrandID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L179">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L180">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L183">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L184">CustomBlockData</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L198">DSPInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L186">TDSPInfo</a></i>
</li>
<details open><summary><b>Message TDSPInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L187">DSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L188">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L189">PageDspOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L190">PartnerShare</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L196">RF</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L192">TRangeFrequency</a></i>
</li>
<details open><summary><b>Message TRangeFrequency</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L193">Interval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L194">ShowsCount</a></b>  <i>int64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L200">DSPType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L201">DirectLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L208">Geo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L203">TGeo</a></i>
</li>
<details open><summary><b>Message TGeo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L204">GeoID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L205">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L206">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L209">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L210">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L211">InterstitialBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L212">MultiState</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L213">OptimizeType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L214">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L215">OverrideSizes</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L228">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L229">PageImpOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L230">PremiumVideoFormat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L231">PrivateAuction</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L232">RtbDesign</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L238">Sizes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L234">TSize</a></i>
</li>
<details open><summary><b>Message TSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L235">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L236">Width</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L239">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L264">Video</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L241">TVideo</a></i>
</li>
<details open><summary><b>Message TVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L242">API</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L243">BroadcastReplace</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L244">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L245">Collapse</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L246">ColorScheme</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L247">CountPositions</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L248">MaxDuration</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L249">MaxRepeatCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L250">MetadataAdEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L251">Pip</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L252">Preload</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L253">Protocols</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L254">Repeat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L255">RepeatAfter</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L256">ServerSide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L257">StartTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L258">Stick</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L259">StickTo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L260">TryClient</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L261">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L262">BlockVideoTypes</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L265">VmapID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L271">WrapperAds</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L267">TWrapperAds</a></i>
</li>
<details open><summary><b>Message TWrapperAds</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L268">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L269">End</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L277">WrapperPromo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L273">TWrapperPromo</a></i>
</li>
<details open><summary><b>Message TWrapperPromo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L274">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L275">Promo</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L278">Design</a></b>  <i>string</i>
<p> DirectBlock only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L279">CPMCurrency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L280">AdfoxOwnerID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L281">AdfoxPlaceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L282">PCodeSettings</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L296">DSPSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L284">TDSPSettings</a></i>
</li>
<details open><summary><b>Message TDSPSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L292">DSPBindMode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L285">EDSPBindMode</a></i>
</li>
<details open><summary><b>Enum EDSPBindMode</b></summary>
<ul>
<li><span style="color:#1D7373">AUTO</span></li>
<li><span style="color:#1D7373">WHITELIST</span></li>
<li><span style="color:#1D7373">BLACKLIST</span></li>
<li><span style="color:#1D7373">FORCE</span></li>
<li><span style="color:#1D7373">EXTRA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L293">DSP</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L294">Unmoderated</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L297">MinCPM</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L300">DirectBlocks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L130">TBlock</a></i>
<p> only BlockModel and Design fields </p>

</li>
<details open><summary><b>Message TBlock</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L131">BlockID</a></b>  <i>uint64</i>
<p> ImpID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L133">AdBlockBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L134">AdFoxBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L153">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L148">TAdType</a></i>
</li>
<details open><summary><b>Message TAdType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L149">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L150">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L151">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L159">AdTypeSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L155">TAdTypeSet</a></i>
</li>
<details open><summary><b>Message TAdTypeSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L156">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L157">Value</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L160">AllowedImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L161">AltHeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L162">AltWidth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L163">AlternativeCode</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L164">AlternativeTraffPart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L171">Article</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L166">TArticle</a></i>
</li>
<details open><summary><b>Message TArticle</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L167">ArticleID</a></b>  <i>int64</i>
<p> NOTE: may be negative </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L168">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L169">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L172">BlindLevel</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L173">BlockCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L174">BlockModel</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L175">BlockType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L182">Brand</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L177">TBrand</a></i>
</li>
<details open><summary><b>Message TBrand</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L178">BrandID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L179">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L180">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L183">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L184">CustomBlockData</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L198">DSPInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L186">TDSPInfo</a></i>
</li>
<details open><summary><b>Message TDSPInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L187">DSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L188">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L189">PageDspOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L190">PartnerShare</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L196">RF</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L192">TRangeFrequency</a></i>
</li>
<details open><summary><b>Message TRangeFrequency</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L193">Interval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L194">ShowsCount</a></b>  <i>int64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L200">DSPType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L201">DirectLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L208">Geo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L203">TGeo</a></i>
</li>
<details open><summary><b>Message TGeo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L204">GeoID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L205">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L206">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L209">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L210">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L211">InterstitialBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L212">MultiState</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L213">OptimizeType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L214">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L215">OverrideSizes</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L228">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L229">PageImpOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L230">PremiumVideoFormat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L231">PrivateAuction</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L232">RtbDesign</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L238">Sizes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L234">TSize</a></i>
</li>
<details open><summary><b>Message TSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L235">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L236">Width</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L239">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L264">Video</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L241">TVideo</a></i>
</li>
<details open><summary><b>Message TVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L242">API</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L243">BroadcastReplace</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L244">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L245">Collapse</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L246">ColorScheme</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L247">CountPositions</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L248">MaxDuration</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L249">MaxRepeatCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L250">MetadataAdEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L251">Pip</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L252">Preload</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L253">Protocols</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L254">Repeat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L255">RepeatAfter</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L256">ServerSide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L257">StartTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L258">Stick</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L259">StickTo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L260">TryClient</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L261">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L262">BlockVideoTypes</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L265">VmapID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L271">WrapperAds</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L267">TWrapperAds</a></i>
</li>
<details open><summary><b>Message TWrapperAds</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L268">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L269">End</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L277">WrapperPromo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L273">TWrapperPromo</a></i>
</li>
<details open><summary><b>Message TWrapperPromo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L274">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L275">Promo</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L278">Design</a></b>  <i>string</i>
<p> DirectBlock only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L279">CPMCurrency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L280">AdfoxOwnerID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L281">AdfoxPlaceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L282">PCodeSettings</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L296">DSPSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L284">TDSPSettings</a></i>
</li>
<details open><summary><b>Message TDSPSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L292">DSPBindMode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L285">EDSPBindMode</a></i>
</li>
<details open><summary><b>Enum EDSPBindMode</b></summary>
<ul>
<li><span style="color:#1D7373">AUTO</span></li>
<li><span style="color:#1D7373">WHITELIST</span></li>
<li><span style="color:#1D7373">BLACKLIST</span></li>
<li><span style="color:#1D7373">FORCE</span></li>
<li><span style="color:#1D7373">EXTRA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L293">DSP</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L294">Unmoderated</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L297">MinCPM</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L301">MockMode</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L302">ContentType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L303">DefaultCharset</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L304">TemplateFile</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L305">OrigPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L306">BlockPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L307">DSPPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L308">SourceBit</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L309">CopyParentPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L310">ExtJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L311">MatchJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L312">RFJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L313">PageParamID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L314">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L336">Slots</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L316">TSlot</a></i>
</li>
<details open><summary><b>Message TSlot</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L317">SlotID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L318">Total</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L319">TypeID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L320">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L334">Sequences</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L322">TSequence</a></i>
</li>
<details open><summary><b>Message TSequence</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L323">SequenceID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L324">PrintSlotID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L325">PrintSeqID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L326">PlaceID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L327">PlaceSelect</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L328">SequenceLimit</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L329">SequenceCheck</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L330">SequenceType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L331">ExceptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L332">OrderType</a></b>  <i>sfixed64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L342">PageSelect</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L338">TPageSelect</a></i>
</li>
<details open><summary><b>Message TPageSelect</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L339">Set</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L340">Unset</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L343">AppleStoreID</a></b>  <i>fixed64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L23">CatProfiles</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L19">TCatEngineProfiles</a></i>
</li>
<details open><summary><b>Message TCatEngineProfiles</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L25">Values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L243">TCatEngineProfile</a></i>
</li>
<details open><summary><b>Message TCatEngineProfile</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L244">Entries</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L226">TCatEngineEntry</a></i>
</li>
<details open><summary><b>Message TCatEngineEntry</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L227">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L5">ECategoryType</a></i>
</li>
<details open><summary><b>Enum ECategoryType</b></summary>
<ul>
<li><span style="color:#1D7373">Gender</span></li>
<li><span style="color:#1D7373">Age</span></li>
<li><span style="color:#1D7373">Income</span></li>
<li><span style="color:#1D7373">VisitGoal_Metrika</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaSeg</span></li>
<li><span style="color:#1D7373">VisitGoal_Auditorium</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaCounter</span></li>
<li><span style="color:#1D7373">BmCategories</span></li>
<li><span style="color:#1D7373">KryptaTopDomains</span></li>
<li><span style="color:#1D7373">KryptaAdHocV3</span></li>
<li><span style="color:#1D7373">InstalledMobileApps</span></li>
<li><span style="color:#1D7373">DmpSegmentHashes</span></li>
<li><span style="color:#1D7373">RegionID</span></li>
<li><span style="color:#1D7373">DeviceTypeBT</span></li>
<li><span style="color:#1D7373">DeviceModelHash</span></li>
<li><span style="color:#1D7373">CartOffers</span></li>
<li><span style="color:#1D7373">PurchaseOffers</span></li>
<li><span style="color:#1D7373">DetailOffers</span></li>
<li><span style="color:#1D7373">CartCounterIDs</span></li>
<li><span style="color:#1D7373">PurchaseCounterIDs</span></li>
<li><span style="color:#1D7373">DetailCounterIDs</span></li>
<li><span style="color:#1D7373">ShownOrders</span></li>
<li><span style="color:#1D7373">ShownBanners</span></li>
<li><span style="color:#1D7373">AffinitySites</span></li>
<li><span style="color:#1D7373">DayOfAWeek</span></li>
<li><span style="color:#1D7373">HourOfDay</span></li>
<li><span style="color:#1D7373">NewLongTermInterests</span></li>
<li><span style="color:#1D7373">InnerSegments</span></li>
<li><span style="color:#1D7373">PublicBinarySegments</span></li>
<li><span style="color:#1D7373">ClickedCategories</span></li>
<li><span style="color:#1D7373">PageID</span></li>
<li><span style="color:#1D7373">PageURLHash</span></li>
<li><span style="color:#1D7373">PageQtailID</span></li>
<li><span style="color:#1D7373">MarketVendorID</span></li>
<li><span style="color:#1D7373">MarketCategoryID</span></li>
<li><span style="color:#1D7373">MarketProperties</span></li>
<li><span style="color:#1D7373">VisitedPageID</span></li>
<li><span style="color:#1D7373">MarketComplementaryModels</span></li>
<li><span style="color:#1D7373">HistoryMarketModelID</span></li>
<li><span style="color:#1D7373">HistoryMarketCategorylID</span></li>
<li><span style="color:#1D7373">HistoryMarketVendorID</span></li>
<li><span style="color:#1D7373">AgeSegments</span></li>
<li><span style="color:#1D7373">IncomeSegments</span></li>
<li><span style="color:#1D7373">AffinitySitesWeighted</span></li>
<li><span style="color:#1D7373">ActualCoordinates</span></li>
<li><span style="color:#1D7373">RegularCoordinates</span></li>
<li><span style="color:#1D7373">VisitedOrganizations</span></li>
<li><span style="color:#1D7373">VisitedDomainIDs</span></li>
<li><span style="color:#1D7373">ShortTermInterests</span></li>
<li><span style="color:#1D7373">CategoryProfiles</span></li>
<li><span style="color:#1D7373">AuraGender</span></li>
<li><span style="color:#1D7373">AuraAge</span></li>
<li><span style="color:#1D7373">AuraFollowedUsers</span></li>
<li><span style="color:#1D7373">AuraFollowedKeywords</span></li>
<li><span style="color:#1D7373">AuraCoordinates</span></li>
<li><span style="color:#1D7373">ShownDomains</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersFollowYou</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersYouFollow</span></li>
<li><span style="color:#1D7373">HistoryBeruViewModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewVendorID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderVendorID</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicks</span></li>
<li><span style="color:#1D7373">GeoRubricClicks</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicksFromCard</span></li>
<li><span style="color:#1D7373">GeoRubricsFromRequest</span></li>
<li><span style="color:#1D7373">HourOfWeek</span></li>
<li><span style="color:#1D7373">FreshInstalledApps</span></li>
<li><span style="color:#1D7373">ActiveApps</span></li>
<li><span style="color:#1D7373">AppsCategories</span></li>
<li><span style="color:#1D7373">PrismSegments</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L228">ID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L229">TF</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L245">ProfileType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L117">ECatProfileType</a></i>
</li>
<details open><summary><b>Enum ECatProfileType</b></summary>
<ul>
<li><span style="color:#1D7373">BannerClicks</span></li>
<li><span style="color:#1D7373">RsyaPage</span></li>
<li><span style="color:#1D7373">GeoPermalink</span></li>
<li><span style="color:#1D7373">MarketModel</span></li>
<li><span style="color:#1D7373">User</span></li>
<li><span style="color:#1D7373">CurrentModel</span></li>
<li><span style="color:#1D7373">ModelsHistory</span></li>
<li><span style="color:#1D7373">BannerPrGoodGG</span></li>
<li><span style="color:#1D7373">GroupExportClicks</span></li>
<li><span style="color:#1D7373">GroupExportPrGoodGG</span></li>
<li><span style="color:#1D7373">DomainCategoryClicks</span></li>
<li><span style="color:#1D7373">DomainCategoryPrGoodGG</span></li>
<li><span style="color:#1D7373">OrderClicks</span></li>
<li><span style="color:#1D7373">OrderPrGoodGG</span></li>
<li><span style="color:#1D7373">DomainClicks</span></li>
<li><span style="color:#1D7373">DomainPrGoodGG</span></li>
<li><span style="color:#1D7373">EdadealClicks</span></li>
<li><span style="color:#1D7373">VendorCategoryClicks</span></li>
<li><span style="color:#1D7373">TurboHits</span></li>
<li><span style="color:#1D7373">AppInstalls</span></li>
<li><span style="color:#1D7373">BannerSmoothing</span></li>
<li><span style="color:#1D7373">GroupExportSmoothing</span></li>
<li><span style="color:#1D7373">PageSmoothing</span></li>
<li><span style="color:#1D7373">AppInstallSmoothing</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L246">VectorID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L247">Types</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L5">ECategoryType</a></i>
</li>
<details open><summary><b>Enum ECategoryType</b></summary>
<ul>
<li><span style="color:#1D7373">Gender</span></li>
<li><span style="color:#1D7373">Age</span></li>
<li><span style="color:#1D7373">Income</span></li>
<li><span style="color:#1D7373">VisitGoal_Metrika</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaSeg</span></li>
<li><span style="color:#1D7373">VisitGoal_Auditorium</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaCounter</span></li>
<li><span style="color:#1D7373">BmCategories</span></li>
<li><span style="color:#1D7373">KryptaTopDomains</span></li>
<li><span style="color:#1D7373">KryptaAdHocV3</span></li>
<li><span style="color:#1D7373">InstalledMobileApps</span></li>
<li><span style="color:#1D7373">DmpSegmentHashes</span></li>
<li><span style="color:#1D7373">RegionID</span></li>
<li><span style="color:#1D7373">DeviceTypeBT</span></li>
<li><span style="color:#1D7373">DeviceModelHash</span></li>
<li><span style="color:#1D7373">CartOffers</span></li>
<li><span style="color:#1D7373">PurchaseOffers</span></li>
<li><span style="color:#1D7373">DetailOffers</span></li>
<li><span style="color:#1D7373">CartCounterIDs</span></li>
<li><span style="color:#1D7373">PurchaseCounterIDs</span></li>
<li><span style="color:#1D7373">DetailCounterIDs</span></li>
<li><span style="color:#1D7373">ShownOrders</span></li>
<li><span style="color:#1D7373">ShownBanners</span></li>
<li><span style="color:#1D7373">AffinitySites</span></li>
<li><span style="color:#1D7373">DayOfAWeek</span></li>
<li><span style="color:#1D7373">HourOfDay</span></li>
<li><span style="color:#1D7373">NewLongTermInterests</span></li>
<li><span style="color:#1D7373">InnerSegments</span></li>
<li><span style="color:#1D7373">PublicBinarySegments</span></li>
<li><span style="color:#1D7373">ClickedCategories</span></li>
<li><span style="color:#1D7373">PageID</span></li>
<li><span style="color:#1D7373">PageURLHash</span></li>
<li><span style="color:#1D7373">PageQtailID</span></li>
<li><span style="color:#1D7373">MarketVendorID</span></li>
<li><span style="color:#1D7373">MarketCategoryID</span></li>
<li><span style="color:#1D7373">MarketProperties</span></li>
<li><span style="color:#1D7373">VisitedPageID</span></li>
<li><span style="color:#1D7373">MarketComplementaryModels</span></li>
<li><span style="color:#1D7373">HistoryMarketModelID</span></li>
<li><span style="color:#1D7373">HistoryMarketCategorylID</span></li>
<li><span style="color:#1D7373">HistoryMarketVendorID</span></li>
<li><span style="color:#1D7373">AgeSegments</span></li>
<li><span style="color:#1D7373">IncomeSegments</span></li>
<li><span style="color:#1D7373">AffinitySitesWeighted</span></li>
<li><span style="color:#1D7373">ActualCoordinates</span></li>
<li><span style="color:#1D7373">RegularCoordinates</span></li>
<li><span style="color:#1D7373">VisitedOrganizations</span></li>
<li><span style="color:#1D7373">VisitedDomainIDs</span></li>
<li><span style="color:#1D7373">ShortTermInterests</span></li>
<li><span style="color:#1D7373">CategoryProfiles</span></li>
<li><span style="color:#1D7373">AuraGender</span></li>
<li><span style="color:#1D7373">AuraAge</span></li>
<li><span style="color:#1D7373">AuraFollowedUsers</span></li>
<li><span style="color:#1D7373">AuraFollowedKeywords</span></li>
<li><span style="color:#1D7373">AuraCoordinates</span></li>
<li><span style="color:#1D7373">ShownDomains</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersFollowYou</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersYouFollow</span></li>
<li><span style="color:#1D7373">HistoryBeruViewModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewVendorID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderVendorID</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicks</span></li>
<li><span style="color:#1D7373">GeoRubricClicks</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicksFromCard</span></li>
<li><span style="color:#1D7373">GeoRubricsFromRequest</span></li>
<li><span style="color:#1D7373">HourOfWeek</span></li>
<li><span style="color:#1D7373">FreshInstalledApps</span></li>
<li><span style="color:#1D7373">ActiveApps</span></li>
<li><span style="color:#1D7373">AppsCategories</span></li>
<li><span style="color:#1D7373">PrismSegments</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L248">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L232">TCatEngineCounter</a></i>
</li>
<details open><summary><b>Message TCatEngineCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L233">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L5">ECategoryType</a></i>
</li>
<details open><summary><b>Enum ECategoryType</b></summary>
<ul>
<li><span style="color:#1D7373">Gender</span></li>
<li><span style="color:#1D7373">Age</span></li>
<li><span style="color:#1D7373">Income</span></li>
<li><span style="color:#1D7373">VisitGoal_Metrika</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaSeg</span></li>
<li><span style="color:#1D7373">VisitGoal_Auditorium</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaCounter</span></li>
<li><span style="color:#1D7373">BmCategories</span></li>
<li><span style="color:#1D7373">KryptaTopDomains</span></li>
<li><span style="color:#1D7373">KryptaAdHocV3</span></li>
<li><span style="color:#1D7373">InstalledMobileApps</span></li>
<li><span style="color:#1D7373">DmpSegmentHashes</span></li>
<li><span style="color:#1D7373">RegionID</span></li>
<li><span style="color:#1D7373">DeviceTypeBT</span></li>
<li><span style="color:#1D7373">DeviceModelHash</span></li>
<li><span style="color:#1D7373">CartOffers</span></li>
<li><span style="color:#1D7373">PurchaseOffers</span></li>
<li><span style="color:#1D7373">DetailOffers</span></li>
<li><span style="color:#1D7373">CartCounterIDs</span></li>
<li><span style="color:#1D7373">PurchaseCounterIDs</span></li>
<li><span style="color:#1D7373">DetailCounterIDs</span></li>
<li><span style="color:#1D7373">ShownOrders</span></li>
<li><span style="color:#1D7373">ShownBanners</span></li>
<li><span style="color:#1D7373">AffinitySites</span></li>
<li><span style="color:#1D7373">DayOfAWeek</span></li>
<li><span style="color:#1D7373">HourOfDay</span></li>
<li><span style="color:#1D7373">NewLongTermInterests</span></li>
<li><span style="color:#1D7373">InnerSegments</span></li>
<li><span style="color:#1D7373">PublicBinarySegments</span></li>
<li><span style="color:#1D7373">ClickedCategories</span></li>
<li><span style="color:#1D7373">PageID</span></li>
<li><span style="color:#1D7373">PageURLHash</span></li>
<li><span style="color:#1D7373">PageQtailID</span></li>
<li><span style="color:#1D7373">MarketVendorID</span></li>
<li><span style="color:#1D7373">MarketCategoryID</span></li>
<li><span style="color:#1D7373">MarketProperties</span></li>
<li><span style="color:#1D7373">VisitedPageID</span></li>
<li><span style="color:#1D7373">MarketComplementaryModels</span></li>
<li><span style="color:#1D7373">HistoryMarketModelID</span></li>
<li><span style="color:#1D7373">HistoryMarketCategorylID</span></li>
<li><span style="color:#1D7373">HistoryMarketVendorID</span></li>
<li><span style="color:#1D7373">AgeSegments</span></li>
<li><span style="color:#1D7373">IncomeSegments</span></li>
<li><span style="color:#1D7373">AffinitySitesWeighted</span></li>
<li><span style="color:#1D7373">ActualCoordinates</span></li>
<li><span style="color:#1D7373">RegularCoordinates</span></li>
<li><span style="color:#1D7373">VisitedOrganizations</span></li>
<li><span style="color:#1D7373">VisitedDomainIDs</span></li>
<li><span style="color:#1D7373">ShortTermInterests</span></li>
<li><span style="color:#1D7373">CategoryProfiles</span></li>
<li><span style="color:#1D7373">AuraGender</span></li>
<li><span style="color:#1D7373">AuraAge</span></li>
<li><span style="color:#1D7373">AuraFollowedUsers</span></li>
<li><span style="color:#1D7373">AuraFollowedKeywords</span></li>
<li><span style="color:#1D7373">AuraCoordinates</span></li>
<li><span style="color:#1D7373">ShownDomains</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersFollowYou</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersYouFollow</span></li>
<li><span style="color:#1D7373">HistoryBeruViewModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewVendorID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderVendorID</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicks</span></li>
<li><span style="color:#1D7373">GeoRubricClicks</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicksFromCard</span></li>
<li><span style="color:#1D7373">GeoRubricsFromRequest</span></li>
<li><span style="color:#1D7373">HourOfWeek</span></li>
<li><span style="color:#1D7373">FreshInstalledApps</span></li>
<li><span style="color:#1D7373">ActiveApps</span></li>
<li><span style="color:#1D7373">AppsCategories</span></li>
<li><span style="color:#1D7373">PrismSegments</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L234">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L249">Items</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L237">TCatEngineItem</a></i>
</li>
<details open><summary><b>Message TCatEngineItem</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L238">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L5">ECategoryType</a></i>
</li>
<details open><summary><b>Enum ECategoryType</b></summary>
<ul>
<li><span style="color:#1D7373">Gender</span></li>
<li><span style="color:#1D7373">Age</span></li>
<li><span style="color:#1D7373">Income</span></li>
<li><span style="color:#1D7373">VisitGoal_Metrika</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaSeg</span></li>
<li><span style="color:#1D7373">VisitGoal_Auditorium</span></li>
<li><span style="color:#1D7373">VisitGoal_MetrikaCounter</span></li>
<li><span style="color:#1D7373">BmCategories</span></li>
<li><span style="color:#1D7373">KryptaTopDomains</span></li>
<li><span style="color:#1D7373">KryptaAdHocV3</span></li>
<li><span style="color:#1D7373">InstalledMobileApps</span></li>
<li><span style="color:#1D7373">DmpSegmentHashes</span></li>
<li><span style="color:#1D7373">RegionID</span></li>
<li><span style="color:#1D7373">DeviceTypeBT</span></li>
<li><span style="color:#1D7373">DeviceModelHash</span></li>
<li><span style="color:#1D7373">CartOffers</span></li>
<li><span style="color:#1D7373">PurchaseOffers</span></li>
<li><span style="color:#1D7373">DetailOffers</span></li>
<li><span style="color:#1D7373">CartCounterIDs</span></li>
<li><span style="color:#1D7373">PurchaseCounterIDs</span></li>
<li><span style="color:#1D7373">DetailCounterIDs</span></li>
<li><span style="color:#1D7373">ShownOrders</span></li>
<li><span style="color:#1D7373">ShownBanners</span></li>
<li><span style="color:#1D7373">AffinitySites</span></li>
<li><span style="color:#1D7373">DayOfAWeek</span></li>
<li><span style="color:#1D7373">HourOfDay</span></li>
<li><span style="color:#1D7373">NewLongTermInterests</span></li>
<li><span style="color:#1D7373">InnerSegments</span></li>
<li><span style="color:#1D7373">PublicBinarySegments</span></li>
<li><span style="color:#1D7373">ClickedCategories</span></li>
<li><span style="color:#1D7373">PageID</span></li>
<li><span style="color:#1D7373">PageURLHash</span></li>
<li><span style="color:#1D7373">PageQtailID</span></li>
<li><span style="color:#1D7373">MarketVendorID</span></li>
<li><span style="color:#1D7373">MarketCategoryID</span></li>
<li><span style="color:#1D7373">MarketProperties</span></li>
<li><span style="color:#1D7373">VisitedPageID</span></li>
<li><span style="color:#1D7373">MarketComplementaryModels</span></li>
<li><span style="color:#1D7373">HistoryMarketModelID</span></li>
<li><span style="color:#1D7373">HistoryMarketCategorylID</span></li>
<li><span style="color:#1D7373">HistoryMarketVendorID</span></li>
<li><span style="color:#1D7373">AgeSegments</span></li>
<li><span style="color:#1D7373">IncomeSegments</span></li>
<li><span style="color:#1D7373">AffinitySitesWeighted</span></li>
<li><span style="color:#1D7373">ActualCoordinates</span></li>
<li><span style="color:#1D7373">RegularCoordinates</span></li>
<li><span style="color:#1D7373">VisitedOrganizations</span></li>
<li><span style="color:#1D7373">VisitedDomainIDs</span></li>
<li><span style="color:#1D7373">ShortTermInterests</span></li>
<li><span style="color:#1D7373">CategoryProfiles</span></li>
<li><span style="color:#1D7373">AuraGender</span></li>
<li><span style="color:#1D7373">AuraAge</span></li>
<li><span style="color:#1D7373">AuraFollowedUsers</span></li>
<li><span style="color:#1D7373">AuraFollowedKeywords</span></li>
<li><span style="color:#1D7373">AuraCoordinates</span></li>
<li><span style="color:#1D7373">ShownDomains</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersFollowYou</span></li>
<li><span style="color:#1D7373">AuraLikesByUsersYouFollow</span></li>
<li><span style="color:#1D7373">HistoryBeruViewModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruViewVendorID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderModelID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderCategorylID</span></li>
<li><span style="color:#1D7373">HistoryBeruOrderVendorID</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicks</span></li>
<li><span style="color:#1D7373">GeoRubricClicks</span></li>
<li><span style="color:#1D7373">GeoPermalinkClicksFromCard</span></li>
<li><span style="color:#1D7373">GeoRubricsFromRequest</span></li>
<li><span style="color:#1D7373">HourOfWeek</span></li>
<li><span style="color:#1D7373">FreshInstalledApps</span></li>
<li><span style="color:#1D7373">ActiveApps</span></li>
<li><span style="color:#1D7373">AppsCategories</span></li>
<li><span style="color:#1D7373">PrismSegments</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L239">Ids</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L240">Tfs</a></b>  <i>float</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L26">PackedValues</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L20">TCatEnginePackedProfile</a></i>
</li>
<details open><summary><b>Message TCatEnginePackedProfile</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L21">ProfileType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/quality/adv_machine/lib/catmachine/protos/protos.proto?rev=r9795881#L117">ECatProfileType</a></i>
</li>
<details open><summary><b>Enum ECatProfileType</b></summary>
<ul>
<li><span style="color:#1D7373">BannerClicks</span></li>
<li><span style="color:#1D7373">RsyaPage</span></li>
<li><span style="color:#1D7373">GeoPermalink</span></li>
<li><span style="color:#1D7373">MarketModel</span></li>
<li><span style="color:#1D7373">User</span></li>
<li><span style="color:#1D7373">CurrentModel</span></li>
<li><span style="color:#1D7373">ModelsHistory</span></li>
<li><span style="color:#1D7373">BannerPrGoodGG</span></li>
<li><span style="color:#1D7373">GroupExportClicks</span></li>
<li><span style="color:#1D7373">GroupExportPrGoodGG</span></li>
<li><span style="color:#1D7373">DomainCategoryClicks</span></li>
<li><span style="color:#1D7373">DomainCategoryPrGoodGG</span></li>
<li><span style="color:#1D7373">OrderClicks</span></li>
<li><span style="color:#1D7373">OrderPrGoodGG</span></li>
<li><span style="color:#1D7373">DomainClicks</span></li>
<li><span style="color:#1D7373">DomainPrGoodGG</span></li>
<li><span style="color:#1D7373">EdadealClicks</span></li>
<li><span style="color:#1D7373">VendorCategoryClicks</span></li>
<li><span style="color:#1D7373">TurboHits</span></li>
<li><span style="color:#1D7373">AppInstalls</span></li>
<li><span style="color:#1D7373">BannerSmoothing</span></li>
<li><span style="color:#1D7373">GroupExportSmoothing</span></li>
<li><span style="color:#1D7373">PageSmoothing</span></li>
<li><span style="color:#1D7373">AppInstallSmoothing</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L22">Data</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L27">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L37">Resources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L25">TResources</a></i>
</li>
<details open><summary><b>Message TResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L26">CSPage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L134">TCSPage</a></i>
</li>
<details open><summary><b>Message TCSPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L135">PageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L136">TargetType</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L137">State</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L138">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L139">ContentType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L140">DefaultCharset</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L141">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L142">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L143">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L144">CookieMatchTag</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L145">CategoryKeywordID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L146">TagKeywordID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L147">Options</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L148">OptionsAsString</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L149">Labels</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L150">ExpGroupID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L151">PageSelect</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L152">UniqKeywordID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L153">BannerLang</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L155">DisabledFlags</a></b>  <i>fixed64</i>
<p> deleted 20 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L156">TemplateFile</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L157">OrigPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L158">BlockPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L159">DSPPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L160">MockMode</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L161">SourceBit</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L162">CopyParentPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L163">ExtJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L164">MatchJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L165">RFJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L166">PageParamID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L167">UpdateTime</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L168">EditTime</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L169">DisabledTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L170">SSPID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L172">CTRPredictionID</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L173">ImpCPMParamID</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L174">MixTargetingParamID</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L175">PerfLimitParamID</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L176">SearchSouthParamID</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L177">MinCPMPICategoryIAB</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L178">BannerLangAsString</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L180">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L181">ReadOnly</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L182">CreateTime</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L183">StartTime</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L184">Store</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L186">PageImpItems</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L20">TPageImp</a></i>
</li>
<details open><summary><b>Message TPageImp</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L21">PageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L22">ImpID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L23">BlockSettingsID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L24">DSPType</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L25">AdType</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L26">MinCPMAdvertiser</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L27">MinCPMBrand</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L28">MinCPMArticle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L29">MinCPMRegion</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L30">MinCPMContent</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L31">MinCPMAdType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L32">MinCPMProductTypeGeo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L33">OptimizeType</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L34">BlindDataGroup</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L35">Options</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L36">RangeFrequency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L37">AllowedImageType</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L38">Settings</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L39">CustomData</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L40">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L41">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L42">WrapperBegin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L43">WrapperEnd</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L44">MinCPMPICategoryIAB</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L45">VmapID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L46">UpdateTime</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L48">OptionsAsString</a></b>  <i>string</i>
<p> for debug only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L50">AdfoxOwnerID</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L51">AdfoxPlaceID</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L53">PCodeSettings</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L54">FrequencyShowsOptions</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L56">IsFromReplica</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L57">BlockWidth</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L58">BlockHeight</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L59">BlockAltWidth</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L60">BlockAltHeight</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L61">Sizes</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L62">DirectCount</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L63">ADM</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L65">BlockSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L9">TBlockSettings</a></i>
</li>
<details open><summary><b>Message TBlockSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L10">BlockSettingsID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L11">PageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L12">ImpID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L13">DSPID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L15">Design</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L16">DesignAsJson</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L17">Settings</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L66">MinCPM</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L67">DSPSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L284">TDSPSettings</a></i>
</li>
<details open><summary><b>Message TDSPSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L292">DSPBindMode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L285">EDSPBindMode</a></i>
</li>
<details open><summary><b>Enum EDSPBindMode</b></summary>
<ul>
<li><span style="color:#1D7373">AUTO</span></li>
<li><span style="color:#1D7373">WHITELIST</span></li>
<li><span style="color:#1D7373">BLACKLIST</span></li>
<li><span style="color:#1D7373">FORCE</span></li>
<li><span style="color:#1D7373">EXTRA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L293">DSP</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L294">Unmoderated</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L68">BlockAltTemplateFileResponse</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L69">BlockTemplateFileResponse</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L70">ResponseContentType</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L197">PartnerPage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L188">TPartnerPage</a></i>
</li>
<details open><summary><b>Message TPartnerPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L189">PageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L190">PartnerID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L191">DomainList</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L192">DomainFilter</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L193">DomainPicFilter</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L194">URLTemplate</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L195">Login</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L199">AppleStoreID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L201">SSPPageMappings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L385">TSSPPageMapping</a></i>
</li>
<details open><summary><b>Message TSSPPageMapping</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L386">SSPID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L387">PageToken</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/cs/importers/caesar_page/lib/protos/caesar_page.proto?rev=r9795881#L388">PageID</a></b>  <i>sfixed64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L27">CSPageHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L28">CSPageUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L29">PartnerPageFromProtoTopic</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L3">TPartnerPage</a></i>
</li>
<details open><summary><b>Message TPartnerPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L4">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L6">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L7">PageCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L8">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L9">Domain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L10">PartnerID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L17">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L12">EState</a></i>
</li>
<details open><summary><b>Enum EState</b></summary>
<ul>
<li><span style="color:#1D7373">DISABLED</span></li>
<li><span style="color:#1D7373">TESTING</span></li>
<li><span style="color:#1D7373">ENABLED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L18">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L19">Login</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L20">Mirrors</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L21">ProductID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L22">ProductType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L23">BannerLang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L24">CPA</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L25">CreateDate</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L26">TargetType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L27">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L28">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L29">DisabledFlags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L30">MobileAppMode</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L31">PPCTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L32">AppID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L33">CookieMatchTag</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L35">IsRegularUpdate</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L36">IsTesting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L37">MobileApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L38">OnlyPicture</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L80">RtbVideo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L40">TRtbVideo</a></i>
</li>
<details open><summary><b>Message TRtbVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L41">BufferEmptyLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L42">BufferFullTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L49">Categories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L44">TCategory</a></i>
</li>
<details open><summary><b>Message TCategory</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L45">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L46">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L47">Archive</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L55">Contents</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L51">TContent</a></i>
</li>
<details open><summary><b>Message TContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L52">ContentID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L53">CPM</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L57">Platform</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L58">Skin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L59">SkinTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L60">SkipDelay</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L61">SkipTimeLeftShow</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L62">TimeLeftShow</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L63">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L64">VASTTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L65">VPAIDEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L66">VPAIDTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L67">VideoTimeout</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L75">VmapIDs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L69">TVmap</a></i>
</li>
<details open><summary><b>Message TVmap</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L70">VmapID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L71">SingleVideoSession</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L72">SingleVideoSessionInterval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L73">UseInterestingPoints</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L77">WrapperMaxCount</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L78">WrapperTimeout</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L81">SSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L82">SSPPageToken</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L83">Store</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L84">Sad</a></b>  <i>bool</i>
<p> src sad </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L90">Options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L86">TOption</a></i>
<p> E.g. "dontshowbehavior=1;BlockTitle=Реклама;ReloadTimeout=30" </p>

</li>
<details open><summary><b>Message TOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L87">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L88">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L96">PageOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L117">Places</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L99">TPlace</a></i>
</li>
<details open><summary><b>Message TPlace</b></summary>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/partner_interface_object/page.h?rev=r8404394#L52 </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L100">PlaceID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L106">MediaSize</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L102">TMediaSize</a></i>
</li>
<details open><summary><b>Message TMediaSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L103">Width</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L104">Height</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L114">StripeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L108">EStripeType</a></i>
</li>
<details open><summary><b>Enum EStripeType</b></summary>
<ul>
<li><span style="color:#1D7373">FLOATING</span></li>
<li><span style="color:#1D7373">SHIFTING</span></li>
<li><span style="color:#1D7373">BOTTOM</span></li>
<li><span style="color:#1D7373">SCROLL_ON</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L115">StripeAnimation</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L118">ExcludedDomains</a></b>  <i>string</i>
<p> src excludeddomains </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L120">FastContext</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L121">BusinessUnit</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L122">IsGraySite</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L123">IsYandexPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L124">IsPi2</a></b>  <i>bool</i>
<p> src isPi2 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L125">PicturesEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L127">UpdateTime</a></b>  <i>int64</i>
<p> src UpdateTimePI </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L128">EditTime</a></b>  <i>int64</i>
<p> src PIEditTime </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L299">RtbBlocks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L130">TBlock</a></i>
</li>
<details open><summary><b>Message TBlock</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L131">BlockID</a></b>  <i>uint64</i>
<p> ImpID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L133">AdBlockBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L134">AdFoxBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L153">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L148">TAdType</a></i>
</li>
<details open><summary><b>Message TAdType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L149">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L150">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L151">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L159">AdTypeSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L155">TAdTypeSet</a></i>
</li>
<details open><summary><b>Message TAdTypeSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L156">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L157">Value</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L160">AllowedImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L161">AltHeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L162">AltWidth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L163">AlternativeCode</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L164">AlternativeTraffPart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L171">Article</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L166">TArticle</a></i>
</li>
<details open><summary><b>Message TArticle</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L167">ArticleID</a></b>  <i>int64</i>
<p> NOTE: may be negative </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L168">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L169">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L172">BlindLevel</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L173">BlockCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L174">BlockModel</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L175">BlockType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L182">Brand</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L177">TBrand</a></i>
</li>
<details open><summary><b>Message TBrand</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L178">BrandID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L179">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L180">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L183">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L184">CustomBlockData</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L198">DSPInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L186">TDSPInfo</a></i>
</li>
<details open><summary><b>Message TDSPInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L187">DSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L188">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L189">PageDspOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L190">PartnerShare</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L196">RF</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L192">TRangeFrequency</a></i>
</li>
<details open><summary><b>Message TRangeFrequency</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L193">Interval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L194">ShowsCount</a></b>  <i>int64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L200">DSPType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L201">DirectLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L208">Geo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L203">TGeo</a></i>
</li>
<details open><summary><b>Message TGeo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L204">GeoID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L205">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L206">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L209">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L210">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L211">InterstitialBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L212">MultiState</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L213">OptimizeType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L214">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L215">OverrideSizes</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L228">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L229">PageImpOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L230">PremiumVideoFormat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L231">PrivateAuction</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L232">RtbDesign</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L238">Sizes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L234">TSize</a></i>
</li>
<details open><summary><b>Message TSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L235">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L236">Width</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L239">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L264">Video</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L241">TVideo</a></i>
</li>
<details open><summary><b>Message TVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L242">API</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L243">BroadcastReplace</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L244">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L245">Collapse</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L246">ColorScheme</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L247">CountPositions</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L248">MaxDuration</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L249">MaxRepeatCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L250">MetadataAdEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L251">Pip</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L252">Preload</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L253">Protocols</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L254">Repeat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L255">RepeatAfter</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L256">ServerSide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L257">StartTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L258">Stick</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L259">StickTo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L260">TryClient</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L261">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L262">BlockVideoTypes</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L265">VmapID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L271">WrapperAds</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L267">TWrapperAds</a></i>
</li>
<details open><summary><b>Message TWrapperAds</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L268">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L269">End</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L277">WrapperPromo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L273">TWrapperPromo</a></i>
</li>
<details open><summary><b>Message TWrapperPromo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L274">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L275">Promo</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L278">Design</a></b>  <i>string</i>
<p> DirectBlock only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L279">CPMCurrency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L280">AdfoxOwnerID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L281">AdfoxPlaceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L282">PCodeSettings</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L296">DSPSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L284">TDSPSettings</a></i>
</li>
<details open><summary><b>Message TDSPSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L292">DSPBindMode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L285">EDSPBindMode</a></i>
</li>
<details open><summary><b>Enum EDSPBindMode</b></summary>
<ul>
<li><span style="color:#1D7373">AUTO</span></li>
<li><span style="color:#1D7373">WHITELIST</span></li>
<li><span style="color:#1D7373">BLACKLIST</span></li>
<li><span style="color:#1D7373">FORCE</span></li>
<li><span style="color:#1D7373">EXTRA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L293">DSP</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L294">Unmoderated</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L297">MinCPM</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L300">DirectBlocks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L130">TBlock</a></i>
<p> only BlockModel and Design fields </p>

</li>
<details open><summary><b>Message TBlock</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L131">BlockID</a></b>  <i>uint64</i>
<p> ImpID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L133">AdBlockBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L134">AdFoxBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L153">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L148">TAdType</a></i>
</li>
<details open><summary><b>Message TAdType</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L149">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L150">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L151">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L159">AdTypeSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L155">TAdTypeSet</a></i>
</li>
<details open><summary><b>Message TAdTypeSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L156">AdType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L136">EAdType</a></i>
</li>
<details open><summary><b>Enum EAdType</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">TEXT</span></li>
<li><span style="color:#1D7373">MEDIA</span></li>
<li><span style="color:#1D7373">MEDIA_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO</span></li>
<li><span style="color:#1D7373">VIDEO_PERFORMANCE</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">AUDIO</span></li>
<li><span style="color:#1D7373">VIDEO_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L157">Value</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L160">AllowedImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L161">AltHeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L162">AltWidth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L163">AlternativeCode</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L164">AlternativeTraffPart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L171">Article</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L166">TArticle</a></i>
</li>
<details open><summary><b>Message TArticle</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L167">ArticleID</a></b>  <i>int64</i>
<p> NOTE: may be negative </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L168">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L169">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L172">BlindLevel</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L173">BlockCaption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L174">BlockModel</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L175">BlockType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L182">Brand</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L177">TBrand</a></i>
</li>
<details open><summary><b>Message TBrand</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L178">BrandID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L179">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L180">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L183">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L184">CustomBlockData</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L198">DSPInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L186">TDSPInfo</a></i>
</li>
<details open><summary><b>Message TDSPInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L187">DSPID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L188">CPM</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L189">PageDspOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L190">PartnerShare</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L196">RF</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L192">TRangeFrequency</a></i>
</li>
<details open><summary><b>Message TRangeFrequency</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L193">Interval</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L194">ShowsCount</a></b>  <i>int64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L200">DSPType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L201">DirectLimit</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L208">Geo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L203">TGeo</a></i>
</li>
<details open><summary><b>Message TGeo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L204">GeoID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L205">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L206">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L209">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L210">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L211">InterstitialBlock</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L212">MultiState</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L213">OptimizeType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L214">OrderTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L215">OverrideSizes</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L228">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L229">PageImpOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L92">TPageOption</a></i>
</li>
<details open><summary><b>Message TPageOption</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L93">Disable</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L94">Enable</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L230">PremiumVideoFormat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L231">PrivateAuction</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L232">RtbDesign</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L238">Sizes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L234">TSize</a></i>
</li>
<details open><summary><b>Message TSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L235">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L236">Width</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L239">TargetTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L264">Video</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L241">TVideo</a></i>
</li>
<details open><summary><b>Message TVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L242">API</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L243">BroadcastReplace</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L244">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L245">Collapse</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L246">ColorScheme</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L247">CountPositions</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L248">MaxDuration</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L249">MaxRepeatCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L250">MetadataAdEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L251">Pip</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L252">Preload</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L253">Protocols</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L254">Repeat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L255">RepeatAfter</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L256">ServerSide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L257">StartTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L258">Stick</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L259">StickTo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L260">TryClient</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L261">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L262">BlockVideoTypes</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L265">VmapID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L271">WrapperAds</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L267">TWrapperAds</a></i>
</li>
<details open><summary><b>Message TWrapperAds</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L268">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L269">End</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L277">WrapperPromo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L273">TWrapperPromo</a></i>
</li>
<details open><summary><b>Message TWrapperPromo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L274">Begin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L275">Promo</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L278">Design</a></b>  <i>string</i>
<p> DirectBlock only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L279">CPMCurrency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L280">AdfoxOwnerID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L281">AdfoxPlaceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L282">PCodeSettings</a></b>  <i>string</i>
<p> json here </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L296">DSPSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L284">TDSPSettings</a></i>
</li>
<details open><summary><b>Message TDSPSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L292">DSPBindMode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L285">EDSPBindMode</a></i>
</li>
<details open><summary><b>Enum EDSPBindMode</b></summary>
<ul>
<li><span style="color:#1D7373">AUTO</span></li>
<li><span style="color:#1D7373">WHITELIST</span></li>
<li><span style="color:#1D7373">BLACKLIST</span></li>
<li><span style="color:#1D7373">FORCE</span></li>
<li><span style="color:#1D7373">EXTRA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L293">DSP</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L294">Unmoderated</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L297">MinCPM</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L301">MockMode</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L302">ContentType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L303">DefaultCharset</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L304">TemplateFile</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L305">OrigPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L306">BlockPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L307">DSPPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L308">SourceBit</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L309">CopyParentPageID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L310">ExtJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L311">MatchJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L312">RFJsonOptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L313">PageParamID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L314">PICategoryIAB</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L217">TPICategoryIAB</a></i>
</li>
<details open><summary><b>Message TPICategoryIAB</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L218">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L219">MediaCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L220">MediaImageReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L221">Direct</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L222">MediaCreative</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L223">MediaImage</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L224">MediaSmart</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L225">VideoCreativeReach</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L226">AllProducts</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L336">Slots</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L316">TSlot</a></i>
</li>
<details open><summary><b>Message TSlot</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L317">SlotID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L318">Total</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L319">TypeID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L320">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L334">Sequences</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L322">TSequence</a></i>
</li>
<details open><summary><b>Message TSequence</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L323">SequenceID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L324">PrintSlotID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L325">PrintSeqID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L326">PlaceID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L327">PlaceSelect</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L328">SequenceLimit</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L329">SequenceCheck</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L330">SequenceType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L331">ExceptionID</a></b>  <i>sfixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L332">OrderType</a></b>  <i>sfixed64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L342">PageSelect</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L338">TPageSelect</a></i>
</li>
<details open><summary><b>Message TPageSelect</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L339">Set</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L340">Unset</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/partner/proto/page.proto?rev=r9795881#L343">AppleStoreID</a></b>  <i>fixed64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L35">MoneyMap</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L31">TMoneyMap</a></i>
</li>
<details open><summary><b>Message TMoneyMap</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L32">MoneyMapPage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L5">TMoneyMapPage</a></i>
</li>
<details open><summary><b>Message TMoneyMapPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L6">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L7">ImpID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L9">AbcID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L10">AbcIDRuName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L11">AbcOebsID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L12">AbcOebsIDRuName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L13">IsInternal</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L14">OebsService</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L15">Os</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L16">Platform</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L17">TrafficSubSubType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L18">TrafficSubType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L19">TrafficType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L20">ZenDeviceType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L21">ZenIntegration</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L22">ZenLevel1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L23">ZenLevel2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L24">ZenLevel3</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L25">ZenLevel4</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L26">ZenOsName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L27">ZenProduct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L29">UpdateTime</a></b>  <i>uint64</i>
<p> synthetic field, filled by resharder </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L33">MoneyMapPageImp</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L5">TMoneyMapPage</a></i>
</li>
<details open><summary><b>Message TMoneyMapPage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L6">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L7">ImpID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L9">AbcID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L10">AbcIDRuName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L11">AbcOebsID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L12">AbcOebsIDRuName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L13">IsInternal</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L14">OebsService</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L15">Os</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L16">Platform</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L17">TrafficSubSubType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L18">TrafficSubType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L19">TrafficType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L20">ZenDeviceType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L21">ZenIntegration</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L22">ZenLevel1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L23">ZenLevel2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L24">ZenLevel3</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L25">ZenLevel4</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L26">ZenOsName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L27">ZenProduct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/money_map_page.proto?rev=r9795881#L29">UpdateTime</a></b>  <i>uint64</i>
<p> synthetic field, filled by resharder </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/page.proto?rev=r9795881#L40">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
