
## Message TBannerProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L561">BannerID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L562">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L58">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L65">CtrCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L59">TCtrCounter</a></i>
</li>
<details open><summary><b>Message TCtrCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L60">Clicks</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L61">Shows</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L63">UpdateTime</a></b>  <i>fixed32</i>
<p> shows and clicks decayed to UpdateTime </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L66">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L563">Resources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L69">TResources</a></i>
</li>
<details open><summary><b>Message TResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L328">Href</a></b>  <i>bytes</i>
<p> Banner URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L329">ContentStoreHref</a></b>  <i>bytes</i>
<p> Banner URL for mobile applications (after redirect) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L330">HrefText</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L331">Title</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L332">Body</a></b>  <i>bytes</i>
<p> Banner text </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L333">Site</a></b>  <i>bytes</i>
<p> Domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L334">SiteID</a></b>  <i>uint64</i>
<p> REMOVED FIELD, REMOVE LATER </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L335">ApplicationID</a></b>  <i>uint64</i>
<p> MobileAppID in Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L336">Categories</a></b>  <i>uint64</i>
<p> TargetFlat in Direct, CategoryIDs in BannerLand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L337">TemplateID</a></b>  <i>uint64</i>
<p> Banner template, see //home/yabs/dict/TemplateBanner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L338">Version</a></b>  <i>uint64</i>
<p> IterID in Direct, DeltaTimestamp in BannerLand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L340">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L341">TargetDomain</a></b>  <i>string</i>
<p> Detected by TargetDomainID using //home/yabs/dict/TargetDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L342">TargetDomainFromDirect</a></b>  <i>string</i>
<p> DomainFilter OR TargetDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L344">GroupBannerID</a></b>  <i>uint64</i>
<p> GroupExportID for smart banners </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L345">Tsars</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
</li>
<details open><summary><b>Message TEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L7">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L9">VectorID</a></b>  <i>uint64</i>
<p> https://wiki.yandex-team.ru/adsquality/car-reglament/ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L11">Vector</a></b>  <i>float</i>
<p> factors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L13">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/compress_vectors/proto/compress_info.proto?rev=r9795881#L5">ECompressionType</a></i>
</li>
<details open><summary><b>Enum ECompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">NO_COMPRESSION</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_24_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_28_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_200_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_V2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_RANK_LOSS_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_65_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_IMAGES_DSSM_APPLIER_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_QUORUM_66_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_NEW_QUORUM_67_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_BANNER_RELEV_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_136_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_JULY_4_76_UNIFORM_8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L14">CompressedVector</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L347">MultikCategories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L70">TMultikCategories</a></i>
</li>
<details open><summary><b>Message TMultikCategories</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L76">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L77">Categories</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L78">CategoriesSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L71">ECategoriesSource</a></i>
</li>
<details open><summary><b>Enum ECategoriesSource</b></summary>
<ul>
<li><span style="color:#1D7373">ML</span></li>
<li><span style="color:#1D7373">AppStore</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L79">ModelID</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L348">Multiks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L70">TMultikCategories</a></i>
</li>
<details open><summary><b>Message TMultikCategories</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L76">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L77">Categories</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L78">CategoriesSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L71">ECategoriesSource</a></i>
</li>
<details open><summary><b>Enum ECategoriesSource</b></summary>
<ul>
<li><span style="color:#1D7373">ML</span></li>
<li><span style="color:#1D7373">AppStore</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L79">ModelID</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L351">TitleMediaSmart</a></b>  <i>string</i>
<p> smart-banners only </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L352">TitleExtension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L354">Url</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L82">TUrl</a></i>
</li>
<details open><summary><b>Message TUrl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L83">SpyLogTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L84">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L85">LandingTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L86">LandingUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L87">FeedSendTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L88">LandingUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L90">IsHrefChanged</a></b>  <i>bool</i>
<p> true, if url has been changed, after finding info about new url in NormalizedUrls this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L94">AppearanceUrlWithoutTitleTime</a></b>  <i>uint64</i>
<p> first time of appearance url without any info  if url has LandingUrl, this field will be not filled  when href сhanges, this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L97">LandingTitleDownloadTime</a></b>  <i>uint64</i>
<p> time of the first appearance of any info about url  when href changes, this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L99">Urldat</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L5">TUrldat</a></i>
<p> robot factors </p>

</li>
<details open><summary><b>Message TUrldat</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L6">Host</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L7">Path</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L8">LastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L9">ExportTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L10">TextCRC</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L12">HttpModTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L13">HttpCode</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L14">MimeType</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L15">Language</a></b>  <i>uint32</i>
<p> Again type should be same as in Gemini </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L16">Encoding</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L17">LangRegion</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L18">HasContent</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L19">HostIsNotAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L20">HostIsBannedByRobotTxt</a></b>  <i>bool</i>
<p> Disallow /. Applied with delay. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L21">HostIsUncrawlable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L22">HostIsSmuggling</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L23">UrlIsBannedByRobotTxt</a></b>  <i>bool</i>
<p> Applied with delay. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L24">IsContentExport</a></b>  <i>bool</i>
<p> Not propagated to new states </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L25">HostIsMultiLang</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L26">IP</a></b>  <i>uint32</i>
<p> Not used. TODO: can be removed? </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L27">SimpleSimhash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L28">Simhash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L29">TitleHash</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L30">SimhashDocLength</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L31">SimhashData</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L32">RelCanonicalTarget</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L33">IsRedirect</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L34">RedirTarget</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L35">IsMetaRefreshTargetRedir</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L39">CanonizedRedirTarget</a></b>  <i>string</i>
<p> Canonized version of RedirTarget. Canonized by robots.txt and RFL. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L41">SourceId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L42">SourceName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L43">IsBannedByRfl</a></b>  <i>bool</i>
<p> Result of RflCanonized->CheckFiltered </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L45">CanonizedPath</a></b>  <i>string</i>
<p> Path canonized by robots.txt and RFL. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L47">DelayedUrlPenalty</a></b>  <i>uint64</i>
<p> Number of bases url has been delayed for. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L48">FetchTime</a></b>  <i>uint32</i>
<p> Time it took spider to fetch document. In microseconds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L50">LemurAddTime</a></b>  <i>uint32</i>
<p> Time when document was discovered by Lemur/Samovar. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L51">FreshTimestampFrom</a></b>  <i>uint32</i>
<p> Source of url discovery </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L52">FreshTimestamp</a></b>  <i>uint32</i>
<p></p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L55">OriginalHost</a></b>  <i>string</i>
<p> Intermediate fields. Used in floodgate when inverting redirects. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L56">OriginalPath</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L57">RedirTargetIsBannedByRobots</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L60">ZoraCtxFlags</a></b>  <i>uint64</i>
<p> Saved flags from Zora context </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L62">IsAlisaBusinessChat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L63">IsAlisaLanding</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L64">BasesAge</a></b>  <i>uint64</i>
<p> TODO(alexromanov): remove BasesAge </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L66">SamovarConsumers</a></b>  <i>bytes</i>
<p> serialized TSamovarConsumerVector </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L68">IsProcessedByRotor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L69">WasIntendedForRotor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L70">IsRotorCorrupted</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L76">ReachableFromMordaSince</a></b>  <i>uint32</i>
<p> ReachableFromMordaSince means "document is reachable from morda since value base-state" (see JUPITER-942)   * null - document never was reachable from morda;   * 0 - document was known before ReachableFromMordaSince was added and has no update since there;   * timestamp = document is reachable from morda since base with state $timestamp. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L77">IsRandomCrawl</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L78">UrlTransliterationData</a></b>  <i>bytes</i>
<p> serialized TUrlTransliterationData </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L79">ZoraCtx</a></b>  <i>bytes</i>
<p> serialized TUkropZoraContext </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L80">FromSitemap</a></b>  <i>bool</i>
<p> url was in sitemap somewhen </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L81">LastWatchLogCounterId</a></b>  <i>uint64</i>
<p> last counter id used for validity </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L82">WasManualCrawl</a></b>  <i>bool</i>
<p> indexed by forced, addurl or sitemap somewhen </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L83">FirstKnownValidTs</a></b>  <i>uint32</i>
<p> time of valid detection </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L84">JupiterAddTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L85">IsTranslatedDocument</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L86">IsRemoved</a></b>  <i>bool</i>
<p> used to merge RT Jupiter delta with remerge </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L87">SpiderTimestampUs</a></b>  <i>uint64</i>
<p> used to distinct rows with the same LastAccess </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L88">DelayedAddTime</a></b>  <i>uint64</i>
<p> set in delayed doc contour TODO(alexromanov): delete in June 2022 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L89">IsMock</a></b>  <i>bool</i>
<p> page was obtained using mock pages parser </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L90">ValidFromMetrikaLastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L91">IsHitrenimals</a></b>  <i>bool</i>
<p> page was downloaded via hitrenimals; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L92">IsFake</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L93">ValidFromIndexNowLastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L94">IsFrozen</a></b>  <i>bool</i>
<p> we shouldn't update this doc (see JUPITER-1809) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L95">DelayedLastAccess</a></b>  <i>uint64</i>
<p> contains LastAccess for delayed doc contour deduplication </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L96">HasTriggerWords</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L100">Erf</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L3">SDocErf2InfoProto</a></i>
</li>
<details open><summary><b>Message SDocErf2InfoProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L4">YabarUrlLcAc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L5">HasLerf</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L6">nNews</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L7">nShop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L8">nCatalog</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L9">nLongPureText</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L10">nRoot</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L11">IsShop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L12">HasPayments</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L13">TitleComm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L14">Language</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L15">AddTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L16">DocDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L17">IsBlog</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L18">MtimeAccuracy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L19">IsNotMobileBeauty</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L20">YabarUrlDownloads</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L21">Hops</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L22">TextFeatures</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L23">AutoAssessorStaticRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L24">TextLike</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L25">SegmentAuxAlphasInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L26">SegmentAuxSpacesInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L27">SegmentContentCommasInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L28">WikiLinkCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L29">YabarUrlCRCs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L30">MetrikaUrlHostVisitTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L31">DocLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L32">UrlLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L33">MetrikaUrlHostVisitDepth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L34">IsRunet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L35">IsPorno</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L36">IsComm</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L37">IsFake</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L38">IsSEO</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L39">IsCommEshop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L40">IsUnreachable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L41">Eshop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L42">IsForum</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L43">TrashAdv</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L44">UrlNGramsModel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L45">TitleBM25Ex</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L46">Adultness</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L47">PornoValue</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L48">PessimizeLevel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L50">AdultnessProd</a></b>  <i>uint32</i>
<p> 46 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L51">AdultnessBeta</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L52">Unused4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L53">MetrikaUrlVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L54">MetrikaUrlAvgTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L55">MetrikaUrlCoreAudience</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L56">MetrikaUrlVisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L57">YabarUrlVisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L58">YabarUrlVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L59">YabarUrlAvgTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L60">AuraDocLogOrigin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L61">AuraDocMeanFltAuthorSource</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L62">UrlQueryVariety</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L63">BrowserBookmarks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L64">IsPopunder</a></b>  <i>bool</i>
<p> Deprecated </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L65">IsCommByKeywords</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L66">ManualAdultness</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L67">DocDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L68">IsPornoAdvert</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L69">DocDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L70">ThinPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L71">DaterFrom1</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L72">Poetry</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L73">PoetryQuad</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L74">DocSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L75">HopsFixed</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L76">VideoRating</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L77">IsClickunder</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L78">HasBigPicture</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L79">UrlHasDigits</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L80">DaterYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L81">DaterFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L82">DaterMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L83">DaterDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L84">WatchVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L85">DownloadVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L86">IsHostAdultnessZero</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L87">SynS1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L88">SynFLremap1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L89">SynFLremap2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L90">SessNormDurRate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L91">SynPercentBadWordPairs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L92">SynNumBadWordPairs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L93">DocStaticSignature1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L94">DocStaticSignature2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L95">LastAccess</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L96">NumLatinLetters</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L97">WordsInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L98">WordsInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L99">MeanWordLength</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L100">PercentWordsInLinks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L101">PercentVisibleContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L102">PercentFreqWords</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L103">PercentUsedFreqWords</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L104">Timestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L105">GeoCountryFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L106">TrigramsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L107">TrigramsCondProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L108">NumeralsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L109">ParticlesPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L110">AdjPronounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L111">AdvPronounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L112">VerbsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L113">FemAndMasNounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L114">HttpModTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L115">AddTimeFull</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L116">UrlHash1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L117">UrlHash2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L118">LongestText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L119">TimestampFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L120">HasStructuredData</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L121">MinorLanguagesBoost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L122">HasLiRuCNT</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L123">PeriodicDatesPercent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L124">UrlLen2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L125">GeoCityFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L126">DomainId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L127">HostId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L128">UrlTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L129">NumNonLettersInUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L130">DaterStatsPrevYearsInTitleContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L131">ReservedLanguageRegion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L132">IsTranslatedDocument</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L133">DaterStatsMaxYearInContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L134">Wap</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L135">DaterStatsMinYearInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L136">NumSlashes</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L137">DaterStatsMaxYearInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L138">IsLJ</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L139">IsHTML</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L140">AuraDocLogShared</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L141">AuraDocLogAuthor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L142">AuraDocMeanSharedWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L143">Soft404</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L144">GskUrlModel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L145">MtimeFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L146">ReservedUrlWasOnSearch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L147">IsMainPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L148">IsHub</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L149">IsUkr</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L150">IsObsolete</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L151">Mtime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L152">FNormalTextIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L153">TotalScore</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L154">NumLink</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L155">NewScore</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L156">NumNonRussianLink</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L157">TitleInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L158">HasLinkQuality</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L159">LangDispersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L160">NumLinksFromMP</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L161">GeoDispersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L162">LinksAlive</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L163">UrlLinkPercent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L164">TitleLRBM25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L165">LinksInTitleTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L166">SOMaxSumSourceRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L167">PageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L168">UkrainPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L169">DocTLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L170">TitleLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L171">HeadingLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L172">NormalTextLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L173">DocIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L174">FDocTfIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L175">FTitleIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L176">FHeadingIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L177">ForeignDMOZPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L178">ForeignTRPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L179">AlmostPeriod</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L180">DifferentInternalLinks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L181">DaterStatsFullDatesInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L182">DaterStatsUniqYearsInContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L183">NastyContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L184">IsDictionary</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L185">IsReview</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L186">AntispamBanDoc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L187">FooterInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L188">LinksInFooterTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L189">HasUserReviewL</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L190">HasUserReviewH</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L191">NoUserReview</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L192">IsMainMirrorUrl</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L193">IsIndexPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L194">IsIndexPageSoft</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L195">HasDownloadLinkOnFile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L196">HasDownloadLinkOnFileHosting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L197">MinSemiDuplicatesPathLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L198">FirstPostDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L199">FirstPostDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L200">FirstPostDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L201">LastPostDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L202">LastPostDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L203">LastPostDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L204">NumForumPosts</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L205">NumForumAuthors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L206">TotalDups</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L207">IsEbookForRead</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L208">HasHtml5VideoPlayer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L209">Soft404Antispam</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L210">IsRTA</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L211">UniqueSEOTrash0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L212">YellowAdv</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L213">BoostMarketDoc</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L214">IsReferat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L215">HasVacancy</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L216">EmptyVacancy</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L217">SmartSoft404</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L218">IsChildish</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L219">DirtyLang</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L220">IsNarco</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L221">IsSuicide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L222">RssLinkDate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L223">LanguageDistribution</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L224">AuraDocRelAuthor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L225">AuraDocRelOrigin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L226">IsFakeForRedirect</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L227">IsFakeForBan</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L228">KidSessionLevel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L229">HasTurLinks</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L230">EnoughRusLinks</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L231">Html5Video</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L232">ReservedAura</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L233">SearchRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L234">AntispamFlags</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L235">ClickedWithAnotherSEClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L236">ShowsWithAnotherSEClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L237">CommRus</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L238">NastyURL</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L239">NastyImage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L240">IsRepost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L241">TestAntiSpamFeatures</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L242">EmbedVideoBroken</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L243">WikiInfoboxLink</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L244">UrlHasVisits</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L245">DaterStatsAverageSourceSegment</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L246">DaterStatsYearNormLikelihood</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L247">DocCreateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L248">DocUpdateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L249">SegmentWordPortionFromMainContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L250">HasMultimedia</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L251">NoDirectBroadmatch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L252">UrlInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L253">LinksInUrlTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L254">YabarUrlUserBack</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L255">YabarUrlFirstOnHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L256">YabarUrlRevisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L257">MaxGcFrcRegionRatio</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L258">MaxGcFrcRegionWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L259">NastyImageValue</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L260">IsFakeKiwi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L261">MaxGcFrcRegion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L262">MaxFreq</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L263">TrashAdvForCleanSearch</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L264">IsNotCgi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L265">IsPagination</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L266">PageHasMapsApi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L267">IsMobileBeauty</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L268">RegionFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L269">RegionFromUrlProbability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L270">TitleFirstBreak</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L271">TitleLastBreak</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L272">HtmlLz4Size</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L273">HtmlEntropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L274">HtmlLz4Entropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L275">TextCompressionRatio</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L276">HtmlSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L277">TextSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L278">HorizontalOversize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L279">TextOverflow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L280">FontLessThan12PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L281">FontLessThan14PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L282">FontLessThan20PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L283">SmallestControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L284">LargestControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L285">AvgControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L286">TextDensityNormalized</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L287">MatrixNetModelValueNormalized</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L288">ImageOverflow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L289">HasViewPort</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L290">HasFlash</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L291">HasApplet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L292">HasSilverlight</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L293">SumFlashArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L294">USLongPeriodCtr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L295">USLongPeriodDt3600Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L296">USLongPeriodDt180Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L297">USLongPeriodLongClickProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L298">USLongPeriodShows</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L299">USLongPeriodWinsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L300">USLongPeriodLossesProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L301">NastyVideo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L302">MobileTrashAdv</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L303">Artroz</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L304">ArtrozRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L305">USLongPeriodMobileDt180Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L306">USLongPeriodMobileLongClickProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L307">USLongPeriodMobileLossesProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L308">AdultnessUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L309">UBLongPeriodVisitsSNProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L310">UBLongPeriodDirectHChildren90CntFromExtHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L311">UBLongPeriodDepthFromExtHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L312">UBLongPeriodBrowseFrc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L313">UBLongPeriodAvgSearchDuration600</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L314">UBLongPeriodSearchPercentEnd</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L315">UBLongPeriodSearchPercentMiddle30</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L316">UBLongPeriodVisit120Prob</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L317">UBLongPeriodLeavesCnt</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L318">UBLongPeriodDtUrlHChildrenCut600</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L319">UBLongPeriodMinTimeWhenPageShow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L320">UBLongPeriodDeltaAvgMinTimeWhenPageShow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L321">UBLongPeriodLatitude</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L322">UBLongPeriodLongitude</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L323">UBLongPeriodDownloadsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L324">UBLongPeriodDownloadsImageProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L325">UBLongPeriodDownloadsTorrentProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L331">PornoUrlFix</a></b>  <i>uint32</i>
<p> 337 deprecated.  338 deprecated.  339 deprecated.  340 deprecated.  341 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L332">AntispamTestUrl1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L333">AntispamTestUrl2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L334">AntispamTestUrl3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L335">RobotBan1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L336">RobotBan2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L337">HasVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L338">HasTurbo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L339">NotFresh</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L340">RobotDateTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L341">RobotDateScore</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L342">RobotAddTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L343">ZenFeaturesClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L344">ZenFeaturesShows</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L345">ItdItpHasImage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L346">MemorandumUrlType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L347">RandomLogHostTopClickedUrlsIsMobileRequestLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L348">RandomLogHostTopClickedUrlsNanobtaniumQueryWordTitle5nDist2maxXMaxIsMobileRequestLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L349">HasTurboDesktop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L350">HasTurboMobile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L351">SRTimestamp</a></b>  <i>uint32</i>
<p> SelectionRank timestamp </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L352">IsFreshVital</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L353">SelectionRankRuleNew</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L354">SelectionRankRuleNewPosition</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L355">SelectionRankRuleUpdate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L356">SelectionRankRuleUpdatePosition</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L357">FirstKnownValidTs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L358">HasTurboApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L359">RcSpylogCountersVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L360">RcSpylogCountersTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L361">RcSpylogCounter0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L362">RcSpylogCounter1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L363">RcSpylogCounter2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L364">RcSpylogCounter3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L365">RcSpylogCounter4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L366">RcSpylogCounter5</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L367">RcSpylogCounter6</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L368">RcSpylogCounter7</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L370">ShopInShopUrl</a></b>  <i>bool</i>
<p> 380 is deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L372">UrlIsMarketOffer</a></b>  <i>bool</i>
<p> 382 is deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L373">RcSearchCountersVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L374">RcSearchCounter0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L375">RcSearchCounter1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L376">RcSearchCounter2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L377">RcSearchCounter3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L378">RcSearchCounter4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L379">RcSearchCounter5</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L380">RcSearchCounter6</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L381">RcSearchCounter7</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L382">RcSearchCounter8</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L383">RcSearchCounter9</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L384">RcSearchCounter10</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L385">IsFeedOffer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L386">IsFeedListing</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L387">IsFeedMain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L388">IsFeedStratocaster</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L389">IsFeedAny</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L390">BlenderNewsJudgement</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L391">NoProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L392">OneProductProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L393">ManyProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L394">ProductOfferAvailability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L395">ProductOfferPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L396">ProductOfferCurrency</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L397">ProductOfferNumberOfProducts</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L398">ProductOfferMinPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L399">ProductOfferMaxPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L400">ProductOfferAnyAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L401">ProductOfferPreAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L402">ProductOfferNotAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L403">NavParasites</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L404">SosDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L405">MedDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L406">FinLawDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L407">CrueltyDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L408">OfferAvailabilityIsSetUp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L409">OfferAvailability</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L410">ReservedFreeForAll71</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L411">MedDssmWithTrash</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L412">FinLawDssmWithTrash</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L413">UBLongPeriodRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L414">HasTurboEcom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L415">DssmPageQualityRTHub</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L416">DssmPageQualityRTHubSlot2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L417">HasCloaking</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L418">SocialUrlIsVerified</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L419">UrlToQueryShows</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L420">DssmLanguageClassifierRusL2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L421">DssmLanguageClassifierEngL2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L422">DssmLanguageClassifierOthL2</a></b>  <i>float</i>
<p> next tag is 438 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L101">Bert</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L99">TExportableDocResult</a></i>
</li>
<details open><summary><b>Message TExportableDocResult</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L100">ExportIdentifier</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L101">DataParts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L66">TDataPart</a></i>
</li>
<details open><summary><b>Message TDataPart</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L67">DocumentDataLayerName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L68">DataTag</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L3">EDocumentResultTag</a></i>
</li>
<details open><summary><b>Enum EDocumentResultTag</b></summary>
<ul>
<li><span style="color:#1D7373">LayerNamedTag</span></li>
<li><span style="color:#1D7373">DocumentEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingInputMaskEmbed</span></li>
<li><span style="color:#1D7373">QueryEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingInputMaskEmbed</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed1</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed2</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed3</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed4</span></li>
<li><span style="color:#1D7373">RelevEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingInputMaskEmbed</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L69">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L30">EResultCompressionType</a></i>
</li>
<details open><summary><b>Enum EResultCompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">EmbedCompression_NonCompressed</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToOneByteWithMaxCoordRenorm</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToHalfByteWithMaxCoordRenorm</span></li>
<li><span style="color:#1D7373">EmbedCompression_SizeBitMaskAsInts</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToSixBitsWithMaxCoordRenormAsFp16</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L71">NonCompressedEmbed</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L72">FloatToOneByteCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L73">FloatToOneByteCompressionScale</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L74">FloatToOneByteCompressionBias</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L76">SizeBitMaskAsIntCompressedLenSum</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L77">SizeBitMaskAsIntCompressedLenOnesPrefix</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L79">FloatToHalfByteCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L80">FloatToHalfByteCompressionScale</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L81">FloatToHalfByteCompressionBias</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L82">FloatToHalfByteIsOddLength</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L84">FloatToSixBitsCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L85">FloatToSixBitsCompressionRenormAsFp16</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L86">FloatToSixBitsCompressionInputSize</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L102">Predicts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L89">TPredictData</a></i>
</li>
<details open><summary><b>Message TPredictData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L90">PredictName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L91">Value</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L103">NotModelIdUsedAsIdentifier</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L104">TextData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L94">TTextData</a></i>
</li>
<details open><summary><b>Message TTextData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L95">TextName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L96">TextValue</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L103">GeminiUrl</a></b>  <i>string</i>
<p> normalized by Gemini href </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L104">IsGeminiUrlBad</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L105">GeminiUrlUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L106">MarketOfferContent</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L332">MarketOfferContent</a></i>
</li>
<details open><summary><b>Message MarketOfferContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L334">category_id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L335">category_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L337">vendor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L338">vendor_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L340">model_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L341">model_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L343">market_sku_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L344">market_sku_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L346">title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L348">params</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L18">MarketParameterValue</a></i>
</li>
<details open><summary><b>Message MarketParameterValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L20">value_source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L71">MarketValueSource</a></i>
<p> Откуда текущее значение, его качество </p>

</li>
<details open><summary><b>Enum MarketValueSource</b></summary>
<p> mbo-шный ModificationSource на первый взгляд кажется слишком большим </p>

<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_SOURCE</span></li>
<li><span style="color:#1D7373">PARTNER</span></li>
<li><span style="color:#1D7373">FORMALIZATION</span></li>
<li><span style="color:#1D7373">RULE</span></li>
<li><span style="color:#1D7373">PARTNER_CONTENT_MAPPING</span></li>
<li><span style="color:#1D7373">CONTENT_EXCEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L21">value_state</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L61">MarketValueState</a></i>
<p> Тип значения, по сути это - своего рода команда для диффа </p>

</li>
<details open><summary><b>Enum MarketValueState</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_STATE</span></li>
<li><span style="color:#1D7373">DEFAULT</span></li>
<li><span style="color:#1D7373">REMOVE</span></li>
<li><span style="color:#1D7373">FORCE_ADD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L23">param_id</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L28">param_name</a></b>  <i>string</i>
<p> Есть желание дублировать название параметра, которое вводил партнёр тут.  Если param_id невалиден в заданной категории, то по этому полю можно понять, про что было значение.  Если param_id есть и валиден то это поле не используется в обработке. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L30">value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L33">MarketValue</a></i>
</li>
<details open><summary><b>Message MarketValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L35">value_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L51">MarketValueType</a></i>
<p> Тип значения параметра копируется из param-а при создании + для enum/numeric_enum может быть тип HYPOTHESIS </p>

</li>
<details open><summary><b>Enum MarketValueType</b></summary>
<p> На данный момент отличается от MboParameters.ValueType в части HYPOTHESIS </p>

<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_TYPE</span></li>
<li><span style="color:#1D7373">BOOLEAN</span></li>
<li><span style="color:#1D7373">ENUM</span></li>
<li><span style="color:#1D7373">NUMERIC</span></li>
<li><span style="color:#1D7373">NUMERIC_ENUM</span></li>
<li><span style="color:#1D7373">STRING</span></li>
<li><span style="color:#1D7373">HYPOTHESIS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L38">bool_value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L39">numeric_value</a></b>  <i>string</i>
<p> Строка с числом, ^d+(.d+)?$ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L40">option_id</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L47">str_value</a></b>  <i>string</i>
<p> То, что ввёл пользователь:  - если есть option_id - мы просто копируем сюда значение - также, как и param_id это поможет при изменении/эволюции категории  - гипотеза = value_type == HYPOTHESIS + str_value, NUMERIC_ENUM - считаем так же  - если STRING - то значение строки </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L350">market_b2c_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L351">market_sku_type</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L353">source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L326">EMarketOfferContentMappingSource</a></i>
</li>
<details open><summary><b>Enum EMarketOfferContentMappingSource</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_MAPPING_SOURCE</span></li>
<li><span style="color:#1D7373">ULTRACONTROLLER</span></li>
<li><span style="color:#1D7373">SMARTMATCHER</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L107">EcomFeatures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L51">TEcomFeatures</a></i>
</li>
<details open><summary><b>Message TEcomFeatures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L52">OneProductProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L53">ManyProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L54">NoProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L55">Version</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L56">IsOneProductRegexChosen</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L108">LandingHttpCode</a></b>  <i>uint64</i>
<p> max 19 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L355">LegacyUrl</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L82">TUrl</a></i>
</li>
<details open><summary><b>Message TUrl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L83">SpyLogTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L84">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L85">LandingTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L86">LandingUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L87">FeedSendTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L88">LandingUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L90">IsHrefChanged</a></b>  <i>bool</i>
<p> true, if url has been changed, after finding info about new url in NormalizedUrls this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L94">AppearanceUrlWithoutTitleTime</a></b>  <i>uint64</i>
<p> first time of appearance url without any info  if url has LandingUrl, this field will be not filled  when href сhanges, this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L97">LandingTitleDownloadTime</a></b>  <i>uint64</i>
<p> time of the first appearance of any info about url  when href changes, this field will be cleared </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L99">Urldat</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L5">TUrldat</a></i>
<p> robot factors </p>

</li>
<details open><summary><b>Message TUrldat</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L6">Host</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L7">Path</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L8">LastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L9">ExportTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L10">TextCRC</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L12">HttpModTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L13">HttpCode</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L14">MimeType</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L15">Language</a></b>  <i>uint32</i>
<p> Again type should be same as in Gemini </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L16">Encoding</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L17">LangRegion</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L18">HasContent</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L19">HostIsNotAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L20">HostIsBannedByRobotTxt</a></b>  <i>bool</i>
<p> Disallow /. Applied with delay. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L21">HostIsUncrawlable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L22">HostIsSmuggling</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L23">UrlIsBannedByRobotTxt</a></b>  <i>bool</i>
<p> Applied with delay. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L24">IsContentExport</a></b>  <i>bool</i>
<p> Not propagated to new states </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L25">HostIsMultiLang</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L26">IP</a></b>  <i>uint32</i>
<p> Not used. TODO: can be removed? </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L27">SimpleSimhash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L28">Simhash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L29">TitleHash</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L30">SimhashDocLength</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L31">SimhashData</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L32">RelCanonicalTarget</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L33">IsRedirect</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L34">RedirTarget</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L35">IsMetaRefreshTargetRedir</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L39">CanonizedRedirTarget</a></b>  <i>string</i>
<p> Canonized version of RedirTarget. Canonized by robots.txt and RFL. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L41">SourceId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L42">SourceName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L43">IsBannedByRfl</a></b>  <i>bool</i>
<p> Result of RflCanonized->CheckFiltered </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L45">CanonizedPath</a></b>  <i>string</i>
<p> Path canonized by robots.txt and RFL. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L47">DelayedUrlPenalty</a></b>  <i>uint64</i>
<p> Number of bases url has been delayed for. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L48">FetchTime</a></b>  <i>uint32</i>
<p> Time it took spider to fetch document. In microseconds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L50">LemurAddTime</a></b>  <i>uint32</i>
<p> Time when document was discovered by Lemur/Samovar. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L51">FreshTimestampFrom</a></b>  <i>uint32</i>
<p> Source of url discovery </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L52">FreshTimestamp</a></b>  <i>uint32</i>
<p></p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L55">OriginalHost</a></b>  <i>string</i>
<p> Intermediate fields. Used in floodgate when inverting redirects. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L56">OriginalPath</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L57">RedirTargetIsBannedByRobots</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L60">ZoraCtxFlags</a></b>  <i>uint64</i>
<p> Saved flags from Zora context </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L62">IsAlisaBusinessChat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L63">IsAlisaLanding</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L64">BasesAge</a></b>  <i>uint64</i>
<p> TODO(alexromanov): remove BasesAge </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L66">SamovarConsumers</a></b>  <i>bytes</i>
<p> serialized TSamovarConsumerVector </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L68">IsProcessedByRotor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L69">WasIntendedForRotor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L70">IsRotorCorrupted</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L76">ReachableFromMordaSince</a></b>  <i>uint32</i>
<p> ReachableFromMordaSince means "document is reachable from morda since value base-state" (see JUPITER-942)   * null - document never was reachable from morda;   * 0 - document was known before ReachableFromMordaSince was added and has no update since there;   * timestamp = document is reachable from morda since base with state $timestamp. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L77">IsRandomCrawl</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L78">UrlTransliterationData</a></b>  <i>bytes</i>
<p> serialized TUrlTransliterationData </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L79">ZoraCtx</a></b>  <i>bytes</i>
<p> serialized TUkropZoraContext </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L80">FromSitemap</a></b>  <i>bool</i>
<p> url was in sitemap somewhen </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L81">LastWatchLogCounterId</a></b>  <i>uint64</i>
<p> last counter id used for validity </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L82">WasManualCrawl</a></b>  <i>bool</i>
<p> indexed by forced, addurl or sitemap somewhen </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L83">FirstKnownValidTs</a></b>  <i>uint32</i>
<p> time of valid detection </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L84">JupiterAddTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L85">IsTranslatedDocument</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L86">IsRemoved</a></b>  <i>bool</i>
<p> used to merge RT Jupiter delta with remerge </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L87">SpiderTimestampUs</a></b>  <i>uint64</i>
<p> used to distinct rows with the same LastAccess </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L88">DelayedAddTime</a></b>  <i>uint64</i>
<p> set in delayed doc contour TODO(alexromanov): delete in June 2022 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L89">IsMock</a></b>  <i>bool</i>
<p> page was obtained using mock pages parser </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L90">ValidFromMetrikaLastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L91">IsHitrenimals</a></b>  <i>bool</i>
<p> page was downloaded via hitrenimals; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L92">IsFake</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L93">ValidFromIndexNowLastAccess</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L94">IsFrozen</a></b>  <i>bool</i>
<p> we shouldn't update this doc (see JUPITER-1809) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L95">DelayedLastAccess</a></b>  <i>uint64</i>
<p> contains LastAccess for delayed doc contour deduplication </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/urldat.proto?rev=r9795881#L96">HasTriggerWords</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L100">Erf</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L3">SDocErf2InfoProto</a></i>
</li>
<details open><summary><b>Message SDocErf2InfoProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L4">YabarUrlLcAc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L5">HasLerf</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L6">nNews</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L7">nShop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L8">nCatalog</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L9">nLongPureText</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L10">nRoot</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L11">IsShop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L12">HasPayments</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L13">TitleComm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L14">Language</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L15">AddTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L16">DocDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L17">IsBlog</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L18">MtimeAccuracy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L19">IsNotMobileBeauty</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L20">YabarUrlDownloads</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L21">Hops</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L22">TextFeatures</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L23">AutoAssessorStaticRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L24">TextLike</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L25">SegmentAuxAlphasInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L26">SegmentAuxSpacesInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L27">SegmentContentCommasInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L28">WikiLinkCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L29">YabarUrlCRCs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L30">MetrikaUrlHostVisitTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L31">DocLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L32">UrlLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L33">MetrikaUrlHostVisitDepth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L34">IsRunet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L35">IsPorno</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L36">IsComm</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L37">IsFake</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L38">IsSEO</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L39">IsCommEshop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L40">IsUnreachable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L41">Eshop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L42">IsForum</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L43">TrashAdv</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L44">UrlNGramsModel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L45">TitleBM25Ex</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L46">Adultness</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L47">PornoValue</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L48">PessimizeLevel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L50">AdultnessProd</a></b>  <i>uint32</i>
<p> 46 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L51">AdultnessBeta</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L52">Unused4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L53">MetrikaUrlVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L54">MetrikaUrlAvgTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L55">MetrikaUrlCoreAudience</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L56">MetrikaUrlVisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L57">YabarUrlVisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L58">YabarUrlVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L59">YabarUrlAvgTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L60">AuraDocLogOrigin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L61">AuraDocMeanFltAuthorSource</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L62">UrlQueryVariety</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L63">BrowserBookmarks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L64">IsPopunder</a></b>  <i>bool</i>
<p> Deprecated </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L65">IsCommByKeywords</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L66">ManualAdultness</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L67">DocDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L68">IsPornoAdvert</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L69">DocDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L70">ThinPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L71">DaterFrom1</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L72">Poetry</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L73">PoetryQuad</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L74">DocSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L75">HopsFixed</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L76">VideoRating</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L77">IsClickunder</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L78">HasBigPicture</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L79">UrlHasDigits</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L80">DaterYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L81">DaterFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L82">DaterMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L83">DaterDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L84">WatchVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L85">DownloadVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L86">IsHostAdultnessZero</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L87">SynS1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L88">SynFLremap1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L89">SynFLremap2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L90">SessNormDurRate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L91">SynPercentBadWordPairs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L92">SynNumBadWordPairs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L93">DocStaticSignature1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L94">DocStaticSignature2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L95">LastAccess</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L96">NumLatinLetters</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L97">WordsInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L98">WordsInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L99">MeanWordLength</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L100">PercentWordsInLinks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L101">PercentVisibleContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L102">PercentFreqWords</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L103">PercentUsedFreqWords</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L104">Timestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L105">GeoCountryFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L106">TrigramsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L107">TrigramsCondProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L108">NumeralsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L109">ParticlesPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L110">AdjPronounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L111">AdvPronounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L112">VerbsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L113">FemAndMasNounsPortion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L114">HttpModTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L115">AddTimeFull</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L116">UrlHash1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L117">UrlHash2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L118">LongestText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L119">TimestampFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L120">HasStructuredData</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L121">MinorLanguagesBoost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L122">HasLiRuCNT</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L123">PeriodicDatesPercent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L124">UrlLen2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L125">GeoCityFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L126">DomainId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L127">HostId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L128">UrlTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L129">NumNonLettersInUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L130">DaterStatsPrevYearsInTitleContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L131">ReservedLanguageRegion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L132">IsTranslatedDocument</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L133">DaterStatsMaxYearInContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L134">Wap</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L135">DaterStatsMinYearInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L136">NumSlashes</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L137">DaterStatsMaxYearInTitle</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L138">IsLJ</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L139">IsHTML</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L140">AuraDocLogShared</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L141">AuraDocLogAuthor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L142">AuraDocMeanSharedWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L143">Soft404</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L144">GskUrlModel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L145">MtimeFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L146">ReservedUrlWasOnSearch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L147">IsMainPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L148">IsHub</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L149">IsUkr</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L150">IsObsolete</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L151">Mtime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L152">FNormalTextIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L153">TotalScore</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L154">NumLink</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L155">NewScore</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L156">NumNonRussianLink</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L157">TitleInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L158">HasLinkQuality</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L159">LangDispersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L160">NumLinksFromMP</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L161">GeoDispersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L162">LinksAlive</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L163">UrlLinkPercent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L164">TitleLRBM25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L165">LinksInTitleTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L166">SOMaxSumSourceRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L167">PageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L168">UkrainPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L169">DocTLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L170">TitleLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L171">HeadingLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L172">NormalTextLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L173">DocIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L174">FDocTfIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L175">FTitleIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L176">FHeadingIdfSum</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L177">ForeignDMOZPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L178">ForeignTRPageRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L179">AlmostPeriod</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L180">DifferentInternalLinks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L181">DaterStatsFullDatesInText</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L182">DaterStatsUniqYearsInContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L183">NastyContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L184">IsDictionary</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L185">IsReview</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L186">AntispamBanDoc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L187">FooterInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L188">LinksInFooterTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L189">HasUserReviewL</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L190">HasUserReviewH</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L191">NoUserReview</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L192">IsMainMirrorUrl</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L193">IsIndexPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L194">IsIndexPageSoft</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L195">HasDownloadLinkOnFile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L196">HasDownloadLinkOnFileHosting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L197">MinSemiDuplicatesPathLen</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L198">FirstPostDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L199">FirstPostDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L200">FirstPostDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L201">LastPostDateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L202">LastPostDateDay</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L203">LastPostDateYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L204">NumForumPosts</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L205">NumForumAuthors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L206">TotalDups</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L207">IsEbookForRead</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L208">HasHtml5VideoPlayer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L209">Soft404Antispam</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L210">IsRTA</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L211">UniqueSEOTrash0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L212">YellowAdv</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L213">BoostMarketDoc</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L214">IsReferat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L215">HasVacancy</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L216">EmptyVacancy</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L217">SmartSoft404</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L218">IsChildish</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L219">DirtyLang</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L220">IsNarco</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L221">IsSuicide</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L222">RssLinkDate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L223">LanguageDistribution</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L224">AuraDocRelAuthor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L225">AuraDocRelOrigin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L226">IsFakeForRedirect</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L227">IsFakeForBan</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L228">KidSessionLevel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L229">HasTurLinks</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L230">EnoughRusLinks</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L231">Html5Video</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L232">ReservedAura</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L233">SearchRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L234">AntispamFlags</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L235">ClickedWithAnotherSEClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L236">ShowsWithAnotherSEClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L237">CommRus</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L238">NastyURL</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L239">NastyImage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L240">IsRepost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L241">TestAntiSpamFeatures</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L242">EmbedVideoBroken</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L243">WikiInfoboxLink</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L244">UrlHasVisits</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L245">DaterStatsAverageSourceSegment</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L246">DaterStatsYearNormLikelihood</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L247">DocCreateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L248">DocUpdateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L249">SegmentWordPortionFromMainContent</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L250">HasMultimedia</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L251">NoDirectBroadmatch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L252">UrlInLinksTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L253">LinksInUrlTrigrams</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L254">YabarUrlUserBack</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L255">YabarUrlFirstOnHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L256">YabarUrlRevisits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L257">MaxGcFrcRegionRatio</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L258">MaxGcFrcRegionWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L259">NastyImageValue</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L260">IsFakeKiwi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L261">MaxGcFrcRegion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L262">MaxFreq</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L263">TrashAdvForCleanSearch</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L264">IsNotCgi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L265">IsPagination</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L266">PageHasMapsApi</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L267">IsMobileBeauty</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L268">RegionFromUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L269">RegionFromUrlProbability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L270">TitleFirstBreak</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L271">TitleLastBreak</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L272">HtmlLz4Size</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L273">HtmlEntropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L274">HtmlLz4Entropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L275">TextCompressionRatio</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L276">HtmlSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L277">TextSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L278">HorizontalOversize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L279">TextOverflow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L280">FontLessThan12PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L281">FontLessThan14PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L282">FontLessThan20PxFraction</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L283">SmallestControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L284">LargestControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L285">AvgControlArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L286">TextDensityNormalized</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L287">MatrixNetModelValueNormalized</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L288">ImageOverflow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L289">HasViewPort</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L290">HasFlash</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L291">HasApplet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L292">HasSilverlight</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L293">SumFlashArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L294">USLongPeriodCtr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L295">USLongPeriodDt3600Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L296">USLongPeriodDt180Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L297">USLongPeriodLongClickProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L298">USLongPeriodShows</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L299">USLongPeriodWinsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L300">USLongPeriodLossesProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L301">NastyVideo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L302">MobileTrashAdv</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L303">Artroz</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L304">ArtrozRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L305">USLongPeriodMobileDt180Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L306">USLongPeriodMobileLongClickProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L307">USLongPeriodMobileLossesProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L308">AdultnessUrl</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L309">UBLongPeriodVisitsSNProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L310">UBLongPeriodDirectHChildren90CntFromExtHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L311">UBLongPeriodDepthFromExtHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L312">UBLongPeriodBrowseFrc</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L313">UBLongPeriodAvgSearchDuration600</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L314">UBLongPeriodSearchPercentEnd</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L315">UBLongPeriodSearchPercentMiddle30</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L316">UBLongPeriodVisit120Prob</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L317">UBLongPeriodLeavesCnt</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L318">UBLongPeriodDtUrlHChildrenCut600</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L319">UBLongPeriodMinTimeWhenPageShow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L320">UBLongPeriodDeltaAvgMinTimeWhenPageShow</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L321">UBLongPeriodLatitude</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L322">UBLongPeriodLongitude</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L323">UBLongPeriodDownloadsProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L324">UBLongPeriodDownloadsImageProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L325">UBLongPeriodDownloadsTorrentProb</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L331">PornoUrlFix</a></b>  <i>uint32</i>
<p> 337 deprecated.  338 deprecated.  339 deprecated.  340 deprecated.  341 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L332">AntispamTestUrl1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L333">AntispamTestUrl2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L334">AntispamTestUrl3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L335">RobotBan1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L336">RobotBan2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L337">HasVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L338">HasTurbo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L339">NotFresh</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L340">RobotDateTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L341">RobotDateScore</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L342">RobotAddTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L343">ZenFeaturesClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L344">ZenFeaturesShows</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L345">ItdItpHasImage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L346">MemorandumUrlType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L347">RandomLogHostTopClickedUrlsIsMobileRequestLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L348">RandomLogHostTopClickedUrlsNanobtaniumQueryWordTitle5nDist2maxXMaxIsMobileRequestLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L349">HasTurboDesktop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L350">HasTurboMobile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L351">SRTimestamp</a></b>  <i>uint32</i>
<p> SelectionRank timestamp </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L352">IsFreshVital</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L353">SelectionRankRuleNew</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L354">SelectionRankRuleNewPosition</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L355">SelectionRankRuleUpdate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L356">SelectionRankRuleUpdatePosition</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L357">FirstKnownValidTs</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L358">HasTurboApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L359">RcSpylogCountersVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L360">RcSpylogCountersTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L361">RcSpylogCounter0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L362">RcSpylogCounter1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L363">RcSpylogCounter2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L364">RcSpylogCounter3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L365">RcSpylogCounter4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L366">RcSpylogCounter5</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L367">RcSpylogCounter6</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L368">RcSpylogCounter7</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L370">ShopInShopUrl</a></b>  <i>bool</i>
<p> 380 is deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L372">UrlIsMarketOffer</a></b>  <i>bool</i>
<p> 382 is deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L373">RcSearchCountersVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L374">RcSearchCounter0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L375">RcSearchCounter1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L376">RcSearchCounter2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L377">RcSearchCounter3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L378">RcSearchCounter4</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L379">RcSearchCounter5</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L380">RcSearchCounter6</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L381">RcSearchCounter7</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L382">RcSearchCounter8</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L383">RcSearchCounter9</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L384">RcSearchCounter10</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L385">IsFeedOffer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L386">IsFeedListing</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L387">IsFeedMain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L388">IsFeedStratocaster</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L389">IsFeedAny</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L390">BlenderNewsJudgement</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L391">NoProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L392">OneProductProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L393">ManyProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L394">ProductOfferAvailability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L395">ProductOfferPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L396">ProductOfferCurrency</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L397">ProductOfferNumberOfProducts</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L398">ProductOfferMinPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L399">ProductOfferMaxPrice</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L400">ProductOfferAnyAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L401">ProductOfferPreAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L402">ProductOfferNotAvailable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L403">NavParasites</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L404">SosDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L405">MedDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L406">FinLawDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L407">CrueltyDssm</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L408">OfferAvailabilityIsSetUp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L409">OfferAvailability</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L410">ReservedFreeForAll71</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L411">MedDssmWithTrash</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L412">FinLawDssmWithTrash</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L413">UBLongPeriodRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L414">HasTurboEcom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L415">DssmPageQualityRTHub</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L416">DssmPageQualityRTHubSlot2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L417">HasCloaking</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L418">SocialUrlIsVerified</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L419">UrlToQueryShows</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L420">DssmLanguageClassifierRusL2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L421">DssmLanguageClassifierEngL2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L422">DssmLanguageClassifierOthL2</a></b>  <i>float</i>
<p> next tag is 438 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L101">Bert</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L99">TExportableDocResult</a></i>
</li>
<details open><summary><b>Message TExportableDocResult</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L100">ExportIdentifier</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L101">DataParts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L66">TDataPart</a></i>
</li>
<details open><summary><b>Message TDataPart</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L67">DocumentDataLayerName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L68">DataTag</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L3">EDocumentResultTag</a></i>
</li>
<details open><summary><b>Enum EDocumentResultTag</b></summary>
<ul>
<li><span style="color:#1D7373">LayerNamedTag</span></li>
<li><span style="color:#1D7373">DocumentEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">DocumentPaddingInputMaskEmbed</span></li>
<li><span style="color:#1D7373">QueryEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">QueryPaddingInputMaskEmbed</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed1</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed2</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed3</span></li>
<li><span style="color:#1D7373">MultitargetQueryEmbed4</span></li>
<li><span style="color:#1D7373">RelevEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingInputIdsEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingSegmentIdsEmbed</span></li>
<li><span style="color:#1D7373">RelevPaddingInputMaskEmbed</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L69">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L30">EResultCompressionType</a></i>
</li>
<details open><summary><b>Enum EResultCompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">EmbedCompression_NonCompressed</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToOneByteWithMaxCoordRenorm</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToHalfByteWithMaxCoordRenorm</span></li>
<li><span style="color:#1D7373">EmbedCompression_SizeBitMaskAsInts</span></li>
<li><span style="color:#1D7373">EmbedCompression_ToSixBitsWithMaxCoordRenormAsFp16</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L71">NonCompressedEmbed</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L72">FloatToOneByteCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L73">FloatToOneByteCompressionScale</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L74">FloatToOneByteCompressionBias</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L76">SizeBitMaskAsIntCompressedLenSum</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L77">SizeBitMaskAsIntCompressedLenOnesPrefix</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L79">FloatToHalfByteCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L80">FloatToHalfByteCompressionScale</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L81">FloatToHalfByteCompressionBias</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L82">FloatToHalfByteIsOddLength</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L84">FloatToSixBitsCompressionResult</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L85">FloatToSixBitsCompressionRenormAsFp16</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L86">FloatToSixBitsCompressionInputSize</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L102">Predicts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L89">TPredictData</a></i>
</li>
<details open><summary><b>Message TPredictData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L90">PredictName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L91">Value</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L103">NotModelIdUsedAsIdentifier</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L104">TextData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L94">TTextData</a></i>
</li>
<details open><summary><b>Message TTextData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L95">TextName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/quality/relev_tools/bert_models/lib/model_descr_metadata/result_descr.proto?rev=r9795881#L96">TextValue</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L103">GeminiUrl</a></b>  <i>string</i>
<p> normalized by Gemini href </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L104">IsGeminiUrlBad</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L105">GeminiUrlUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L106">MarketOfferContent</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L332">MarketOfferContent</a></i>
</li>
<details open><summary><b>Message MarketOfferContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L334">category_id</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L335">category_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L337">vendor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L338">vendor_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L340">model_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L341">model_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L343">market_sku_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L344">market_sku_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L346">title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L348">params</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L18">MarketParameterValue</a></i>
</li>
<details open><summary><b>Message MarketParameterValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L20">value_source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L71">MarketValueSource</a></i>
<p> Откуда текущее значение, его качество </p>

</li>
<details open><summary><b>Enum MarketValueSource</b></summary>
<p> mbo-шный ModificationSource на первый взгляд кажется слишком большим </p>

<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_SOURCE</span></li>
<li><span style="color:#1D7373">PARTNER</span></li>
<li><span style="color:#1D7373">FORMALIZATION</span></li>
<li><span style="color:#1D7373">RULE</span></li>
<li><span style="color:#1D7373">PARTNER_CONTENT_MAPPING</span></li>
<li><span style="color:#1D7373">CONTENT_EXCEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L21">value_state</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L61">MarketValueState</a></i>
<p> Тип значения, по сути это - своего рода команда для диффа </p>

</li>
<details open><summary><b>Enum MarketValueState</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_STATE</span></li>
<li><span style="color:#1D7373">DEFAULT</span></li>
<li><span style="color:#1D7373">REMOVE</span></li>
<li><span style="color:#1D7373">FORCE_ADD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L23">param_id</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L28">param_name</a></b>  <i>string</i>
<p> Есть желание дублировать название параметра, которое вводил партнёр тут.  Если param_id невалиден в заданной категории, то по этому полю можно понять, про что было значение.  Если param_id есть и валиден то это поле не используется в обработке. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L30">value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L33">MarketValue</a></i>
</li>
<details open><summary><b>Message MarketValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L35">value_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L51">MarketValueType</a></i>
<p> Тип значения параметра копируется из param-а при создании + для enum/numeric_enum может быть тип HYPOTHESIS </p>

</li>
<details open><summary><b>Enum MarketValueType</b></summary>
<p> На данный момент отличается от MboParameters.ValueType в части HYPOTHESIS </p>

<ul>
<li><span style="color:#1D7373">UNDEFINED_MARKET_VALUE_TYPE</span></li>
<li><span style="color:#1D7373">BOOLEAN</span></li>
<li><span style="color:#1D7373">ENUM</span></li>
<li><span style="color:#1D7373">NUMERIC</span></li>
<li><span style="color:#1D7373">NUMERIC_ENUM</span></li>
<li><span style="color:#1D7373">STRING</span></li>
<li><span style="color:#1D7373">HYPOTHESIS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L38">bool_value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L39">numeric_value</a></b>  <i>string</i>
<p> Строка с числом, ^d+(.d+)?$ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L40">option_id</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/proto/ir/MarketParameters.proto?rev=r9795881#L47">str_value</a></b>  <i>string</i>
<p> То, что ввёл пользователь:  - если есть option_id - мы просто копируем сюда значение - также, как и param_id это поможет при изменении/эволюции категории  - гипотеза = value_type == HYPOTHESIS + str_value, NUMERIC_ENUM - считаем так же  - если STRING - то значение строки </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L350">market_b2c_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L351">market_sku_type</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L353">source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/external/Offer.proto?rev=r9795881#L326">EMarketOfferContentMappingSource</a></i>
</li>
<details open><summary><b>Enum EMarketOfferContentMappingSource</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_MAPPING_SOURCE</span></li>
<li><span style="color:#1D7373">ULTRACONTROLLER</span></li>
<li><span style="color:#1D7373">SMARTMATCHER</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L107">EcomFeatures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L51">TEcomFeatures</a></i>
</li>
<details open><summary><b>Message TEcomFeatures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L52">OneProductProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L53">ManyProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L54">NoProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L55">Version</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L56">IsOneProductRegexChosen</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L108">LandingHttpCode</a></b>  <i>uint64</i>
<p> max 19 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L357">ModAdvertBannerTexts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L163">TModAdvertBannerTexts</a></i>
</li>
<details open><summary><b>Message TModAdvertBannerTexts</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L164">Timestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L165">BrandsDescription</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L166">ContentDescription</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L167">ObjectVersion</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L360">EssOrderID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L9">TVersionedUint64</a></i>
<p> Из ESS  Когда запустим ESS в продакшен - уберем префикс Ess и заменим предыдущие данные. </p>

</li>
<details open><summary><b>Message TVersionedUint64</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L10">Value</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L11">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L361">EssAdGroupID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L9">TVersionedUint64</a></i>
<p> баннерная группа, ренейм GroupBannerID и т.п. </p>

</li>
<details open><summary><b>Message TVersionedUint64</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L10">Value</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L11">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L362">EssDirectBannerExportID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L9">TVersionedUint64</a></i>
<p> ID баннера с точки зрения директа </p>

</li>
<details open><summary><b>Message TVersionedUint64</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L10">Value</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L11">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L363">EssDeletedTime</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L9">TVersionedUint64</a></i>
<p> некое время удаления? </p>

</li>
<details open><summary><b>Message TVersionedUint64</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L10">Value</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L11">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L364">EssTitle</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L365">EssBody</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L366">EssButton</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L118">TVersionedButton</a></i>
</li>
<details open><summary><b>Message TVersionedButton</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L119">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_button.proto?rev=r9795881#L8">Button</a></i>
</li>
<details open><summary><b>Message Button</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_button.proto?rev=r9795881#L9">button_key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_button.proto?rev=r9795881#L10">button_caption</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_button.proto?rev=r9795881#L11">button_href</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L120">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L367">EssLogo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L123">TVersionedLogo</a></i>
</li>
<details open><summary><b>Message TVersionedLogo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L124">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L8">Logo</a></i>
</li>
<details open><summary><b>Message Logo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L9">formats</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L12">Format</a></i>
</li>
<details open><summary><b>Message Format</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L13">format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L14">width</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L15">height</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_logo.proto?rev=r9795881#L16">url</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L125">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L369">GalleryBanners</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L128">TVersionedGalleryBanners</a></i>
</li>
<details open><summary><b>Message TVersionedGalleryBanners</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L129">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L3">TGalleryBanner</a></i>
</li>
<details open><summary><b>Message TGalleryBanner</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L4">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L5">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L6">Images</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L7">Price</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L8">Relevance</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L9">Body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L10">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L11">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/gallery_banners.proto?rev=r9795881#L12">Flags</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L130">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L371">EssPermalinkID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L9">TVersionedUint64</a></i>
</li>
<details open><summary><b>Message TVersionedUint64</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L10">Value</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L11">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L372">EssPermalinkAssignType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L373">EssPermalinkChainIDs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L31">TVersionedUint64List</a></i>
</li>
<details open><summary><b>Message TVersionedUint64List</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L32">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/common.proto?rev=r9795881#L9">UInt64List</a></i>
</li>
<details open><summary><b>Message UInt64List</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/common.proto?rev=r9795881#L10">values</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L33">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L375">EssPlatformName</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L133">TVersionedPlatformName</a></i>
<p>структура с названием сервиса и постфиксами для вёрсток </p>

</li>
<details open><summary><b>Message TVersionedPlatformName</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L134">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L8">PlatformName</a></i>
</li>
<details open><summary><b>Message PlatformName</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L17">name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L18">forms</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L9">Forms</a></i>
</li>
<details open><summary><b>Message Forms</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L10">simple</a></b>  <i>string</i>
<p> "Дзен" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L11">simple_ya_full</a></b>  <i>string</i>
<p> "Яндекс.Дзен" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L12">simple_ya_short</a></b>  <i>string</i>
<p> "Я.Дзен" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L13">postfix</a></b>  <i>string</i>
<p> "на Дзене" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L14">postfix_ya_full</a></b>  <i>string</i>
<p> "на Яндекс.Дзене" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_platform_name.proto?rev=r9795881#L15">postfix_ya_short</a></b>  <i>string</i>
<p> "на Я.Дзене" </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L135">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L377">Favicon</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L170">TFavicon</a></i>
</li>
<details open><summary><b>Message TFavicon</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L171">OriginalHeight</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L172">OriginalWidth</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L173">UpdateTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L379">TurboUrl</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L176">TTurboUrl</a></i>
</li>
<details open><summary><b>Message TTurboUrl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L177">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L178">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L381">AppDataEss</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L181">TAppData</a></i>
</li>
<details open><summary><b>Message TAppData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L182">BundleId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L183">SourceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L184">RegionName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L185">LocaleName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L186">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L382">DirectBannersLogFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L36">TDirectBannersLogFields</a></i>
</li>
<details open><summary><b>Message TDirectBannersLogFields</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L101">Resources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L37">TResources</a></i>
</li>
<details open><summary><b>Message TResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L38">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L39">VisitHref</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L40">VideoMetadata</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L41">TurboGalleryHref</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L42">TurboAppType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L43">TurboAppId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L44">TurboAppContent</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L55">TemplateVariables</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L46">TTemplateVariable</a></i>
</li>
<details open><summary><b>Message TTemplateVariable</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L47">Value</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L48">TemplateResourceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L49">TemplateResourceNo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L50">TemplatePartNo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L51">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L52">Height</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L56">RenderInfo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L57">PackshotHref</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L58">MetaData</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L66">MediaImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L60">TMediaImage</a></i>
</li>
<details open><summary><b>Message TMediaImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L61">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L62">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L63">Height</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L67">Experiment</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L74">Dialog</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L69">TDialog</a></i>
</li>
<details open><summary><b>Message TDialog</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L70">ID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L71">BotID</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L75">CreativeComposedFrom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L76">AutoVideoCreative</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L77">Domain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L79">CreativeHref1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L80">CreativeHref2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L81">CreativeHref3</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L83">CreativeTurboLandingId1</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L84">CreativeTurboLandingHref1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L85">CreativeTurboLandingId2</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L86">CreativeTurboLandingHref2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L87">CreativeTurboLandingId3</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L88">CreativeTurboLandingHref3</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L97">AssetHashes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L90">TAssetHashes</a></i>
</li>
<details open><summary><b>Message TAssetHashes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L91">TitleAssetHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L92">TextBodyAssetHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L93">ImageAssetHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L94">VideoAssetHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L95">Html5AssetHash</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L98">UnifiedTemplateVariables</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L46">TTemplateVariable</a></i>
</li>
<details open><summary><b>Message TTemplateVariable</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L47">Value</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L48">TemplateResourceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L49">TemplateResourceNo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L50">TemplatePartNo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L51">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L52">Height</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L111">Sitelinks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L103">TSitelink</a></i>
</li>
<details open><summary><b>Message TSitelink</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L104">Href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L105">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L106">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L107">TurboLandingHref</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L108">TurboLandingId</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L113">CalloutSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L7">TCalloutSet</a></i>
</li>
<details open><summary><b>Message TCalloutSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L13">CalloutsList</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L14">Callouts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L8">TCallout</a></i>
</li>
<details open><summary><b>Message TCallout</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L9">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L10">Value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L114">MetrikaCounter</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L115">ViewNoticeHrefs</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L116">PriorityID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L125">PageModeration</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L118">TPageModeration</a></i>
</li>
<details open><summary><b>Message TPageModeration</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L119">PageID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L120">StatusModerate</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L121">Version</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L122">TaskUrl</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L126">MarketRating</a></b>  <i>int32</i>
<p> Deprecated, empty. Use instead Banner.Resources.DomainMarketRating.Rating </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L127">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L128">HrefText</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L129">Flags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L130">DynamicDisclaimer</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L131">DisplayedDomainAlias</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L132">ContentAction</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L164">ContactInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L134">TContactInfo</a></i>
</li>
<details open><summary><b>Message TContactInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L145">Phone</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L146">Country</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L147">City</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L148">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L149">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L150">GeoID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L151">ContactPerson</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L152">Metro</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L153">OGRN</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L154">IMClient</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L155">IMLogin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L156">ExtraMessage</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L157">ContactEmail</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L158">WorkTime</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L159">WorkTimeRaw</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L160">Map</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L135">TMap</a></i>
</li>
<details open><summary><b>Message TMap</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L136">X1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L137">Y1</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L138">X2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L139">Y2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L140">X</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L141">Y</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L142">Precision</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L161">IsCorrectContactInfo</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L165">ClusterDomain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L167">BannerPrice</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L17">TBannerPrice</a></i>
</li>
<details open><summary><b>Message TBannerPrice</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L19">Price</a></b>  <i>string</i>
<p> https://direct-dev.yandex-team.ru/db/ppc/tables/banner_prices.html </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L20">OldPrice</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L21">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L22">Prefix</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L23">Discount</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L168">Age</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L176">Creatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L170">TCreative</a></i>
</li>
<details open><summary><b>Message TCreative</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L171">CreativeID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L172">Status</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L173">CreativeType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L174">Version</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L185">Measurers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L178">TMeasurers</a></i>
</li>
<details open><summary><b>Message TMeasurers</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L179">Mediascope</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L180">Admetrica</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L181">Moat</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L182">Adloox</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L183">Weborama</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L186">TurboLandingId</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L187">TurboLandingHref</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L188">PermalinkAdPhone</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L189">DirectBannerID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L190">BannerLandData</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L191">ImpressionUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L192">MobileTracker</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L193">HrefS2S</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L194">ContentStoreHrefS2S</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L195">DistributionFormatID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L383">Options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L200">TOptions</a></i>
</li>
<details open><summary><b>Message TOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L201">IsMediaCreativeOutdoor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L202">IsGeoFlag</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L203">IsFakeTitle</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L204">IsFakeBody</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L205">IsVideoCreativeNonSkippable</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L206">IsAudioCreative</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L207">IsVideoCreativeIndoor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L208">HideStoreContentRating</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L209">HideStoreContentPrice</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L210">HideDomain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L211">HideContentReviewCount</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L212">HideContentIcon</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L213">IsBrandLift</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L214">IsMediaCreativeSurvey</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L215">IsMediaCreativeReachSurvey</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L216">IsVideoCreativeSurvey</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L217">IsVideoCreativeReachSurvey</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L218">IsPerformanceMain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L219">IsOffer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L220">IsMainPage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L224">IsMobile</a></b>  <i>bool</i>
<p> MySQL BannerXX.Options </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L225">IsDynamicTemplate</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L226">IsAutoVideo</a></b>  <i>bool</i>
<p> MySQL auto-video-direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L227">IsMediaImage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L228">IsMediaCreative</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L229">IsVideoCreative</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L230">IsDeleted</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L231">IsPicture</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L232">IsDynamic</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L233">IsMobileApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L234">IsVideoCreativeOutdoor</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L235">IsPerformance</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L236">IsNoValidCreative</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/banner_resources.proto?rev=r9795881#L237">IsPerformanceTgo</a></b>  <i>bool</i>
<p> max 34 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L385">ResourceFlags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L203">TResourceFlags</a></i>
</li>
<details open><summary><b>Message TResourceFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L204">Abuse</a></b>  <i>bool</i>
<p> "close" button on the banner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L205">HideDomain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L206">Card</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L207">AddrPhoneCard</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L208">MobileCard</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L209">HideIcon</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L210">HidePrice</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L211">HideRating</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L212">HideReviewCount</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L387">SiteFilterID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L388">SiteFilter</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L390">ClusterDomainId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L392">MobileAppData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L189">TMobileAppDataContainer</a></i>
</li>
<details open><summary><b>Message TMobileAppDataContainer</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L191">AppData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L64">TMobileAppData</a></i>
<p> filled if key fields in TAppData is not empty </p>

</li>
<details open><summary><b>Message TMobileAppData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L65">BMCategories</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L66">ContentAdvisoryRating</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L67">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L68">HasAds</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L69">MinOsVersion</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L70">MobileInterests</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L71">PriceValueRUB</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L72">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L73">SizeBytes</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L74">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L75">UsersCountByBigB</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L76">VendorNameRaw</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L77">Version</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L78">Votes</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L79">HasPurchases</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L80">VendorWebsite</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L81">HasVideo</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L82">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L18">TMobileAppDataCounters</a></i>
</li>
<details open><summary><b>Message TMobileAppDataCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L19">ActiveAppsUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L20">AttrInstalledUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L21">ClickedUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L22">FreshActiveUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L23">FreshAttrInstallUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L24">FreshClickUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L25">FreshInstallUsers</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L26">InAppUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L27">InstalledUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L28">LaunchedUsers</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L29">PurchasedUser</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L30">SnownedUser</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L83">Downloads</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L84">PriceCurrencyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L85">PriceValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L86">PriceCurrencySymbol</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L87">PlatformID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L88">StoreContentId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L89">IsFree</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L90">Icons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L34">TMobileAppDataImage</a></i>
</li>
<details open><summary><b>Message TMobileAppDataImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L35">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L36">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L37">Width</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L91">Screens</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L34">TMobileAppDataImage</a></i>
</li>
<details open><summary><b>Message TMobileAppDataImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L35">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L36">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L37">Width</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L92">Reviews</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L40">TMobileAppDataReview</a></i>
</li>
<details open><summary><b>Message TMobileAppDataReview</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L41">Author</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L42">Datetime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L43">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L44">Text</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L45">Title</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L93">LalCategories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L48">TMobileAppDataLalCategories</a></i>
</li>
<details open><summary><b>Message TMobileAppDataLalCategories</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L49">CentroidDistance</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L50">ClusterId</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L94">AllPrices</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L59">TMobileAppDataAllPrices</a></i>
</li>
<details open><summary><b>Message TMobileAppDataAllPrices</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L60">RegionName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L61">Download</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L53">TMobileAppDataDownload</a></i>
</li>
<details open><summary><b>Message TMobileAppDataDownload</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L54">PriceCurrencyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L55">PriceCurrencySymbol</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L56">PriceValue</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L95">Categories</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_app.proto?rev=r9795881#L96">SubCategories</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L193">UpdateTimestamp</a></b>  <i>uint64</i>
<p> timestamp of last update in seconds </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L394">BannerLandSpecificFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L215">TBannerLandSpecificFields</a></i>
</li>
<details open><summary><b>Message TBannerLandSpecificFields</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L216">BannerlandBeginTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L217">DisplayInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L58">TDisplayInfo</a></i>
</li>
<details open><summary><b>Message TDisplayInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L60">description_for_direct</a></b>  <i>string</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/package/plugin/settings.py?rev=7547566#L3426 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L61">business_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L62">offer_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L63">legal</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L64">sizes</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L65">sizes_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L66">consist</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L67">consist_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L68">colors</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L69">facility</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L70">facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L71">run</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L72">vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L73">model</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L74">year</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L75">location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L76">class</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L77">go_from</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L78">go_to</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L79">realty_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L80">sub_location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L81">building_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L82">metro</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L83">metro_time_on_foot</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L84">metro_time_on_transport</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L85">address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L89">engine_volume</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L90">engine_power</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L92">owners_number</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L93">color_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L7">EColor</a></i>
</li>
<details open><summary><b>Enum EColor</b></summary>
<ul>
<li><span style="color:#1D7373">COLOR_UNKNOWN</span></li>
<li><span style="color:#1D7373">COLOR_BEIGE</span></li>
<li><span style="color:#1D7373">COLOR_WHITE</span></li>
<li><span style="color:#1D7373">COLOR_COLORLESS</span></li>
<li><span style="color:#1D7373">COLOR_CYAN</span></li>
<li><span style="color:#1D7373">COLOR_YELLOW</span></li>
<li><span style="color:#1D7373">COLOR_GREEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLDEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLD</span></li>
<li><span style="color:#1D7373">COLOR_BROWN</span></li>
<li><span style="color:#1D7373">COLOR_RED</span></li>
<li><span style="color:#1D7373">COLOR_ORANGE</span></li>
<li><span style="color:#1D7373">COLOR_MAGENTA</span></li>
<li><span style="color:#1D7373">COLOR_PINK</span></li>
<li><span style="color:#1D7373">COLOR_SILVERY</span></li>
<li><span style="color:#1D7373">COLOR_SILVER</span></li>
<li><span style="color:#1D7373">COLOR_GRAY</span></li>
<li><span style="color:#1D7373">COLOR_BLUE</span></li>
<li><span style="color:#1D7373">COLOR_PURPLE</span></li>
<li><span style="color:#1D7373">COLOR_BLACK</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L94">body_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L30">EBodyType</a></i>
</li>
<details open><summary><b>Enum EBodyType</b></summary>
<ul>
<li><span style="color:#1D7373">BT_UNKNOWN</span></li>
<li><span style="color:#1D7373">BT_SEDAN_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_SEDAN</span></li>
<li><span style="color:#1D7373">BT_CABRIOLET</span></li>
<li><span style="color:#1D7373">BT_COMPACTVAN</span></li>
<li><span style="color:#1D7373">BT_COUPE_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_COUPE</span></li>
<li><span style="color:#1D7373">BT_FASTBACK</span></li>
<li><span style="color:#1D7373">BT_VAN</span></li>
<li><span style="color:#1D7373">BT_HATCHBACK</span></li>
<li><span style="color:#1D7373">BT_LANDAU</span></li>
<li><span style="color:#1D7373">BT_LIFTBACK</span></li>
<li><span style="color:#1D7373">BT_LIMOUSINE</span></li>
<li><span style="color:#1D7373">BT_MICROVAN</span></li>
<li><span style="color:#1D7373">BT_MINIVAN</span></li>
<li><span style="color:#1D7373">BT_SUV</span></li>
<li><span style="color:#1D7373">BT_PHAETON_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_PHAETON</span></li>
<li><span style="color:#1D7373">BT_PICKUP</span></li>
<li><span style="color:#1D7373">BT_ROADSTER</span></li>
<li><span style="color:#1D7373">BT_TARGA</span></li>
<li><span style="color:#1D7373">BT_SPEEDSTER</span></li>
<li><span style="color:#1D7373">BT_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_CROSSOVER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L95">gearbox_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L57">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<ul>
<li><span style="color:#1D7373">GB_UNKNOWN</span></li>
<li><span style="color:#1D7373">GB_MANUAL</span></li>
<li><span style="color:#1D7373">GB_AUTOMATIC</span></li>
<li><span style="color:#1D7373">GB_VARIATOR</span></li>
<li><span style="color:#1D7373">GB_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L96">engine_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L97">drive_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L98">state_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L100">floor</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L101">floors_total</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L102">rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L103">renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L104">building_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L105">deal_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L106">ready_quarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L107">building_state</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L108">new_flat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L109">region</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L65">ERealtyRegion</a></i>
</li>
<details open><summary><b>Enum ERealtyRegion</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW_DISTRICT</span></li>
<li><span style="color:#1D7373">REGION_LENINGRAD</span></li>
<li><span style="color:#1D7373">REGION_SVERDLOVSK</span></li>
<li><span style="color:#1D7373">REGION_KRASNODAR</span></li>
<li><span style="color:#1D7373">REGION_NOVOSIBIRSK</span></li>
<li><span style="color:#1D7373">REGION_OMSK</span></li>
<li><span style="color:#1D7373">REGION_ROSTOV</span></li>
<li><span style="color:#1D7373">REGION_SAMARA</span></li>
<li><span style="color:#1D7373">REGION_TUMEN</span></li>
<li><span style="color:#1D7373">REGION_VORONEJ</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW</span></li>
<li><span style="color:#1D7373">REGION_HABAROVSK</span></li>
<li><span style="color:#1D7373">REGION_NIJEGOROD</span></li>
<li><span style="color:#1D7373">REGION_TATARSTAN</span></li>
<li><span style="color:#1D7373">REGION_KRASNOYARSK</span></li>
<li><span style="color:#1D7373">REGION_BASHKORTOSTAN</span></li>
<li><span style="color:#1D7373">REGION_VLADIMIR</span></li>
<li><span style="color:#1D7373">REGION_CRIMEA</span></li>
<li><span style="color:#1D7373">REGION_SARATOV</span></li>
<li><span style="color:#1D7373">REGION_CHELYABINSK</span></li>
<li><span style="color:#1D7373">REGION_KOMI</span></li>
<li><span style="color:#1D7373">REGION_VOLGOGRAD</span></li>
<li><span style="color:#1D7373">REGION_ULYANOVSK</span></li>
<li><span style="color:#1D7373">REGION_TULA</span></li>
<li><span style="color:#1D7373">REGION_TVER</span></li>
<li><span style="color:#1D7373">REGION_LIPECK</span></li>
<li><span style="color:#1D7373">REGION_HANTI</span></li>
<li><span style="color:#1D7373">REGION_BELGOROD</span></li>
<li><span style="color:#1D7373">REGION_RYAZAN</span></li>
<li><span style="color:#1D7373">REGION_IRKUTSK</span></li>
<li><span style="color:#1D7373">REGION_KALUGA</span></li>
<li><span style="color:#1D7373">REGION_PENZA</span></li>
<li><span style="color:#1D7373">REGION_KEMEROV</span></li>
<li><span style="color:#1D7373">REGION_PERM</span></li>
<li><span style="color:#1D7373">REGION_YAROSLAVL</span></li>
<li><span style="color:#1D7373">REGION_KALININGRAD</span></li>
<li><span style="color:#1D7373">REGION_ALTAI</span></li>
<li><span style="color:#1D7373">REGION_STAVROPOL</span></li>
<li><span style="color:#1D7373">REGION_TOMSK</span></li>
<li><span style="color:#1D7373">REGION_ASTRAKHAN</span></li>
<li><span style="color:#1D7373">REGION_KOSTROMA</span></li>
<li><span style="color:#1D7373">REGION_UDMURTHIA</span></li>
<li><span style="color:#1D7373">REGION_IVANOVSK</span></li>
<li><span style="color:#1D7373">REGION_SMOLENSK</span></li>
<li><span style="color:#1D7373">REGION_ORENBURG</span></li>
<li><span style="color:#1D7373">REGION_CHUVASHIA</span></li>
<li><span style="color:#1D7373">REGION_KIROV</span></li>
<li><span style="color:#1D7373">REGION_MARIY_EL</span></li>
<li><span style="color:#1D7373">REGION_NOVGOROD</span></li>
<li><span style="color:#1D7373">REGION_ADIGEI</span></li>
<li><span style="color:#1D7373">REGION_PRIMORYE</span></li>
<li><span style="color:#1D7373">REGION_PSKOV</span></li>
<li><span style="color:#1D7373">REGION_BRYANSK</span></li>
<li><span style="color:#1D7373">REGION_OREL</span></li>
<li><span style="color:#1D7373">REGION_KURSK</span></li>
<li><span style="color:#1D7373">REGION_ARHANGELSK</span></li>
<li><span style="color:#1D7373">REGION_TAMBOV</span></li>
<li><span style="color:#1D7373">REGION_KURGAN</span></li>
<li><span style="color:#1D7373">REGION_VOLOGODSK</span></li>
<li><span style="color:#1D7373">REGION_KARELIYA</span></li>
<li><span style="color:#1D7373">REGION_BURYATIA</span></li>
<li><span style="color:#1D7373">REGION_NORTH_OSETIA</span></li>
<li><span style="color:#1D7373">REGION_YAMAL</span></li>
<li><span style="color:#1D7373">REGION_MORDOVIA</span></li>
<li><span style="color:#1D7373">REGION_DAGESTAN</span></li>
<li><span style="color:#1D7373">REGION_AMUR</span></li>
<li><span style="color:#1D7373">REGION_SAHA</span></li>
<li><span style="color:#1D7373">REGION_MURMANSK</span></li>
<li><span style="color:#1D7373">REGION_ZABAYKALSK</span></li>
<li><span style="color:#1D7373">REGION_KBR</span></li>
<li><span style="color:#1D7373">REGION_HAKASIA</span></li>
<li><span style="color:#1D7373">REGION_ALTAI_REPUBLIC</span></li>
<li><span style="color:#1D7373">REGION_SAKHALIN</span></li>
<li><span style="color:#1D7373">REGION_KAMCHATKA</span></li>
<li><span style="color:#1D7373">REGION_KCHR</span></li>
<li><span style="color:#1D7373">REGION_MAGADAN</span></li>
<li><span style="color:#1D7373">REGION_CHECHNYA</span></li>
<li><span style="color:#1D7373">REGION_TIVA</span></li>
<li><span style="color:#1D7373">REGION_JEWISH_AUTONOMOUS</span></li>
<li><span style="color:#1D7373">REGION_KALMIKIYA</span></li>
<li><span style="color:#1D7373">REGION_INGUSHETIA</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L218">ModelInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L11">TModelInfo</a></i>
</li>
<details open><summary><b>Message TModelInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L14">MarketModelID</a></b>  <i>uint64</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/db/schema.h?rev=7545212#L1563  https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/mkdb/resource.cpp?rev=7577587#L489 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L15">MarketCategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L16">AdvType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L17">AdvTypeDirectAllowed</a></b>  <i>bool</i>
<p> bl_type_direct_allowed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L34">Market</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L20">TMarketData</a></i>
</li>
<details open><summary><b>Message TMarketData</b></summary>
<p> market: </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L21">PriceMin</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L22">PriceAvg</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L23">PriceMax</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L24">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L25">RatingCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L26">MaxRating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L27">OfferClass</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L28">OfferCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L29">IsNew</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L30">Vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L31">Model</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L35">LocationID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L36">BLPhraseTemplateID</a></b>  <i>uint64</i>
<p> git rid of this please! </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L219">OfferID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L220">BannerHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L221">UpdateTime</a></b>  <i>uint64</i>
<p> "UpdateTime" field in BannerLand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L222">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L223">AutogeneratedOfferID</a></b>  <i>string</i>
<p> if SITE - will be filled. If not matched with OfferID -> this OfferID existed before autogenerated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L225">BusinessId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L226">OfferYabsId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L227">ShopId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L229">OfferPrepareDuration</a></b>  <i>uint64</i>
<p> Duration of offer preparing before BannerLand (in DataCamp) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L230">CaesarImportTimestamp</a></b>  <i>uint64</i>
<p> Timestamp of banner import to CaeSaR </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L231">OfferProperties</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L328">TOffer</a></i>
</li>
<details open><summary><b>Message TOffer</b></summary>
<p> *******************************  ** Id fields                 **  ** proto range from 1 to 100 **  ******************************* </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L336">BusinessId</a></b>  <i>uint32</i>
<p> Composite unique key of offer  Patner identifier in Yandex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L338">OfferId</a></b>  <i>string</i>
<p> B2B offer identifier from partner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L340">OfferYabsId</a></b>  <i>uint64</i>
<p> Hash of B2B identifier (should be unique in subset of all offers from one partner) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L342">ShopId</a></b>  <i>uint32</i>
<p> Identifier of Yandex services set (known as shop) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L346">ClientId</a></b>  <i>uint64</i>
<p> Additional identifiers  Partner identifier in accounting balance </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L348">FeedId</a></b>  <i>uint32</i>
<p> Feed identifier in B2C Yndex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L350">DirectFeedId</a></b>  <i>uint64</i>
<p> Feed identifier in Yandex.Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L351">WareMd5</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L353">OriginalSku</a></b>  <i>string</i>
<p> SKU in parnter content system </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L355">FeedItemGroupId</a></b>  <i>string</i>
<p> Id of group inside feed. Needed to create retargeting for group of e.g. iPhones 13 of different colors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L364">TimestampSeconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L367">DataType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L37">EDataType</a></i>
<p> Data type for BannerLand </p>

</li>
<details open><summary><b>Enum EDataType</b></summary>
<ul>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_MARKET</span></li>
<li><span style="color:#1D7373">DATA_TYPE_AUTORU</span></li>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_MERCHANT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_FLIGHT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_TRAVEL</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_HOTEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L370">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
<p> Offer source (feed or site) </p>

</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L373">ProductType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L68">EProductType</a></i>
<p> Product type for offer </p>

</li>
<details open><summary><b>Enum EProductType</b></summary>
<ul>
<li><span style="color:#1D7373">PRODUCT_TYPE_UNKNOWN</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AUTO_ACCESSORIES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AVIA_TICKETS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BEAUTY_HEALTH</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BUILDING_MATERIALS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CARS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHILDRENS_GOODS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHINESE_SITES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_DSE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_EXTERNAL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_FURNITURE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_GAMES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_HOTELS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_LIST</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_PROMOCODES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_REALTY</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_SPORTS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TIRES_DISKS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TRAVEL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_WEAR</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BOOKS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L375">OfferType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L64">EOfferType</a></i>
<p> Offer type </p>

</li>
<details open><summary><b>Enum EOfferType</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_TYPE_VENDOR_MODEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L378">OfferLanguage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L48">ELanguageCode</a></i>
<p> Offer texts language </p>

</li>
<details open><summary><b>Enum ELanguageCode</b></summary>
<ul>
<li><span style="color:#1D7373">LANGUAGE_UNKNOWN</span></li>
<li><span style="color:#1D7373">LANGUAGE_RU</span></li>
<li><span style="color:#1D7373">LANGUAGE_EN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L381">DisableStatus</a></b>  <i>bool</i>
<p> Is offer active </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L389">Model</a></b>  <i>string</i>
<p> Model name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L391">Vendor</a></b>  <i>string</i>
<p> Manufacturer or brand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L393">TypePrefix</a></b>  <i>string</i>
<p> Type or category name of good (used in title) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L395">Name</a></b>  <i>string</i>
<p> Full offer name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L398">Description</a></b>  <i>string</i>
<p> Detailed description of offer </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L401">Url</a></b>  <i>string</i>
<p> URL to offer on partner site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L403">UrlOriginalDomain</a></b>  <i>string</i>
<p> Domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L405">UrlOriginalDomainId</a></b>  <i>uint64</i>
<p> Id of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L407">UrlMainMirror</a></b>  <i>string</i>
<p> Main mirror (after redirects) of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L409">UrlMainMirrorId</a></b>  <i>uint64</i>
<p> Id of main mirror domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L412">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L110">TImageData</a></i>
<p> Offer images data (original URLs and avatars) </p>

</li>
<details open><summary><b>Message TImageData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L123">SourceUrl</a></b>  <i>string</i>
<p> Image URL on client site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L126">Status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L112">EAvatarizationStatus</a></i>
<p> Status of image loading into avatars service </p>

</li>
<details open><summary><b>Enum EAvatarizationStatus</b></summary>
<p> TODO: Replace with Market.DataCamp.MarketPicture.Status after complete MARKETINDEXER-41756 </p>

<ul>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_UNKNOWN</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_AVAILABLE</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_FAILED</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_REMOVED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L129">AvatarsInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
<p> Image avatars information </p>

</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L415">Currency</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L36">Currency</a></i>
<p> Offer currency </p>

</li>
<details open><summary><b>Enum Currency</b></summary>
<ul>
<li><span style="color:#1D7373">CURRENCY_UNDEFINED</span></li>
<li><span style="color:#1D7373">RUR</span></li>
<li><span style="color:#1D7373">USD</span></li>
<li><span style="color:#1D7373">EUR</span></li>
<li><span style="color:#1D7373">UAH</span></li>
<li><span style="color:#1D7373">KZT</span></li>
<li><span style="color:#1D7373">BYN</span></li>
<li><span style="color:#1D7373">GBP</span></li>
<li><span style="color:#1D7373">TRY</span></li>
<li><span style="color:#1D7373">ALL</span></li>
<li><span style="color:#1D7373">AFN</span></li>
<li><span style="color:#1D7373">ARS</span></li>
<li><span style="color:#1D7373">AWG</span></li>
<li><span style="color:#1D7373">AUD</span></li>
<li><span style="color:#1D7373">AZN</span></li>
<li><span style="color:#1D7373">BBD</span></li>
<li><span style="color:#1D7373">BZD</span></li>
<li><span style="color:#1D7373">BMD</span></li>
<li><span style="color:#1D7373">BOB</span></li>
<li><span style="color:#1D7373">BAM</span></li>
<li><span style="color:#1D7373">BWP</span></li>
<li><span style="color:#1D7373">BGN</span></li>
<li><span style="color:#1D7373">BRL</span></li>
<li><span style="color:#1D7373">BND</span></li>
<li><span style="color:#1D7373">KHR</span></li>
<li><span style="color:#1D7373">CAD</span></li>
<li><span style="color:#1D7373">KYD</span></li>
<li><span style="color:#1D7373">CLP</span></li>
<li><span style="color:#1D7373">CNY</span></li>
<li><span style="color:#1D7373">COP</span></li>
<li><span style="color:#1D7373">CRC</span></li>
<li><span style="color:#1D7373">HRK</span></li>
<li><span style="color:#1D7373">CUP</span></li>
<li><span style="color:#1D7373">CZK</span></li>
<li><span style="color:#1D7373">DKK</span></li>
<li><span style="color:#1D7373">DOP</span></li>
<li><span style="color:#1D7373">XCD</span></li>
<li><span style="color:#1D7373">EGP</span></li>
<li><span style="color:#1D7373">SVC</span></li>
<li><span style="color:#1D7373">FKP</span></li>
<li><span style="color:#1D7373">FJD</span></li>
<li><span style="color:#1D7373">GHS</span></li>
<li><span style="color:#1D7373">GIP</span></li>
<li><span style="color:#1D7373">GTQ</span></li>
<li><span style="color:#1D7373">GYD</span></li>
<li><span style="color:#1D7373">HNL</span></li>
<li><span style="color:#1D7373">HKD</span></li>
<li><span style="color:#1D7373">HUF</span></li>
<li><span style="color:#1D7373">ISK</span></li>
<li><span style="color:#1D7373">INR</span></li>
<li><span style="color:#1D7373">IDR</span></li>
<li><span style="color:#1D7373">IRR</span></li>
<li><span style="color:#1D7373">ILS</span></li>
<li><span style="color:#1D7373">JMD</span></li>
<li><span style="color:#1D7373">JPY</span></li>
<li><span style="color:#1D7373">KPW</span></li>
<li><span style="color:#1D7373">KRW</span></li>
<li><span style="color:#1D7373">KGS</span></li>
<li><span style="color:#1D7373">LAK</span></li>
<li><span style="color:#1D7373">LBP</span></li>
<li><span style="color:#1D7373">LRD</span></li>
<li><span style="color:#1D7373">MKD</span></li>
<li><span style="color:#1D7373">MYR</span></li>
<li><span style="color:#1D7373">MUR</span></li>
<li><span style="color:#1D7373">MXN</span></li>
<li><span style="color:#1D7373">MNT</span></li>
<li><span style="color:#1D7373">MAD</span></li>
<li><span style="color:#1D7373">MZN</span></li>
<li><span style="color:#1D7373">NAD</span></li>
<li><span style="color:#1D7373">NPR</span></li>
<li><span style="color:#1D7373">ANG</span></li>
<li><span style="color:#1D7373">NZD</span></li>
<li><span style="color:#1D7373">NIO</span></li>
<li><span style="color:#1D7373">NGN</span></li>
<li><span style="color:#1D7373">NOK</span></li>
<li><span style="color:#1D7373">OMR</span></li>
<li><span style="color:#1D7373">PKR</span></li>
<li><span style="color:#1D7373">PAB</span></li>
<li><span style="color:#1D7373">PYG</span></li>
<li><span style="color:#1D7373">PEN</span></li>
<li><span style="color:#1D7373">PHP</span></li>
<li><span style="color:#1D7373">PLN</span></li>
<li><span style="color:#1D7373">QAR</span></li>
<li><span style="color:#1D7373">RON</span></li>
<li><span style="color:#1D7373">SHP</span></li>
<li><span style="color:#1D7373">SAR</span></li>
<li><span style="color:#1D7373">RSD</span></li>
<li><span style="color:#1D7373">SCR</span></li>
<li><span style="color:#1D7373">SGD</span></li>
<li><span style="color:#1D7373">SBD</span></li>
<li><span style="color:#1D7373">SOS</span></li>
<li><span style="color:#1D7373">ZAR</span></li>
<li><span style="color:#1D7373">LKR</span></li>
<li><span style="color:#1D7373">SEK</span></li>
<li><span style="color:#1D7373">CHF</span></li>
<li><span style="color:#1D7373">SRD</span></li>
<li><span style="color:#1D7373">SYP</span></li>
<li><span style="color:#1D7373">TWD</span></li>
<li><span style="color:#1D7373">THB</span></li>
<li><span style="color:#1D7373">TTD</span></li>
<li><span style="color:#1D7373">AED</span></li>
<li><span style="color:#1D7373">UYU</span></li>
<li><span style="color:#1D7373">UZS</span></li>
<li><span style="color:#1D7373">VEF</span></li>
<li><span style="color:#1D7373">VND</span></li>
<li><span style="color:#1D7373">YER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L417">Price</a></b>  <i>uint64</i>
<p> Price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L419">PriceMicrosPart</a></b>  <i>uint64</i>
<p> Price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L421">OldPrice</a></b>  <i>uint64</i>
<p> Previous price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L423">OldPriceMicrosPart</a></b>  <i>uint64</i>
<p> Previous price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L426">CategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Offer categoryzation info </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L428">Breadcrumbs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L153">TBreadcrumbsData</a></i>
<p> Navigational path on site </p>

</li>
<details open><summary><b>Message TBreadcrumbsData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L156">Path</a></b>  <i>string</i>
<p> Text path in navigarional tree of site  Each item contains a node name, first item is root element </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L431">Available</a></b>  <i>bool</i>
<p> Is offer available to order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L433">DeliveryOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L144">TDeliveryOptions</a></i>
<p> Detailed delivery options </p>

</li>
<details open><summary><b>Message TDeliveryOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L146">Pickup</a></b>  <i>bool</i>
<p> Available for pickup </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L148">Store</a></b>  <i>bool</i>
<p> Available in store without order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L150">Delivery</a></b>  <i>bool</i>
<p> Available for order with courier delivery </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L436">SalesNotes</a></b>  <i>string</i>
<p> Sales notes as human readable text </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L439">ManufacturerWarranty</a></b>  <i>bool</i>
<p> Offer has manufacturer warranty </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L442">ShopCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Offer category from partner feed </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L445">MarketCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Yandex Market categories </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L448">BannerLandCategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Multik categories </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L451">ParametersData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L159">TOfferParameter</a></i>
<p> Raw unstructured parameters data </p>

</li>
<details open><summary><b>Message TOfferParameter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L160">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L161">Unit</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L162">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L454">Parameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L165">TOfferStructuredParameters</a></i>
<p> Parsed parameters </p>

</li>
<details open><summary><b>Message TOfferStructuredParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L166">Age</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L167">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L168">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L169">Season</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L170">Sex</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L171">Corpus</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L172">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L173">Collection</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L174">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L175">Length</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L176">Width</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L177">Height</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L178">SizeUnit</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L457">Age</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
<p> Product age for moderation </p>

</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L460">Adult</a></b>  <i>bool</i>
<p> Product offer for adults </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L463">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L791">FormalCondition</a></i>
<p> Product condition: used or like new; reason for condition </p>

</li>
<details open><summary><b>Message FormalCondition</b></summary>
<p> Cостояние товара  https://yandex.ru/support/partnermarket/elements/condition.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L800">type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L793">Type</a></i>
</li>
<details open><summary><b>Enum Type</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_TYPE</span></li>
<li><span style="color:#1D7373">LIKENEW</span></li>
<li><span style="color:#1D7373">USED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L801">reason</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L465">VideoCreatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L16">ProcessedVideo</a></i>
</li>
<details open><summary><b>Message ProcessedVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L22">id</a></b>  <i>string</i>
<p> ID креатива </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L23">status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L17">Status</a></i>
</li>
<details open><summary><b>Enum Status</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED</span></li>
<li><span style="color:#1D7373">AVAILABLE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L24">original_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L25">creative_id</a></b>  <i>uint64</i>
<p> ID креатива, число </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L466">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L473">Custom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L193">TCustomData</a></i>
</li>
<details open><summary><b>Message TCustomData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L194">OriginalOfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L195">Id2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L196">CustomPhrases</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L474">GoogleMerchant</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L181">TGoogleMerchantData</a></i>
</li>
<details open><summary><b>Message TGoogleMerchantData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L182">AgeGroup</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L134">EGoogleMerchantAgeGroup</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantAgeGroup</b></summary>
<ul>
<li><span style="color:#1D7373">GM_AGE_NEWBORN</span></li>
<li><span style="color:#1D7373">GM_AGE_INFANT</span></li>
<li><span style="color:#1D7373">GM_AGE_TODDLER</span></li>
<li><span style="color:#1D7373">GM_AGE_KIDS</span></li>
<li><span style="color:#1D7373">GM_AGE_ADULT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L183">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L184">Gender</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L142">EGoogleMerchantGender</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantGender</b></summary>
<ul>
<li><span style="color:#1D7373">GM_GENDER_MALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_FEMALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_UNISEX</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L185">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L186">Pattern</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L187">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L188">SizeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L148">EGoogleMerchantSizeType</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeType</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_TYPE_REGULAR</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PETITE</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PLUS</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_TALL</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_BIG</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_MATERNITY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L189">SizeSystem</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L157">EGoogleMerchantSizeSystem</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeSystem</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_AU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_BR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_CN</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_DE</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_EU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_FR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_IT</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_JP</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_MEX</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_UK</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_US</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L190">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L17">EGoogleMerchantCondition</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantCondition</b></summary>
<ul>
<li><span style="color:#1D7373">GM_CONDITION_NEW</span></li>
<li><span style="color:#1D7373">GM_CONDITION_REFURBISHED</span></li>
<li><span style="color:#1D7373">GM_CONDITION_USED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L475">Car</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L210">TCarData</a></i>
</li>
<details open><summary><b>Message TCarData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L211">UniqueId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L212">VIN</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L214">ModificationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L215">ModificationInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L199">TCarModificationInfo</a></i>
</li>
<details open><summary><b>Message TCarModificationInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L200">EngineVolume</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L201">EngineVolumeValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L202">EnginePower</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L203">EnginePowerValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L204">EnginePowerUnit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L104">ECarPowerUnit</a></i>
</li>
<details open><summary><b>Enum ECarPowerUnit</b></summary>
<p> Единицы измерения мощности двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_HORSEPOWER_UNIT</span></li>
<li><span style="color:#1D7373">CAR_KILOWATT_UNIT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L205">EngineType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L206">Gearbox</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L44">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<p> Тип коробки передач </p>

<ul>
<li><span style="color:#1D7373">CAR_GEARBOX_MANUAL</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_AUTOMATIC</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_VARIATOR</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L207">Drive</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L217">ComplectationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L218">BodyType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L219">SteeringWheel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L25">ECarSteeringWheel</a></i>
</li>
<details open><summary><b>Enum ECarSteeringWheel</b></summary>
<p> Расположение руля (левый или правый) </p>

<ul>
<li><span style="color:#1D7373">CAR_LEFT_HAND_DRIVE</span></li>
<li><span style="color:#1D7373">CAR_RIGHT_HAND_DRIVE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L220">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L221">Metallic</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L222">CustomStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L77">ECarCustomStatus</a></i>
</li>
<details open><summary><b>Enum ECarCustomStatus</b></summary>
<p> Таможенный статус </p>

<ul>
<li><span style="color:#1D7373">CAR_CUSTOM_CLEARED</span></li>
<li><span style="color:#1D7373">CAR_CUSTOM_NOT_CLEARED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L223">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L224">OwnersNumber</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L95">ECarOwnersNumber</a></i>
</li>
<details open><summary><b>Enum ECarOwnersNumber</b></summary>
<p> Количество владельцев по ПТС </p>

<ul>
<li><span style="color:#1D7373">CAR_NO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_ONE_OWNER</span></li>
<li><span style="color:#1D7373">CAR_TWO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_THREE_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_FOUR_OR_MORE_OWNERS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L225">Run</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L226">Year</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L227">RegistryYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L228">DoorsCount</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L476">Travel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L239">TTravelData</a></i>
</li>
<details open><summary><b>Message TTravelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L241">DestinationId</a></b>  <i>string</i>
<p> Пункт назначения </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L242">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L245">OriginId</a></b>  <i>string</i>
<p> Пункт отправления </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L246">OriginName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L477">Hotel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L249">THotelData</a></i>
</li>
<details open><summary><b>Message THotelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L250">PropertyId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L252">PropertyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L254">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L257">StarRating</a></b>  <i>uint32</i>
<p> Number stars at the hotel (from 1 to 5) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L260">Score</a></b>  <i>double</i>
<p> User score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L263">MaxScore</a></b>  <i>uint32</i>
<p> The max allowed user's score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L265">Facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L267">Category</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L269">Address</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L478">Flight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L231">TFlightData</a></i>
</li>
<details open><summary><b>Message TFlightData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L232">OriginId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L233">OriginName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L235">DestinationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L236">DestinationName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L479">Realty</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L303">TRealtyData</a></i>
</li>
<details open><summary><b>Message TRealtyData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L304">RealtyCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L28">ERealtyCategory</a></i>
</li>
<details open><summary><b>Enum ERealtyCategory</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_COMMERCIAL</span></li>
<li><span style="color:#1D7373">REALTY_COTTAGE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_WITH_LOT</span></li>
<li><span style="color:#1D7373">REALTY_LOT</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_PART</span></li>
<li><span style="color:#1D7373">REALTY_FLAT</span></li>
<li><span style="color:#1D7373">REALTY_ROOM</span></li>
<li><span style="color:#1D7373">REALTY_TOWNHOUSE</span></li>
<li><span style="color:#1D7373">REALTY_DUPLEX</span></li>
<li><span style="color:#1D7373">REALTY_GARAGE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L305">Location</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L278">TRealtyLocation</a></i>
</li>
<details open><summary><b>Message TRealtyLocation</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L279">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L280">Region</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L281">LocalityName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L282">MetroName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L283">MetroTimeOnFoot</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L284">MetroTimeOnTransport</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L306">DealStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L307">RealtyObjectData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L287">TRealtyObjectData</a></i>
</li>
<details open><summary><b>Message TRealtyObjectData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L288">Area</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L273">TRealtyArea</a></i>
</li>
<details open><summary><b>Message TRealtyArea</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L274">Value</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L275">Unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L80">ERealtyAreaUnit</a></i>
</li>
<details open><summary><b>Enum ERealtyAreaUnit</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_SQUARE_METER</span></li>
<li><span style="color:#1D7373">REALTY_ARE</span></li>
<li><span style="color:#1D7373">REALTY_HECTARE</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L289">Rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L290">Floor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L291">Renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L292">NewFlat</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L308">BuildingData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L295">TRealtyBuildingData</a></i>
</li>
<details open><summary><b>Message TRealtyBuildingData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L296">BuildingType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L297">FloorsTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L298">BuiltYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L299">ReadyQuarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L300">BuildingState</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L488">ClientAdTitle</a></b>  <i>string</i>
<p> Fixed banner title (filled by UseAsName) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L491">ClientAdBody</a></b>  <i>string</i>
<p> Fixed banner body (filled by UseAsBody) </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L232">VendorIDFromOffer</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L397">ParentExportID</a></b>  <i>uint64</i>
<p> parent's ExportID for dyn banners and non-image banner's ExportID for image banners  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L399">EssGreenUrlTextPrefix</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L400">EssGreenUrlTextSuffix</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L401">EssFeedInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L138">TVersionedFeedInfo</a></i>
</li>
<details open><summary><b>Message TVersionedFeedInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L139">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L8">FeedInfo</a></i>
</li>
<details open><summary><b>Message FeedInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L9">market_business_id</a></b>  <i>uint64</i>
<p> Идентификатор бизнеса в Маркете, которому принадлежит фид </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L10">market_shop_id</a></b>  <i>uint64</i>
<p> Идентификатор магазина которому принадлежит фид в Маркете </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L11">market_feed_id</a></b>  <i>uint64</i>
<p> Идентификатор фида в Маркете </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L12">direct_feed_id</a></b>  <i>uint64</i>
<p> Идентификатор фида в Директе </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_feed_info.proto?rev=r9795881#L13">filter_id</a></b>  <i>uint64</i>
<p> Идентификатор фильтра для фида </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L140">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L402">DomainMarketRating</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L235">TDomainMarketRating</a></i>
</li>
<details open><summary><b>Message TDomainMarketRating</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L236">Rating</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L237">ReviewsLink</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L238">ReviewsCount</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L404">MobileAppDeeplinks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L196">TMobileAppDeeplinksContainer</a></i>
</li>
<details open><summary><b>Message TMobileAppDeeplinksContainer</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L198">AppDeeplinks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L17">TMobileAppDeeplinks</a></i>
<p> filled if key fields in TAppData is not empty </p>

</li>
<details open><summary><b>Message TMobileAppDeeplinks</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L18">AppGalleryDeeplink</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L19">AppGalleryDownloadDeeplink</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L20">AppGalleryTTL</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L21">AppGetDeeplink</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/mobile_deeplinks.proto?rev=r9795881#L22">AppGetDownloadDeeplink</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L200">UpdateTimestamp</a></b>  <i>uint64</i>
<p> timestamp of last update in seconds </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L405">AdGroupType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L406">Host</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L112">THost</a></i>
</li>
<details open><summary><b>Message THost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L113">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L115">Herf</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L426">THostErfInfoProto</a></i>
<p> robot factors </p>

</li>
<details open><summary><b>Message THostErfInfoProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L427">ReservedHasTimeProfiles</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L429">IsVendor</a></b>  <i>bool</i>
<p> 2 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L430">IsLib</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L431">AntispamBanHostFresh</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L432">IsImportant</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L435">YabarHostVisits</a></b>  <i>uint32</i>
<p> 7 deprecated.  8 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L436">CommLinksHostSEO</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L437">YaBar</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L438">LogCtrMean</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L439">TestAntispamFeatures</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L440">Mascot01</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L441">AdsMarker</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L442">RankCommGoodnessUA</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L443">OwnerMeanRelevMx</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L444">Mascot02</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L445">TorrentQueryShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L446">TorrentClickShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L447">Mascot04</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L448">Mascot07</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L449">Mascot10</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L450">Mascot14</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L451">Mascot16</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L452">Mascot18</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L453">Mascot19</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L454">Mascot24</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L455">Mascot25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L456">Mascot26</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L457">Mascot32</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L458">Mascot33</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L459">Mascot35</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L460">Mascot39</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L461">Mascot40</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L463">MascotDirectoryReviewsDeprecated</a></b>  <i>uint32</i>
<p> 198 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L464">MascotRankArtroz</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L465">AntispamBanHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L466">MascotDirectoryLongtitudeDeprecated</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L467">MascotDirectoryLatitudeDeprecated</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L468">MascotDirectoryRubric0Deprecated</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L469">MascotDirectoryRubric1Deprecated</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L470">AntispamBanOwner</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L471">MascotDirectoryRubric2Deprecated</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L472">MascotDirectoryAddressesDeprecated</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L473">MascotMore120SecVisitsSearchShareUserSessions</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L474">More120SecVisitsShareGsm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L475">More120SecVisitsShareTouchWifi</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L476">AdultnessHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L491">Bookmarks</a></b>  <i>uint32</i>
<p> 70 deprecated.  71 deprecated.  72 deprecated.  73 deprecated.  74 deprecated.  75 deprecated.  76 deprecated.  77 deprecated.  78 deprecated.  79 deprecated.  80 deprecated.  81 deprecated.  82 deprecated.  83 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L492">HostRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L493">NewsCit</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L494">Spam2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L495">Nevasca1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L496">Nevasca2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L497">Nevasca3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L498">LiruInternalTraffic1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L499">LiruInternalTraffic2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L500">LiruOutTraffic1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L501">LiruOutTraffic2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L502">LiruSearchTraffic1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L503">LiruSearchTraffic2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L504">YaBarCoreOwner</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L505">IsCom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L506">IsHostCISLanguagesDominance</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L507">DaterStatsYearInHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L508">IsCommercial</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L509">IsInternational</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L510">IsTasix</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L511">IsInternationalDomain</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L512">HostCommercialRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L513">YaBarCoreHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L514">YabarHostSearchTraffic</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L515">YabarHostInternalTraffic</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L516">YabarHostAvgTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L517">YabarHostAvgTime2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L518">YabarHostAvgActions</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L519">YabarHostBrowseRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L520">OwnerClicksPCTR</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L521">OwnerSDiffClickEntropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L522">OwnerSDiffShowEntropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L523">OwnerSDiffCSRatioEntropy</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L524">OwnerSessNormDur</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L525">NoSpam</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L526">HostSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L527">HostLanguage</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L528">HostQuality</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L529">HasAdv</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L530">HasYandexAdv</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L531">IsWikipedia</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L532">StevensonBinary</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L533">AuraOwnerLogUnique</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L534">AuraOwnerLogShared</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L535">AuraOwnerLogAuthor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L536">AuraOwnerLogUnauth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L537">AuraOwnerMeanSharedSpread</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L538">TrafHostRank</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L539">NationalDomainId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L540">BadBookmarks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L541">BookmarkUsers</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L542">OwnerReqsPopularity</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L543">HostSpeed</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L544">HostReliability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L545">AntispamBanHostGsm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L546">StevensonUrlsPerClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L547">StevensonUrlsPerShows</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L548">StevensonUrlsPerShows10</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L549">StevensonWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L550">StevensonPlayers</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L551">MascotScorePercentile</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L552">HostAdultness</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L553">AddTimeMP</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L554">YabarHostVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L555">OwnerNavQuota</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L556">OwnerSatisfied4Rate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L557">OwnerEnoughClicked</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L558">AuraOwnerLogOrigin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L559">SeoInPayLinks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L560">RankOnlineShop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L561">RankBoostGoodness</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L562">ReservedFromMarket</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L563">IsBoard</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L564">IsCatalogueCard</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L565">IsWikipediaHost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L566">AdvAspam</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L567">QueriesCommRatioLe005</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L568">QueriesRatioMorda</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L569">QueriesAvgCM2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L570">NumUrls</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L571">RegionalClicks</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L572">IsReferatHost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L573">ReservedWmidSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L574">VideoPirate</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L575">RankComGoodness</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L576">RankComGoodnessBar</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L577">IsEncyc</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L579">AuraOwnerRelAuthor</a></b>  <i>uint32</i>
<p> 186 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L580">YabarHostSurfTrNdHgGr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L581">TrashAdv</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L582">AntispamPess</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L583">YabarHostSurfTrDpNdLeafLn</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L584">YabarHostSurfTrNdTmGrDsp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L585">YabarHostSurfTrNdTmLeafLn90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L586">HostDownloadProbability</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L587">HostHash</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L588">OwnerHash</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L589">NastyHost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L590">PornoHostFix</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L591">ReservedMonthUniqueVisitorsAbs_desktop_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L593">MonthUniqueVisitorsAbs_gsm_all</a></b>  <i>uint32</i>
<p> 215 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L594">AntispamTTrust</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L595">MonthReturnVisitorsLog_touchwifi_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L596">MonthReturnVisitorsLog_gsm_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L597">MonthReturnVisitorsLog_desktop_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L598">MonthReturnVisitorsLog_touchwifi_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L599">MonthReturnVisitorsLog_gsm_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L600">More160VisitorsShare_desktop_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L601">More160VisitorsShare_touchwifi_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L602">More160VisitorsShare_gsm_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L603">More160VisitorsShare_desktop_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L604">More160VisitorsShare_touchwifi_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L605">More160VisitorsShare_gsm_kub</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L606">MonthReturnVisitorsShare_desktop_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L607">MonthReturnVisitorsShare_touchwifi_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L608">MonthReturnVisitorsShare_gsm_all</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L609">RuTraffShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L610">TouchwifiTraffShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L611">RandomLogHostHasPaymentsAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L612">RandomLogHostIsVideoQueryAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L613">RandomLogHostSyntQualityAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L614">RandomLogHostGeoRegionalityVNewPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L615">RandomLogHostQClassDownloadAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L616">RandomLogHostIsMusicAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L617">RandomLogHostQueryThEncyclopedicPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L618">RandomLogHostCommercialOwnerRankRegAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L619">RandomLogHostYabarWordDNGIPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L620">RandomLogHostPopularSEFRCBrowserAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L621">RandomLogHostURLClicksMaxGeoRegionFRCRatioAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L622">RandomLogHostUBLongPeriodDirectHChildren90CntPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L623">RandomLogHostUBLongPeriodDtUrlHChildrenPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L624">RandomLogHostIsPictureAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L625">RandomLogHostErratumLogQueryProbabilityAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L626">RandomLogHostQiQueryCountAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L627">IsMobileVersion</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L629">YellownessImgMax</a></b>  <i>uint32</i>
<p> 254 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L630">YellownessImgAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L631">YellowImgShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L632">YellowImgCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L633">TeasersCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L634">TeasersArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L635">YellownessTxtMin</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L636">YellownessTxtAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L637">HasAdvClickableBG</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L638">AdvNetsArea</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L639">AdvNetsAreaFirstPage</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L640">AdvNetsCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L641">AdvTraffOutShareDesktop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L642">RTBTraffOutShareDesktop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L644">NewsAgencyRating</a></b>  <i>float</i>
<p> 269 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L646">RandomLogHostVisitsFromWikiAvg</a></b>  <i>uint32</i>
<p> 271 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L647">RandomLogHostWeightedSumIsIndexPageIsNavMxQueryPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L648">RandomLogHostNavLinearPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L649">RandomLogHostFoundPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L650">RandomLogHostSubqueryThMatchAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L651">RandomLogHostNavLinearAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L652">RandomLogHostSegmentWordPortionFromMainContentAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L653">RandomLogHostXfDtShowAllMaxFFieldSet2Bm15FLogK0001Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L654">RandomLogHostQueryRegionSizeAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L655">RandomLogHostAvgSessionLenPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L656">RandomLogHostIsRelevLocaleUAAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L657">RandomLogHostQfufAllSumWFSumWFieldSet3BclmWeightedFLogW0K0001Perc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L658">RandomLogHostDssmBoostingCtrQuerySelfSimilarityPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L659">RandomLogHostQueryToDocAllSumFCountTextBocm11Norm256Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L660">RandomLogHostIsNavMxQueryPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L661">RandomLogHostSubqueryThMatchAPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L662">RandomLogHostDBM15Wares2Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L663">RandomLogHostUrlNGramsModelPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L664">RandomLogHostUBLongPeriodDeltaAvgMinTimeWhenPageShowPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L665">RandomLogHostDssmAggregatedAnnRegAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L666">RandomLogHostDssmBoostingCtrKMeans1ScoreScaledSumWeightedQEPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L667">RandomLogHostLongClickMobileAllWcmWeightedValuePerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L668">RandomLogHostDssmVkPopularityPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L669">RandomLogHostUBLongPeriodVisitsSNProbAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L670">RandomLogHostCountryQueryRegionalityPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L671">RandomLogHostTRhitwPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L672">RandomLogHostUBLongPeriodAvgSearchDuration600Perc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L673">RandomLogHostRequestIsFromIOSAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L674">RandomLogHostDssmQueryEmbeddingCtrNoMinerPca4Perc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L675">RandomLogHostXfDtShowAllMaxFFieldSetUTBm15FLogW0Avg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L676">RandomLogHostUrlTrigramsPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L677">RandomLogHostDssmQueryEmbeddingCtrNoMinerPca1Perc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L678">RandomLogHostIsRelevLocaleKZAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L679">RandomLogHostTextFeaturesPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L680">HasJsFromMarketgidCom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L681">HasJsFromRfityCom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L682">HasJsFromGoogleAnalyticsCom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L683">HasJsFromGoogleApisCom</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L684">HasJsFromFacebookNet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L685">HasJsFromMcYandexRu</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L686">Official</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L688">Nevasca2ShareWeight</a></b>  <i>uint32</i>
<p> 313 deprecated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L689">Nevasca2FreshWeek</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L690">TrafgraphInGT_share_d</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L691">TrafgraphInGT_share_m</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L692">GreenTrafficDesktop_log</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L693">ReturnRateMonth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L694">Cy100log</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L695">BizKernel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L696">BizKernelQuantile</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L697">Speed</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L698">RandomLogHostLongRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L699">RandomLogHostIsOrgRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L700">RandomLogHostGskUrlModelRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L701">RandomLogHostDaterStatsAverageSourceSegmentRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L702">RandomLogHostVisitsFromWikiRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L703">RandomLogHostXfDtShowBagOfWordsTitleCosineMaxMatchRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L704">RandomLogHostUBLongPeriodDownloadsProbRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L705">RandomLogHostMetaAvgIsNotCgiRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L706">RandomLogHostMetaRmsSynPercentBadWordPairsRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L707">RandomLogHostMetaPosTrigramsProbRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L708">RandomLogHostBocmPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L709">RandomLogHostSegmentWordPortionFromMainContentPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L710">RandomLogHostIsMobileBeautyPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L711">RandomLogHostUSLongPeriodUrlWinsProbPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L712">RandomLogHostDssmBoostingXfWeightKMeans5AvgTop02ScoreQEPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L713">RandomLogHostDssmBoostingCtrKMeans1ScorePerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L714">RandomLogHostSDIsNavMxQueryMaxPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L715">RandomLogHostMetaWeb764Web1076ProductInvAvgPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L716">RandomLogHostMetaWeb1099Web1219ProductInvPosPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L717">RandomLogHostMetaMaxDssmMiddleVsShortLongHardNoClicksPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L718">RandomLogHostNumLinksFromMPMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L719">RandomLogHostNavLinearMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L720">RandomLogHostDaterStatsAverageSourceSegmentMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L721">RandomLogHostWeightedSumIsIndexPageIsNavMxQueryMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L722">RandomLogHostQueryToDocAllSumFCountTextBocm11Norm256Max</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L723">RandomLogHostDssmBigramsQueryDerivativeMaxMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L724">RandomLogHostDssmQueryCountryToUrlEstimatedDistanceMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L725">RandomLogHostMetaWeb764Web1076ProductInvAvgMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L726">RandomLogHostTextFeaturesLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L727">RandomLogHostDocLenLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L728">RandomLogHostIsHTMLLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L729">RandomLogHostHasLevensht1QueryFragmentLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L730">RandomLogHostHeadingIdfSumFixedLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L731">RandomLogHostAdvPronounsPortionLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L732">RandomLogHostLongestTextLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L733">RandomLogHostCountryHourLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L734">RandomLogHostMetrikaUrlAvgTimeLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L735">RandomLogHostWikiLinkCountLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L736">RandomLogHostBrowserUrlDwellTimeRegionFrcLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L737">RandomLogHostWikiInfoboxLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L738">RandomLogHostQueryDocTitleRangesMatchingScoreLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L739">RandomLogHostIsMobileBeautyLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L740">RandomLogHostQueryToTextAllSumWFSumWBodyMinWindowSizeLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L741">RandomLogHostDssmRandomLogQueryAvgDifferentInternalLinksLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L742">RandomLogHostMetaUrlDirectChildrenCntLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L743">RandomLogHostMetaWeb1241Web1299ProductInvPosLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L744">RandomLogHostMetaEpsHashShareNationalLanguageLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L745">DwellTimeSumFractionPercentale25Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L746">VideoDistributor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L747">AverageReturnTimePercentale99Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L748">AverageReturnTimePercentale97Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L749">AverageReturnTimeGreaterFraction99Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L750">AverageLogReturnTimePercentale99Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L751">AverageLogReturnTimeGreaterFraction90Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L752">FirstClickDwellTimeLessFraction5Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L753">AverageVisitsPer3HoursWeightedAverageAggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L754">LegalPlayers</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L755">SocialNetworksPlayers</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L756">AverageDwellTimePerHourWeightedAverageAggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L757">AverageDwellTimePer3HoursLessFraction10Aggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L758">AverageDwellTimePerWeekMaxAggr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L759">RandomLogOwnerRandomLogWordMaxMetaNumUrlsPerHostFixedPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L760">RandomLogOwnerMetaWeb1099Web1219ProductInvPosLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L761">RandomLogOwnerDssmDwelltimeRegChainTrainedEmbeddingPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L762">RandomLogOwnerDssmRandomLogQueryAvgHasPaymentsLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L763">RandomLogOwnerUBLongPeriodBrowseFrcPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L764">RandomLogOwnerMetaUrlChildrenCntLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L765">RandomLogOwnerMetaRmsDifferentInternalLinksPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L766">RandomLogOwnerRandomLogWordMaxHasNoTrPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L767">RandomLogOwnerMetaResidUSLongPeriodUrlWinsProbRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L768">RandomLogOwnerPornoQueryLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L769">RandomLogOwnerNationalLanguageLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L770">RandomLogOwnerPercentVisibleContentPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L771">RandomLogOwnerMetaWeb1241Web1299ProductInvPosPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L772">RandomLogOwnerLinkAnnFloatMultiplicityAttenV1Bm15K001LogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L773">RandomLogOwnerUBLongPeriodLeavesCntRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L774">RandomLogOwnerNumLinksFromMPLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L775">RandomLogOwnerDssmRandomLogQueryAvgDifferentInternalLinksPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L776">RandomLogOwnerIsOrgRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L777">RandomLogOwnerQSegmentsBM25Max</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L778">RandomLogOwnerSegmentAuxAlphasInTextRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L779">RandomLogOwnerRandomLogQueryDwelltimeWeightedAvgUrlDomainFractionLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L780">RandomLogOwnerRandomLogWordSkipStopWordsMaxIsDesktopRequestLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L781">RandomLogOwnerVisitsFromWikiRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L782">RandomLogOwnerIsTextRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L783">RandomLogOwnerDBMSubstantiveMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L784">RandomLogOwnerDaterStatsAverageSourceSegmentRmse</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L785">RandomLogOwnerIsMobileBeautyLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L786">RandomLogOwnerLongClickSPMixMatchWeightedValuePerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L787">RandomLogOwnerFemAndMasNounsPortionLogAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L788">RandomLogOwnerTrigramsProbPerc90</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L789">RandomLogOwnerDaterStatsYearNormLikelihoodPerc25</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L790">RandomLogOwnerUrlPathAndParamsFractionMax</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L791">IsMobileBeautyHost</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L792">WebFreshHostAvg30DaysSurplus</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L793">WebFreshHost30DaysPositiveSurplusRate</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L794">MascotVisitorsLogNorm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L795">RandomComm</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L796">QueriesRatioMorda2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L797">SerpClicksByHopPart_0_30</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L798">QueriesAvgTop</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L799">TrafgraphMobileDesktopSE_share</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L800">TrafgraphMobileDesktopOutAll_share</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L801">AvgIsOrg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L802">AvgQsFPunctBlanksRat</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L803">VideoDistributorProd</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L804">MemorandumWeight</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L807">HostHasFeedUrls</a></b>  <i>float</i>
<p> 431 deprecated  432 deprecated </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L808">EcomKernel1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L809">EcomKernel2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L810">EcomKernel3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L811">NumSovetnik</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L812">HostIsMarketOffer</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L813">MedicalHostQuality</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L814">OwnerIsActualShop</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L815">OwnerIsService</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L816">ReservedFreeForAll2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L817">RcSpylogCountersVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L818">RcSpylogCountersTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L819">RcSpylogCounter0</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L820">RcSpylogCounter1</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L821">RcSpylogCounter2</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L822">RcSpylogCounter3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L823">TrafgraphOutAll_share_d</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L824">TrafgraphOutAll_share_m</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L825">TrafgraphOutAllSE_share_d</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L826">TrafgraphOutAllSE_share_m</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L827">NoExtClicksShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L828">More120SecVisitsNotSearchShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L829">VisitsPVisitors</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L830">MarketQualityRating</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L831">OwnerIsPartner</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L832">DistributorHosts</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L833">PayDetectorPredictAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L834">OneProductProbabilityAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L835">ManyProductsProbabilityAvg</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L836">ReservedFreeForAll3</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L837">HostIsEcomPurchase</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L838">HostIsVisitLogsPurchase</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L839">OwnerIsEcomPurchase</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L840">OwnerIsVisitLogsPurchase</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L841">MedicalHostQualityMetric</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L842">MedicalHostQualityFresh</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L843">Medical2HostQuality</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L844">Medical2HostQualityFresh</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L845">SosHostQuality</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L846">SosHostQualityFresh</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L847">FinLawHostQuality</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L848">FinLawHostQualityFresh</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L849">OwnerUserLeakage</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L850">PageQualityHost</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/web_factors.proto?rev=r9795881#L851">IsMusicYandexRu</a></b>  <i>bool</i>
<p> next tag is 478 </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L407">DirectBannersLogUpdateTime</a></b>  <i>uint64</i>
<p> without regular reexport (full_export_flag) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L408">DirectBannersLogTouchTime</a></b>  <i>uint64</i>
<p> including regular reexport </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L410">FeedID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L411">FilterID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L413">EssLeadButton</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L143">TVersionedLeadButton</a></i>
</li>
<details open><summary><b>Message TVersionedLeadButton</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L144">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_lead_button.proto?rev=r9795881#L8">LeadButton</a></i>
</li>
<details open><summary><b>Message LeadButton</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_lead_button.proto?rev=r9795881#L9">href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_lead_button.proto?rev=r9795881#L10">text</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L145">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L414">SpravCompany</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L254">TSpravCompany</a></i>
</li>
<details open><summary><b>Message TSpravCompany</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L255">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L256">ReviewsLink</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L257">ReviewsCount</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L258">UpdateTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L259">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L260">WorkIntervals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L271">WorkInterval</a></i>
</li>
<details open><summary><b>Message WorkInterval</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L284">day</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L272">Day</a></i>
</li>
<details open><summary><b>Enum Day</b></summary>
<ul>
<li><span style="color:#1D7373">Monday</span></li>
<li><span style="color:#1D7373">Tuesday</span></li>
<li><span style="color:#1D7373">Wednesday</span></li>
<li><span style="color:#1D7373">Thursday</span></li>
<li><span style="color:#1D7373">Friday</span></li>
<li><span style="color:#1D7373">Saturday</span></li>
<li><span style="color:#1D7373">Sunday</span></li>
<li><span style="color:#1D7373">Weekdays</span></li>
<li><span style="color:#1D7373">Weekend</span></li>
<li><span style="color:#1D7373">Everyday</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L286">time_minutes_begin</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L288">time_minutes_end</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L261">CompanyUrls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L248">TSpravCompanyUrl</a></i>
<p> urls in SpravDict </p>

</li>
<details open><summary><b>Message TSpravCompanyUrl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L249">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company.proto?rev=r9795881#L165">Type</a></i>
</li>
<details open><summary><b>Enum Type</b></summary>
<ul>
<li><span style="color:#1D7373">Main</span></li>
<li><span style="color:#1D7373">Alternative</span></li>
<li><span style="color:#1D7373">Mirror</span></li>
<li><span style="color:#1D7373">Social</span></li>
<li><span style="color:#1D7373">Attribution</span></li>
<li><span style="color:#1D7373">Showtimes</span></li>
<li><span style="color:#1D7373">Booking</span></li>
<li><span style="color:#1D7373">Mining</span></li>
<li><span style="color:#1D7373">Menu</span></li>
<li><span style="color:#1D7373">Deeplink</span></li>
<li><span style="color:#1D7373">ChainBranch</span></li>
<li><span style="color:#1D7373">Ymapsbm</span></li>
<li><span style="color:#1D7373">DeliveryService</span></li>
<li><span style="color:#1D7373">GiftCertificate</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L250">Value</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L251">Legality</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/sprav/protos/company_enums.proto?rev=r9795881#L83">Legality</a></i>
</li>
<details open><summary><b>Enum Legality</b></summary>
<ul>
<li><span style="color:#1D7373">Legal</span></li>
<li><span style="color:#1D7373">Illegal</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L415">RknBannerHash</a></b>  <i>uint64</i>
<p> check if there were changes needed for resend </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L416">BrowserRating</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L299">TBrowserRating</a></i>
</li>
<details open><summary><b>Message TBrowserRating</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L300">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L301">RatingsCount</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L417">Realty</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L304">TRealty</a></i>
</li>
<details open><summary><b>Message TRealty</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L305">Address</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L418">OrgRegDate</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L419">BannerPriceStats</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L308">TBannerPriceStats</a></i>
</li>
<details open><summary><b>Message TBannerPriceStats</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L309">AvgBannerPriceMonthly</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L310">AvgBannerPriceSqrMonthly</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L311">LastPrice</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L312">UpdateTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L313">LastCurrency</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L420">EssMulticardSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L148">TVersionedMulticardSet</a></i>
</li>
<details open><summary><b>Message TVersionedMulticardSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L149">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L10">MulticardSet</a></i>
</li>
<details open><summary><b>Message MulticardSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L11">cards</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L16">Multicard</a></i>
</li>
<details open><summary><b>Message Multicard</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L17">order</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L18">image</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L19">text</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L20">href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L21">mds_meta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L22">price</a></b>  <i>uint64</i>
<p> цена товара рекламодателя в единицах валюты, не микродоли </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L23">price_old</a></b>  <i>uint64</i>
<p> старая цена товара рекламодателя в единицах валюты </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L24">currency</a></b>  <i>string</i>
<p> код валюты цены товара </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L12">multicard_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L27">MulticardType</a></i>
</li>
<details open><summary><b>Enum MulticardType</b></summary>
<ul>
<li><span style="color:#1D7373">TYPE_OTHER</span></li>
<li><span style="color:#1D7373">TYPE_PRODUCT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_multicard_set.proto?rev=r9795881#L13">button_text</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L150">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L421">OrgAspects</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L294">TOrgAspects</a></i>
</li>
<details open><summary><b>Message TOrgAspects</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L295">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L296">Scores</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L424">OriginalHref</a></b>  <i>bytes</i>
<p> if href is a tracking url, then this is the original href before canonization </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L426">CanonizedHref</a></b>  <i>bytes</i>
<p> ... and CanonizedUrl - after canonization </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L427">Sitelinks</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L428">OriginalSitelinks</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L429">CanonizedSitelinks</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L430">OrgTopAspect</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L431">NearestStation</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L432">EssPromoExtension</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L153">TVersionedPromoExtension</a></i>
</li>
<details open><summary><b>Message TVersionedPromoExtension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L154">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L8">PromoExtension</a></i>
</li>
<details open><summary><b>Message PromoExtension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L9">promo_extension_id</a></b>  <i>uint64</i>
<p> Идентификатор промоакции </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L10">description</a></b>  <i>string</i>
<p> Текст промоакции </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L11">href</a></b>  <i>string</i>
<p> Ссылка на промоакцию </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L12">start_time</a></b>  <i>uint64</i>
<p> Время начала промоакции, по факту дата </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L13">finish_time</a></b>  <i>uint64</i>
<p> Время окончания промоакции, по факту дата </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_promo_extension.proto?rev=r9795881#L14">type</a></b>  <i>uint32</i>
<p> Тип, соответствует PromoExtensionType </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L155">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L433">MarketModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L276">TMarketModel</a></i>
</li>
<details open><summary><b>Message TMarketModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L278">MarketModelDictPart</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_model_dict.proto?rev=r9795881#L7">TMarketModel</a></i>
<p> data we fill from dyn table </p>

</li>
<details open><summary><b>Message TMarketModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_model_dict.proto?rev=r9795881#L8">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_model_dict.proto?rev=r9795881#L9">PictureHeight</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_model_dict.proto?rev=r9795881#L10">PictureWidth</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_model_dict.proto?rev=r9795881#L11">PictureUrl</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L279">UpdateTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L281">MarketModelSummaryReviews</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L264">TMarketModelSummaryReviews</a></i>
<p> 3 factors with max value </p>

</li>
<details open><summary><b>Message TMarketModelSummaryReviews</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L265">Value</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L266">FactorName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L282">MarketModelRating</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L269">TMarketModelRating</a></i>
</li>
<details open><summary><b>Message TMarketModelRating</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L270">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L271">RatingsCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L272">ReviewsCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L273">Url</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L283">VendorID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L284">VendorName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L285">CategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L286">CategoryName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L287">BoughtNTimes</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L288">CustomersChoice</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L289">ViewedNTimes</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L290">Features</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L291">FeaturesUpdateTimestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L434">AppData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L181">TAppData</a></i>
</li>
<details open><summary><b>Message TAppData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L182">BundleId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L183">SourceID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L184">RegionName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L185">LocaleName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L186">Timestamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L436">EssMetrikaSnippetZen</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L316">TVersionedMetrikaSnippetZen</a></i>
</li>
<details open><summary><b>Message TVersionedMetrikaSnippetZen</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L317">Value</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_metrika_snippet.proto?rev=r9795881#L8">MetrikaSnippet</a></i>
</li>
<details open><summary><b>Message MetrikaSnippet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_metrika_snippet.proto?rev=r9795881#L9">counter</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/banner_resources/banner_metrika_snippet.proto?rev=r9795881#L10">goal</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L318">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L437">EssPublisherItemId</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L25">TVersionedBytes</a></i>
</li>
<details open><summary><b>Message TVersionedBytes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L26">Value</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L27">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L439">EssShowTitleAndBody</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L158">TVersionedShowTitleAndBody</a></i>
</li>
<details open><summary><b>Message TVersionedShowTitleAndBody</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L159">Value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L160">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L440">DeeplinksFlags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L97">TDeeplinksFlags</a></i>
</li>
<details open><summary><b>Message TDeeplinksFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L98">EnableAppGallery</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L99">EnableAppGet</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L100">EnableGalaxyStore</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L101">Timestamp</a></b>  <i>fixed32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L441">PreviousTargetDomainIDUpdate</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/target_domain_id_update.proto?rev=r9795881#L3">TTargetDomainIDUpdate</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDUpdate</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/target_domain_id_update.proto?rev=r9795881#L4">OrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/target_domain_id_update.proto?rev=r9795881#L7">TimeStamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/target_domain_id_update.proto?rev=r9795881#L8">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/target_domain_id_update.proto?rev=r9795881#L9">Sign</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L442">IsPromoBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L443">AlternativeTexts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L321">TAlternativeText</a></i>
</li>
<details open><summary><b>Message TAlternativeText</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L322">Version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L323">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L324">Body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L325">Embeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
</li>
<details open><summary><b>Message TEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L7">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L9">VectorID</a></b>  <i>uint64</i>
<p> https://wiki.yandex-team.ru/adsquality/car-reglament/ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L11">Vector</a></b>  <i>float</i>
<p> factors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L13">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/compress_vectors/proto/compress_info.proto?rev=r9795881#L5">ECompressionType</a></i>
</li>
<details open><summary><b>Enum ECompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">NO_COMPRESSION</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_24_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_28_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_200_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_V2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_RANK_LOSS_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_65_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_IMAGES_DSSM_APPLIER_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_QUORUM_66_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_NEW_QUORUM_67_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_BANNER_RELEV_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_136_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_JULY_4_76_UNIFORM_8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L14">CompressedVector</a></b>  <i>bytes</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L444">GoodsRating</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L241">TGoodsRating</a></i>
</li>
<details open><summary><b>Message TGoodsRating</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L242">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L243">GradesCount</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L244">ReviewsCount</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L245">IsValidated</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L446">DefaultTitleEmbeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
</li>
<details open><summary><b>Message TEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L7">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L9">VectorID</a></b>  <i>uint64</i>
<p> https://wiki.yandex-team.ru/adsquality/car-reglament/ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L11">Vector</a></b>  <i>float</i>
<p> factors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L13">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/compress_vectors/proto/compress_info.proto?rev=r9795881#L5">ECompressionType</a></i>
</li>
<details open><summary><b>Enum ECompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">NO_COMPRESSION</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_24_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_28_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_200_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_V2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_RANK_LOSS_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_65_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_IMAGES_DSSM_APPLIER_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_QUORUM_66_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_NEW_QUORUM_67_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_BANNER_RELEV_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_136_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_JULY_4_76_UNIFORM_8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L14">CompressedVector</a></b>  <i>bytes</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L564">TsarVectors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L17">TEmbeddings</a></i>
</li>
<details open><summary><b>Message TEmbeddings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L18">Vectors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
</li>
<details open><summary><b>Message TEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L7">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L9">VectorID</a></b>  <i>uint64</i>
<p> https://wiki.yandex-team.ru/adsquality/car-reglament/ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L11">Vector</a></b>  <i>float</i>
<p> factors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L13">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/compress_vectors/proto/compress_info.proto?rev=r9795881#L5">ECompressionType</a></i>
</li>
<details open><summary><b>Enum ECompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">NO_COMPRESSION</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_24_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_28_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_200_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_V2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_RANK_LOSS_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_65_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_IMAGES_DSSM_APPLIER_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_QUORUM_66_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_NEW_QUORUM_67_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_BANNER_RELEV_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_136_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_JULY_4_76_UNIFORM_8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L14">CompressedVector</a></b>  <i>bytes</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L565">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L451">TFlags</a></i>
</li>
<details open><summary><b>Message TFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L452">Stop</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L453">Archive</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L454">Version</a></b>  <i>uint64</i>
<p> IterID in Direct, DeltaTimestamp in BannerLand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L455">Source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_source.proto?rev=r9795881#L6">EBannerSource</a></i>
</li>
<details open><summary><b>Enum EBannerSource</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">DIRECT</span></li>
<li><span style="color:#1D7373">BANNER_LAND_DYNAMIC</span></li>
<li><span style="color:#1D7373">BANNER_LAND_SMART</span></li>
<li><span style="color:#1D7373">TMP_MODADVERT_BANNER_TEXTS</span></li>
<li><span style="color:#1D7373">TMP_MODADVERT_BANNER_VERDICT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L456">EngineID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L457">IsGenocided</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L458">LastOrderArchiveCheckedTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L459">SetArchiveByOrderTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L460">OrderStopTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L461">IsFromGrut</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L462">IsReady</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L463">FirstSeenInCaesarTimestamp</a></b>  <i>uint64</i>
<p> without history. Filled from 2021-12-xx </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L464">FirstActiveTimestamp</a></b>  <i>uint64</i>
<p> not included Order active flag. without history. Filled from 2021-12-xx </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L465">LastActiveTimestamp</a></b>  <i>uint64</i>
<p> not included Order active flag. without history. Filled from 2021-12-xx </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L466">GenocideRate</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L467">GenocideRateV2</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L468">OrderUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L470">RemovalTimestamp</a></b>  <i>fixed32</i>
<p> The time when object was removed from GrUT. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L472">GrutVersion</a></b>  <i>uint64</i>
<p> Grut Object Version. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L474">ShowPlatformChangeTimestamp</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L475">ShowPlatform</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/enums/campaign_platform.proto?rev=r9795881#L9">ECampaignPlatform</a></i>
</li>
<details open><summary><b>Enum ECampaignPlatform</b></summary>
<p> Типы площадок для показа. </p>

<ul>
<li><span style="color:#1D7373">CP_UNKNOWN</span></li>
<li><span style="color:#1D7373">CP_SEARCH</span></li>
<li><span style="color:#1D7373">CP_PARTNER</span></li>
<li><span style="color:#1D7373">CP_BOTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L476">StopFlagUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L478">GenocideRateV3</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L479">LastCandidatesCheck</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L566">OrderID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L567">BroadPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L485">TBroadPhrases</a></i>
</li>
<details open><summary><b>Message TBroadPhrases</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L486">Values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L16">TBroadPhrase</a></i>
<p> broadphrases of this banner. Incluing ids, normtype and text. </p>

</li>
<details open><summary><b>Message TBroadPhrase</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L17">BroadPhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L18">SimDistance</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L19">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L21">Timestamp</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L22">UpdateTime</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L25">NormType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L6">ENormType</a></i>
</li>
<details open><summary><b>Enum ENormType</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/norm_type.h </p>

<ul>
<li><span style="color:#1D7373">NoneType</span></li>
<li><span style="color:#1D7373">Norm</span></li>
<li><span style="color:#1D7373">Snorm</span></li>
<li><span style="color:#1D7373">Offer</span></li>
<li><span style="color:#1D7373">OfferGroup</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L26">PhraseData</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L568">BannerLandFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L482">TBannerLandFields</a></i>
<p> UNUSED </p>

</li>
<details open><summary><b>Message TBannerLandFields</b></summary>
<p> UNUSED </p>

<ul>
<span>empty</span>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L569">ModerationData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L489">TModerationData</a></i>
</li>
<details open><summary><b>Message TModerationData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L490">TimestampMilliseconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L492">MarkupFlags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/markup_flags.proto?rev=r9795881#L81">EMarkupFlag</a></i>
</li>
<details open><summary><b>Enum EMarkupFlag</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_RU</span></li>
<li><span style="color:#1D7373">REGION_KZ</span></li>
<li><span style="color:#1D7373">REGION_UA</span></li>
<li><span style="color:#1D7373">REGION_RB</span></li>
<li><span style="color:#1D7373">REGION_TR</span></li>
<li><span style="color:#1D7373">REGION_UZ</span></li>
<li><span style="color:#1D7373">REGION_OTHER</span></li>
<li><span style="color:#1D7373">DIETARYSUPPL</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON</span></li>
<li><span style="color:#1D7373">FINANCE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PROJECT_DECLARATION</span></li>
<li><span style="color:#1D7373">MED_SERVICES</span></li>
<li><span style="color:#1D7373">MED_EQUIPMENT</span></li>
<li><span style="color:#1D7373">PHARMACY</span></li>
<li><span style="color:#1D7373">SUGARING</span></li>
<li><span style="color:#1D7373">LOAN</span></li>
<li><span style="color:#1D7373">INSURANCE</span></li>
<li><span style="color:#1D7373">BANKS</span></li>
<li><span style="color:#1D7373">MATERNITY_CAPITAL</span></li>
<li><span style="color:#1D7373">PAWNSHOP</span></li>
<li><span style="color:#1D7373">CREDIT_CONSUMER_COOPERATIVE</span></li>
<li><span style="color:#1D7373">MFI</span></li>
<li><span style="color:#1D7373">PAYMENT</span></li>
<li><span style="color:#1D7373">FOREX</span></li>
<li><span style="color:#1D7373">FOREX_BROKER</span></li>
<li><span style="color:#1D7373">BINARY_OPTIONS</span></li>
<li><span style="color:#1D7373">CHARITY</span></li>
<li><span style="color:#1D7373">GAMBLE</span></li>
<li><span style="color:#1D7373">LOTTERY</span></li>
<li><span style="color:#1D7373">TOBACCO_EX</span></li>
<li><span style="color:#1D7373">OPTICS</span></li>
<li><span style="color:#1D7373">POPULAR_MEDICINE</span></li>
<li><span style="color:#1D7373">NOT_MEDICINE</span></li>
<li><span style="color:#1D7373">ACIDS</span></li>
<li><span style="color:#1D7373">ALCOHOL_ALLOWED</span></li>
<li><span style="color:#1D7373">BOOKMAKER</span></li>
<li><span style="color:#1D7373">REALTOR</span></li>
<li><span style="color:#1D7373">ELECTRONIC_OSAGO</span></li>
<li><span style="color:#1D7373">TATTOO</span></li>
<li><span style="color:#1D7373">JEWELRY</span></li>
<li><span style="color:#1D7373">COLLECTOR</span></li>
<li><span style="color:#1D7373">CERTIFICATION</span></li>
<li><span style="color:#1D7373">DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">OTHER</span></li>
<li><span style="color:#1D7373">LEGAL_VAPE</span></li>
<li><span style="color:#1D7373">SOCIAL_ADVERTISING</span></li>
<li><span style="color:#1D7373">VETERINARY_PHARMACY</span></li>
<li><span style="color:#1D7373">ABORTION</span></li>
<li><span style="color:#1D7373">MEDICINE</span></li>
<li><span style="color:#1D7373">ALCOHOL</span></li>
<li><span style="color:#1D7373">TOBACCO</span></li>
<li><span style="color:#1D7373">ILLEGAL</span></li>
<li><span style="color:#1D7373">ASOCIAL</span></li>
<li><span style="color:#1D7373">UNFAMILY</span></li>
<li><span style="color:#1D7373">TRAGIC</span></li>
<li><span style="color:#1D7373">MATCHMAKING</span></li>
<li><span style="color:#1D7373">SUSPICIOUS</span></li>
<li><span style="color:#1D7373">ANNOYING</span></li>
<li><span style="color:#1D7373">GOODFACE</span></li>
<li><span style="color:#1D7373">DIPLOMA</span></li>
<li><span style="color:#1D7373">GAMBLE_ONLINE</span></li>
<li><span style="color:#1D7373">TOBACCO_PROHIBITED</span></li>
<li><span style="color:#1D7373">ILLEGAL_DIET</span></li>
<li><span style="color:#1D7373">DRUGS</span></li>
<li><span style="color:#1D7373">TELEMED</span></li>
<li><span style="color:#1D7373">ALCOHOL_PROHIBITED</span></li>
<li><span style="color:#1D7373">MAGIC</span></li>
<li><span style="color:#1D7373">CSW_DISCLAIMER</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE</span></li>
<li><span style="color:#1D7373">AD_ON_TRANSPORT</span></li>
<li><span style="color:#1D7373">ANIMATED</span></li>
<li><span style="color:#1D7373">NOT_ANIMATED</span></li>
<li><span style="color:#1D7373">COLLECTOR_DISCLAIMER</span></li>
<li><span style="color:#1D7373">GAMBLE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">NO_SSP</span></li>
<li><span style="color:#1D7373">MFA</span></li>
<li><span style="color:#1D7373">RELIGION</span></li>
<li><span style="color:#1D7373">GDPR</span></li>
<li><span style="color:#1D7373">NO_WW</span></li>
<li><span style="color:#1D7373">UNDERWEAR</span></li>
<li><span style="color:#1D7373">DETECTIVE</span></li>
<li><span style="color:#1D7373">DYNAMIC_HOMONYMY</span></li>
<li><span style="color:#1D7373">EXPLOSIONS</span></li>
<li><span style="color:#1D7373">FINANCE</span></li>
<li><span style="color:#1D7373">GAME_VALUES</span></li>
<li><span style="color:#1D7373">HTML5_MARK</span></li>
<li><span style="color:#1D7373">MISSPELLING</span></li>
<li><span style="color:#1D7373">NO_FEED_PICTURE</span></li>
<li><span style="color:#1D7373">MED_CLOTHES</span></li>
<li><span style="color:#1D7373">ORTHOPEDICS</span></li>
<li><span style="color:#1D7373">NO_WEAPON</span></li>
<li><span style="color:#1D7373">PLUS18</span></li>
<li><span style="color:#1D7373">RAPID_ENRICHMENT</span></li>
<li><span style="color:#1D7373">SMI</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_QUALITY</span></li>
<li><span style="color:#1D7373">PERSONAL_CHARITY</span></li>
<li><span style="color:#1D7373">NOT_RU_LANG</span></li>
<li><span style="color:#1D7373">NO_TG</span></li>
<li><span style="color:#1D7373">NO_TOBACCO</span></li>
<li><span style="color:#1D7373">FEED_TG_APPROVED</span></li>
<li><span style="color:#1D7373">FEED_TG_FAILED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_APPROVED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_FAILED</span></li>
<li><span style="color:#1D7373">TRANSPORT</span></li>
<li><span style="color:#1D7373">WEAPONS</span></li>
<li><span style="color:#1D7373">BABY_FOOD0</span></li>
<li><span style="color:#1D7373">BABY_FOOD1</span></li>
<li><span style="color:#1D7373">BABY_FOOD2</span></li>
<li><span style="color:#1D7373">BABY_FOOD3</span></li>
<li><span style="color:#1D7373">BABY_FOOD4</span></li>
<li><span style="color:#1D7373">BABY_FOOD5</span></li>
<li><span style="color:#1D7373">BABY_FOOD6</span></li>
<li><span style="color:#1D7373">BABY_FOOD7</span></li>
<li><span style="color:#1D7373">BABY_FOOD8</span></li>
<li><span style="color:#1D7373">BABY_FOOD9</span></li>
<li><span style="color:#1D7373">BABY_FOOD10</span></li>
<li><span style="color:#1D7373">BABY_FOOD11</span></li>
<li><span style="color:#1D7373">BABY_FOOD12</span></li>
<li><span style="color:#1D7373">AGE0</span></li>
<li><span style="color:#1D7373">AGE6</span></li>
<li><span style="color:#1D7373">AGE12</span></li>
<li><span style="color:#1D7373">AGE16</span></li>
<li><span style="color:#1D7373">AGE18</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS0</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS1</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS2</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS3</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS9</span></li>
<li><span style="color:#1D7373">YA_PAGES_REMOVE</span></li>
<li><span style="color:#1D7373">YA_PAGES_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_DZEN_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_ANYWHERE</span></li>
<li><span style="color:#1D7373">RKN</span></li>
<li><span style="color:#1D7373">AD_BLOCK</span></li>
<li><span style="color:#1D7373">AUTO_SEO</span></li>
<li><span style="color:#1D7373">AVIA</span></li>
<li><span style="color:#1D7373">BUILDING</span></li>
<li><span style="color:#1D7373">CASINO</span></li>
<li><span style="color:#1D7373">CHILDREN</span></li>
<li><span style="color:#1D7373">COUNTERFEIT</span></li>
<li><span style="color:#1D7373">DIET</span></li>
<li><span style="color:#1D7373">EDUCATION</span></li>
<li><span style="color:#1D7373">FOR_UPDATE</span></li>
<li><span style="color:#1D7373">LAW</span></li>
<li><span style="color:#1D7373">MASSAGE</span></li>
<li><span style="color:#1D7373">MEDIA_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PEOPLE</span></li>
<li><span style="color:#1D7373">POLITICS</span></li>
<li><span style="color:#1D7373">PORNO</span></li>
<li><span style="color:#1D7373">SEX</span></li>
<li><span style="color:#1D7373">SPAM</span></li>
<li><span style="color:#1D7373">SPY</span></li>
<li><span style="color:#1D7373">TM</span></li>
<li><span style="color:#1D7373">TOUR_OPERATORS</span></li>
<li><span style="color:#1D7373">FINANCE_INTERMEDIARY</span></li>
<li><span style="color:#1D7373">NOT_COMMERCIAL_ADV</span></li>
<li><span style="color:#1D7373">ADULT</span></li>
<li><span style="color:#1D7373">CAR_NUMBERS</span></li>
<li><span style="color:#1D7373">COOP_WARN</span></li>
<li><span style="color:#1D7373">COPYRIGHT</span></li>
<li><span style="color:#1D7373">CRYPTOCURRENCY</span></li>
<li><span style="color:#1D7373">DETECTIVE_EQUIPMENT</span></li>
<li><span style="color:#1D7373">DIRECTMOD_DICT</span></li>
<li><span style="color:#1D7373">DISCOUNT</span></li>
<li><span style="color:#1D7373">EGE</span></li>
<li><span style="color:#1D7373">ETHYL</span></li>
<li><span style="color:#1D7373">FILTER_FOR_PERFORMANCE</span></li>
<li><span style="color:#1D7373">FOREIGN_TRADE</span></li>
<li><span style="color:#1D7373">GOOD_ANIMATION</span></li>
<li><span style="color:#1D7373">MEDIATION</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE2</span></li>
<li><span style="color:#1D7373">MODERATEBADWORDTYPE</span></li>
<li><span style="color:#1D7373">NO_DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">NO_DYNAMIC_CREATIVE</span></li>
<li><span style="color:#1D7373">NOTARY</span></li>
<li><span style="color:#1D7373">PIRACY</span></li>
<li><span style="color:#1D7373">PROMOTIONAL_ACTIVITIES</span></li>
<li><span style="color:#1D7373">PSEUDOSEX</span></li>
<li><span style="color:#1D7373">REGION_OTHERS</span></li>
<li><span style="color:#1D7373">SECURITY</span></li>
<li><span style="color:#1D7373">SEO</span></li>
<li><span style="color:#1D7373">SOFTWARE</span></li>
<li><span style="color:#1D7373">SPORTS_NUTRITION</span></li>
<li><span style="color:#1D7373">STRIPTEASE</span></li>
<li><span style="color:#1D7373">STUDY</span></li>
<li><span style="color:#1D7373">TECH_INSPECTION</span></li>
<li><span style="color:#1D7373">TELECOM</span></li>
<li><span style="color:#1D7373">VETERINARY</span></li>
<li><span style="color:#1D7373">WHITE</span></li>
<li><span style="color:#1D7373">WORK_ABROAD</span></li>
<li><span style="color:#1D7373">XRAY</span></li>
<li><span style="color:#1D7373">STOCK</span></li>
<li><span style="color:#1D7373">STOCKMANAG</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON_ACCESSORIES</span></li>
<li><span style="color:#1D7373">NON_ALCOHOL</span></li>
<li><span style="color:#1D7373">COLLECTOR_NO_CONTACTS</span></li>
<li><span style="color:#1D7373">MILITARY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L493">DataHash</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L494">CandidateDataHash</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L495">Verdict</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/moderation_units.proto?rev=r9795881#L8">EVerdict</a></i>
</li>
<details open><summary><b>Enum EVerdict</b></summary>
<ul>
<li><span style="color:#1D7373">NO</span></li>
<li><span style="color:#1D7373">YES</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L496">Result</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L23">TBannerLandVerdict</a></i>
</li>
<details open><summary><b>Message TBannerLandVerdict</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L31">Verdict</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/moderation_units.proto?rev=r9795881#L8">EVerdict</a></i>
<p> TODO: add me to top level </p>

</li>
<details open><summary><b>Enum EVerdict</b></summary>
<ul>
<li><span style="color:#1D7373">NO</span></li>
<li><span style="color:#1D7373">YES</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L32">Reasons</a></b>  <i>uint32</i>
<p> TODO: add me to top level </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L33">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/markup_flags.proto?rev=r9795881#L81">EMarkupFlag</a></i>
<p> TODO: add me to top level </p>

</li>
<details open><summary><b>Enum EMarkupFlag</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_RU</span></li>
<li><span style="color:#1D7373">REGION_KZ</span></li>
<li><span style="color:#1D7373">REGION_UA</span></li>
<li><span style="color:#1D7373">REGION_RB</span></li>
<li><span style="color:#1D7373">REGION_TR</span></li>
<li><span style="color:#1D7373">REGION_UZ</span></li>
<li><span style="color:#1D7373">REGION_OTHER</span></li>
<li><span style="color:#1D7373">DIETARYSUPPL</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON</span></li>
<li><span style="color:#1D7373">FINANCE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PROJECT_DECLARATION</span></li>
<li><span style="color:#1D7373">MED_SERVICES</span></li>
<li><span style="color:#1D7373">MED_EQUIPMENT</span></li>
<li><span style="color:#1D7373">PHARMACY</span></li>
<li><span style="color:#1D7373">SUGARING</span></li>
<li><span style="color:#1D7373">LOAN</span></li>
<li><span style="color:#1D7373">INSURANCE</span></li>
<li><span style="color:#1D7373">BANKS</span></li>
<li><span style="color:#1D7373">MATERNITY_CAPITAL</span></li>
<li><span style="color:#1D7373">PAWNSHOP</span></li>
<li><span style="color:#1D7373">CREDIT_CONSUMER_COOPERATIVE</span></li>
<li><span style="color:#1D7373">MFI</span></li>
<li><span style="color:#1D7373">PAYMENT</span></li>
<li><span style="color:#1D7373">FOREX</span></li>
<li><span style="color:#1D7373">FOREX_BROKER</span></li>
<li><span style="color:#1D7373">BINARY_OPTIONS</span></li>
<li><span style="color:#1D7373">CHARITY</span></li>
<li><span style="color:#1D7373">GAMBLE</span></li>
<li><span style="color:#1D7373">LOTTERY</span></li>
<li><span style="color:#1D7373">TOBACCO_EX</span></li>
<li><span style="color:#1D7373">OPTICS</span></li>
<li><span style="color:#1D7373">POPULAR_MEDICINE</span></li>
<li><span style="color:#1D7373">NOT_MEDICINE</span></li>
<li><span style="color:#1D7373">ACIDS</span></li>
<li><span style="color:#1D7373">ALCOHOL_ALLOWED</span></li>
<li><span style="color:#1D7373">BOOKMAKER</span></li>
<li><span style="color:#1D7373">REALTOR</span></li>
<li><span style="color:#1D7373">ELECTRONIC_OSAGO</span></li>
<li><span style="color:#1D7373">TATTOO</span></li>
<li><span style="color:#1D7373">JEWELRY</span></li>
<li><span style="color:#1D7373">COLLECTOR</span></li>
<li><span style="color:#1D7373">CERTIFICATION</span></li>
<li><span style="color:#1D7373">DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">OTHER</span></li>
<li><span style="color:#1D7373">LEGAL_VAPE</span></li>
<li><span style="color:#1D7373">SOCIAL_ADVERTISING</span></li>
<li><span style="color:#1D7373">VETERINARY_PHARMACY</span></li>
<li><span style="color:#1D7373">ABORTION</span></li>
<li><span style="color:#1D7373">MEDICINE</span></li>
<li><span style="color:#1D7373">ALCOHOL</span></li>
<li><span style="color:#1D7373">TOBACCO</span></li>
<li><span style="color:#1D7373">ILLEGAL</span></li>
<li><span style="color:#1D7373">ASOCIAL</span></li>
<li><span style="color:#1D7373">UNFAMILY</span></li>
<li><span style="color:#1D7373">TRAGIC</span></li>
<li><span style="color:#1D7373">MATCHMAKING</span></li>
<li><span style="color:#1D7373">SUSPICIOUS</span></li>
<li><span style="color:#1D7373">ANNOYING</span></li>
<li><span style="color:#1D7373">GOODFACE</span></li>
<li><span style="color:#1D7373">DIPLOMA</span></li>
<li><span style="color:#1D7373">GAMBLE_ONLINE</span></li>
<li><span style="color:#1D7373">TOBACCO_PROHIBITED</span></li>
<li><span style="color:#1D7373">ILLEGAL_DIET</span></li>
<li><span style="color:#1D7373">DRUGS</span></li>
<li><span style="color:#1D7373">TELEMED</span></li>
<li><span style="color:#1D7373">ALCOHOL_PROHIBITED</span></li>
<li><span style="color:#1D7373">MAGIC</span></li>
<li><span style="color:#1D7373">CSW_DISCLAIMER</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE</span></li>
<li><span style="color:#1D7373">AD_ON_TRANSPORT</span></li>
<li><span style="color:#1D7373">ANIMATED</span></li>
<li><span style="color:#1D7373">NOT_ANIMATED</span></li>
<li><span style="color:#1D7373">COLLECTOR_DISCLAIMER</span></li>
<li><span style="color:#1D7373">GAMBLE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">NO_SSP</span></li>
<li><span style="color:#1D7373">MFA</span></li>
<li><span style="color:#1D7373">RELIGION</span></li>
<li><span style="color:#1D7373">GDPR</span></li>
<li><span style="color:#1D7373">NO_WW</span></li>
<li><span style="color:#1D7373">UNDERWEAR</span></li>
<li><span style="color:#1D7373">DETECTIVE</span></li>
<li><span style="color:#1D7373">DYNAMIC_HOMONYMY</span></li>
<li><span style="color:#1D7373">EXPLOSIONS</span></li>
<li><span style="color:#1D7373">FINANCE</span></li>
<li><span style="color:#1D7373">GAME_VALUES</span></li>
<li><span style="color:#1D7373">HTML5_MARK</span></li>
<li><span style="color:#1D7373">MISSPELLING</span></li>
<li><span style="color:#1D7373">NO_FEED_PICTURE</span></li>
<li><span style="color:#1D7373">MED_CLOTHES</span></li>
<li><span style="color:#1D7373">ORTHOPEDICS</span></li>
<li><span style="color:#1D7373">NO_WEAPON</span></li>
<li><span style="color:#1D7373">PLUS18</span></li>
<li><span style="color:#1D7373">RAPID_ENRICHMENT</span></li>
<li><span style="color:#1D7373">SMI</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_QUALITY</span></li>
<li><span style="color:#1D7373">PERSONAL_CHARITY</span></li>
<li><span style="color:#1D7373">NOT_RU_LANG</span></li>
<li><span style="color:#1D7373">NO_TG</span></li>
<li><span style="color:#1D7373">NO_TOBACCO</span></li>
<li><span style="color:#1D7373">FEED_TG_APPROVED</span></li>
<li><span style="color:#1D7373">FEED_TG_FAILED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_APPROVED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_FAILED</span></li>
<li><span style="color:#1D7373">TRANSPORT</span></li>
<li><span style="color:#1D7373">WEAPONS</span></li>
<li><span style="color:#1D7373">BABY_FOOD0</span></li>
<li><span style="color:#1D7373">BABY_FOOD1</span></li>
<li><span style="color:#1D7373">BABY_FOOD2</span></li>
<li><span style="color:#1D7373">BABY_FOOD3</span></li>
<li><span style="color:#1D7373">BABY_FOOD4</span></li>
<li><span style="color:#1D7373">BABY_FOOD5</span></li>
<li><span style="color:#1D7373">BABY_FOOD6</span></li>
<li><span style="color:#1D7373">BABY_FOOD7</span></li>
<li><span style="color:#1D7373">BABY_FOOD8</span></li>
<li><span style="color:#1D7373">BABY_FOOD9</span></li>
<li><span style="color:#1D7373">BABY_FOOD10</span></li>
<li><span style="color:#1D7373">BABY_FOOD11</span></li>
<li><span style="color:#1D7373">BABY_FOOD12</span></li>
<li><span style="color:#1D7373">AGE0</span></li>
<li><span style="color:#1D7373">AGE6</span></li>
<li><span style="color:#1D7373">AGE12</span></li>
<li><span style="color:#1D7373">AGE16</span></li>
<li><span style="color:#1D7373">AGE18</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS0</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS1</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS2</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS3</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS9</span></li>
<li><span style="color:#1D7373">YA_PAGES_REMOVE</span></li>
<li><span style="color:#1D7373">YA_PAGES_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_DZEN_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_ANYWHERE</span></li>
<li><span style="color:#1D7373">RKN</span></li>
<li><span style="color:#1D7373">AD_BLOCK</span></li>
<li><span style="color:#1D7373">AUTO_SEO</span></li>
<li><span style="color:#1D7373">AVIA</span></li>
<li><span style="color:#1D7373">BUILDING</span></li>
<li><span style="color:#1D7373">CASINO</span></li>
<li><span style="color:#1D7373">CHILDREN</span></li>
<li><span style="color:#1D7373">COUNTERFEIT</span></li>
<li><span style="color:#1D7373">DIET</span></li>
<li><span style="color:#1D7373">EDUCATION</span></li>
<li><span style="color:#1D7373">FOR_UPDATE</span></li>
<li><span style="color:#1D7373">LAW</span></li>
<li><span style="color:#1D7373">MASSAGE</span></li>
<li><span style="color:#1D7373">MEDIA_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PEOPLE</span></li>
<li><span style="color:#1D7373">POLITICS</span></li>
<li><span style="color:#1D7373">PORNO</span></li>
<li><span style="color:#1D7373">SEX</span></li>
<li><span style="color:#1D7373">SPAM</span></li>
<li><span style="color:#1D7373">SPY</span></li>
<li><span style="color:#1D7373">TM</span></li>
<li><span style="color:#1D7373">TOUR_OPERATORS</span></li>
<li><span style="color:#1D7373">FINANCE_INTERMEDIARY</span></li>
<li><span style="color:#1D7373">NOT_COMMERCIAL_ADV</span></li>
<li><span style="color:#1D7373">ADULT</span></li>
<li><span style="color:#1D7373">CAR_NUMBERS</span></li>
<li><span style="color:#1D7373">COOP_WARN</span></li>
<li><span style="color:#1D7373">COPYRIGHT</span></li>
<li><span style="color:#1D7373">CRYPTOCURRENCY</span></li>
<li><span style="color:#1D7373">DETECTIVE_EQUIPMENT</span></li>
<li><span style="color:#1D7373">DIRECTMOD_DICT</span></li>
<li><span style="color:#1D7373">DISCOUNT</span></li>
<li><span style="color:#1D7373">EGE</span></li>
<li><span style="color:#1D7373">ETHYL</span></li>
<li><span style="color:#1D7373">FILTER_FOR_PERFORMANCE</span></li>
<li><span style="color:#1D7373">FOREIGN_TRADE</span></li>
<li><span style="color:#1D7373">GOOD_ANIMATION</span></li>
<li><span style="color:#1D7373">MEDIATION</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE2</span></li>
<li><span style="color:#1D7373">MODERATEBADWORDTYPE</span></li>
<li><span style="color:#1D7373">NO_DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">NO_DYNAMIC_CREATIVE</span></li>
<li><span style="color:#1D7373">NOTARY</span></li>
<li><span style="color:#1D7373">PIRACY</span></li>
<li><span style="color:#1D7373">PROMOTIONAL_ACTIVITIES</span></li>
<li><span style="color:#1D7373">PSEUDOSEX</span></li>
<li><span style="color:#1D7373">REGION_OTHERS</span></li>
<li><span style="color:#1D7373">SECURITY</span></li>
<li><span style="color:#1D7373">SEO</span></li>
<li><span style="color:#1D7373">SOFTWARE</span></li>
<li><span style="color:#1D7373">SPORTS_NUTRITION</span></li>
<li><span style="color:#1D7373">STRIPTEASE</span></li>
<li><span style="color:#1D7373">STUDY</span></li>
<li><span style="color:#1D7373">TECH_INSPECTION</span></li>
<li><span style="color:#1D7373">TELECOM</span></li>
<li><span style="color:#1D7373">VETERINARY</span></li>
<li><span style="color:#1D7373">WHITE</span></li>
<li><span style="color:#1D7373">WORK_ABROAD</span></li>
<li><span style="color:#1D7373">XRAY</span></li>
<li><span style="color:#1D7373">STOCK</span></li>
<li><span style="color:#1D7373">STOCKMANAG</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON_ACCESSORIES</span></li>
<li><span style="color:#1D7373">NON_ALCOHOL</span></li>
<li><span style="color:#1D7373">COLLECTOR_NO_CONTACTS</span></li>
<li><span style="color:#1D7373">MILITARY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L34">MinusRegions</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L35">Timestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L36">Lang</a></b>  <i>string</i>
<p> lang of source text; ISO 639-1 format </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L37">TranslatedData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L24">TTranslatedData</a></i>
</li>
<details open><summary><b>Message TTranslatedData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L25">Lang</a></b>  <i>string</i>
<p> lang translated to; ISO 639-1 format </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L26">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L27">TitleExtension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/verdict.proto?rev=r9795881#L28">Body</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L498">SendTimestampMilliseconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L500">DynamicBannerCandidate</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L9">TDynBanner</a></i>
</li>
<details open><summary><b>Message TDynBanner</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L12">BannerID</a></b>  <i>int64</i>
<p> banner ids  key column </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L13">OrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L14">GroupExportID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L15">CampaignId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L16">DirectFeedID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L19">Title</a></b>  <i>string</i>
<p> resources </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L20">TitleExtension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L21">Body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L22">Href</a></b>  <i>string</i>
<p> Banner Url </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L23">HrefText</a></b>  <i>string</i>
<p> was: UrlText </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L24">Site</a></b>  <i>string</i>
<p> OrigDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L25">SiteID</a></b>  <i>uint64</i>
<p> OrigDomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L26">SiteFilter</a></b>  <i>string</i>
<p> OrigDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L27">SiteFilterID</a></b>  <i>uint64</i>
<p> OrigDomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L28">TargetDomain</a></b>  <i>string</i>
<p> Domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L29">TargetDomainID</a></b>  <i>uint64</i>
<p> DomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L33">CategoryIDs</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L34">LangID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L8">ELang</a></i>
</li>
<details open><summary><b>Enum ELang</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/lang_code.h </p>

<ul>
<li><span style="color:#1D7373">DEFAULT</span></li>
<li><span style="color:#1D7373">RU</span></li>
<li><span style="color:#1D7373">UK</span></li>
<li><span style="color:#1D7373">EN</span></li>
<li><span style="color:#1D7373">BY</span></li>
<li><span style="color:#1D7373">KZ</span></li>
<li><span style="color:#1D7373">TR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L35">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L36">TemplateID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L37">ClientID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L38">AllowedInProductGallery</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L43">ImagesInfoDirectFormat</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L44">BannerPrice</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L17">TBannerPrice</a></i>
</li>
<details open><summary><b>Message TBannerPrice</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L19">Price</a></b>  <i>string</i>
<p> https://direct-dev.yandex-team.ru/db/ppc/tables/banner_prices.html </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L20">OldPrice</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L21">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L22">Prefix</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L23">Discount</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L47">DisplayInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L58">TDisplayInfo</a></i>
</li>
<details open><summary><b>Message TDisplayInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L60">description_for_direct</a></b>  <i>string</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/package/plugin/settings.py?rev=7547566#L3426 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L61">business_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L62">offer_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L63">legal</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L64">sizes</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L65">sizes_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L66">consist</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L67">consist_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L68">colors</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L69">facility</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L70">facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L71">run</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L72">vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L73">model</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L74">year</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L75">location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L76">class</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L77">go_from</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L78">go_to</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L79">realty_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L80">sub_location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L81">building_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L82">metro</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L83">metro_time_on_foot</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L84">metro_time_on_transport</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L85">address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L89">engine_volume</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L90">engine_power</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L92">owners_number</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L93">color_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L7">EColor</a></i>
</li>
<details open><summary><b>Enum EColor</b></summary>
<ul>
<li><span style="color:#1D7373">COLOR_UNKNOWN</span></li>
<li><span style="color:#1D7373">COLOR_BEIGE</span></li>
<li><span style="color:#1D7373">COLOR_WHITE</span></li>
<li><span style="color:#1D7373">COLOR_COLORLESS</span></li>
<li><span style="color:#1D7373">COLOR_CYAN</span></li>
<li><span style="color:#1D7373">COLOR_YELLOW</span></li>
<li><span style="color:#1D7373">COLOR_GREEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLDEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLD</span></li>
<li><span style="color:#1D7373">COLOR_BROWN</span></li>
<li><span style="color:#1D7373">COLOR_RED</span></li>
<li><span style="color:#1D7373">COLOR_ORANGE</span></li>
<li><span style="color:#1D7373">COLOR_MAGENTA</span></li>
<li><span style="color:#1D7373">COLOR_PINK</span></li>
<li><span style="color:#1D7373">COLOR_SILVERY</span></li>
<li><span style="color:#1D7373">COLOR_SILVER</span></li>
<li><span style="color:#1D7373">COLOR_GRAY</span></li>
<li><span style="color:#1D7373">COLOR_BLUE</span></li>
<li><span style="color:#1D7373">COLOR_PURPLE</span></li>
<li><span style="color:#1D7373">COLOR_BLACK</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L94">body_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L30">EBodyType</a></i>
</li>
<details open><summary><b>Enum EBodyType</b></summary>
<ul>
<li><span style="color:#1D7373">BT_UNKNOWN</span></li>
<li><span style="color:#1D7373">BT_SEDAN_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_SEDAN</span></li>
<li><span style="color:#1D7373">BT_CABRIOLET</span></li>
<li><span style="color:#1D7373">BT_COMPACTVAN</span></li>
<li><span style="color:#1D7373">BT_COUPE_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_COUPE</span></li>
<li><span style="color:#1D7373">BT_FASTBACK</span></li>
<li><span style="color:#1D7373">BT_VAN</span></li>
<li><span style="color:#1D7373">BT_HATCHBACK</span></li>
<li><span style="color:#1D7373">BT_LANDAU</span></li>
<li><span style="color:#1D7373">BT_LIFTBACK</span></li>
<li><span style="color:#1D7373">BT_LIMOUSINE</span></li>
<li><span style="color:#1D7373">BT_MICROVAN</span></li>
<li><span style="color:#1D7373">BT_MINIVAN</span></li>
<li><span style="color:#1D7373">BT_SUV</span></li>
<li><span style="color:#1D7373">BT_PHAETON_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_PHAETON</span></li>
<li><span style="color:#1D7373">BT_PICKUP</span></li>
<li><span style="color:#1D7373">BT_ROADSTER</span></li>
<li><span style="color:#1D7373">BT_TARGA</span></li>
<li><span style="color:#1D7373">BT_SPEEDSTER</span></li>
<li><span style="color:#1D7373">BT_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_CROSSOVER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L95">gearbox_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L57">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<ul>
<li><span style="color:#1D7373">GB_UNKNOWN</span></li>
<li><span style="color:#1D7373">GB_MANUAL</span></li>
<li><span style="color:#1D7373">GB_AUTOMATIC</span></li>
<li><span style="color:#1D7373">GB_VARIATOR</span></li>
<li><span style="color:#1D7373">GB_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L96">engine_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L97">drive_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L98">state_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L100">floor</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L101">floors_total</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L102">rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L103">renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L104">building_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L105">deal_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L106">ready_quarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L107">building_state</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L108">new_flat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L109">region</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L65">ERealtyRegion</a></i>
</li>
<details open><summary><b>Enum ERealtyRegion</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW_DISTRICT</span></li>
<li><span style="color:#1D7373">REGION_LENINGRAD</span></li>
<li><span style="color:#1D7373">REGION_SVERDLOVSK</span></li>
<li><span style="color:#1D7373">REGION_KRASNODAR</span></li>
<li><span style="color:#1D7373">REGION_NOVOSIBIRSK</span></li>
<li><span style="color:#1D7373">REGION_OMSK</span></li>
<li><span style="color:#1D7373">REGION_ROSTOV</span></li>
<li><span style="color:#1D7373">REGION_SAMARA</span></li>
<li><span style="color:#1D7373">REGION_TUMEN</span></li>
<li><span style="color:#1D7373">REGION_VORONEJ</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW</span></li>
<li><span style="color:#1D7373">REGION_HABAROVSK</span></li>
<li><span style="color:#1D7373">REGION_NIJEGOROD</span></li>
<li><span style="color:#1D7373">REGION_TATARSTAN</span></li>
<li><span style="color:#1D7373">REGION_KRASNOYARSK</span></li>
<li><span style="color:#1D7373">REGION_BASHKORTOSTAN</span></li>
<li><span style="color:#1D7373">REGION_VLADIMIR</span></li>
<li><span style="color:#1D7373">REGION_CRIMEA</span></li>
<li><span style="color:#1D7373">REGION_SARATOV</span></li>
<li><span style="color:#1D7373">REGION_CHELYABINSK</span></li>
<li><span style="color:#1D7373">REGION_KOMI</span></li>
<li><span style="color:#1D7373">REGION_VOLGOGRAD</span></li>
<li><span style="color:#1D7373">REGION_ULYANOVSK</span></li>
<li><span style="color:#1D7373">REGION_TULA</span></li>
<li><span style="color:#1D7373">REGION_TVER</span></li>
<li><span style="color:#1D7373">REGION_LIPECK</span></li>
<li><span style="color:#1D7373">REGION_HANTI</span></li>
<li><span style="color:#1D7373">REGION_BELGOROD</span></li>
<li><span style="color:#1D7373">REGION_RYAZAN</span></li>
<li><span style="color:#1D7373">REGION_IRKUTSK</span></li>
<li><span style="color:#1D7373">REGION_KALUGA</span></li>
<li><span style="color:#1D7373">REGION_PENZA</span></li>
<li><span style="color:#1D7373">REGION_KEMEROV</span></li>
<li><span style="color:#1D7373">REGION_PERM</span></li>
<li><span style="color:#1D7373">REGION_YAROSLAVL</span></li>
<li><span style="color:#1D7373">REGION_KALININGRAD</span></li>
<li><span style="color:#1D7373">REGION_ALTAI</span></li>
<li><span style="color:#1D7373">REGION_STAVROPOL</span></li>
<li><span style="color:#1D7373">REGION_TOMSK</span></li>
<li><span style="color:#1D7373">REGION_ASTRAKHAN</span></li>
<li><span style="color:#1D7373">REGION_KOSTROMA</span></li>
<li><span style="color:#1D7373">REGION_UDMURTHIA</span></li>
<li><span style="color:#1D7373">REGION_IVANOVSK</span></li>
<li><span style="color:#1D7373">REGION_SMOLENSK</span></li>
<li><span style="color:#1D7373">REGION_ORENBURG</span></li>
<li><span style="color:#1D7373">REGION_CHUVASHIA</span></li>
<li><span style="color:#1D7373">REGION_KIROV</span></li>
<li><span style="color:#1D7373">REGION_MARIY_EL</span></li>
<li><span style="color:#1D7373">REGION_NOVGOROD</span></li>
<li><span style="color:#1D7373">REGION_ADIGEI</span></li>
<li><span style="color:#1D7373">REGION_PRIMORYE</span></li>
<li><span style="color:#1D7373">REGION_PSKOV</span></li>
<li><span style="color:#1D7373">REGION_BRYANSK</span></li>
<li><span style="color:#1D7373">REGION_OREL</span></li>
<li><span style="color:#1D7373">REGION_KURSK</span></li>
<li><span style="color:#1D7373">REGION_ARHANGELSK</span></li>
<li><span style="color:#1D7373">REGION_TAMBOV</span></li>
<li><span style="color:#1D7373">REGION_KURGAN</span></li>
<li><span style="color:#1D7373">REGION_VOLOGODSK</span></li>
<li><span style="color:#1D7373">REGION_KARELIYA</span></li>
<li><span style="color:#1D7373">REGION_BURYATIA</span></li>
<li><span style="color:#1D7373">REGION_NORTH_OSETIA</span></li>
<li><span style="color:#1D7373">REGION_YAMAL</span></li>
<li><span style="color:#1D7373">REGION_MORDOVIA</span></li>
<li><span style="color:#1D7373">REGION_DAGESTAN</span></li>
<li><span style="color:#1D7373">REGION_AMUR</span></li>
<li><span style="color:#1D7373">REGION_SAHA</span></li>
<li><span style="color:#1D7373">REGION_MURMANSK</span></li>
<li><span style="color:#1D7373">REGION_ZABAYKALSK</span></li>
<li><span style="color:#1D7373">REGION_KBR</span></li>
<li><span style="color:#1D7373">REGION_HAKASIA</span></li>
<li><span style="color:#1D7373">REGION_ALTAI_REPUBLIC</span></li>
<li><span style="color:#1D7373">REGION_SAKHALIN</span></li>
<li><span style="color:#1D7373">REGION_KAMCHATKA</span></li>
<li><span style="color:#1D7373">REGION_KCHR</span></li>
<li><span style="color:#1D7373">REGION_MAGADAN</span></li>
<li><span style="color:#1D7373">REGION_CHECHNYA</span></li>
<li><span style="color:#1D7373">REGION_TIVA</span></li>
<li><span style="color:#1D7373">REGION_JEWISH_AUTONOMOUS</span></li>
<li><span style="color:#1D7373">REGION_KALMIKIYA</span></li>
<li><span style="color:#1D7373">REGION_INGUSHETIA</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L48">OfferProperties</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L328">TOffer</a></i>
<p> Use tests to ensure the existence of fields in this field </p>

</li>
<details open><summary><b>Message TOffer</b></summary>
<p> *******************************  ** Id fields                 **  ** proto range from 1 to 100 **  ******************************* </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L336">BusinessId</a></b>  <i>uint32</i>
<p> Composite unique key of offer  Patner identifier in Yandex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L338">OfferId</a></b>  <i>string</i>
<p> B2B offer identifier from partner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L340">OfferYabsId</a></b>  <i>uint64</i>
<p> Hash of B2B identifier (should be unique in subset of all offers from one partner) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L342">ShopId</a></b>  <i>uint32</i>
<p> Identifier of Yandex services set (known as shop) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L346">ClientId</a></b>  <i>uint64</i>
<p> Additional identifiers  Partner identifier in accounting balance </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L348">FeedId</a></b>  <i>uint32</i>
<p> Feed identifier in B2C Yndex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L350">DirectFeedId</a></b>  <i>uint64</i>
<p> Feed identifier in Yandex.Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L351">WareMd5</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L353">OriginalSku</a></b>  <i>string</i>
<p> SKU in parnter content system </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L355">FeedItemGroupId</a></b>  <i>string</i>
<p> Id of group inside feed. Needed to create retargeting for group of e.g. iPhones 13 of different colors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L364">TimestampSeconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L367">DataType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L37">EDataType</a></i>
<p> Data type for BannerLand </p>

</li>
<details open><summary><b>Enum EDataType</b></summary>
<ul>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_MARKET</span></li>
<li><span style="color:#1D7373">DATA_TYPE_AUTORU</span></li>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_MERCHANT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_FLIGHT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_TRAVEL</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_HOTEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L370">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
<p> Offer source (feed or site) </p>

</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L373">ProductType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L68">EProductType</a></i>
<p> Product type for offer </p>

</li>
<details open><summary><b>Enum EProductType</b></summary>
<ul>
<li><span style="color:#1D7373">PRODUCT_TYPE_UNKNOWN</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AUTO_ACCESSORIES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AVIA_TICKETS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BEAUTY_HEALTH</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BUILDING_MATERIALS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CARS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHILDRENS_GOODS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHINESE_SITES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_DSE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_EXTERNAL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_FURNITURE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_GAMES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_HOTELS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_LIST</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_PROMOCODES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_REALTY</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_SPORTS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TIRES_DISKS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TRAVEL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_WEAR</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BOOKS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L375">OfferType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L64">EOfferType</a></i>
<p> Offer type </p>

</li>
<details open><summary><b>Enum EOfferType</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_TYPE_VENDOR_MODEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L378">OfferLanguage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L48">ELanguageCode</a></i>
<p> Offer texts language </p>

</li>
<details open><summary><b>Enum ELanguageCode</b></summary>
<ul>
<li><span style="color:#1D7373">LANGUAGE_UNKNOWN</span></li>
<li><span style="color:#1D7373">LANGUAGE_RU</span></li>
<li><span style="color:#1D7373">LANGUAGE_EN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L381">DisableStatus</a></b>  <i>bool</i>
<p> Is offer active </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L389">Model</a></b>  <i>string</i>
<p> Model name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L391">Vendor</a></b>  <i>string</i>
<p> Manufacturer or brand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L393">TypePrefix</a></b>  <i>string</i>
<p> Type or category name of good (used in title) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L395">Name</a></b>  <i>string</i>
<p> Full offer name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L398">Description</a></b>  <i>string</i>
<p> Detailed description of offer </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L401">Url</a></b>  <i>string</i>
<p> URL to offer on partner site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L403">UrlOriginalDomain</a></b>  <i>string</i>
<p> Domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L405">UrlOriginalDomainId</a></b>  <i>uint64</i>
<p> Id of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L407">UrlMainMirror</a></b>  <i>string</i>
<p> Main mirror (after redirects) of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L409">UrlMainMirrorId</a></b>  <i>uint64</i>
<p> Id of main mirror domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L412">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L110">TImageData</a></i>
<p> Offer images data (original URLs and avatars) </p>

</li>
<details open><summary><b>Message TImageData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L123">SourceUrl</a></b>  <i>string</i>
<p> Image URL on client site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L126">Status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L112">EAvatarizationStatus</a></i>
<p> Status of image loading into avatars service </p>

</li>
<details open><summary><b>Enum EAvatarizationStatus</b></summary>
<p> TODO: Replace with Market.DataCamp.MarketPicture.Status after complete MARKETINDEXER-41756 </p>

<ul>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_UNKNOWN</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_AVAILABLE</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_FAILED</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_REMOVED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L129">AvatarsInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
<p> Image avatars information </p>

</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L415">Currency</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L36">Currency</a></i>
<p> Offer currency </p>

</li>
<details open><summary><b>Enum Currency</b></summary>
<ul>
<li><span style="color:#1D7373">CURRENCY_UNDEFINED</span></li>
<li><span style="color:#1D7373">RUR</span></li>
<li><span style="color:#1D7373">USD</span></li>
<li><span style="color:#1D7373">EUR</span></li>
<li><span style="color:#1D7373">UAH</span></li>
<li><span style="color:#1D7373">KZT</span></li>
<li><span style="color:#1D7373">BYN</span></li>
<li><span style="color:#1D7373">GBP</span></li>
<li><span style="color:#1D7373">TRY</span></li>
<li><span style="color:#1D7373">ALL</span></li>
<li><span style="color:#1D7373">AFN</span></li>
<li><span style="color:#1D7373">ARS</span></li>
<li><span style="color:#1D7373">AWG</span></li>
<li><span style="color:#1D7373">AUD</span></li>
<li><span style="color:#1D7373">AZN</span></li>
<li><span style="color:#1D7373">BBD</span></li>
<li><span style="color:#1D7373">BZD</span></li>
<li><span style="color:#1D7373">BMD</span></li>
<li><span style="color:#1D7373">BOB</span></li>
<li><span style="color:#1D7373">BAM</span></li>
<li><span style="color:#1D7373">BWP</span></li>
<li><span style="color:#1D7373">BGN</span></li>
<li><span style="color:#1D7373">BRL</span></li>
<li><span style="color:#1D7373">BND</span></li>
<li><span style="color:#1D7373">KHR</span></li>
<li><span style="color:#1D7373">CAD</span></li>
<li><span style="color:#1D7373">KYD</span></li>
<li><span style="color:#1D7373">CLP</span></li>
<li><span style="color:#1D7373">CNY</span></li>
<li><span style="color:#1D7373">COP</span></li>
<li><span style="color:#1D7373">CRC</span></li>
<li><span style="color:#1D7373">HRK</span></li>
<li><span style="color:#1D7373">CUP</span></li>
<li><span style="color:#1D7373">CZK</span></li>
<li><span style="color:#1D7373">DKK</span></li>
<li><span style="color:#1D7373">DOP</span></li>
<li><span style="color:#1D7373">XCD</span></li>
<li><span style="color:#1D7373">EGP</span></li>
<li><span style="color:#1D7373">SVC</span></li>
<li><span style="color:#1D7373">FKP</span></li>
<li><span style="color:#1D7373">FJD</span></li>
<li><span style="color:#1D7373">GHS</span></li>
<li><span style="color:#1D7373">GIP</span></li>
<li><span style="color:#1D7373">GTQ</span></li>
<li><span style="color:#1D7373">GYD</span></li>
<li><span style="color:#1D7373">HNL</span></li>
<li><span style="color:#1D7373">HKD</span></li>
<li><span style="color:#1D7373">HUF</span></li>
<li><span style="color:#1D7373">ISK</span></li>
<li><span style="color:#1D7373">INR</span></li>
<li><span style="color:#1D7373">IDR</span></li>
<li><span style="color:#1D7373">IRR</span></li>
<li><span style="color:#1D7373">ILS</span></li>
<li><span style="color:#1D7373">JMD</span></li>
<li><span style="color:#1D7373">JPY</span></li>
<li><span style="color:#1D7373">KPW</span></li>
<li><span style="color:#1D7373">KRW</span></li>
<li><span style="color:#1D7373">KGS</span></li>
<li><span style="color:#1D7373">LAK</span></li>
<li><span style="color:#1D7373">LBP</span></li>
<li><span style="color:#1D7373">LRD</span></li>
<li><span style="color:#1D7373">MKD</span></li>
<li><span style="color:#1D7373">MYR</span></li>
<li><span style="color:#1D7373">MUR</span></li>
<li><span style="color:#1D7373">MXN</span></li>
<li><span style="color:#1D7373">MNT</span></li>
<li><span style="color:#1D7373">MAD</span></li>
<li><span style="color:#1D7373">MZN</span></li>
<li><span style="color:#1D7373">NAD</span></li>
<li><span style="color:#1D7373">NPR</span></li>
<li><span style="color:#1D7373">ANG</span></li>
<li><span style="color:#1D7373">NZD</span></li>
<li><span style="color:#1D7373">NIO</span></li>
<li><span style="color:#1D7373">NGN</span></li>
<li><span style="color:#1D7373">NOK</span></li>
<li><span style="color:#1D7373">OMR</span></li>
<li><span style="color:#1D7373">PKR</span></li>
<li><span style="color:#1D7373">PAB</span></li>
<li><span style="color:#1D7373">PYG</span></li>
<li><span style="color:#1D7373">PEN</span></li>
<li><span style="color:#1D7373">PHP</span></li>
<li><span style="color:#1D7373">PLN</span></li>
<li><span style="color:#1D7373">QAR</span></li>
<li><span style="color:#1D7373">RON</span></li>
<li><span style="color:#1D7373">SHP</span></li>
<li><span style="color:#1D7373">SAR</span></li>
<li><span style="color:#1D7373">RSD</span></li>
<li><span style="color:#1D7373">SCR</span></li>
<li><span style="color:#1D7373">SGD</span></li>
<li><span style="color:#1D7373">SBD</span></li>
<li><span style="color:#1D7373">SOS</span></li>
<li><span style="color:#1D7373">ZAR</span></li>
<li><span style="color:#1D7373">LKR</span></li>
<li><span style="color:#1D7373">SEK</span></li>
<li><span style="color:#1D7373">CHF</span></li>
<li><span style="color:#1D7373">SRD</span></li>
<li><span style="color:#1D7373">SYP</span></li>
<li><span style="color:#1D7373">TWD</span></li>
<li><span style="color:#1D7373">THB</span></li>
<li><span style="color:#1D7373">TTD</span></li>
<li><span style="color:#1D7373">AED</span></li>
<li><span style="color:#1D7373">UYU</span></li>
<li><span style="color:#1D7373">UZS</span></li>
<li><span style="color:#1D7373">VEF</span></li>
<li><span style="color:#1D7373">VND</span></li>
<li><span style="color:#1D7373">YER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L417">Price</a></b>  <i>uint64</i>
<p> Price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L419">PriceMicrosPart</a></b>  <i>uint64</i>
<p> Price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L421">OldPrice</a></b>  <i>uint64</i>
<p> Previous price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L423">OldPriceMicrosPart</a></b>  <i>uint64</i>
<p> Previous price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L426">CategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Offer categoryzation info </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L428">Breadcrumbs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L153">TBreadcrumbsData</a></i>
<p> Navigational path on site </p>

</li>
<details open><summary><b>Message TBreadcrumbsData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L156">Path</a></b>  <i>string</i>
<p> Text path in navigarional tree of site  Each item contains a node name, first item is root element </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L431">Available</a></b>  <i>bool</i>
<p> Is offer available to order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L433">DeliveryOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L144">TDeliveryOptions</a></i>
<p> Detailed delivery options </p>

</li>
<details open><summary><b>Message TDeliveryOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L146">Pickup</a></b>  <i>bool</i>
<p> Available for pickup </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L148">Store</a></b>  <i>bool</i>
<p> Available in store without order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L150">Delivery</a></b>  <i>bool</i>
<p> Available for order with courier delivery </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L436">SalesNotes</a></b>  <i>string</i>
<p> Sales notes as human readable text </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L439">ManufacturerWarranty</a></b>  <i>bool</i>
<p> Offer has manufacturer warranty </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L442">ShopCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Offer category from partner feed </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L445">MarketCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Yandex Market categories </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L448">BannerLandCategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Multik categories </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L451">ParametersData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L159">TOfferParameter</a></i>
<p> Raw unstructured parameters data </p>

</li>
<details open><summary><b>Message TOfferParameter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L160">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L161">Unit</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L162">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L454">Parameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L165">TOfferStructuredParameters</a></i>
<p> Parsed parameters </p>

</li>
<details open><summary><b>Message TOfferStructuredParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L166">Age</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L167">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L168">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L169">Season</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L170">Sex</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L171">Corpus</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L172">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L173">Collection</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L174">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L175">Length</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L176">Width</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L177">Height</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L178">SizeUnit</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L457">Age</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
<p> Product age for moderation </p>

</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L460">Adult</a></b>  <i>bool</i>
<p> Product offer for adults </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L463">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L791">FormalCondition</a></i>
<p> Product condition: used or like new; reason for condition </p>

</li>
<details open><summary><b>Message FormalCondition</b></summary>
<p> Cостояние товара  https://yandex.ru/support/partnermarket/elements/condition.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L800">type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L793">Type</a></i>
</li>
<details open><summary><b>Enum Type</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_TYPE</span></li>
<li><span style="color:#1D7373">LIKENEW</span></li>
<li><span style="color:#1D7373">USED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L801">reason</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L465">VideoCreatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L16">ProcessedVideo</a></i>
</li>
<details open><summary><b>Message ProcessedVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L22">id</a></b>  <i>string</i>
<p> ID креатива </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L23">status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L17">Status</a></i>
</li>
<details open><summary><b>Enum Status</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED</span></li>
<li><span style="color:#1D7373">AVAILABLE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L24">original_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L25">creative_id</a></b>  <i>uint64</i>
<p> ID креатива, число </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L466">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L473">Custom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L193">TCustomData</a></i>
</li>
<details open><summary><b>Message TCustomData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L194">OriginalOfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L195">Id2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L196">CustomPhrases</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L474">GoogleMerchant</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L181">TGoogleMerchantData</a></i>
</li>
<details open><summary><b>Message TGoogleMerchantData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L182">AgeGroup</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L134">EGoogleMerchantAgeGroup</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantAgeGroup</b></summary>
<ul>
<li><span style="color:#1D7373">GM_AGE_NEWBORN</span></li>
<li><span style="color:#1D7373">GM_AGE_INFANT</span></li>
<li><span style="color:#1D7373">GM_AGE_TODDLER</span></li>
<li><span style="color:#1D7373">GM_AGE_KIDS</span></li>
<li><span style="color:#1D7373">GM_AGE_ADULT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L183">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L184">Gender</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L142">EGoogleMerchantGender</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantGender</b></summary>
<ul>
<li><span style="color:#1D7373">GM_GENDER_MALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_FEMALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_UNISEX</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L185">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L186">Pattern</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L187">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L188">SizeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L148">EGoogleMerchantSizeType</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeType</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_TYPE_REGULAR</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PETITE</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PLUS</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_TALL</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_BIG</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_MATERNITY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L189">SizeSystem</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L157">EGoogleMerchantSizeSystem</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeSystem</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_AU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_BR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_CN</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_DE</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_EU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_FR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_IT</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_JP</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_MEX</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_UK</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_US</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L190">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L17">EGoogleMerchantCondition</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantCondition</b></summary>
<ul>
<li><span style="color:#1D7373">GM_CONDITION_NEW</span></li>
<li><span style="color:#1D7373">GM_CONDITION_REFURBISHED</span></li>
<li><span style="color:#1D7373">GM_CONDITION_USED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L475">Car</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L210">TCarData</a></i>
</li>
<details open><summary><b>Message TCarData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L211">UniqueId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L212">VIN</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L214">ModificationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L215">ModificationInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L199">TCarModificationInfo</a></i>
</li>
<details open><summary><b>Message TCarModificationInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L200">EngineVolume</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L201">EngineVolumeValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L202">EnginePower</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L203">EnginePowerValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L204">EnginePowerUnit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L104">ECarPowerUnit</a></i>
</li>
<details open><summary><b>Enum ECarPowerUnit</b></summary>
<p> Единицы измерения мощности двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_HORSEPOWER_UNIT</span></li>
<li><span style="color:#1D7373">CAR_KILOWATT_UNIT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L205">EngineType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L206">Gearbox</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L44">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<p> Тип коробки передач </p>

<ul>
<li><span style="color:#1D7373">CAR_GEARBOX_MANUAL</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_AUTOMATIC</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_VARIATOR</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L207">Drive</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L217">ComplectationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L218">BodyType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L219">SteeringWheel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L25">ECarSteeringWheel</a></i>
</li>
<details open><summary><b>Enum ECarSteeringWheel</b></summary>
<p> Расположение руля (левый или правый) </p>

<ul>
<li><span style="color:#1D7373">CAR_LEFT_HAND_DRIVE</span></li>
<li><span style="color:#1D7373">CAR_RIGHT_HAND_DRIVE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L220">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L221">Metallic</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L222">CustomStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L77">ECarCustomStatus</a></i>
</li>
<details open><summary><b>Enum ECarCustomStatus</b></summary>
<p> Таможенный статус </p>

<ul>
<li><span style="color:#1D7373">CAR_CUSTOM_CLEARED</span></li>
<li><span style="color:#1D7373">CAR_CUSTOM_NOT_CLEARED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L223">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L224">OwnersNumber</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L95">ECarOwnersNumber</a></i>
</li>
<details open><summary><b>Enum ECarOwnersNumber</b></summary>
<p> Количество владельцев по ПТС </p>

<ul>
<li><span style="color:#1D7373">CAR_NO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_ONE_OWNER</span></li>
<li><span style="color:#1D7373">CAR_TWO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_THREE_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_FOUR_OR_MORE_OWNERS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L225">Run</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L226">Year</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L227">RegistryYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L228">DoorsCount</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L476">Travel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L239">TTravelData</a></i>
</li>
<details open><summary><b>Message TTravelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L241">DestinationId</a></b>  <i>string</i>
<p> Пункт назначения </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L242">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L245">OriginId</a></b>  <i>string</i>
<p> Пункт отправления </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L246">OriginName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L477">Hotel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L249">THotelData</a></i>
</li>
<details open><summary><b>Message THotelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L250">PropertyId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L252">PropertyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L254">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L257">StarRating</a></b>  <i>uint32</i>
<p> Number stars at the hotel (from 1 to 5) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L260">Score</a></b>  <i>double</i>
<p> User score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L263">MaxScore</a></b>  <i>uint32</i>
<p> The max allowed user's score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L265">Facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L267">Category</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L269">Address</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L478">Flight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L231">TFlightData</a></i>
</li>
<details open><summary><b>Message TFlightData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L232">OriginId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L233">OriginName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L235">DestinationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L236">DestinationName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L479">Realty</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L303">TRealtyData</a></i>
</li>
<details open><summary><b>Message TRealtyData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L304">RealtyCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L28">ERealtyCategory</a></i>
</li>
<details open><summary><b>Enum ERealtyCategory</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_COMMERCIAL</span></li>
<li><span style="color:#1D7373">REALTY_COTTAGE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_WITH_LOT</span></li>
<li><span style="color:#1D7373">REALTY_LOT</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_PART</span></li>
<li><span style="color:#1D7373">REALTY_FLAT</span></li>
<li><span style="color:#1D7373">REALTY_ROOM</span></li>
<li><span style="color:#1D7373">REALTY_TOWNHOUSE</span></li>
<li><span style="color:#1D7373">REALTY_DUPLEX</span></li>
<li><span style="color:#1D7373">REALTY_GARAGE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L305">Location</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L278">TRealtyLocation</a></i>
</li>
<details open><summary><b>Message TRealtyLocation</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L279">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L280">Region</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L281">LocalityName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L282">MetroName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L283">MetroTimeOnFoot</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L284">MetroTimeOnTransport</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L306">DealStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L307">RealtyObjectData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L287">TRealtyObjectData</a></i>
</li>
<details open><summary><b>Message TRealtyObjectData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L288">Area</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L273">TRealtyArea</a></i>
</li>
<details open><summary><b>Message TRealtyArea</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L274">Value</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L275">Unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L80">ERealtyAreaUnit</a></i>
</li>
<details open><summary><b>Enum ERealtyAreaUnit</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_SQUARE_METER</span></li>
<li><span style="color:#1D7373">REALTY_ARE</span></li>
<li><span style="color:#1D7373">REALTY_HECTARE</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L289">Rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L290">Floor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L291">Renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L292">NewFlat</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L308">BuildingData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L295">TRealtyBuildingData</a></i>
</li>
<details open><summary><b>Message TRealtyBuildingData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L296">BuildingType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L297">FloorsTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L298">BuiltYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L299">ReadyQuarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L300">BuildingState</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L488">ClientAdTitle</a></b>  <i>string</i>
<p> Fixed banner title (filled by UseAsName) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L491">ClientAdBody</a></b>  <i>string</i>
<p> Fixed banner body (filled by UseAsBody) </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L51">BannerHash</a></b>  <i>uint64</i>
<p> other </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L52">ParentExportID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L53">BannerlandBeginTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L54">UpdateTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L55">OriginalImages</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L56">BusinessId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L57">OfferYabsId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L58">ShopId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L60">Deleted</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L63">DeltaTimestamp</a></b>  <i>uint64</i>
<p> syntetic field (will be filled in Caesar Resharder while reading deltas) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L66">BroadPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L16">TBroadPhrase</a></i>
<p> phrases </p>

</li>
<details open><summary><b>Message TBroadPhrase</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L17">BroadPhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L18">SimDistance</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L19">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L21">Timestamp</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L22">UpdateTime</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L25">NormType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L6">ENormType</a></i>
</li>
<details open><summary><b>Enum ENormType</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/norm_type.h </p>

<ul>
<li><span style="color:#1D7373">NoneType</span></li>
<li><span style="color:#1D7373">Norm</span></li>
<li><span style="color:#1D7373">Snorm</span></li>
<li><span style="color:#1D7373">Offer</span></li>
<li><span style="color:#1D7373">OfferGroup</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L26">PhraseData</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L67">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L68">OfferID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L70">AgeNew</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/dyn_banner.proto?rev=r9795881#L75">VideoCreative</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L501">SmartBannerCandidate</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L9">TPerfBanner</a></i>
</li>
<details open><summary><b>Message TPerfBanner</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L40">BannerID</a></b>  <i>int64</i>
<p> banner ids  key column </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L41">OrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L42">GroupExportID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L43">CampaignId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L44">DirectFeedID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L47">Title</a></b>  <i>string</i>
<p> resources </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L48">TitleMediaSmart</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L49">TitleExtension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L50">Body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L51">Href</a></b>  <i>string</i>
<p> Banner Url </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L52">OfferID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L53">AutogeneratedOfferID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L57">Site</a></b>  <i>string</i>
<p> OrigDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L58">SiteID</a></b>  <i>uint64</i>
<p> OrigDomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L59">SiteFilter</a></b>  <i>string</i>
<p> OrigDomain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L60">SiteFilterID</a></b>  <i>uint64</i>
<p> OrigDomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L61">TargetDomain</a></b>  <i>string</i>
<p> Domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L62">TargetDomainID</a></b>  <i>uint64</i>
<p> DomainID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L63">CategoryIDs</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L64">LangID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L8">ELang</a></i>
<p> Delete field after string Lang in Caesar </p>

</li>
<details open><summary><b>Enum ELang</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/lang_code.h </p>

<ul>
<li><span style="color:#1D7373">DEFAULT</span></li>
<li><span style="color:#1D7373">RU</span></li>
<li><span style="color:#1D7373">UK</span></li>
<li><span style="color:#1D7373">EN</span></li>
<li><span style="color:#1D7373">BY</span></li>
<li><span style="color:#1D7373">KZ</span></li>
<li><span style="color:#1D7373">TR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L65">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L66">HrefText</a></b>  <i>string</i>
<p> was: BSInfo.display_href </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L67">TemplateID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L70">ClientID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L71">VideoCreative</a></b>  <i>uint64</i>
<p> Experiment with adding video for smart banners </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L72">AllowedInProductGallery</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L76">CalloutSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L7">TCalloutSet</a></i>
</li>
<details open><summary><b>Message TCalloutSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L13">CalloutsList</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L14">Callouts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L8">TCallout</a></i>
</li>
<details open><summary><b>Message TCallout</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L9">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L10">Value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L79">ImagesInfoDirectFormat</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L80">BannerPrice</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L17">TBannerPrice</a></i>
</li>
<details open><summary><b>Message TBannerPrice</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L19">Price</a></b>  <i>string</i>
<p> https://direct-dev.yandex-team.ru/db/ppc/tables/banner_prices.html </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L20">OldPrice</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L21">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L22">Prefix</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L23">Discount</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L81">DisplayInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L58">TDisplayInfo</a></i>
</li>
<details open><summary><b>Message TDisplayInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L60">description_for_direct</a></b>  <i>string</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/package/plugin/settings.py?rev=7547566#L3426 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L61">business_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L62">offer_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L63">legal</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L64">sizes</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L65">sizes_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L66">consist</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L67">consist_for_direct</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L68">colors</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L69">facility</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L70">facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L71">run</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L72">vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L73">model</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L74">year</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L75">location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L76">class</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L77">go_from</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L78">go_to</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L79">realty_type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L80">sub_location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L81">building_name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L82">metro</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L83">metro_time_on_foot</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L84">metro_time_on_transport</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L85">address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L89">engine_volume</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L90">engine_power</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L92">owners_number</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L93">color_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L7">EColor</a></i>
</li>
<details open><summary><b>Enum EColor</b></summary>
<ul>
<li><span style="color:#1D7373">COLOR_UNKNOWN</span></li>
<li><span style="color:#1D7373">COLOR_BEIGE</span></li>
<li><span style="color:#1D7373">COLOR_WHITE</span></li>
<li><span style="color:#1D7373">COLOR_COLORLESS</span></li>
<li><span style="color:#1D7373">COLOR_CYAN</span></li>
<li><span style="color:#1D7373">COLOR_YELLOW</span></li>
<li><span style="color:#1D7373">COLOR_GREEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLDEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLD</span></li>
<li><span style="color:#1D7373">COLOR_BROWN</span></li>
<li><span style="color:#1D7373">COLOR_RED</span></li>
<li><span style="color:#1D7373">COLOR_ORANGE</span></li>
<li><span style="color:#1D7373">COLOR_MAGENTA</span></li>
<li><span style="color:#1D7373">COLOR_PINK</span></li>
<li><span style="color:#1D7373">COLOR_SILVERY</span></li>
<li><span style="color:#1D7373">COLOR_SILVER</span></li>
<li><span style="color:#1D7373">COLOR_GRAY</span></li>
<li><span style="color:#1D7373">COLOR_BLUE</span></li>
<li><span style="color:#1D7373">COLOR_PURPLE</span></li>
<li><span style="color:#1D7373">COLOR_BLACK</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L94">body_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L30">EBodyType</a></i>
</li>
<details open><summary><b>Enum EBodyType</b></summary>
<ul>
<li><span style="color:#1D7373">BT_UNKNOWN</span></li>
<li><span style="color:#1D7373">BT_SEDAN_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_SEDAN</span></li>
<li><span style="color:#1D7373">BT_CABRIOLET</span></li>
<li><span style="color:#1D7373">BT_COMPACTVAN</span></li>
<li><span style="color:#1D7373">BT_COUPE_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_COUPE</span></li>
<li><span style="color:#1D7373">BT_FASTBACK</span></li>
<li><span style="color:#1D7373">BT_VAN</span></li>
<li><span style="color:#1D7373">BT_HATCHBACK</span></li>
<li><span style="color:#1D7373">BT_LANDAU</span></li>
<li><span style="color:#1D7373">BT_LIFTBACK</span></li>
<li><span style="color:#1D7373">BT_LIMOUSINE</span></li>
<li><span style="color:#1D7373">BT_MICROVAN</span></li>
<li><span style="color:#1D7373">BT_MINIVAN</span></li>
<li><span style="color:#1D7373">BT_SUV</span></li>
<li><span style="color:#1D7373">BT_PHAETON_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_PHAETON</span></li>
<li><span style="color:#1D7373">BT_PICKUP</span></li>
<li><span style="color:#1D7373">BT_ROADSTER</span></li>
<li><span style="color:#1D7373">BT_TARGA</span></li>
<li><span style="color:#1D7373">BT_SPEEDSTER</span></li>
<li><span style="color:#1D7373">BT_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_CROSSOVER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L95">gearbox_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L57">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<ul>
<li><span style="color:#1D7373">GB_UNKNOWN</span></li>
<li><span style="color:#1D7373">GB_MANUAL</span></li>
<li><span style="color:#1D7373">GB_AUTOMATIC</span></li>
<li><span style="color:#1D7373">GB_VARIATOR</span></li>
<li><span style="color:#1D7373">GB_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L96">engine_type_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L97">drive_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L98">state_enum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L100">floor</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L101">floors_total</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L102">rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L103">renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L104">building_type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L105">deal_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L106">ready_quarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L107">building_state</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L108">new_flat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/common.proto?rev=r9795881#L109">region</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L65">ERealtyRegion</a></i>
</li>
<details open><summary><b>Enum ERealtyRegion</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW_DISTRICT</span></li>
<li><span style="color:#1D7373">REGION_LENINGRAD</span></li>
<li><span style="color:#1D7373">REGION_SVERDLOVSK</span></li>
<li><span style="color:#1D7373">REGION_KRASNODAR</span></li>
<li><span style="color:#1D7373">REGION_NOVOSIBIRSK</span></li>
<li><span style="color:#1D7373">REGION_OMSK</span></li>
<li><span style="color:#1D7373">REGION_ROSTOV</span></li>
<li><span style="color:#1D7373">REGION_SAMARA</span></li>
<li><span style="color:#1D7373">REGION_TUMEN</span></li>
<li><span style="color:#1D7373">REGION_VORONEJ</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW</span></li>
<li><span style="color:#1D7373">REGION_HABAROVSK</span></li>
<li><span style="color:#1D7373">REGION_NIJEGOROD</span></li>
<li><span style="color:#1D7373">REGION_TATARSTAN</span></li>
<li><span style="color:#1D7373">REGION_KRASNOYARSK</span></li>
<li><span style="color:#1D7373">REGION_BASHKORTOSTAN</span></li>
<li><span style="color:#1D7373">REGION_VLADIMIR</span></li>
<li><span style="color:#1D7373">REGION_CRIMEA</span></li>
<li><span style="color:#1D7373">REGION_SARATOV</span></li>
<li><span style="color:#1D7373">REGION_CHELYABINSK</span></li>
<li><span style="color:#1D7373">REGION_KOMI</span></li>
<li><span style="color:#1D7373">REGION_VOLGOGRAD</span></li>
<li><span style="color:#1D7373">REGION_ULYANOVSK</span></li>
<li><span style="color:#1D7373">REGION_TULA</span></li>
<li><span style="color:#1D7373">REGION_TVER</span></li>
<li><span style="color:#1D7373">REGION_LIPECK</span></li>
<li><span style="color:#1D7373">REGION_HANTI</span></li>
<li><span style="color:#1D7373">REGION_BELGOROD</span></li>
<li><span style="color:#1D7373">REGION_RYAZAN</span></li>
<li><span style="color:#1D7373">REGION_IRKUTSK</span></li>
<li><span style="color:#1D7373">REGION_KALUGA</span></li>
<li><span style="color:#1D7373">REGION_PENZA</span></li>
<li><span style="color:#1D7373">REGION_KEMEROV</span></li>
<li><span style="color:#1D7373">REGION_PERM</span></li>
<li><span style="color:#1D7373">REGION_YAROSLAVL</span></li>
<li><span style="color:#1D7373">REGION_KALININGRAD</span></li>
<li><span style="color:#1D7373">REGION_ALTAI</span></li>
<li><span style="color:#1D7373">REGION_STAVROPOL</span></li>
<li><span style="color:#1D7373">REGION_TOMSK</span></li>
<li><span style="color:#1D7373">REGION_ASTRAKHAN</span></li>
<li><span style="color:#1D7373">REGION_KOSTROMA</span></li>
<li><span style="color:#1D7373">REGION_UDMURTHIA</span></li>
<li><span style="color:#1D7373">REGION_IVANOVSK</span></li>
<li><span style="color:#1D7373">REGION_SMOLENSK</span></li>
<li><span style="color:#1D7373">REGION_ORENBURG</span></li>
<li><span style="color:#1D7373">REGION_CHUVASHIA</span></li>
<li><span style="color:#1D7373">REGION_KIROV</span></li>
<li><span style="color:#1D7373">REGION_MARIY_EL</span></li>
<li><span style="color:#1D7373">REGION_NOVGOROD</span></li>
<li><span style="color:#1D7373">REGION_ADIGEI</span></li>
<li><span style="color:#1D7373">REGION_PRIMORYE</span></li>
<li><span style="color:#1D7373">REGION_PSKOV</span></li>
<li><span style="color:#1D7373">REGION_BRYANSK</span></li>
<li><span style="color:#1D7373">REGION_OREL</span></li>
<li><span style="color:#1D7373">REGION_KURSK</span></li>
<li><span style="color:#1D7373">REGION_ARHANGELSK</span></li>
<li><span style="color:#1D7373">REGION_TAMBOV</span></li>
<li><span style="color:#1D7373">REGION_KURGAN</span></li>
<li><span style="color:#1D7373">REGION_VOLOGODSK</span></li>
<li><span style="color:#1D7373">REGION_KARELIYA</span></li>
<li><span style="color:#1D7373">REGION_BURYATIA</span></li>
<li><span style="color:#1D7373">REGION_NORTH_OSETIA</span></li>
<li><span style="color:#1D7373">REGION_YAMAL</span></li>
<li><span style="color:#1D7373">REGION_MORDOVIA</span></li>
<li><span style="color:#1D7373">REGION_DAGESTAN</span></li>
<li><span style="color:#1D7373">REGION_AMUR</span></li>
<li><span style="color:#1D7373">REGION_SAHA</span></li>
<li><span style="color:#1D7373">REGION_MURMANSK</span></li>
<li><span style="color:#1D7373">REGION_ZABAYKALSK</span></li>
<li><span style="color:#1D7373">REGION_KBR</span></li>
<li><span style="color:#1D7373">REGION_HAKASIA</span></li>
<li><span style="color:#1D7373">REGION_ALTAI_REPUBLIC</span></li>
<li><span style="color:#1D7373">REGION_SAKHALIN</span></li>
<li><span style="color:#1D7373">REGION_KAMCHATKA</span></li>
<li><span style="color:#1D7373">REGION_KCHR</span></li>
<li><span style="color:#1D7373">REGION_MAGADAN</span></li>
<li><span style="color:#1D7373">REGION_CHECHNYA</span></li>
<li><span style="color:#1D7373">REGION_TIVA</span></li>
<li><span style="color:#1D7373">REGION_JEWISH_AUTONOMOUS</span></li>
<li><span style="color:#1D7373">REGION_KALMIKIYA</span></li>
<li><span style="color:#1D7373">REGION_INGUSHETIA</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L82">ModelInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L11">TModelInfo</a></i>
</li>
<details open><summary><b>Message TModelInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L14">MarketModelID</a></b>  <i>uint64</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/db/schema.h?rev=7545212#L1563  https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/mkdb/resource.cpp?rev=7577587#L489 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L15">MarketCategoryID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L16">AdvType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L17">AdvTypeDirectAllowed</a></b>  <i>bool</i>
<p> bl_type_direct_allowed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L34">Market</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L20">TMarketData</a></i>
</li>
<details open><summary><b>Message TMarketData</b></summary>
<p> market: </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L21">PriceMin</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L22">PriceAvg</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L23">PriceMax</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L24">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L25">RatingCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L26">MaxRating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L27">OfferClass</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L28">OfferCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L29">IsNew</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L30">Vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L31">Model</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L35">LocationID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L36">BLPhraseTemplateID</a></b>  <i>uint64</i>
<p> git rid of this please! </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L85">OfferProperties</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L328">TOffer</a></i>
<p> Use tests to ensure the existence of fields in this field </p>

</li>
<details open><summary><b>Message TOffer</b></summary>
<p> *******************************  ** Id fields                 **  ** proto range from 1 to 100 **  ******************************* </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L336">BusinessId</a></b>  <i>uint32</i>
<p> Composite unique key of offer  Patner identifier in Yandex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L338">OfferId</a></b>  <i>string</i>
<p> B2B offer identifier from partner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L340">OfferYabsId</a></b>  <i>uint64</i>
<p> Hash of B2B identifier (should be unique in subset of all offers from one partner) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L342">ShopId</a></b>  <i>uint32</i>
<p> Identifier of Yandex services set (known as shop) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L346">ClientId</a></b>  <i>uint64</i>
<p> Additional identifiers  Partner identifier in accounting balance </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L348">FeedId</a></b>  <i>uint32</i>
<p> Feed identifier in B2C Yndex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L350">DirectFeedId</a></b>  <i>uint64</i>
<p> Feed identifier in Yandex.Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L351">WareMd5</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L353">OriginalSku</a></b>  <i>string</i>
<p> SKU in parnter content system </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L355">FeedItemGroupId</a></b>  <i>string</i>
<p> Id of group inside feed. Needed to create retargeting for group of e.g. iPhones 13 of different colors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L364">TimestampSeconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L367">DataType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L37">EDataType</a></i>
<p> Data type for BannerLand </p>

</li>
<details open><summary><b>Enum EDataType</b></summary>
<ul>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_MARKET</span></li>
<li><span style="color:#1D7373">DATA_TYPE_AUTORU</span></li>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_MERCHANT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_FLIGHT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_TRAVEL</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_HOTEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L370">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
<p> Offer source (feed or site) </p>

</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L373">ProductType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L68">EProductType</a></i>
<p> Product type for offer </p>

</li>
<details open><summary><b>Enum EProductType</b></summary>
<ul>
<li><span style="color:#1D7373">PRODUCT_TYPE_UNKNOWN</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AUTO_ACCESSORIES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AVIA_TICKETS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BEAUTY_HEALTH</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BUILDING_MATERIALS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CARS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHILDRENS_GOODS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHINESE_SITES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_DSE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_EXTERNAL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_FURNITURE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_GAMES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_HOTELS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_LIST</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_PROMOCODES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_REALTY</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_SPORTS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TIRES_DISKS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TRAVEL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_WEAR</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BOOKS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L375">OfferType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L64">EOfferType</a></i>
<p> Offer type </p>

</li>
<details open><summary><b>Enum EOfferType</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_TYPE_VENDOR_MODEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L378">OfferLanguage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L48">ELanguageCode</a></i>
<p> Offer texts language </p>

</li>
<details open><summary><b>Enum ELanguageCode</b></summary>
<ul>
<li><span style="color:#1D7373">LANGUAGE_UNKNOWN</span></li>
<li><span style="color:#1D7373">LANGUAGE_RU</span></li>
<li><span style="color:#1D7373">LANGUAGE_EN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L381">DisableStatus</a></b>  <i>bool</i>
<p> Is offer active </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L389">Model</a></b>  <i>string</i>
<p> Model name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L391">Vendor</a></b>  <i>string</i>
<p> Manufacturer or brand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L393">TypePrefix</a></b>  <i>string</i>
<p> Type or category name of good (used in title) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L395">Name</a></b>  <i>string</i>
<p> Full offer name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L398">Description</a></b>  <i>string</i>
<p> Detailed description of offer </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L401">Url</a></b>  <i>string</i>
<p> URL to offer on partner site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L403">UrlOriginalDomain</a></b>  <i>string</i>
<p> Domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L405">UrlOriginalDomainId</a></b>  <i>uint64</i>
<p> Id of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L407">UrlMainMirror</a></b>  <i>string</i>
<p> Main mirror (after redirects) of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L409">UrlMainMirrorId</a></b>  <i>uint64</i>
<p> Id of main mirror domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L412">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L110">TImageData</a></i>
<p> Offer images data (original URLs and avatars) </p>

</li>
<details open><summary><b>Message TImageData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L123">SourceUrl</a></b>  <i>string</i>
<p> Image URL on client site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L126">Status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L112">EAvatarizationStatus</a></i>
<p> Status of image loading into avatars service </p>

</li>
<details open><summary><b>Enum EAvatarizationStatus</b></summary>
<p> TODO: Replace with Market.DataCamp.MarketPicture.Status after complete MARKETINDEXER-41756 </p>

<ul>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_UNKNOWN</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_AVAILABLE</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_FAILED</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_REMOVED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L129">AvatarsInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
<p> Image avatars information </p>

</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L415">Currency</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L36">Currency</a></i>
<p> Offer currency </p>

</li>
<details open><summary><b>Enum Currency</b></summary>
<ul>
<li><span style="color:#1D7373">CURRENCY_UNDEFINED</span></li>
<li><span style="color:#1D7373">RUR</span></li>
<li><span style="color:#1D7373">USD</span></li>
<li><span style="color:#1D7373">EUR</span></li>
<li><span style="color:#1D7373">UAH</span></li>
<li><span style="color:#1D7373">KZT</span></li>
<li><span style="color:#1D7373">BYN</span></li>
<li><span style="color:#1D7373">GBP</span></li>
<li><span style="color:#1D7373">TRY</span></li>
<li><span style="color:#1D7373">ALL</span></li>
<li><span style="color:#1D7373">AFN</span></li>
<li><span style="color:#1D7373">ARS</span></li>
<li><span style="color:#1D7373">AWG</span></li>
<li><span style="color:#1D7373">AUD</span></li>
<li><span style="color:#1D7373">AZN</span></li>
<li><span style="color:#1D7373">BBD</span></li>
<li><span style="color:#1D7373">BZD</span></li>
<li><span style="color:#1D7373">BMD</span></li>
<li><span style="color:#1D7373">BOB</span></li>
<li><span style="color:#1D7373">BAM</span></li>
<li><span style="color:#1D7373">BWP</span></li>
<li><span style="color:#1D7373">BGN</span></li>
<li><span style="color:#1D7373">BRL</span></li>
<li><span style="color:#1D7373">BND</span></li>
<li><span style="color:#1D7373">KHR</span></li>
<li><span style="color:#1D7373">CAD</span></li>
<li><span style="color:#1D7373">KYD</span></li>
<li><span style="color:#1D7373">CLP</span></li>
<li><span style="color:#1D7373">CNY</span></li>
<li><span style="color:#1D7373">COP</span></li>
<li><span style="color:#1D7373">CRC</span></li>
<li><span style="color:#1D7373">HRK</span></li>
<li><span style="color:#1D7373">CUP</span></li>
<li><span style="color:#1D7373">CZK</span></li>
<li><span style="color:#1D7373">DKK</span></li>
<li><span style="color:#1D7373">DOP</span></li>
<li><span style="color:#1D7373">XCD</span></li>
<li><span style="color:#1D7373">EGP</span></li>
<li><span style="color:#1D7373">SVC</span></li>
<li><span style="color:#1D7373">FKP</span></li>
<li><span style="color:#1D7373">FJD</span></li>
<li><span style="color:#1D7373">GHS</span></li>
<li><span style="color:#1D7373">GIP</span></li>
<li><span style="color:#1D7373">GTQ</span></li>
<li><span style="color:#1D7373">GYD</span></li>
<li><span style="color:#1D7373">HNL</span></li>
<li><span style="color:#1D7373">HKD</span></li>
<li><span style="color:#1D7373">HUF</span></li>
<li><span style="color:#1D7373">ISK</span></li>
<li><span style="color:#1D7373">INR</span></li>
<li><span style="color:#1D7373">IDR</span></li>
<li><span style="color:#1D7373">IRR</span></li>
<li><span style="color:#1D7373">ILS</span></li>
<li><span style="color:#1D7373">JMD</span></li>
<li><span style="color:#1D7373">JPY</span></li>
<li><span style="color:#1D7373">KPW</span></li>
<li><span style="color:#1D7373">KRW</span></li>
<li><span style="color:#1D7373">KGS</span></li>
<li><span style="color:#1D7373">LAK</span></li>
<li><span style="color:#1D7373">LBP</span></li>
<li><span style="color:#1D7373">LRD</span></li>
<li><span style="color:#1D7373">MKD</span></li>
<li><span style="color:#1D7373">MYR</span></li>
<li><span style="color:#1D7373">MUR</span></li>
<li><span style="color:#1D7373">MXN</span></li>
<li><span style="color:#1D7373">MNT</span></li>
<li><span style="color:#1D7373">MAD</span></li>
<li><span style="color:#1D7373">MZN</span></li>
<li><span style="color:#1D7373">NAD</span></li>
<li><span style="color:#1D7373">NPR</span></li>
<li><span style="color:#1D7373">ANG</span></li>
<li><span style="color:#1D7373">NZD</span></li>
<li><span style="color:#1D7373">NIO</span></li>
<li><span style="color:#1D7373">NGN</span></li>
<li><span style="color:#1D7373">NOK</span></li>
<li><span style="color:#1D7373">OMR</span></li>
<li><span style="color:#1D7373">PKR</span></li>
<li><span style="color:#1D7373">PAB</span></li>
<li><span style="color:#1D7373">PYG</span></li>
<li><span style="color:#1D7373">PEN</span></li>
<li><span style="color:#1D7373">PHP</span></li>
<li><span style="color:#1D7373">PLN</span></li>
<li><span style="color:#1D7373">QAR</span></li>
<li><span style="color:#1D7373">RON</span></li>
<li><span style="color:#1D7373">SHP</span></li>
<li><span style="color:#1D7373">SAR</span></li>
<li><span style="color:#1D7373">RSD</span></li>
<li><span style="color:#1D7373">SCR</span></li>
<li><span style="color:#1D7373">SGD</span></li>
<li><span style="color:#1D7373">SBD</span></li>
<li><span style="color:#1D7373">SOS</span></li>
<li><span style="color:#1D7373">ZAR</span></li>
<li><span style="color:#1D7373">LKR</span></li>
<li><span style="color:#1D7373">SEK</span></li>
<li><span style="color:#1D7373">CHF</span></li>
<li><span style="color:#1D7373">SRD</span></li>
<li><span style="color:#1D7373">SYP</span></li>
<li><span style="color:#1D7373">TWD</span></li>
<li><span style="color:#1D7373">THB</span></li>
<li><span style="color:#1D7373">TTD</span></li>
<li><span style="color:#1D7373">AED</span></li>
<li><span style="color:#1D7373">UYU</span></li>
<li><span style="color:#1D7373">UZS</span></li>
<li><span style="color:#1D7373">VEF</span></li>
<li><span style="color:#1D7373">VND</span></li>
<li><span style="color:#1D7373">YER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L417">Price</a></b>  <i>uint64</i>
<p> Price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L419">PriceMicrosPart</a></b>  <i>uint64</i>
<p> Price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L421">OldPrice</a></b>  <i>uint64</i>
<p> Previous price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L423">OldPriceMicrosPart</a></b>  <i>uint64</i>
<p> Previous price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L426">CategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Offer categoryzation info </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L428">Breadcrumbs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L153">TBreadcrumbsData</a></i>
<p> Navigational path on site </p>

</li>
<details open><summary><b>Message TBreadcrumbsData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L156">Path</a></b>  <i>string</i>
<p> Text path in navigarional tree of site  Each item contains a node name, first item is root element </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L431">Available</a></b>  <i>bool</i>
<p> Is offer available to order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L433">DeliveryOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L144">TDeliveryOptions</a></i>
<p> Detailed delivery options </p>

</li>
<details open><summary><b>Message TDeliveryOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L146">Pickup</a></b>  <i>bool</i>
<p> Available for pickup </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L148">Store</a></b>  <i>bool</i>
<p> Available in store without order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L150">Delivery</a></b>  <i>bool</i>
<p> Available for order with courier delivery </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L436">SalesNotes</a></b>  <i>string</i>
<p> Sales notes as human readable text </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L439">ManufacturerWarranty</a></b>  <i>bool</i>
<p> Offer has manufacturer warranty </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L442">ShopCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Offer category from partner feed </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L445">MarketCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Yandex Market categories </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L448">BannerLandCategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Multik categories </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L451">ParametersData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L159">TOfferParameter</a></i>
<p> Raw unstructured parameters data </p>

</li>
<details open><summary><b>Message TOfferParameter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L160">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L161">Unit</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L162">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L454">Parameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L165">TOfferStructuredParameters</a></i>
<p> Parsed parameters </p>

</li>
<details open><summary><b>Message TOfferStructuredParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L166">Age</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L167">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L168">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L169">Season</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L170">Sex</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L171">Corpus</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L172">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L173">Collection</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L174">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L175">Length</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L176">Width</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L177">Height</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L178">SizeUnit</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L457">Age</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
<p> Product age for moderation </p>

</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L460">Adult</a></b>  <i>bool</i>
<p> Product offer for adults </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L463">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L791">FormalCondition</a></i>
<p> Product condition: used or like new; reason for condition </p>

</li>
<details open><summary><b>Message FormalCondition</b></summary>
<p> Cостояние товара  https://yandex.ru/support/partnermarket/elements/condition.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L800">type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L793">Type</a></i>
</li>
<details open><summary><b>Enum Type</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_TYPE</span></li>
<li><span style="color:#1D7373">LIKENEW</span></li>
<li><span style="color:#1D7373">USED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L801">reason</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L465">VideoCreatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L16">ProcessedVideo</a></i>
</li>
<details open><summary><b>Message ProcessedVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L22">id</a></b>  <i>string</i>
<p> ID креатива </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L23">status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L17">Status</a></i>
</li>
<details open><summary><b>Enum Status</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED</span></li>
<li><span style="color:#1D7373">AVAILABLE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L24">original_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L25">creative_id</a></b>  <i>uint64</i>
<p> ID креатива, число </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L466">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L473">Custom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L193">TCustomData</a></i>
</li>
<details open><summary><b>Message TCustomData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L194">OriginalOfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L195">Id2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L196">CustomPhrases</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L474">GoogleMerchant</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L181">TGoogleMerchantData</a></i>
</li>
<details open><summary><b>Message TGoogleMerchantData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L182">AgeGroup</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L134">EGoogleMerchantAgeGroup</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantAgeGroup</b></summary>
<ul>
<li><span style="color:#1D7373">GM_AGE_NEWBORN</span></li>
<li><span style="color:#1D7373">GM_AGE_INFANT</span></li>
<li><span style="color:#1D7373">GM_AGE_TODDLER</span></li>
<li><span style="color:#1D7373">GM_AGE_KIDS</span></li>
<li><span style="color:#1D7373">GM_AGE_ADULT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L183">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L184">Gender</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L142">EGoogleMerchantGender</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantGender</b></summary>
<ul>
<li><span style="color:#1D7373">GM_GENDER_MALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_FEMALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_UNISEX</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L185">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L186">Pattern</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L187">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L188">SizeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L148">EGoogleMerchantSizeType</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeType</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_TYPE_REGULAR</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PETITE</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PLUS</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_TALL</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_BIG</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_MATERNITY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L189">SizeSystem</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L157">EGoogleMerchantSizeSystem</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeSystem</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_AU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_BR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_CN</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_DE</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_EU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_FR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_IT</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_JP</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_MEX</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_UK</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_US</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L190">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L17">EGoogleMerchantCondition</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantCondition</b></summary>
<ul>
<li><span style="color:#1D7373">GM_CONDITION_NEW</span></li>
<li><span style="color:#1D7373">GM_CONDITION_REFURBISHED</span></li>
<li><span style="color:#1D7373">GM_CONDITION_USED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L475">Car</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L210">TCarData</a></i>
</li>
<details open><summary><b>Message TCarData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L211">UniqueId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L212">VIN</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L214">ModificationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L215">ModificationInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L199">TCarModificationInfo</a></i>
</li>
<details open><summary><b>Message TCarModificationInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L200">EngineVolume</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L201">EngineVolumeValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L202">EnginePower</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L203">EnginePowerValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L204">EnginePowerUnit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L104">ECarPowerUnit</a></i>
</li>
<details open><summary><b>Enum ECarPowerUnit</b></summary>
<p> Единицы измерения мощности двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_HORSEPOWER_UNIT</span></li>
<li><span style="color:#1D7373">CAR_KILOWATT_UNIT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L205">EngineType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L206">Gearbox</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L44">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<p> Тип коробки передач </p>

<ul>
<li><span style="color:#1D7373">CAR_GEARBOX_MANUAL</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_AUTOMATIC</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_VARIATOR</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L207">Drive</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L217">ComplectationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L218">BodyType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L219">SteeringWheel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L25">ECarSteeringWheel</a></i>
</li>
<details open><summary><b>Enum ECarSteeringWheel</b></summary>
<p> Расположение руля (левый или правый) </p>

<ul>
<li><span style="color:#1D7373">CAR_LEFT_HAND_DRIVE</span></li>
<li><span style="color:#1D7373">CAR_RIGHT_HAND_DRIVE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L220">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L221">Metallic</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L222">CustomStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L77">ECarCustomStatus</a></i>
</li>
<details open><summary><b>Enum ECarCustomStatus</b></summary>
<p> Таможенный статус </p>

<ul>
<li><span style="color:#1D7373">CAR_CUSTOM_CLEARED</span></li>
<li><span style="color:#1D7373">CAR_CUSTOM_NOT_CLEARED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L223">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L224">OwnersNumber</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L95">ECarOwnersNumber</a></i>
</li>
<details open><summary><b>Enum ECarOwnersNumber</b></summary>
<p> Количество владельцев по ПТС </p>

<ul>
<li><span style="color:#1D7373">CAR_NO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_ONE_OWNER</span></li>
<li><span style="color:#1D7373">CAR_TWO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_THREE_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_FOUR_OR_MORE_OWNERS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L225">Run</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L226">Year</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L227">RegistryYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L228">DoorsCount</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L476">Travel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L239">TTravelData</a></i>
</li>
<details open><summary><b>Message TTravelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L241">DestinationId</a></b>  <i>string</i>
<p> Пункт назначения </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L242">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L245">OriginId</a></b>  <i>string</i>
<p> Пункт отправления </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L246">OriginName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L477">Hotel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L249">THotelData</a></i>
</li>
<details open><summary><b>Message THotelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L250">PropertyId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L252">PropertyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L254">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L257">StarRating</a></b>  <i>uint32</i>
<p> Number stars at the hotel (from 1 to 5) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L260">Score</a></b>  <i>double</i>
<p> User score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L263">MaxScore</a></b>  <i>uint32</i>
<p> The max allowed user's score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L265">Facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L267">Category</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L269">Address</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L478">Flight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L231">TFlightData</a></i>
</li>
<details open><summary><b>Message TFlightData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L232">OriginId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L233">OriginName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L235">DestinationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L236">DestinationName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L479">Realty</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L303">TRealtyData</a></i>
</li>
<details open><summary><b>Message TRealtyData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L304">RealtyCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L28">ERealtyCategory</a></i>
</li>
<details open><summary><b>Enum ERealtyCategory</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_COMMERCIAL</span></li>
<li><span style="color:#1D7373">REALTY_COTTAGE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_WITH_LOT</span></li>
<li><span style="color:#1D7373">REALTY_LOT</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_PART</span></li>
<li><span style="color:#1D7373">REALTY_FLAT</span></li>
<li><span style="color:#1D7373">REALTY_ROOM</span></li>
<li><span style="color:#1D7373">REALTY_TOWNHOUSE</span></li>
<li><span style="color:#1D7373">REALTY_DUPLEX</span></li>
<li><span style="color:#1D7373">REALTY_GARAGE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L305">Location</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L278">TRealtyLocation</a></i>
</li>
<details open><summary><b>Message TRealtyLocation</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L279">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L280">Region</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L281">LocalityName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L282">MetroName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L283">MetroTimeOnFoot</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L284">MetroTimeOnTransport</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L306">DealStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L307">RealtyObjectData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L287">TRealtyObjectData</a></i>
</li>
<details open><summary><b>Message TRealtyObjectData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L288">Area</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L273">TRealtyArea</a></i>
</li>
<details open><summary><b>Message TRealtyArea</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L274">Value</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L275">Unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L80">ERealtyAreaUnit</a></i>
</li>
<details open><summary><b>Enum ERealtyAreaUnit</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_SQUARE_METER</span></li>
<li><span style="color:#1D7373">REALTY_ARE</span></li>
<li><span style="color:#1D7373">REALTY_HECTARE</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L289">Rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L290">Floor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L291">Renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L292">NewFlat</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L308">BuildingData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L295">TRealtyBuildingData</a></i>
</li>
<details open><summary><b>Message TRealtyBuildingData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L296">BuildingType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L297">FloorsTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L298">BuiltYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L299">ReadyQuarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L300">BuildingState</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L488">ClientAdTitle</a></b>  <i>string</i>
<p> Fixed banner title (filled by UseAsName) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L491">ClientAdBody</a></b>  <i>string</i>
<p> Fixed banner body (filled by UseAsBody) </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L88">BannerHash</a></b>  <i>uint64</i>
<p> other </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L89">BannerlandBeginTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L90">UpdateTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L92">OriginalImages</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L93">BusinessId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L94">OfferYabsId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L95">ShopId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L97">Deleted</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L100">DeltaTimestamp</a></b>  <i>uint64</i>
<p> syntetic field (will be filled in Caesar Resharder while reading deltas) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L103">BroadPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L16">TBroadPhrase</a></i>
<p> phrases </p>

</li>
<details open><summary><b>Message TBroadPhrase</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L17">BroadPhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L18">SimDistance</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L19">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L21">Timestamp</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L22">UpdateTime</a></b>  <i>uint64</i>
<p> deprecated field, will be removed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L25">NormType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L6">ENormType</a></i>
</li>
<details open><summary><b>Enum ENormType</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/norm_type.h </p>

<ul>
<li><span style="color:#1D7373">NoneType</span></li>
<li><span style="color:#1D7373">Norm</span></li>
<li><span style="color:#1D7373">Snorm</span></li>
<li><span style="color:#1D7373">Offer</span></li>
<li><span style="color:#1D7373">OfferGroup</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/phrase.proto?rev=r9795881#L26">PhraseData</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L104">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L106">ParentExportID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v1/bannerland/perf_banner.proto?rev=r9795881#L108">AgeNew</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L502">BannerLandBannerCandidate</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L39">TBanner</a></i>
<p> new version of banner, superposition of Dynamic and Smart </p>

</li>
<details open><summary><b>Message TBanner</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L198">BannerId</a></b>  <i>uint64</i>
<p> ***************  ** Id fields **  *************** </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L199">OrderId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L200">AdGroupId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L201">ClientId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L202">BusinessId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L203">ShopId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L204">OfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L205">AutogeneratedOfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L206">OfferYabsId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L207">DirectParentBannerId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L208">CampaignId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L213">Title</a></b>  <i>string</i>
<p> **********************  ** Banner resources **  ********************** </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L214">TitleMediaSmart</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L215">TitleExtension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L216">Body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L217">Href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L218">HrefText</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L219">Site</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L220">SiteFilter</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L221">SiteFilterId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L222">TargetDomain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L223">TargetDomainId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L225">CategoryIds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L226">Lang</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L227">TemplateId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L228">AllowedInProductGallery</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L233">CalloutSet</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L7">TCalloutSet</a></i>
<p> ******************************  ** Banner complex resources **  ****************************** </p>

</li>
<details open><summary><b>Message TCalloutSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L13">CalloutsList</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L14">Callouts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L8">TCallout</a></i>
</li>
<details open><summary><b>Message TCallout</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L9">Key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L10">Value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L234">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L235">BannerPrice</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L17">TBannerPrice</a></i>
</li>
<details open><summary><b>Message TBannerPrice</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L19">Price</a></b>  <i>string</i>
<p> https://direct-dev.yandex-team.ru/db/ppc/tables/banner_prices.html </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L20">OldPrice</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L21">Currency</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L22">Prefix</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L23">Discount</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L236">OfferInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L40">TOfferInfo</a></i>
</li>
<details open><summary><b>Message TOfferInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L156">BusinessType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L105">EBusinessType</a></i>
</li>
<details open><summary><b>Enum EBusinessType</b></summary>
<ul>
<li><span style="color:#1D7373">BT_UNKNOWN</span></li>
<li><span style="color:#1D7373">BT_RETAIL</span></li>
<li><span style="color:#1D7373">BT_HOTELS</span></li>
<li><span style="color:#1D7373">BT_REALTY</span></li>
<li><span style="color:#1D7373">BT_AUTO</span></li>
<li><span style="color:#1D7373">BT_FLIGHTS</span></li>
<li><span style="color:#1D7373">BT_OTHER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L157">OfferType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L158">DescriptionForDirect</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L161">AviaTicketParameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L41">TAviaTicketParameters</a></i>
</li>
<details open><summary><b>Message TAviaTicketParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L42">From</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L43">To</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L162">RealtyParameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L46">TRealtyParameters</a></i>
</li>
<details open><summary><b>Message TRealtyParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L47">Legal</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L48">Location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L49">SubLocation</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L50">BuildingName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L51">Metro</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L52">MetroTimeOnFoot</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L53">MetroTimeOnTransport</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L54">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L55">BuiltYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L56">Floor</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L57">FloorsTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L58">Rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L59">Renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L60">BuildingType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L61">DealStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L62">ReadyQuarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L63">BuildingState</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L64">NewFlat</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L65">Region</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L65">ERealtyRegion</a></i>
</li>
<details open><summary><b>Enum ERealtyRegion</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW_DISTRICT</span></li>
<li><span style="color:#1D7373">REGION_LENINGRAD</span></li>
<li><span style="color:#1D7373">REGION_SVERDLOVSK</span></li>
<li><span style="color:#1D7373">REGION_KRASNODAR</span></li>
<li><span style="color:#1D7373">REGION_NOVOSIBIRSK</span></li>
<li><span style="color:#1D7373">REGION_OMSK</span></li>
<li><span style="color:#1D7373">REGION_ROSTOV</span></li>
<li><span style="color:#1D7373">REGION_SAMARA</span></li>
<li><span style="color:#1D7373">REGION_TUMEN</span></li>
<li><span style="color:#1D7373">REGION_VORONEJ</span></li>
<li><span style="color:#1D7373">REGION_MOSCOW</span></li>
<li><span style="color:#1D7373">REGION_HABAROVSK</span></li>
<li><span style="color:#1D7373">REGION_NIJEGOROD</span></li>
<li><span style="color:#1D7373">REGION_TATARSTAN</span></li>
<li><span style="color:#1D7373">REGION_KRASNOYARSK</span></li>
<li><span style="color:#1D7373">REGION_BASHKORTOSTAN</span></li>
<li><span style="color:#1D7373">REGION_VLADIMIR</span></li>
<li><span style="color:#1D7373">REGION_CRIMEA</span></li>
<li><span style="color:#1D7373">REGION_SARATOV</span></li>
<li><span style="color:#1D7373">REGION_CHELYABINSK</span></li>
<li><span style="color:#1D7373">REGION_KOMI</span></li>
<li><span style="color:#1D7373">REGION_VOLGOGRAD</span></li>
<li><span style="color:#1D7373">REGION_ULYANOVSK</span></li>
<li><span style="color:#1D7373">REGION_TULA</span></li>
<li><span style="color:#1D7373">REGION_TVER</span></li>
<li><span style="color:#1D7373">REGION_LIPECK</span></li>
<li><span style="color:#1D7373">REGION_HANTI</span></li>
<li><span style="color:#1D7373">REGION_BELGOROD</span></li>
<li><span style="color:#1D7373">REGION_RYAZAN</span></li>
<li><span style="color:#1D7373">REGION_IRKUTSK</span></li>
<li><span style="color:#1D7373">REGION_KALUGA</span></li>
<li><span style="color:#1D7373">REGION_PENZA</span></li>
<li><span style="color:#1D7373">REGION_KEMEROV</span></li>
<li><span style="color:#1D7373">REGION_PERM</span></li>
<li><span style="color:#1D7373">REGION_YAROSLAVL</span></li>
<li><span style="color:#1D7373">REGION_KALININGRAD</span></li>
<li><span style="color:#1D7373">REGION_ALTAI</span></li>
<li><span style="color:#1D7373">REGION_STAVROPOL</span></li>
<li><span style="color:#1D7373">REGION_TOMSK</span></li>
<li><span style="color:#1D7373">REGION_ASTRAKHAN</span></li>
<li><span style="color:#1D7373">REGION_KOSTROMA</span></li>
<li><span style="color:#1D7373">REGION_UDMURTHIA</span></li>
<li><span style="color:#1D7373">REGION_IVANOVSK</span></li>
<li><span style="color:#1D7373">REGION_SMOLENSK</span></li>
<li><span style="color:#1D7373">REGION_ORENBURG</span></li>
<li><span style="color:#1D7373">REGION_CHUVASHIA</span></li>
<li><span style="color:#1D7373">REGION_KIROV</span></li>
<li><span style="color:#1D7373">REGION_MARIY_EL</span></li>
<li><span style="color:#1D7373">REGION_NOVGOROD</span></li>
<li><span style="color:#1D7373">REGION_ADIGEI</span></li>
<li><span style="color:#1D7373">REGION_PRIMORYE</span></li>
<li><span style="color:#1D7373">REGION_PSKOV</span></li>
<li><span style="color:#1D7373">REGION_BRYANSK</span></li>
<li><span style="color:#1D7373">REGION_OREL</span></li>
<li><span style="color:#1D7373">REGION_KURSK</span></li>
<li><span style="color:#1D7373">REGION_ARHANGELSK</span></li>
<li><span style="color:#1D7373">REGION_TAMBOV</span></li>
<li><span style="color:#1D7373">REGION_KURGAN</span></li>
<li><span style="color:#1D7373">REGION_VOLOGODSK</span></li>
<li><span style="color:#1D7373">REGION_KARELIYA</span></li>
<li><span style="color:#1D7373">REGION_BURYATIA</span></li>
<li><span style="color:#1D7373">REGION_NORTH_OSETIA</span></li>
<li><span style="color:#1D7373">REGION_YAMAL</span></li>
<li><span style="color:#1D7373">REGION_MORDOVIA</span></li>
<li><span style="color:#1D7373">REGION_DAGESTAN</span></li>
<li><span style="color:#1D7373">REGION_AMUR</span></li>
<li><span style="color:#1D7373">REGION_SAHA</span></li>
<li><span style="color:#1D7373">REGION_MURMANSK</span></li>
<li><span style="color:#1D7373">REGION_ZABAYKALSK</span></li>
<li><span style="color:#1D7373">REGION_KBR</span></li>
<li><span style="color:#1D7373">REGION_HAKASIA</span></li>
<li><span style="color:#1D7373">REGION_ALTAI_REPUBLIC</span></li>
<li><span style="color:#1D7373">REGION_SAKHALIN</span></li>
<li><span style="color:#1D7373">REGION_KAMCHATKA</span></li>
<li><span style="color:#1D7373">REGION_KCHR</span></li>
<li><span style="color:#1D7373">REGION_MAGADAN</span></li>
<li><span style="color:#1D7373">REGION_CHECHNYA</span></li>
<li><span style="color:#1D7373">REGION_TIVA</span></li>
<li><span style="color:#1D7373">REGION_JEWISH_AUTONOMOUS</span></li>
<li><span style="color:#1D7373">REGION_KALMIKIYA</span></li>
<li><span style="color:#1D7373">REGION_INGUSHETIA</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L163">HotelParameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L68">THotelParameters</a></i>
</li>
<details open><summary><b>Message THotelParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L69">HotelClass</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L70">Location</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L71">Facilities</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L164">ClothesParameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L74">TClothesParameters</a></i>
</li>
<details open><summary><b>Message TClothesParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L79">Size</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L75">TSize</a></i>
</li>
<details open><summary><b>Message TSize</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L76">Unit</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L77">Values</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L81">Colors</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L165">AutoParameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L84">TAutoParameters</a></i>
</li>
<details open><summary><b>Message TAutoParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L85">VehicleDetails</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L86">Run</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L87">Year</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L88">BodyType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L30">EBodyType</a></i>
</li>
<details open><summary><b>Enum EBodyType</b></summary>
<ul>
<li><span style="color:#1D7373">BT_UNKNOWN</span></li>
<li><span style="color:#1D7373">BT_SEDAN_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_SEDAN</span></li>
<li><span style="color:#1D7373">BT_CABRIOLET</span></li>
<li><span style="color:#1D7373">BT_COMPACTVAN</span></li>
<li><span style="color:#1D7373">BT_COUPE_HARDTOP</span></li>
<li><span style="color:#1D7373">BT_COUPE</span></li>
<li><span style="color:#1D7373">BT_FASTBACK</span></li>
<li><span style="color:#1D7373">BT_VAN</span></li>
<li><span style="color:#1D7373">BT_HATCHBACK</span></li>
<li><span style="color:#1D7373">BT_LANDAU</span></li>
<li><span style="color:#1D7373">BT_LIFTBACK</span></li>
<li><span style="color:#1D7373">BT_LIMOUSINE</span></li>
<li><span style="color:#1D7373">BT_MICROVAN</span></li>
<li><span style="color:#1D7373">BT_MINIVAN</span></li>
<li><span style="color:#1D7373">BT_SUV</span></li>
<li><span style="color:#1D7373">BT_PHAETON_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_PHAETON</span></li>
<li><span style="color:#1D7373">BT_PICKUP</span></li>
<li><span style="color:#1D7373">BT_ROADSTER</span></li>
<li><span style="color:#1D7373">BT_TARGA</span></li>
<li><span style="color:#1D7373">BT_SPEEDSTER</span></li>
<li><span style="color:#1D7373">BT_UNIVERSAL</span></li>
<li><span style="color:#1D7373">BT_CROSSOVER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L89">Gearbox</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L57">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<ul>
<li><span style="color:#1D7373">GB_UNKNOWN</span></li>
<li><span style="color:#1D7373">GB_MANUAL</span></li>
<li><span style="color:#1D7373">GB_AUTOMATIC</span></li>
<li><span style="color:#1D7373">GB_VARIATOR</span></li>
<li><span style="color:#1D7373">GB_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L90">EngineVolume</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L91">EnginePower</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L92">OwnersNumber</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L93">EngineType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L94">Drive</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L95">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L168">AdvType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L117">EAdvType</a></i>
</li>
<details open><summary><b>Enum EAdvType</b></summary>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/db/schema.h?rev=7545212#L1563  https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/cs/libs/mkdb/resource.cpp?rev=7577587#L489 </p>

<ul>
<li><span style="color:#1D7373">AT_UNKNOWN</span></li>
<li><span style="color:#1D7373">AT_AUTO_ACCESSORIES</span></li>
<li><span style="color:#1D7373">AT_BEAUTY_HEALTH</span></li>
<li><span style="color:#1D7373">AT_BUILDING_MATERIALS</span></li>
<li><span style="color:#1D7373">AT_CARS</span></li>
<li><span style="color:#1D7373">AT_CHILDRENS_GOODS</span></li>
<li><span style="color:#1D7373">AT_CHINESE_SITES</span></li>
<li><span style="color:#1D7373">AT_CLOTHES</span></li>
<li><span style="color:#1D7373">AT_CUSTOM</span></li>
<li><span style="color:#1D7373">AT_FLIGHTS</span></li>
<li><span style="color:#1D7373">AT_FURNITURE</span></li>
<li><span style="color:#1D7373">AT_GAMES</span></li>
<li><span style="color:#1D7373">AT_HOTEL</span></li>
<li><span style="color:#1D7373">AT_PROMOCODES</span></li>
<li><span style="color:#1D7373">AT_REALTY</span></li>
<li><span style="color:#1D7373">AT_RETAIL</span></li>
<li><span style="color:#1D7373">AT_SPORTS</span></li>
<li><span style="color:#1D7373">AT_TIRES_DISKS</span></li>
<li><span style="color:#1D7373">AT_TRAVEL</span></li>
<li><span style="color:#1D7373">AT_TURKEY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L169">IsSmartTGAAllowed</a></b>  <i>bool</i>
<p> bl_type_direct_allowed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L170">MarketData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L141">TMarketData</a></i>
</li>
<details open><summary><b>Message TMarketData</b></summary>
<p> market: </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L142">PriceMin</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L143">PriceAvg</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L144">PriceMax</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L145">Rating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L146">RatingCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L147">MaxRating</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L148">OfferClass</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L149">OfferCount</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L150">IsNew</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L152">MarketModelId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L153">MarketCategoryId</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L171">LocationId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L172">Vendor</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L173">Model</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L177">ColorEnum</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/yabs_enums/enums.proto?rev=r9795881#L7">EColor</a></i>
</li>
<details open><summary><b>Enum EColor</b></summary>
<ul>
<li><span style="color:#1D7373">COLOR_UNKNOWN</span></li>
<li><span style="color:#1D7373">COLOR_BEIGE</span></li>
<li><span style="color:#1D7373">COLOR_WHITE</span></li>
<li><span style="color:#1D7373">COLOR_COLORLESS</span></li>
<li><span style="color:#1D7373">COLOR_CYAN</span></li>
<li><span style="color:#1D7373">COLOR_YELLOW</span></li>
<li><span style="color:#1D7373">COLOR_GREEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLDEN</span></li>
<li><span style="color:#1D7373">COLOR_GOLD</span></li>
<li><span style="color:#1D7373">COLOR_BROWN</span></li>
<li><span style="color:#1D7373">COLOR_RED</span></li>
<li><span style="color:#1D7373">COLOR_ORANGE</span></li>
<li><span style="color:#1D7373">COLOR_MAGENTA</span></li>
<li><span style="color:#1D7373">COLOR_PINK</span></li>
<li><span style="color:#1D7373">COLOR_SILVERY</span></li>
<li><span style="color:#1D7373">COLOR_SILVER</span></li>
<li><span style="color:#1D7373">COLOR_GRAY</span></li>
<li><span style="color:#1D7373">COLOR_BLUE</span></li>
<li><span style="color:#1D7373">COLOR_PURPLE</span></li>
<li><span style="color:#1D7373">COLOR_BLACK</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L238">BroadPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L6">TPhrase</a></i>
</li>
<details open><summary><b>Message TPhrase</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L24">BroadPhraseId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L25">SimDistance</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L26">PhraseId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L27">NormType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L9">ENormType</a></i>
</li>
<details open><summary><b>Enum ENormType</b></summary>
<p> compliant with https://arcanum.yandex-team.ru/arc/trunk/arcadia/yabs/server/libs/enums/norm_type.h </p>

<ul>
<li><span style="color:#1D7373">NONE_TYPE</span></li>
<li><span style="color:#1D7373">NORM</span></li>
<li><span style="color:#1D7373">SNORM</span></li>
<li><span style="color:#1D7373">OFFER</span></li>
<li><span style="color:#1D7373">OFFER_GROUP</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L28">PhraseData</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L30">PhraseDebugInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L18">TPhraseDebugInfo</a></i>
</li>
<details open><summary><b>Message TPhraseDebugInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L19">PhraseTemplate</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L20">PhraseTemplateType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/phrase.proto?rev=r9795881#L21">SearchCount</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L239">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L240">SelectionRankPredictions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L180">TPrediction</a></i>
</li>
<details open><summary><b>Message TPrediction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L181">ModelId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L182">Prediction</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L183">TimeStamp</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L241">Age</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L242">OfferProperties</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L328">TOffer</a></i>
<p> Use tests to ensure the existence of fields in this field </p>

</li>
<details open><summary><b>Message TOffer</b></summary>
<p> *******************************  ** Id fields                 **  ** proto range from 1 to 100 **  ******************************* </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L336">BusinessId</a></b>  <i>uint32</i>
<p> Composite unique key of offer  Patner identifier in Yandex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L338">OfferId</a></b>  <i>string</i>
<p> B2B offer identifier from partner </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L340">OfferYabsId</a></b>  <i>uint64</i>
<p> Hash of B2B identifier (should be unique in subset of all offers from one partner) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L342">ShopId</a></b>  <i>uint32</i>
<p> Identifier of Yandex services set (known as shop) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L346">ClientId</a></b>  <i>uint64</i>
<p> Additional identifiers  Partner identifier in accounting balance </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L348">FeedId</a></b>  <i>uint32</i>
<p> Feed identifier in B2C Yndex.Market cabinet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L350">DirectFeedId</a></b>  <i>uint64</i>
<p> Feed identifier in Yandex.Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L351">WareMd5</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L353">OriginalSku</a></b>  <i>string</i>
<p> SKU in parnter content system </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L355">FeedItemGroupId</a></b>  <i>string</i>
<p> Id of group inside feed. Needed to create retargeting for group of e.g. iPhones 13 of different colors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L364">TimestampSeconds</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L367">DataType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L37">EDataType</a></i>
<p> Data type for BannerLand </p>

</li>
<details open><summary><b>Enum EDataType</b></summary>
<ul>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_MARKET</span></li>
<li><span style="color:#1D7373">DATA_TYPE_AUTORU</span></li>
<li><span style="color:#1D7373">DATA_TYPE_YANDEX_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_MERCHANT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_CUSTOM</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_FLIGHT</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_TRAVEL</span></li>
<li><span style="color:#1D7373">DATA_TYPE_GOOGLE_HOTEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L370">OfferSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L54">EOfferSource</a></i>
<p> Offer source (feed or site) </p>

</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_SOURCE_FEED</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SITE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_SPECIAL_URL</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_CRAWLER</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_DSE</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_LINKS</span></li>
<li><span style="color:#1D7373">OFFER_SOURCE_TSKV_GEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L373">ProductType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L68">EProductType</a></i>
<p> Product type for offer </p>

</li>
<details open><summary><b>Enum EProductType</b></summary>
<ul>
<li><span style="color:#1D7373">PRODUCT_TYPE_UNKNOWN</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AUTO_ACCESSORIES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_AVIA_TICKETS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BEAUTY_HEALTH</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BUILDING_MATERIALS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CARS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHILDRENS_GOODS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_CHINESE_SITES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_DSE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_EXTERNAL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_FURNITURE</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_GAMES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_HOTELS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_LIST</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_PROMOCODES</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_REALTY</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_SPORTS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TIRES_DISKS</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_TRAVEL</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_WEAR</span></li>
<li><span style="color:#1D7373">PRODUCT_TYPE_BOOKS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L375">OfferType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L64">EOfferType</a></i>
<p> Offer type </p>

</li>
<details open><summary><b>Enum EOfferType</b></summary>
<ul>
<li><span style="color:#1D7373">OFFER_TYPE_VENDOR_MODEL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L378">OfferLanguage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L48">ELanguageCode</a></i>
<p> Offer texts language </p>

</li>
<details open><summary><b>Enum ELanguageCode</b></summary>
<ul>
<li><span style="color:#1D7373">LANGUAGE_UNKNOWN</span></li>
<li><span style="color:#1D7373">LANGUAGE_RU</span></li>
<li><span style="color:#1D7373">LANGUAGE_EN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L381">DisableStatus</a></b>  <i>bool</i>
<p> Is offer active </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L389">Model</a></b>  <i>string</i>
<p> Model name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L391">Vendor</a></b>  <i>string</i>
<p> Manufacturer or brand </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L393">TypePrefix</a></b>  <i>string</i>
<p> Type or category name of good (used in title) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L395">Name</a></b>  <i>string</i>
<p> Full offer name </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L398">Description</a></b>  <i>string</i>
<p> Detailed description of offer </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L401">Url</a></b>  <i>string</i>
<p> URL to offer on partner site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L403">UrlOriginalDomain</a></b>  <i>string</i>
<p> Domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L405">UrlOriginalDomainId</a></b>  <i>uint64</i>
<p> Id of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L407">UrlMainMirror</a></b>  <i>string</i>
<p> Main mirror (after redirects) of domain in offer URL </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L409">UrlMainMirrorId</a></b>  <i>uint64</i>
<p> Id of main mirror domain </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L412">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L110">TImageData</a></i>
<p> Offer images data (original URLs and avatars) </p>

</li>
<details open><summary><b>Message TImageData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L123">SourceUrl</a></b>  <i>string</i>
<p> Image URL on client site </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L126">Status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L112">EAvatarizationStatus</a></i>
<p> Status of image loading into avatars service </p>

</li>
<details open><summary><b>Enum EAvatarizationStatus</b></summary>
<p> TODO: Replace with Market.DataCamp.MarketPicture.Status after complete MARKETINDEXER-41756 </p>

<ul>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_UNKNOWN</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_AVAILABLE</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_FAILED</span></li>
<li><span style="color:#1D7373">AVATARIZATION_STATUS_REMOVED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L129">AvatarsInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L26">TImagesInfo</a></i>
<p> Image avatars information </p>

</li>
<details open><summary><b>Message TImagesInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L85">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L27">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L35">Format</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L36">Width</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L37">Height</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L38">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L41">SmartCenters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order.  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L43">SmartCenter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L28">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L29">X</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L30">Y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L31">W</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L32">H</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L86">ImageType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L89">MdsMeta</a></b>  <i>string</i>
<p> MdsMeta is deprecated and will soon stop being recorded.  Use ParsedMdsMeta instead. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L90">IsImageBanner</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L91">AvatarsImage</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L94">ParsedMdsMeta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L56">TMdsMeta</a></i>
<p> Set of fields from "meta" part of the Avatarnitsa response  that is useful for profile consumers. </p>

</li>
<details open><summary><b>Message TMdsMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L66">ColorWizBack</a></b>  <i>string</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz  </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L68">ColorWizButton</a></b>  <i>string</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L70">ColorWizButtonText</a></b>  <i>string</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L72">AverageColor</a></b>  <i>string</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L75">ImageQuality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L78">BackgroundColors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L57">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L58">Bottom</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L59">Left</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L60">Right</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L61">Top</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L80">MainColor</a></b>  <i>string</i>
<p> Dominant image color </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L82">Crc64</a></b>  <i>uint64</i>
<p> Image hash code </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L415">Currency</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L36">Currency</a></i>
<p> Offer currency </p>

</li>
<details open><summary><b>Enum Currency</b></summary>
<ul>
<li><span style="color:#1D7373">CURRENCY_UNDEFINED</span></li>
<li><span style="color:#1D7373">RUR</span></li>
<li><span style="color:#1D7373">USD</span></li>
<li><span style="color:#1D7373">EUR</span></li>
<li><span style="color:#1D7373">UAH</span></li>
<li><span style="color:#1D7373">KZT</span></li>
<li><span style="color:#1D7373">BYN</span></li>
<li><span style="color:#1D7373">GBP</span></li>
<li><span style="color:#1D7373">TRY</span></li>
<li><span style="color:#1D7373">ALL</span></li>
<li><span style="color:#1D7373">AFN</span></li>
<li><span style="color:#1D7373">ARS</span></li>
<li><span style="color:#1D7373">AWG</span></li>
<li><span style="color:#1D7373">AUD</span></li>
<li><span style="color:#1D7373">AZN</span></li>
<li><span style="color:#1D7373">BBD</span></li>
<li><span style="color:#1D7373">BZD</span></li>
<li><span style="color:#1D7373">BMD</span></li>
<li><span style="color:#1D7373">BOB</span></li>
<li><span style="color:#1D7373">BAM</span></li>
<li><span style="color:#1D7373">BWP</span></li>
<li><span style="color:#1D7373">BGN</span></li>
<li><span style="color:#1D7373">BRL</span></li>
<li><span style="color:#1D7373">BND</span></li>
<li><span style="color:#1D7373">KHR</span></li>
<li><span style="color:#1D7373">CAD</span></li>
<li><span style="color:#1D7373">KYD</span></li>
<li><span style="color:#1D7373">CLP</span></li>
<li><span style="color:#1D7373">CNY</span></li>
<li><span style="color:#1D7373">COP</span></li>
<li><span style="color:#1D7373">CRC</span></li>
<li><span style="color:#1D7373">HRK</span></li>
<li><span style="color:#1D7373">CUP</span></li>
<li><span style="color:#1D7373">CZK</span></li>
<li><span style="color:#1D7373">DKK</span></li>
<li><span style="color:#1D7373">DOP</span></li>
<li><span style="color:#1D7373">XCD</span></li>
<li><span style="color:#1D7373">EGP</span></li>
<li><span style="color:#1D7373">SVC</span></li>
<li><span style="color:#1D7373">FKP</span></li>
<li><span style="color:#1D7373">FJD</span></li>
<li><span style="color:#1D7373">GHS</span></li>
<li><span style="color:#1D7373">GIP</span></li>
<li><span style="color:#1D7373">GTQ</span></li>
<li><span style="color:#1D7373">GYD</span></li>
<li><span style="color:#1D7373">HNL</span></li>
<li><span style="color:#1D7373">HKD</span></li>
<li><span style="color:#1D7373">HUF</span></li>
<li><span style="color:#1D7373">ISK</span></li>
<li><span style="color:#1D7373">INR</span></li>
<li><span style="color:#1D7373">IDR</span></li>
<li><span style="color:#1D7373">IRR</span></li>
<li><span style="color:#1D7373">ILS</span></li>
<li><span style="color:#1D7373">JMD</span></li>
<li><span style="color:#1D7373">JPY</span></li>
<li><span style="color:#1D7373">KPW</span></li>
<li><span style="color:#1D7373">KRW</span></li>
<li><span style="color:#1D7373">KGS</span></li>
<li><span style="color:#1D7373">LAK</span></li>
<li><span style="color:#1D7373">LBP</span></li>
<li><span style="color:#1D7373">LRD</span></li>
<li><span style="color:#1D7373">MKD</span></li>
<li><span style="color:#1D7373">MYR</span></li>
<li><span style="color:#1D7373">MUR</span></li>
<li><span style="color:#1D7373">MXN</span></li>
<li><span style="color:#1D7373">MNT</span></li>
<li><span style="color:#1D7373">MAD</span></li>
<li><span style="color:#1D7373">MZN</span></li>
<li><span style="color:#1D7373">NAD</span></li>
<li><span style="color:#1D7373">NPR</span></li>
<li><span style="color:#1D7373">ANG</span></li>
<li><span style="color:#1D7373">NZD</span></li>
<li><span style="color:#1D7373">NIO</span></li>
<li><span style="color:#1D7373">NGN</span></li>
<li><span style="color:#1D7373">NOK</span></li>
<li><span style="color:#1D7373">OMR</span></li>
<li><span style="color:#1D7373">PKR</span></li>
<li><span style="color:#1D7373">PAB</span></li>
<li><span style="color:#1D7373">PYG</span></li>
<li><span style="color:#1D7373">PEN</span></li>
<li><span style="color:#1D7373">PHP</span></li>
<li><span style="color:#1D7373">PLN</span></li>
<li><span style="color:#1D7373">QAR</span></li>
<li><span style="color:#1D7373">RON</span></li>
<li><span style="color:#1D7373">SHP</span></li>
<li><span style="color:#1D7373">SAR</span></li>
<li><span style="color:#1D7373">RSD</span></li>
<li><span style="color:#1D7373">SCR</span></li>
<li><span style="color:#1D7373">SGD</span></li>
<li><span style="color:#1D7373">SBD</span></li>
<li><span style="color:#1D7373">SOS</span></li>
<li><span style="color:#1D7373">ZAR</span></li>
<li><span style="color:#1D7373">LKR</span></li>
<li><span style="color:#1D7373">SEK</span></li>
<li><span style="color:#1D7373">CHF</span></li>
<li><span style="color:#1D7373">SRD</span></li>
<li><span style="color:#1D7373">SYP</span></li>
<li><span style="color:#1D7373">TWD</span></li>
<li><span style="color:#1D7373">THB</span></li>
<li><span style="color:#1D7373">TTD</span></li>
<li><span style="color:#1D7373">AED</span></li>
<li><span style="color:#1D7373">UYU</span></li>
<li><span style="color:#1D7373">UZS</span></li>
<li><span style="color:#1D7373">VEF</span></li>
<li><span style="color:#1D7373">VND</span></li>
<li><span style="color:#1D7373">YER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L417">Price</a></b>  <i>uint64</i>
<p> Price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L419">PriceMicrosPart</a></b>  <i>uint64</i>
<p> Price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L421">OldPrice</a></b>  <i>uint64</i>
<p> Previous price in currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L423">OldPriceMicrosPart</a></b>  <i>uint64</i>
<p> Previous price fractional part in micro-currency (fractional price part multiplied by 10^6) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L426">CategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Offer categoryzation info </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L428">Breadcrumbs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L153">TBreadcrumbsData</a></i>
<p> Navigational path on site </p>

</li>
<details open><summary><b>Message TBreadcrumbsData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L156">Path</a></b>  <i>string</i>
<p> Text path in navigarional tree of site  Each item contains a node name, first item is root element </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L431">Available</a></b>  <i>bool</i>
<p> Is offer available to order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L433">DeliveryOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L144">TDeliveryOptions</a></i>
<p> Detailed delivery options </p>

</li>
<details open><summary><b>Message TDeliveryOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L146">Pickup</a></b>  <i>bool</i>
<p> Available for pickup </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L148">Store</a></b>  <i>bool</i>
<p> Available in store without order </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L150">Delivery</a></b>  <i>bool</i>
<p> Available for order with courier delivery </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L436">SalesNotes</a></b>  <i>string</i>
<p> Sales notes as human readable text </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L439">ManufacturerWarranty</a></b>  <i>bool</i>
<p> Offer has manufacturer warranty </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L442">ShopCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Offer category from partner feed </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L445">MarketCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> Yandex Market categories </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L448">BannerLandCategoryPath</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L139">TCategoryPath</a></i>
<p> Multik categories </p>

</li>
<details open><summary><b>Message TCategoryPath</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L141">Nodes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L132">TCategoryNode</a></i>
<p> List of nodes in path from categorization hierarchy (in order from root to leaf) </p>

</li>
<details open><summary><b>Message TCategoryNode</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L134">Id</a></b>  <i>uint64</i>
<p> Unique id of node in categorization hierarchy </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L136">Name</a></b>  <i>string</i>
<p> Category name </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L451">ParametersData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L159">TOfferParameter</a></i>
<p> Raw unstructured parameters data </p>

</li>
<details open><summary><b>Message TOfferParameter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L160">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L161">Unit</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L162">Value</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L454">Parameters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L165">TOfferStructuredParameters</a></i>
<p> Parsed parameters </p>

</li>
<details open><summary><b>Message TOfferStructuredParameters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L166">Age</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L167">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L168">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L169">Season</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L170">Sex</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L171">Corpus</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L172">Type</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L173">Collection</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L174">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L175">Length</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L176">Width</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L177">Height</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L178">SizeUnit</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L457">Age</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L30">FormalAge</a></i>
<p> Product age for moderation </p>

</li>
<details open><summary><b>Message FormalAge</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L32">time</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L33">unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L19">TimeUnit</a></i>
</li>
<details open><summary><b>Enum TimeUnit</b></summary>
<ul>
<li><span style="color:#1D7373">INVALID_TIME_UNIT</span></li>
<li><span style="color:#1D7373">HOUR</span></li>
<li><span style="color:#1D7373">DAY</span></li>
<li><span style="color:#1D7373">WEEK</span></li>
<li><span style="color:#1D7373">MONTH</span></li>
<li><span style="color:#1D7373">YEAR</span></li>
<li><span style="color:#1D7373">UNLIMITED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L460">Adult</a></b>  <i>bool</i>
<p> Product offer for adults </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L463">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L791">FormalCondition</a></i>
<p> Product condition: used or like new; reason for condition </p>

</li>
<details open><summary><b>Message FormalCondition</b></summary>
<p> Cостояние товара  https://yandex.ru/support/partnermarket/elements/condition.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L800">type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L793">Type</a></i>
</li>
<details open><summary><b>Enum Type</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN_TYPE</span></li>
<li><span style="color:#1D7373">LIKENEW</span></li>
<li><span style="color:#1D7373">USED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L801">reason</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L465">VideoCreatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L16">ProcessedVideo</a></i>
</li>
<details open><summary><b>Message ProcessedVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L22">id</a></b>  <i>string</i>
<p> ID креатива </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L23">status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L17">Status</a></i>
</li>
<details open><summary><b>Enum Status</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED</span></li>
<li><span style="color:#1D7373">AVAILABLE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L24">original_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L25">creative_id</a></b>  <i>uint64</i>
<p> ID креатива, число </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L466">ImagesInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L473">Custom</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L193">TCustomData</a></i>
</li>
<details open><summary><b>Message TCustomData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L194">OriginalOfferId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L195">Id2</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L196">CustomPhrases</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L474">GoogleMerchant</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L181">TGoogleMerchantData</a></i>
</li>
<details open><summary><b>Message TGoogleMerchantData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L182">AgeGroup</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L134">EGoogleMerchantAgeGroup</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantAgeGroup</b></summary>
<ul>
<li><span style="color:#1D7373">GM_AGE_NEWBORN</span></li>
<li><span style="color:#1D7373">GM_AGE_INFANT</span></li>
<li><span style="color:#1D7373">GM_AGE_TODDLER</span></li>
<li><span style="color:#1D7373">GM_AGE_KIDS</span></li>
<li><span style="color:#1D7373">GM_AGE_ADULT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L183">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L184">Gender</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L142">EGoogleMerchantGender</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantGender</b></summary>
<ul>
<li><span style="color:#1D7373">GM_GENDER_MALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_FEMALE</span></li>
<li><span style="color:#1D7373">GM_GENDER_UNISEX</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L185">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L186">Pattern</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L187">Size</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L188">SizeType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L148">EGoogleMerchantSizeType</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeType</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_TYPE_REGULAR</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PETITE</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_PLUS</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_TALL</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_BIG</span></li>
<li><span style="color:#1D7373">GM_SIZE_TYPE_MATERNITY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L189">SizeSystem</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L157">EGoogleMerchantSizeSystem</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantSizeSystem</b></summary>
<ul>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_AU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_BR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_CN</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_DE</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_EU</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_FR</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_IT</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_JP</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_MEX</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_UK</span></li>
<li><span style="color:#1D7373">GM_SIZE_SYSTEM_US</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L190">Condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/GoogleMerchantSpecific.proto?rev=r9795881#L17">EGoogleMerchantCondition</a></i>
</li>
<details open><summary><b>Enum EGoogleMerchantCondition</b></summary>
<ul>
<li><span style="color:#1D7373">GM_CONDITION_NEW</span></li>
<li><span style="color:#1D7373">GM_CONDITION_REFURBISHED</span></li>
<li><span style="color:#1D7373">GM_CONDITION_USED</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L475">Car</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L210">TCarData</a></i>
</li>
<details open><summary><b>Message TCarData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L211">UniqueId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L212">VIN</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L214">ModificationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L215">ModificationInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L199">TCarModificationInfo</a></i>
</li>
<details open><summary><b>Message TCarModificationInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L200">EngineVolume</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L201">EngineVolumeValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L202">EnginePower</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L203">EnginePowerValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L204">EnginePowerUnit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L104">ECarPowerUnit</a></i>
</li>
<details open><summary><b>Enum ECarPowerUnit</b></summary>
<p> Единицы измерения мощности двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_HORSEPOWER_UNIT</span></li>
<li><span style="color:#1D7373">CAR_KILOWATT_UNIT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L205">EngineType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L31">ECarEngineType</a></i>
</li>
<details open><summary><b>Enum ECarEngineType</b></summary>
<p> Тип двигателя </p>

<ul>
<li><span style="color:#1D7373">CAR_ENGINE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_PETROL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYBRID</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_ELECTRO</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_HYDROGEN</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_DIESEL</span></li>
<li><span style="color:#1D7373">CAR_ENGINE_GAS_POWERED_PETROL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L206">Gearbox</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L44">ECarGearbox</a></i>
</li>
<details open><summary><b>Enum ECarGearbox</b></summary>
<p> Тип коробки передач </p>

<ul>
<li><span style="color:#1D7373">CAR_GEARBOX_MANUAL</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_AUTOMATIC</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_VARIATOR</span></li>
<li><span style="color:#1D7373">CAR_GEARBOX_ROBOT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L207">Drive</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L52">ECarDrive</a></i>
</li>
<details open><summary><b>Enum ECarDrive</b></summary>
<p> Привод автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_FWD</span></li>
<li><span style="color:#1D7373">CAR_RWD</span></li>
<li><span style="color:#1D7373">CAR_AWD</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L217">ComplectationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L218">BodyType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L219">SteeringWheel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L25">ECarSteeringWheel</a></i>
</li>
<details open><summary><b>Enum ECarSteeringWheel</b></summary>
<p> Расположение руля (левый или правый) </p>

<ul>
<li><span style="color:#1D7373">CAR_LEFT_HAND_DRIVE</span></li>
<li><span style="color:#1D7373">CAR_RIGHT_HAND_DRIVE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L220">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L221">Metallic</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L222">CustomStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L77">ECarCustomStatus</a></i>
</li>
<details open><summary><b>Enum ECarCustomStatus</b></summary>
<p> Таможенный статус </p>

<ul>
<li><span style="color:#1D7373">CAR_CUSTOM_CLEARED</span></li>
<li><span style="color:#1D7373">CAR_CUSTOM_NOT_CLEARED</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L223">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L85">ECarState</a></i>
</li>
<details open><summary><b>Enum ECarState</b></summary>
<p> Состояние автомобиля </p>

<ul>
<li><span style="color:#1D7373">CAR_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">CAR_STATE_EXCELLENT</span></li>
<li><span style="color:#1D7373">CAR_STATE_GOOD</span></li>
<li><span style="color:#1D7373">CAR_STATE_NORMAL</span></li>
<li><span style="color:#1D7373">CAR_STATE_REQUIRE_REPAIR</span></li>
<li><span style="color:#1D7373">CAR_STATE_DOESNT_REQUIRE_REPAIR</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L224">OwnersNumber</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/CarSpecific.proto?rev=r9795881#L95">ECarOwnersNumber</a></i>
</li>
<details open><summary><b>Enum ECarOwnersNumber</b></summary>
<p> Количество владельцев по ПТС </p>

<ul>
<li><span style="color:#1D7373">CAR_NO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_ONE_OWNER</span></li>
<li><span style="color:#1D7373">CAR_TWO_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_THREE_OWNERS</span></li>
<li><span style="color:#1D7373">CAR_FOUR_OR_MORE_OWNERS</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L225">Run</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L226">Year</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L227">RegistryYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L228">DoorsCount</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L476">Travel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L239">TTravelData</a></i>
</li>
<details open><summary><b>Message TTravelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L241">DestinationId</a></b>  <i>string</i>
<p> Пункт назначения </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L242">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L245">OriginId</a></b>  <i>string</i>
<p> Пункт отправления </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L246">OriginName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L477">Hotel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L249">THotelData</a></i>
</li>
<details open><summary><b>Message THotelData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L250">PropertyId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L252">PropertyName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L254">DestinationName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L257">StarRating</a></b>  <i>uint32</i>
<p> Number stars at the hotel (from 1 to 5) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L260">Score</a></b>  <i>double</i>
<p> User score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L263">MaxScore</a></b>  <i>uint32</i>
<p> The max allowed user's score </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L265">Facilities</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L267">Category</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L269">Address</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L478">Flight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L231">TFlightData</a></i>
</li>
<details open><summary><b>Message TFlightData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L232">OriginId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L233">OriginName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L235">DestinationId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L236">DestinationName</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L479">Realty</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L303">TRealtyData</a></i>
</li>
<details open><summary><b>Message TRealtyData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L304">RealtyCategory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L28">ERealtyCategory</a></i>
</li>
<details open><summary><b>Enum ERealtyCategory</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_COMMERCIAL</span></li>
<li><span style="color:#1D7373">REALTY_COTTAGE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_WITH_LOT</span></li>
<li><span style="color:#1D7373">REALTY_LOT</span></li>
<li><span style="color:#1D7373">REALTY_HOUSE_PART</span></li>
<li><span style="color:#1D7373">REALTY_FLAT</span></li>
<li><span style="color:#1D7373">REALTY_ROOM</span></li>
<li><span style="color:#1D7373">REALTY_TOWNHOUSE</span></li>
<li><span style="color:#1D7373">REALTY_DUPLEX</span></li>
<li><span style="color:#1D7373">REALTY_GARAGE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L305">Location</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L278">TRealtyLocation</a></i>
</li>
<details open><summary><b>Message TRealtyLocation</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L279">Address</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L280">Region</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L281">LocalityName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L282">MetroName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L283">MetroTimeOnFoot</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L284">MetroTimeOnTransport</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L306">DealStatus</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L155">ERealtyDealStatus</a></i>
</li>
<details open><summary><b>Enum ERealtyDealStatus</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_DEAL_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_REASSIGMENT</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_PRIMARY_SALE_OF_SECONDARY</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_COUNTERSALE</span></li>
<li><span style="color:#1D7373">REALTY_DEAL_SALE_FROM_DEVELOPER</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L307">RealtyObjectData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L287">TRealtyObjectData</a></i>
</li>
<details open><summary><b>Message TRealtyObjectData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L288">Area</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L273">TRealtyArea</a></i>
</li>
<details open><summary><b>Message TRealtyArea</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L274">Value</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L275">Unit</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L80">ERealtyAreaUnit</a></i>
</li>
<details open><summary><b>Enum ERealtyAreaUnit</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_SQUARE_METER</span></li>
<li><span style="color:#1D7373">REALTY_ARE</span></li>
<li><span style="color:#1D7373">REALTY_HECTARE</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L289">Rooms</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L290">Floor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L291">Renovation</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L196">ERealtyRenovation</a></i>
</li>
<details open><summary><b>Enum ERealtyRenovation</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_RENOVATION_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_EURO</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_COSMETIC</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_DESIGNER</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_REQUIRES_REPAIR</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_FINE_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_KEY</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_ROUGH_FINISH</span></li>
<li><span style="color:#1D7373">REALTY_RENOVATION_WITH_FINISH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L292">NewFlat</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L308">BuildingData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L295">TRealtyBuildingData</a></i>
</li>
<details open><summary><b>Message TRealtyBuildingData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L296">BuildingType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L174">ERealtyBuildingType</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingType</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_BLOCK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_WOODEN_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_BRICK_MONOLITHIC_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_PANEL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_METAL_BUILDING</span></li>
<li><span style="color:#1D7373">REALTY_MONOLITHIC_CARCASS_BUILDING</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L297">FloorsTotal</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L298">BuiltYear</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L299">ReadyQuarter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L217">ERealtyReadyQuarter</a></i>
</li>
<details open><summary><b>Enum ERealtyReadyQuarter</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_QUARTER_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FIRST</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_SECOND</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_THIRD</span></li>
<li><span style="color:#1D7373">REALTY_QUARTER_FOURTH</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L300">BuildingState</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/specific/RealtySpecific.proto?rev=r9795881#L209">ERealtyBuildingState</a></i>
</li>
<details open><summary><b>Enum ERealtyBuildingState</b></summary>
<ul>
<li><span style="color:#1D7373">REALTY_STATE_UNKNOWN</span></li>
<li><span style="color:#1D7373">REALTY_STATE_BUILT</span></li>
<li><span style="color:#1D7373">REALTY_STATE_HANDOVER</span></li>
<li><span style="color:#1D7373">REALTY_STATE_UNFINISHED</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L488">ClientAdTitle</a></b>  <i>string</i>
<p> Fixed banner title (filled by UseAsName) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/offer/offer.proto?rev=r9795881#L491">ClientAdBody</a></b>  <i>string</i>
<p> Fixed banner body (filled by UseAsBody) </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L245">VideoCreatives</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L16">ProcessedVideo</a></i>
</li>
<details open><summary><b>Message ProcessedVideo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L22">id</a></b>  <i>string</i>
<p> ID креатива </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L23">status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L17">Status</a></i>
</li>
<details open><summary><b>Enum Status</b></summary>
<ul>
<li><span style="color:#1D7373">UNDEFINED</span></li>
<li><span style="color:#1D7373">AVAILABLE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L24">original_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Video.proto?rev=r9795881#L25">creative_id</a></b>  <i>uint64</i>
<p> ID креатива, число </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L246">Images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L260">BannerHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L261">RowId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L262">BannerDebugInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L186">TBannerDebugInfo</a></i>
</li>
<details open><summary><b>Message TBannerDebugInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L187">ExperimentalGenerationId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L188">TitleSource</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L189">TitleTemplate</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L190">TitleTemplateType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L191">TaskGroupingId</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L192">BannerRankPredictions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L180">TPrediction</a></i>
</li>
<details open><summary><b>Message TPrediction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L181">ModelId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L182">Prediction</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L183">TimeStamp</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L263">Timings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L251">TTimings</a></i>
</li>
<details open><summary><b>Message TTimings</b></summary>
<p> *******************  ** System fields **  ******************* </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L252">BannerlandBeginTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L253">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L254">OfferPrepareTime</a></b>  <i>uint64</i>
<p> Time from downloading offer in DC to import BL. Not updating on Service Log. See https://st.yandex-team.ru/BLRT-219 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L255">FeedDownloadTimestamp</a></b>  <i>uint64</i>
<p> Timestamp when feed was downloaded. See https://st.yandex-team.ru/MARKETINDEXER-43038#618ce67833798276fb67f1f9 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L256">StartParsingTimestamp</a></b>  <i>uint64</i>
<p> Start parsing feed timestamp. See https://st.yandex-team.ru/MARKETINDEXER-43038#618ce67833798276fb67f1f9 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L257">EndParsingTimestamp</a></b>  <i>uint64</i>
<p> End parsing feed timestamp. See https://st.yandex-team.ru/MARKETINDEXER-43038#618ce67833798276fb67f1f9 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/v2/bannerland/banner.proto?rev=r9795881#L268">CanonizedUrl</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L504">CandidateCaesarImportTimestamp</a></b>  <i>uint64</i>
<p> Timestamp of import new banner in caesar </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L505">ModerationDuration</a></b>  <i>uint64</i>
<p> Full moderation duration (Send banner from CaeSaR to Modadvert -> Receive in CaeSaR) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L506">BannerFlags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/irt/bannerland/proto/banner_flags/banner_flags.proto?rev=r9795881#L10">EBannerFlag</a></i>
<p> merge MarkupFlags and MinusRegions to BannerFlags </p>

</li>
<details open><summary><b>Enum EBannerFlag</b></summary>
<ul>
<li><span style="color:#1D7373">REGION_RU</span></li>
<li><span style="color:#1D7373">REGION_KZ</span></li>
<li><span style="color:#1D7373">REGION_UA</span></li>
<li><span style="color:#1D7373">REGION_RB</span></li>
<li><span style="color:#1D7373">REGION_TR</span></li>
<li><span style="color:#1D7373">REGION_UZ</span></li>
<li><span style="color:#1D7373">REGION_OTHER</span></li>
<li><span style="color:#1D7373">DIETARYSUPPL</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON</span></li>
<li><span style="color:#1D7373">FINANCE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PROJECT_DECLARATION</span></li>
<li><span style="color:#1D7373">MED_SERVICES</span></li>
<li><span style="color:#1D7373">MED_EQUIPMENT</span></li>
<li><span style="color:#1D7373">PHARMACY</span></li>
<li><span style="color:#1D7373">SUGARING</span></li>
<li><span style="color:#1D7373">LOAN</span></li>
<li><span style="color:#1D7373">INSURANCE</span></li>
<li><span style="color:#1D7373">BANKS</span></li>
<li><span style="color:#1D7373">MATERNITY_CAPITAL</span></li>
<li><span style="color:#1D7373">PAWNSHOP</span></li>
<li><span style="color:#1D7373">CREDIT_CONSUMER_COOPERATIVE</span></li>
<li><span style="color:#1D7373">MFI</span></li>
<li><span style="color:#1D7373">PAYMENT</span></li>
<li><span style="color:#1D7373">FOREX</span></li>
<li><span style="color:#1D7373">FOREX_BROKER</span></li>
<li><span style="color:#1D7373">BINARY_OPTIONS</span></li>
<li><span style="color:#1D7373">CHARITY</span></li>
<li><span style="color:#1D7373">GAMBLE</span></li>
<li><span style="color:#1D7373">LOTTERY</span></li>
<li><span style="color:#1D7373">TOBACCO_EX</span></li>
<li><span style="color:#1D7373">OPTICS</span></li>
<li><span style="color:#1D7373">POPULAR_MEDICINE</span></li>
<li><span style="color:#1D7373">NOT_MEDICINE</span></li>
<li><span style="color:#1D7373">ACIDS</span></li>
<li><span style="color:#1D7373">ALCOHOL_ALLOWED</span></li>
<li><span style="color:#1D7373">BOOKMAKER</span></li>
<li><span style="color:#1D7373">REALTOR</span></li>
<li><span style="color:#1D7373">ELECTRONIC_OSAGO</span></li>
<li><span style="color:#1D7373">TATTOO</span></li>
<li><span style="color:#1D7373">JEWELRY</span></li>
<li><span style="color:#1D7373">COLLECTOR</span></li>
<li><span style="color:#1D7373">CERTIFICATION</span></li>
<li><span style="color:#1D7373">DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">OTHER</span></li>
<li><span style="color:#1D7373">LEGAL_VAPE</span></li>
<li><span style="color:#1D7373">SOCIAL_ADVERTISING</span></li>
<li><span style="color:#1D7373">VETERINARY_PHARMACY</span></li>
<li><span style="color:#1D7373">ABORTION</span></li>
<li><span style="color:#1D7373">MEDICINE</span></li>
<li><span style="color:#1D7373">ALCOHOL</span></li>
<li><span style="color:#1D7373">TOBACCO</span></li>
<li><span style="color:#1D7373">ILLEGAL</span></li>
<li><span style="color:#1D7373">ASOCIAL</span></li>
<li><span style="color:#1D7373">UNFAMILY</span></li>
<li><span style="color:#1D7373">TRAGIC</span></li>
<li><span style="color:#1D7373">MATCHMAKING</span></li>
<li><span style="color:#1D7373">SUSPICIOUS</span></li>
<li><span style="color:#1D7373">ANNOYING</span></li>
<li><span style="color:#1D7373">GOODFACE</span></li>
<li><span style="color:#1D7373">DIPLOMA</span></li>
<li><span style="color:#1D7373">GAMBLE_ONLINE</span></li>
<li><span style="color:#1D7373">TOBACCO_PROHIBITED</span></li>
<li><span style="color:#1D7373">ILLEGAL_DIET</span></li>
<li><span style="color:#1D7373">DRUGS</span></li>
<li><span style="color:#1D7373">TELEMED</span></li>
<li><span style="color:#1D7373">ALCOHOL_PROHIBITED</span></li>
<li><span style="color:#1D7373">MAGIC</span></li>
<li><span style="color:#1D7373">CSW_DISCLAIMER</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE</span></li>
<li><span style="color:#1D7373">AD_ON_TRANSPORT</span></li>
<li><span style="color:#1D7373">ANIMATED</span></li>
<li><span style="color:#1D7373">NOT_ANIMATED</span></li>
<li><span style="color:#1D7373">COLLECTOR_DISCLAIMER</span></li>
<li><span style="color:#1D7373">GAMBLE_DISCLAIMER</span></li>
<li><span style="color:#1D7373">NO_SSP</span></li>
<li><span style="color:#1D7373">MFA</span></li>
<li><span style="color:#1D7373">RELIGION</span></li>
<li><span style="color:#1D7373">GDPR</span></li>
<li><span style="color:#1D7373">NO_WW</span></li>
<li><span style="color:#1D7373">UNDERWEAR</span></li>
<li><span style="color:#1D7373">DETECTIVE</span></li>
<li><span style="color:#1D7373">DYNAMIC_HOMONYMY</span></li>
<li><span style="color:#1D7373">EXPLOSIONS</span></li>
<li><span style="color:#1D7373">FINANCE</span></li>
<li><span style="color:#1D7373">GAME_VALUES</span></li>
<li><span style="color:#1D7373">HTML5_MARK</span></li>
<li><span style="color:#1D7373">MISSPELLING</span></li>
<li><span style="color:#1D7373">NO_FEED_PICTURE</span></li>
<li><span style="color:#1D7373">MED_CLOTHES</span></li>
<li><span style="color:#1D7373">ORTHOPEDICS</span></li>
<li><span style="color:#1D7373">NO_WEAPON</span></li>
<li><span style="color:#1D7373">PLUS18</span></li>
<li><span style="color:#1D7373">RAPID_ENRICHMENT</span></li>
<li><span style="color:#1D7373">SMI</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_QUALITY</span></li>
<li><span style="color:#1D7373">PERSONAL_CHARITY</span></li>
<li><span style="color:#1D7373">NOT_RU_LANG</span></li>
<li><span style="color:#1D7373">NO_TG</span></li>
<li><span style="color:#1D7373">NO_TOBACCO</span></li>
<li><span style="color:#1D7373">FEED_TG_APPROVED</span></li>
<li><span style="color:#1D7373">FEED_TG_FAILED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_APPROVED</span></li>
<li><span style="color:#1D7373">DOMAIN_TG_FAILED</span></li>
<li><span style="color:#1D7373">TRANSPORT</span></li>
<li><span style="color:#1D7373">WEAPONS</span></li>
<li><span style="color:#1D7373">BABY_FOOD0</span></li>
<li><span style="color:#1D7373">BABY_FOOD1</span></li>
<li><span style="color:#1D7373">BABY_FOOD2</span></li>
<li><span style="color:#1D7373">BABY_FOOD3</span></li>
<li><span style="color:#1D7373">BABY_FOOD4</span></li>
<li><span style="color:#1D7373">BABY_FOOD5</span></li>
<li><span style="color:#1D7373">BABY_FOOD6</span></li>
<li><span style="color:#1D7373">BABY_FOOD7</span></li>
<li><span style="color:#1D7373">BABY_FOOD8</span></li>
<li><span style="color:#1D7373">BABY_FOOD9</span></li>
<li><span style="color:#1D7373">BABY_FOOD10</span></li>
<li><span style="color:#1D7373">BABY_FOOD11</span></li>
<li><span style="color:#1D7373">BABY_FOOD12</span></li>
<li><span style="color:#1D7373">AGE0</span></li>
<li><span style="color:#1D7373">AGE6</span></li>
<li><span style="color:#1D7373">AGE12</span></li>
<li><span style="color:#1D7373">AGE16</span></li>
<li><span style="color:#1D7373">AGE18</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS0</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS1</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS2</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS3</span></li>
<li><span style="color:#1D7373">SUSPICIOUS_GOODS9</span></li>
<li><span style="color:#1D7373">YA_PAGES_REMOVE</span></li>
<li><span style="color:#1D7373">YA_PAGES_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_DZEN_PORTAL</span></li>
<li><span style="color:#1D7373">YA_PAGES_ANYWHERE</span></li>
<li><span style="color:#1D7373">RKN</span></li>
<li><span style="color:#1D7373">AD_BLOCK</span></li>
<li><span style="color:#1D7373">AUTO_SEO</span></li>
<li><span style="color:#1D7373">AVIA</span></li>
<li><span style="color:#1D7373">BUILDING</span></li>
<li><span style="color:#1D7373">CASINO</span></li>
<li><span style="color:#1D7373">CHILDREN</span></li>
<li><span style="color:#1D7373">COUNTERFEIT</span></li>
<li><span style="color:#1D7373">DIET</span></li>
<li><span style="color:#1D7373">EDUCATION</span></li>
<li><span style="color:#1D7373">FOR_UPDATE</span></li>
<li><span style="color:#1D7373">LAW</span></li>
<li><span style="color:#1D7373">MASSAGE</span></li>
<li><span style="color:#1D7373">MEDIA_DISCLAIMER</span></li>
<li><span style="color:#1D7373">PEOPLE</span></li>
<li><span style="color:#1D7373">POLITICS</span></li>
<li><span style="color:#1D7373">PORNO</span></li>
<li><span style="color:#1D7373">SEX</span></li>
<li><span style="color:#1D7373">SPAM</span></li>
<li><span style="color:#1D7373">SPY</span></li>
<li><span style="color:#1D7373">TM</span></li>
<li><span style="color:#1D7373">TOUR_OPERATORS</span></li>
<li><span style="color:#1D7373">FINANCE_INTERMEDIARY</span></li>
<li><span style="color:#1D7373">NOT_COMMERCIAL_ADV</span></li>
<li><span style="color:#1D7373">ADULT</span></li>
<li><span style="color:#1D7373">CAR_NUMBERS</span></li>
<li><span style="color:#1D7373">COOP_WARN</span></li>
<li><span style="color:#1D7373">COPYRIGHT</span></li>
<li><span style="color:#1D7373">CRYPTOCURRENCY</span></li>
<li><span style="color:#1D7373">DETECTIVE_EQUIPMENT</span></li>
<li><span style="color:#1D7373">DIRECTMOD_DICT</span></li>
<li><span style="color:#1D7373">DISCOUNT</span></li>
<li><span style="color:#1D7373">EGE</span></li>
<li><span style="color:#1D7373">ETHYL</span></li>
<li><span style="color:#1D7373">FILTER_FOR_PERFORMANCE</span></li>
<li><span style="color:#1D7373">FOREIGN_TRADE</span></li>
<li><span style="color:#1D7373">GOOD_ANIMATION</span></li>
<li><span style="color:#1D7373">MEDIATION</span></li>
<li><span style="color:#1D7373">MILK_SUBSTITUTE2</span></li>
<li><span style="color:#1D7373">MODERATEBADWORDTYPE</span></li>
<li><span style="color:#1D7373">NO_DISTANCE_SALES</span></li>
<li><span style="color:#1D7373">NO_DYNAMIC_CREATIVE</span></li>
<li><span style="color:#1D7373">NOTARY</span></li>
<li><span style="color:#1D7373">PIRACY</span></li>
<li><span style="color:#1D7373">PROMOTIONAL_ACTIVITIES</span></li>
<li><span style="color:#1D7373">PSEUDOSEX</span></li>
<li><span style="color:#1D7373">REGION_OTHERS</span></li>
<li><span style="color:#1D7373">SECURITY</span></li>
<li><span style="color:#1D7373">SEO</span></li>
<li><span style="color:#1D7373">SOFTWARE</span></li>
<li><span style="color:#1D7373">SPORTS_NUTRITION</span></li>
<li><span style="color:#1D7373">STRIPTEASE</span></li>
<li><span style="color:#1D7373">STUDY</span></li>
<li><span style="color:#1D7373">TECH_INSPECTION</span></li>
<li><span style="color:#1D7373">TELECOM</span></li>
<li><span style="color:#1D7373">VETERINARY</span></li>
<li><span style="color:#1D7373">WHITE</span></li>
<li><span style="color:#1D7373">WORK_ABROAD</span></li>
<li><span style="color:#1D7373">XRAY</span></li>
<li><span style="color:#1D7373">STOCK</span></li>
<li><span style="color:#1D7373">STOCKMANAG</span></li>
<li><span style="color:#1D7373">PSEUDOWEAPON_ACCESSORIES</span></li>
<li><span style="color:#1D7373">NON_ALCOHOL</span></li>
<li><span style="color:#1D7373">COLLECTOR_NO_CONTACTS</span></li>
<li><span style="color:#1D7373">MILITARY</span></li>
<li><span style="color:#1D7373">MINUS_REGION_RU</span></li>
<li><span style="color:#1D7373">MINUS_REGION_KZ</span></li>
<li><span style="color:#1D7373">MINUS_REGION_UA</span></li>
<li><span style="color:#1D7373">MINUS_REGION_RB</span></li>
<li><span style="color:#1D7373">MINUS_REGION_TR</span></li>
<li><span style="color:#1D7373">MINUS_REGION_UZ</span></li>
<li><span style="color:#1D7373">MINUS_REGION_OTHER</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L570">UrlData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L509">TUrlData</a></i>
</li>
<details open><summary><b>Message TUrlData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L512">UpdateTime</a></b>  <i>uint64</i>
<p> save here new url info/factors  move here Bert, Erf, Herf, Urldat? </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L513">ContentAttrsOffer</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L5">TContentAttrsOffer</a></i>
<p> SerializedOffer filtered (BIGB-2087) </p>

</li>
<details open><summary><b>Message TContentAttrsOffer</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L6">SerializedOffer</a></b>  <i>bytes</i>
<p> NWatson::NEcom::TOffer </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L8">NoProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L9">OneProductProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L10">ManyProductsProbability</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L13">ShopVendor</a></b>  <i>string</i>
<p>AUTOPARSER-50 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L14">Color</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L15">Material</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/robot/jupiter/protos/compatibility/offer.proto?rev=r9795881#L17">Gender</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/quality/functionality/parsepl/ecom/proto/gender.proto?rev=r9795881#L6">EGender</a></i>
</li>
<details open><summary><b>Enum EGender</b></summary>
<p>AUTOPARSER-109 </p>

<ul>
<li><span style="color:#1D7373">man</span></li>
<li><span style="color:#1D7373">woman</span></li>
<li><span style="color:#1D7373">boy</span></li>
<li><span style="color:#1D7373">girl</span></li>
<li><span style="color:#1D7373">kid</span></li>
<li><span style="color:#1D7373">unisex</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L571">CatProfiles</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L19">TCatEngineProfiles</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L573">AvatarsMetaData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L527">TAvatarsMetaData</a></i>
<p> do we want to make global last UpdateTimeStamp here ? - no </p>

</li>
<details open><summary><b>Message TAvatarsMetaData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L529">LastAvatarsResponseTime</a></b>  <i>uint64</i>
<p> All fields should have numbers greater 10 to make it merge easier with TMdsMeta </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L530">ImageClassifiers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L516">TImageClassifiers</a></i>
</li>
<details open><summary><b>Message TImageClassifiers</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L517">ImageID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L518">Classifiers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/classifiers.proto?rev=r9795881#L20">TClassifier</a></i>
</li>
<details open><summary><b>Message TClassifier</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/classifiers.proto?rev=r9795881#L21">ClassifierID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/classifiers.proto?rev=r9795881#L5">EAvatarsClassifier</a></i>
</li>
<details open><summary><b>Enum EAvatarsClassifier</b></summary>
<ul>
<li><span style="color:#1D7373">AC_UNKNOWN</span></li>
<li><span style="color:#1D7373">AC_AESTHETIC</span></li>
<li><span style="color:#1D7373">AC_500PX</span></li>
<li><span style="color:#1D7373">AC_AADB_AESTHETIC</span></li>
<li><span style="color:#1D7373">AC_CLOTHES</span></li>
<li><span style="color:#1D7373">AC_LOOK</span></li>
<li><span style="color:#1D7373">AC_OCR_TEXT</span></li>
<li><span style="color:#1D7373">AC_PAIRWISE_ATTR</span></li>
<li><span style="color:#1D7373">AC_WATERMARKS</span></li>
<li><span style="color:#1D7373">AC_CLOTHES_FEMALE</span></li>
<li><span style="color:#1D7373">AC_CLOTHES_ADULT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/classifiers.proto?rev=r9795881#L22">Value</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L531">ImageEmbeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L521">TImageEmbeddings</a></i>
</li>
<details open><summary><b>Message TImageEmbeddings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L522">ImageID</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L45">TAvatarsImage</a></i>
</li>
<details open><summary><b>Message TAvatarsImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L50">Namespace</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L51">ImageGroupId</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L52">ImageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L53">OriginalImageUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L54">Mode</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/experimental/banner/banner_resources.proto?rev=r9795881#L46">EMode</a></i>
</li>
<details open><summary><b>Enum EMode</b></summary>
<ul>
<li><span style="color:#1D7373">PROD</span></li>
<li><span style="color:#1D7373">TEST</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L524">Embeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
<p> TEmbedding protobuf field VectorID should match with Tsar ID from TsarModelServiceConfig </p>

</li>
<details open><summary><b>Message TEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L7">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L9">VectorID</a></b>  <i>uint64</i>
<p> https://wiki.yandex-team.ru/adsquality/car-reglament/ </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L11">Vector</a></b>  <i>float</i>
<p> factors </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L13">CompressionType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/compress_vectors/proto/compress_info.proto?rev=r9795881#L5">ECompressionType</a></i>
</li>
<details open><summary><b>Enum ECompressionType</b></summary>
<ul>
<li><span style="color:#1D7373">NO_COMPRESSION</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_1_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_24_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_28_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_PHRASE_200_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_USER_BODY_V2_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_CUSTOM_RANK_LOSS_16</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_65_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_1_IMAGES_DSSM_APPLIER_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_QUORUM_66_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_NEW_QUORUM_67_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_BANNER_RELEV_UNIFORM_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_136_8</span></li>
<li><span style="color:#1D7373">MIN_MAX_DSSM_GALLERY_JULY_4_76_UNIFORM_8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L14">CompressedVector</a></b>  <i>bytes</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L574">GrutObject</a></b>  <i>TBannerV2</i>
</li>
<details open><summary><b>Message TBannerV2</b></summary>
<ul>
<li><b>meta</b>  <i>TBannerV2Meta</i>
</li>
<details open><summary><b>Message TBannerV2Meta</b></summary>
<ul>
<li><b>id</b>  <i>uint64</i>
</li>

<li><b>direct_id</b>  <i>uint64</i>
</li>

<li><b>campaign_id</b>  <i>uint64</i>
</li>

<li><b>source</b>  <i>int32</i>
</li>

<li><b>direct_type</b>  <i>int32</i>
</li>

<li><b>image_banner_id</b>  <i>uint64</i>
</li>

<li><b>uuid</b>  <i>string</i>
</li>

<li><b>name</b>  <i>string</i>
</li>

<li><b>ad_group_id</b>  <i>uint64</i>
<p> Service fields: </p>

</li>

<li><b>type</b>  <i>EObjectType</i>
</li>
<details open><summary><b>Enum EObjectType</b></summary>
<ul>
<li><span style="color:#1D7373">OT_NULL</span></li>
<li><span style="color:#1D7373">OT_CLIENT</span></li>
<li><span style="color:#1D7373">OT_CAMPAIGN</span></li>
<li><span style="color:#1D7373">OT_AD_GROUP</span></li>
<li><span style="color:#1D7373">OT_ASSET</span></li>
<li><span style="color:#1D7373">OT_APP_INFO</span></li>
<li><span style="color:#1D7373">OT_BANNER</span></li>
<li><span style="color:#1D7373">OT_CAMPAIGN_V2</span></li>
<li><span style="color:#1D7373">OT_AD_GROUP_V2</span></li>
<li><span style="color:#1D7373">OT_USER</span></li>
<li><span style="color:#1D7373">OT_GROUP</span></li>
<li><span style="color:#1D7373">OT_BANNER_V2</span></li>
<li><span style="color:#1D7373">OT_OFFER</span></li>
<li><span style="color:#1D7373">OT_BANNER_CANDIDATE</span></li>
<li><span style="color:#1D7373">OT_MINUS_PHRASE</span></li>
<li><span style="color:#1D7373">OT_MOBILE_CONTENT</span></li>
<li><span style="color:#1D7373">OT_VCARD</span></li>
<li><span style="color:#1D7373">OT_CONVERSION_SOURCE</span></li>
<li><span style="color:#1D7373">OT_BIDDABLE_SHOW_CONDITION</span></li>
<li><span style="color:#1D7373">OT_CREATIVE</span></li>
<li><span style="color:#1D7373">OT_BANNERLAND_BANNER</span></li>
<li><span style="color:#1D7373">OT_BID_MODIFIER</span></li>
<li><span style="color:#1D7373">OT_BIZ_LANDING</span></li>
<li><span style="color:#1D7373">OT_BANNERLAND_GENERATION_TASK</span></li>
<li><span style="color:#1D7373">OT_RETARGETING_CONDITION</span></li>
<li><span style="color:#1D7373">OT_STRATEGY</span></li>
<li><span style="color:#1D7373">OT_AD_GROUP_BRIEF</span></li>
<li><span style="color:#1D7373">OT_CLIENT_MOBILE_APP</span></li>
<li><span style="color:#1D7373">OT_PACKAGE</span></li>
<li><span style="color:#1D7373">OT_SCHEMA</span></li>
<li><span style="color:#1D7373">OT_WATCH_LOG_CONSUMER</span></li>
<li><span style="color:#1D7373">OT_SEMAPHORE</span></li>
<li><span style="color:#1D7373">OT_SEMAPHORE_SET</span></li>
</ul></details>
<li><b>creation_time</b>  <i>uint64</i>
</li>

<li><b>inherit_acl</b>  <i>bool</i>
</li>

<li><b>acl</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L32">TAccessControlEntry</a></i>
</li>
<details open><summary><b>Message TAccessControlEntry</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L35">action</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L8">EAccessControlAction</a></i>
<p> Determines the access control action to take upon a match. </p>

</li>
<details open><summary><b>Enum EAccessControlAction</b></summary>
<ul>
<li><span style="color:#1D7373">ACA_ALLOW</span></li>
<li><span style="color:#1D7373">ACA_DENY</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L38">permissions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L17">EAccessControlPermission</a></i>
<p> List of permissions this entry applies to. </p>

</li>
<details open><summary><b>Enum EAccessControlPermission</b></summary>
<ul>
<li><span style="color:#1D7373">ACP_NONE</span></li>
<li><span style="color:#1D7373">ACP_READ</span></li>
<li><span style="color:#1D7373">ACA_WRITE</span></li>
<li><span style="color:#1D7373">ACA_CREATE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L41">subjects</a></b>  <i>string</i>
<p> List of subjects (users and groups) this entry applies to. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/access_control.proto?rev=r9795881#L45">attributes</a></b>  <i>string</i>
<p> List of attribute paths this entry applies to.  If this list is not specified or empty, this entry is applied to the root attribute path. </p>

</li>


</ul></details>
<li><b>fqid</b>  <i>string</i>
</li>

<li><b>key</b>  <i>string</i>
</li>

<li><b>parent_key</b>  <i>string</i>
</li>


</ul></details>
<li><b>spec</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L45">TBannerV2Spec</a></i>
</li>
<details open><summary><b>Message TBannerV2Spec</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L167">status</a></b>  <i>int32</i>
<p> enum EBannerStatus </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L168">is_mobile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L170">href_asset_id</a></b>  <i>uint64</i>
<p> для обратной совместимости с хранением ассетов </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L171">title_asset_id</a></b>  <i>uint64</i>
<p> для обратной совместимости с хранением ассетов </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L173">href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L175">domain</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L176">title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L177">title_extension</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L178">body</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L180">language</a></b>  <i>int32</i>
<p> enum ELanguage (https://a.yandex-team.ru/arc/trunk/arcadia/grut/libs/proto/objects/language.proto) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L182">flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L153">TFlags</a></i>
<p> Набор флагов. </p>

</li>
<details open><summary><b>Message TFlags</b></summary>
<p> Бинарные флаги баннера. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L158">geoflag</a></b>  <i>bool</i>
<p> Нужно ли выводить город, при показе баннера на выдаче (геотаргетинг достаточно узкий)  сейчас вычисляется при сохранении баннера в Директе и пишется в mysql в banners.opts  вычисляется путём мёрджа гео на группе и данных геобазы, в будущем сохранять явно не планируем  вместо этого планируем вычислять в Цезаре. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L185">moderation_flags</a></b>  <i>int64</i>
<p> Cписок флагов, может меняться клиентом. Флаги модерации (https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/markup_flags.proto)  и подмерженные минус-регионы в зарезервированном диапазоне (https://a.yandex-team.ru/arc_vcs/modadvert/bigmod/protos/interface/markup_flags.proto?rev=r9143354#L1701) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L188">turbolanding_href_params</a></b>  <i>string</i>
<p> Параметры, добавляемые к ссылкам турболендингов баннера, через & (включая турболендинги сайтлинков). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L191">turbolanding_id</a></b>  <i>uint64</i>
<p> Turbolanding на баннере в качестве основной ссылки. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L192">turbolanding_href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L194">sitelink_set</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L46">TSitelinkSet</a></i>
</li>
<details open><summary><b>Message TSitelinkSet</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L56">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L57">sitelinks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L47">TSitelink</a></i>
</li>
<details open><summary><b>Message TSitelink</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L48">asset_id</a></b>  <i>uint64</i>
<p> для обратной совместимости с хранением ассетов </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L49">href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L50">title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L51">description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L52">turbolanding_href</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L53">turbolanding_id</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L197">images</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L79">TImage</a></i>
</li>
<details open><summary><b>Message TImage</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L100">asset_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L102">image_hash</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L103">mds_file_info</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L8">TMdsFileInfo</a></i>
</li>
<details open><summary><b>Message TMdsFileInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L19">namespace</a></b>  <i>string</i>
<p> Имя неймспейса для аватарницы, в терминах MDS это bucket. Подробнее про MDS https://wiki.yandex-team.ru/mds/dev/protocol/ и Аватарницу https://wiki.yandex-team.ru/mds/avatars/. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L21">group_id</a></b>  <i>uint32</i>
<p> Идентификатор группы файлов в MDS/группы картинок, генерируется автоматически при загрузке файла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L23">source_url</a></b>  <i>string</i>
<p> Исходный URL, откуда файл/картинка/... был скачен. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L25">mds_file_name</a></b>  <i>string</i>
<p> Имя файла, сгенерированного для mds. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L27">user_file_name</a></b>  <i>string</i>
<p> Имя файла, которое задал пользователь. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/mds_info.proto?rev=r9795881#L29">environment</a></b>  <i>int32</i>
<p> enum EEnvironment </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L104">avatars_image_meta</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L8">TAvatarsImageMeta</a></i>
</li>
<details open><summary><b>Message TAvatarsImageMeta</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L37">create_time</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L41">color_wiz_background</a></b>  <i>uint64</i>
<p> Dominant image background color produced by ColorWiz Algorithm.  https://wiki.yandex-team.ru/mds/avatars/#colorwiz </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L43">color_wiz_button</a></b>  <i>uint64</i>
<p> Button color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L45">color_wiz_button_text</a></b>  <i>uint64</i>
<p> Button text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L47">average_color</a></b>  <i>uint64</i>
<p> Average color of all image. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L50">image_quality</a></b>  <i>float</i>
<p> Quality of image metric: the value from the interval [0;1].  https://st.yandex-team.ru/BSSERVER-8915 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L53">background_colors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L30">TBackgroundColors</a></i>
<p> Average background color for sides of image.  https://st.yandex-team.ru/MDS-13718 </p>

</li>
<details open><summary><b>Message TBackgroundColors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L31">bottom</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L32">left</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L33">right</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L34">top</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L55">main_color</a></b>  <i>uint64</i>
<p> Dominant image color. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L57">crc64</a></b>  <i>uint64</i>
<p> Checksum. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L60">formats</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L9">TFormat</a></i>
<p> Информация о форматах картинки. </p>

</li>
<details open><summary><b>Message TFormat</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L18">format_name</a></b>  <i>string</i>
<p> Название формата, например, "x80", "x90". </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L20">width</a></b>  <i>int32</i>
<p> Ширина картинки. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L22">height</a></b>  <i>int32</i>
<p> Высота картинки. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L25">smart_centers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L10">TSmartCenter</a></i>
<p> Interesting image areas for some image ratios sorted lexicographically in ascending order  Ex.: 0 -> 16:5; 1 -> 16:9, 2 -> 1:1, 3 -> 3:4, ... </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L11">x</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L12">y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L13">w</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L14">h</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L27">smart_center</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L10">TSmartCenter</a></i>
<p> The most interesting image area for any image ratio. </p>

</li>
<details open><summary><b>Message TSmartCenter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L11">x</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L12">y</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L13">w</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L14">h</a></b>  <i>int32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L63">color_wiz_text</a></b>  <i>uint64</i>
<p> Text color produced by ColorWiz Algorithm. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L65">orig_format</a></b>  <i>string</i>
<p> Original image format. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L67">orig_animated</a></b>  <i>bool</i>
<p> Is original image animated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/mds_info.proto?rev=r9795881#L69">orig_size_bytes</a></b>  <i>int32</i>
<p> Size of original image. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L107">image_type</a></b>  <i>int32</i>
<p> EImageType  Тип картинки в Директе. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L200">permalink</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L60">TPermalink</a></i>
</li>
<details open><summary><b>Message TPermalink</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L72">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L73">phone_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L74">prefer_vcard_over_permalink</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L76">assign_type</a></b>  <i>int32</i>
<p> enum EAssignType </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L201">mobile_content</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L110">TMobileContent</a></i>
</li>
<details open><summary><b>Message TMobileContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L147">primary_action</a></b>  <i>int32</i>
<p> enum EPrimaryAction </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L148">reflected_attributes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L139">TReflectedAttribute</a></i>
</li>
<details open><summary><b>Message TReflectedAttribute</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L140">rating</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L141">price</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L142">icon</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L143">rating_votes</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L149">impression_url</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L204">pixels</a></b>  <i>string</i>
<p> Набор URL счётчиков для внешних систем учёта показа рекламы. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L207">internal_ad_options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L161">TInternalAdOptions</a></i>
<p> Поля внутренней рекламы. </p>

</li>
<details open><summary><b>Message TInternalAdOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L163">template_id</a></b>  <i>uint64</i>
<p> TemplateId для внутренних баннеров, в директе хранится в banners_internal.template_id. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L210">vcard_id</a></b>  <i>uint64</i>
<p> id визитки, сама визитка хранится в отдельной таблице </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L216">creative_ids</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b>status</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L223">TBannerV2Status</a></i>
</li>
<details open><summary><b>Message TBannerV2Status</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L276">moderation_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L226">TModerationStatus</a></i>
</li>
<details open><summary><b>Message TModerationStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L256">main_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L257">sitelink_set_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L258">creatives_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L259">images_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L262">moderation_flags</a></b>  <i>int64</i>
<p> Список флагов, может меняться модерацией (с подмерженными минус-регионами)  Конечные флаги собираются из двух полей: флагов от модерации и от клиента </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L263">turbolanding_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L264">vcard_status</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L245">TItemStatus</a></i>
</li>
<details open><summary><b>Message TItemStatus</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L247">verdict</a></b>  <i>int32</i>
<p> enum EVerdict </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L248">version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L249">reasons</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L237">TReason</a></i>
</li>
<details open><summary><b>Message TReason</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
<p> Идентификатор причины отклонения. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L241">comment</a></b>  <i>string</i>
<p> Дополнительный уточняющий комментарий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L243">screenshot_links</a></b>  <i>string</i>
<p> Ссылки на дополнительные уточняющие скриншоты. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L250">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L254">extracted_text</a></b>  <i>string</i>
<p> Заполняется модерацией из соответствующего объекта, если применимо.  Например, в main_status будет текст из картинки (аналог mysql images.image_text),  а в creatives_status будет текст из креатива (аналог mysql banners_performance.extracted_text). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L266">disclaimer</a></b>  <i>string</i>
<p> Текст дисклеймера. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L277">skip_moderation</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L278">ord_options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L269">TOrdOptions</a></i>
</li>
<details open><summary><b>Message TOrdOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L271">rkn_hash</a></b>  <i>uint64</i>
<p> Хеш от значимых для Единого Реестра Интернет Рекламы (ЕРИР) полей. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/banner_v2.proto?rev=r9795881#L273">rkn_registration_time</a></b>  <i>fixed32</i>
<p> Время регистрации в Единый Реестр Интернет Рекламы (ЕРИР). </p>

</li>


</ul></details>

</ul></details>
<li><b>labels</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yt/yt_proto/yt/core/ytree/proto/attributes.proto?rev=r9795881#L19">TAttributeDictionary</a></i>
</li>
<details open><summary><b>Message TAttributeDictionary</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yt/yt_proto/yt/core/ytree/proto/attributes.proto?rev=r9795881#L22">attributes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yt/yt_proto/yt/core/ytree/proto/attributes.proto?rev=r9795881#L13">TAttribute</a></i>
</li>
<details open><summary><b>Message TAttribute</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yt/yt_proto/yt/core/ytree/proto/attributes.proto?rev=r9795881#L15">key</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yt/yt_proto/yt/core/ytree/proto/attributes.proto?rev=r9795881#L16">value</a></b>  <i>bytes</i>
</li>


</ul></details>

</ul></details>
<li><b>control</b>  <i>TBannerV2Control</i>
</li>
<details open><summary><b>Message TBannerV2Control</b></summary>
<ul>
<li><b>touch_index</b>  <i>TObjectTouchIndex</i>
</li>
<details open><summary><b>Message TObjectTouchIndex</b></summary>
<ul>
<li><b>index_name</b>  <i>string</i>
</li>


</ul></details>
<li><b>touch</b>  <i>TObjectTouch</i>
</li>
<details open><summary><b>Message TObjectTouch</b></summary>
<ul>
<li><b>lock_removal</b>  <i>bool</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L575">LastUpdateInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L534">TLastUpdateInfo</a></i>
</li>
<details open><summary><b>Message TLastUpdateInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L536">GrutSyncTimestamp</a></b>  <i>fixed32</i>
<p> The time of sync GrutObject. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L538">GrutObjectUpdateTimestamp</a></b>  <i>fixed32</i>
<p> The time of object update in GrUT </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L576">ComputedFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L542">TComputedFields</a></i>
</li>
<details open><summary><b>Message TComputedFields</b></summary>
<p> Derivative from GrutObject. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L543">TargetDomainID</a></b>  <i>uint64</i>
<p> dont use yet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L544">TargetDomain</a></b>  <i>string</i>
<p> dont use yet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L549">Title</a></b>  <i>string</i>
<p> Replaces the Direct Title template for phrase substitution with a template understandable to the engine  example:  "#Бесплатный поиск авиабилетов!# Доступно 860 рейсов!" -> "{PHRASEБесплатный поиск авиабилетов!} Доступно 860 рейсов!"  where "Бесплатный поиск авиабилетов!" will be used as a default value </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L551">Body</a></b>  <i>string</i>
<p> The same as Title but for Body field from Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L553">TitleExtension</a></b>  <i>string</i>
<p> The same as Title but for TitleExtension field from Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L554">SiteFilter</a></b>  <i>string</i>
<p> dont use yet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L555">SiteFilterID</a></b>  <i>uint64</i>
<p> dont use yet </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L556">LastDomain</a></b>  <i>string</i>
<p> Last domain used for generating TargetDomain, TargetDomainID, SiteFilter, SiteFilterID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L557">Href</a></b>  <i>string</i>
<p> TODO(galievilshat): add href computation description </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L558">TemplateID</a></b>  <i>uint32</i>
<p> Banner template, see //home/yabs/dict/TemplateBanner </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/banner.proto?rev=r9795881#L579">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
