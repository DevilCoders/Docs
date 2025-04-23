
## Message TOfferProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L144">OfferIDMd5</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L145">BusinessID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L146">ShopID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L148">Resources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L25">TResources</a></i>
</li>
<details open><summary><b>Message TResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L104">Version</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/common/Types.proto?rev=r9795881#L68">Version</a></i>
</li>
<details open><summary><b>Message Version</b></summary>
<p> Не до конца зафиксированный формат, может в дальнейшем меняться </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/common/Types.proto?rev=r9795881#L70">version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L105">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L106">OfferID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L107">FeedID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L108">TurboShopID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L109">CounterID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L110">CounterOfferID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L111">Price</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L30">TPrice</a></i>
</li>
<details open><summary><b>Message TPrice</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L31">Currency</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/contract/Types.proto?rev=r9795881#L36">Currency</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L32">Price</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L33">OldPrice</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L34">PriceInRUB</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L35">Discount</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L112">OriginalContent</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L38">TPartnerContent</a></i>
</li>
<details open><summary><b>Message TPartnerContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L39">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L40">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L41">AdultOnly</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L113">MarketContent</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L53">TMarketContent</a></i>
</li>
<details open><summary><b>Message TMarketContent</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L54">CategoryID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L55">CategoryName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L57">Vendor</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L58">VendorName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L60">ModelID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L61">ModelName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L63">Title</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L65">ReviewsCount</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L66">ReviewsAvg</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L114">ActualPictures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L69">TMarketPictures</a></i>
</li>
<details open><summary><b>Message TMarketPictures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L79">Pictures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L70">TPicture</a></i>
</li>
<details open><summary><b>Message TPicture</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L71">Name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L72">Url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L73">Width</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L74">Height</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L75">ContainerWidth</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L76">ContainerHeight</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L115">RegionsInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L88">TRegionsInfo</a></i>
</li>
<details open><summary><b>Message TRegionsInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L89">Regions</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L90">PriorityRegions</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L91">PickupRegions</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L116">Url</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L94">TUrl</a></i>
</li>
<details open><summary><b>Message TUrl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L95">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L96">LandingUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L97">LandingTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L98">SpyLogTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L99">GeminiUrl</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L100">IsGeminiUrlBad</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L101">GeminiUrlUpdateTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L117">MultikCategories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L82">TMultikCategories</a></i>
</li>
<details open><summary><b>Message TMultikCategories</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L83">ComputedTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L84">Categories</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L85">ModelID</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L118">Listings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L44">TListings</a></i>
</li>
<details open><summary><b>Message TListings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L49">Listings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L45">TListing</a></i>
</li>
<details open><summary><b>Message TListing</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L46">ID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L47">CanonizedUrlMd5</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L50">UpdateTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L119">FeedCategories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L26">TFeedCategories</a></i>
</li>
<details open><summary><b>Message TFeedCategories</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L27">Categories</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L120">FilterIDs</a></b>  <i>uint64</i>
<p> max id: 17 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L149">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L124">TFlags</a></i>
</li>
<details open><summary><b>Message TFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L137">Version</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/common/Types.proto?rev=r9795881#L68">Version</a></i>
</li>
<details open><summary><b>Message Version</b></summary>
<p> Не до конца зафиксированный формат, может в дальнейшем меняться </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/proto/common/Types.proto?rev=r9795881#L70">version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L138">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L139">Source</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L125">EOfferSource</a></i>
</li>
<details open><summary><b>Enum EOfferSource</b></summary>
<ul>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">DATACAMP</span></li>
<li><span style="color:#1D7373">SHUBERT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L140">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L131">EOfferType</a></i>
</li>
<details open><summary><b>Enum EOfferType</b></summary>
<ul>
<li><span style="color:#1D7373">NONE</span></li>
<li><span style="color:#1D7373">TURBO</span></li>
<li><span style="color:#1D7373">MARKET</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L141">LastProcessTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L150">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L11">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L12">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L151">ImageEmbeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L15">TImageEmbeddings</a></i>
</li>
<details open><summary><b>Message TImageEmbeddings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L21">Vectors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L16">TImageEmbedding</a></i>
</li>
<details open><summary><b>Message TImageEmbedding</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L17">ModelName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L18">Vector</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L22">UpdateTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L152">TsarVectors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L17">TEmbeddings</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/offer.proto?rev=r9795881#L155">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
