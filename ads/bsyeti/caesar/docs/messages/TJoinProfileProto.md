
## Message TJoinProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L26">JoinID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L27">State</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L16">TState</a></i>
</li>
<details open><summary><b>Message TState</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L17">ChEvents</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L5">TBsChEvent</a></i>
</li>
<details open><summary><b>Message TBsChEvent</b></summary>
<p> original proto is here https://a.yandex-team.ru/arc/trunk/arcadia/yabs/sbyt/lbyt/proto/logs/bs_chevent_log.proto  there is only field required in caesar processing </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L6">EventTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L7">PageID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L8">PlaceID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L9">ParentBannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L10">CounterType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L11">Gender</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L12">Age</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L13">DomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L14">TargetPhraseID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L15">SelectType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L16">ContextType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L17">FraudBits</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L18">Income</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L19">HitDetailedDeviceTypeAsInt</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L21">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L22">ShowTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L23">EventID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L24">PhraseID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L25">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L26">UniqID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L27">GroupBannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L28">ImpID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L29">OrderID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L30">BMCategoryID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L31">SSPID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L32">PageDomainMD5</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L33">URLClusterID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L34">RegionID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L35">ProductTypeAsInt</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L36">ProductType</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L38">Position</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L39">TypeID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L40">Options</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L41">ImpressionOptions</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L42">HitLogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L44">SearchReqId</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L45">ICookie</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L46">PrebillingCostBits</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L47">PrebillingFraudBits</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L48">GroupOrderID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L50">EventCost</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L51">EventCostCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L52">CostCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L53">AutobudgetExperimentID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L54">AutobudgetOptions</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L55">AutobudgetExperimentTrafficShare</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L56">AutobudgetStrategyID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L57">DistributionTagID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L58">MobileAppBundleID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L59">DetailedDeviceType</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_chevent.proto?rev=r9795881#L60">PageTokenTagIDMD5</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L18">SearchBannerTexts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L7">FactorsBannerText</a></i>
</li>
<details open><summary><b>Message FactorsBannerText</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L10">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L11">HitLogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L13">EventID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L14">ShowTime</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L15">UniqID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L16">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L17">Phrase</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L18">BannerTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L19">BannerText</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L20">SecondTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L21">SitelinkCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L22">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L23">BroadPhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L24">BMCategory1ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L25">BMCategory2ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L26">BMCategory3ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/factors_banner_text.proto?rev=r9795881#L27">BannerURL</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L19">RsyaBannerTexts</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L7">WideBannerText</a></i>
</li>
<details open><summary><b>Message WideBannerText</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L10">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L11">HitLogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L13">EventID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L14">ShowTime</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L15">UniqID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L16">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L17">Phrase</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L18">BannerTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L19">BannerText</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L20">SecondTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L21">SitelinkCount</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L22">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L23">BroadPhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L24">BMCategory1ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L25">BMCategory2ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L26">BMCategory3ID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/wide_banner_text.proto?rev=r9795881#L27">BannerURL</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L20">Hits</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L8">TCaesarNarrowYabsHit</a></i>
</li>
<details open><summary><b>Message TCaesarNarrowYabsHit</b></summary>
<p> filtered yabs::proto::log::Hit for caesar internal use  copy paste fields from https://a.yandex-team.ru/arc/trunk/arcadia/yabs/server/proto/log/hit.proto  there is only field required in caesar processing </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L9">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L10">HitRequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L11">HitLogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L12">ShowTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L13">EventID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L14">PageID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L15">PlaceID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L16">UniqID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L17">DeviceType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L18">SearchQuery</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L19">CryptaID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L20">EventTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L21">RtbBidReqID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L23">ImpressionOptions</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_hit.proto?rev=r9795881#L24">BannerCountPremium</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L21">Postclicks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L3">TBsMobilePostclick</a></i>
</li>
<details open><summary><b>Message TBsMobilePostclick</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L4">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L5">DetailedDeviceType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L6">IDFA</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L7">LogID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L8">OAID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L9">GoogleAdID</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L10">EventTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L11">CryptaIDv2</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L12">UserID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L13">PageID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L14">ImpID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L15">OrderID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L16">Goals_ID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L17">PackageName</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L18">Sign</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L19">EventType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L20">FraudBits</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L21">SelectType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L22">CounterType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L23">GroupBannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L24">DomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L25">TypeID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L26">ImpressionOptions</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/bs_mobile_postclick.proto?rev=r9795881#L27">PlaceID</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L22">Postbacks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L5">TUniformPostback</a></i>
</li>
<details open><summary><b>Message TUniformPostback</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L68">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L69">LogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L70">GoogleAdID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L71">IDFA</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L72">MatchType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L39">EMatchType</a></i>
</li>
<details open><summary><b>Enum EMatchType</b></summary>
<ul>
<li><span style="color:#1D7373">MT_UNKNOWN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L73">UserAgent</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L74">RemoteIP6</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L75">ClientIP6</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L76">PackageName</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L77">PostBackTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L78">DecodeErrors</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L79">DecodeErrorsAsString</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L80">ExtPostBack</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L81">PackageID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L82">AppTrackerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L83">EventType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L7">EEventType</a></i>
</li>
<details open><summary><b>Enum EEventType</b></summary>
<ul>
<li><span style="color:#1D7373">ET_UNKNOWN</span></li>
<li><span style="color:#1D7373">ET_INSTALL</span></li>
<li><span style="color:#1D7373">ET_IN_APP</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L84">EventName</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L13">EEventName</a></i>
</li>
<details open><summary><b>Enum EEventName</b></summary>
<ul>
<li><span style="color:#1D7373">EN_UNKNOWN</span></li>
<li><span style="color:#1D7373">EN_INSTALL_APP</span></li>
<li><span style="color:#1D7373">EN_ACHIEVED_LEVEL</span></li>
<li><span style="color:#1D7373">EN_APP_LAUNCHED</span></li>
<li><span style="color:#1D7373">EN_ADDED_PAYMENT_INFO</span></li>
<li><span style="color:#1D7373">EN_ADDED_TO_CART</span></li>
<li><span style="color:#1D7373">EN_ADDED_TO_WISHLIST</span></li>
<li><span style="color:#1D7373">EN_COMPLETED_REGISTRATION</span></li>
<li><span style="color:#1D7373">EN_COMPLETED_TUTORIAL</span></li>
<li><span style="color:#1D7373">EN_INITIATED_CHECKOUT</span></li>
<li><span style="color:#1D7373">EN_PURCHASED</span></li>
<li><span style="color:#1D7373">EN_RATED</span></li>
<li><span style="color:#1D7373">EN_REMOVED_FROM_CART</span></li>
<li><span style="color:#1D7373">EN_SEARCHED</span></li>
<li><span style="color:#1D7373">EN_SPENT_CREDITS</span></li>
<li><span style="color:#1D7373">EN_UNLOCKED_ACHIEVEMENT</span></li>
<li><span style="color:#1D7373">EN_VIEWED_CONTENT</span></li>
<li><span style="color:#1D7373">EN_SPENT_TIME_IN_APP</span></li>
<li><span style="color:#1D7373">EN_SHARED</span></li>
<li><span style="color:#1D7373">EN_EVENT_1</span></li>
<li><span style="color:#1D7373">EN_EVENT_2</span></li>
<li><span style="color:#1D7373">EN_EVENT_3</span></li>
<li><span style="color:#1D7373">EN_CUSTOM_EVENT</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L85">EventTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L86">EventValue</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L44">TEventValue</a></i>
</li>
<details open><summary><b>Message TEventValue</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L57">Ecommerce</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L45">TEcommerce</a></i>
</li>
<details open><summary><b>Message TEcommerce</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L54">Products</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L46">TProduct</a></i>
</li>
<details open><summary><b>Message TProduct</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L47">ID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L48">Name</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L49">Category</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L50">Price</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L51">Quantity</a></b>  <i>int64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L58">PhoneHash</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L59">EmailHash</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L87">Revenue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L88">CurrencyID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L89">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L90">OAID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L91">YandexAppID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L92">EcommerceCounterID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L93">EventSource</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L62">EEventSource</a></i>
</li>
<details open><summary><b>Enum EEventSource</b></summary>
<ul>
<li><span style="color:#1D7373">ES_UNKNOWN</span></li>
<li><span style="color:#1D7373">ES_POSTBACK</span></li>
<li><span style="color:#1D7373">ES_APPMETRICA_ECOMMERCE</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L94">EventID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L95">IDFV</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L96">UpdateTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L97">InstallTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L98">PhoneHash</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/sbyt/ytstatcollector/log_generators/proto/uniform_postback.proto?rev=r9795881#L99">EmailHash</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L23">StatMxFeatures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L58">StatMxFeatures</a></i>
</li>
<details open><summary><b>Message StatMxFeatures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L66">RequestID</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L67">HostID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L68">ShowTime</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L70">BannerID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L71">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L72">ContextType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L73">ProductType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/common_enums.proto?rev=r9795881#L213">ProductTypeEnum</a></i>
</li>
<details open><summary><b>Enum ProductTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">ZERO_PRODUCT</span></li>
<li><span style="color:#1D7373">DIRECT</span></li>
<li><span style="color:#1D7373">MEDIA_SMART</span></li>
<li><span style="color:#1D7373">MEDIA_IMAGE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE</span></li>
<li><span style="color:#1D7373">VIDEO_SMART</span></li>
<li><span style="color:#1D7373">AUTO_VIDEO_DIRECT</span></li>
<li><span style="color:#1D7373">MEDIA_IMAGE_REACH</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH</span></li>
<li><span style="color:#1D7373">VIDEO_MOTION</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH_OUTDOOR</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH_INDOOR</span></li>
<li><span style="color:#1D7373">AUDIO_CREATIVE_REACH</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH_NON_SKIPPABLE</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_SURVEY</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH_SURVEY</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_SURVEY</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH_SURVEY</span></li>
<li><span style="color:#1D7373">DIRECT_ACTION_CHARGED</span></li>
<li><span style="color:#1D7373">MEDIA_CREATIVE_REACH_MAIN</span></li>
<li><span style="color:#1D7373">VIDEO_CREATIVE_REACH_MAIN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L74">FilterReason</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L75">StatValue</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L77">CtrMxFeatures</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L53">TFeatures</a></i>
</li>
<details open><summary><b>Message TFeatures</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L55">Features</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L79">Ctr</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L80">Cost</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L81">BidCorrection</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L82">ABConversionCostCoef</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L83">HitLogID</a></b>  <i>fixed64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L85">L1PosByProduct</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L86">L1PosByProductGroup</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L87">StatGroup</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L88">OrderID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L89">GroupExportID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L90">BannerFactors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L25">TBannerFactors</a></i>
</li>
<details open><summary><b>Message TBannerFactors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L32">BannerTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L33">BannerText</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L34">SecondTitle</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L35">BannerUrl</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L36">BannerPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L16">TBannerPhraseInfo</a></i>
</li>
<details open><summary><b>Message TBannerPhraseInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L19">ContextType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L20">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L21">Bid</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L22">PhraseText</a></b>  <i>bytes</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L37">BidCoefficients</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L9">TBidCoefficient</a></i>
</li>
<details open><summary><b>Message TBidCoefficient</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L11">Coef</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L12">CoefType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/event.proto?rev=r9795881#L229">UserCoefTypeEnum</a></i>
</li>
<details open><summary><b>Enum UserCoefTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">PRODUCT_TYPE</span></li>
<li><span style="color:#1D7373">INVENTORY_TYPE</span></li>
<li><span style="color:#1D7373">DESKTOP_COST</span></li>
<li><span style="color:#1D7373">MOBILE_COST</span></li>
<li><span style="color:#1D7373">TABLET_COST</span></li>
<li><span style="color:#1D7373">EXPR_TIME</span></li>
<li><span style="color:#1D7373">EXPR_SOCDEM</span></li>
<li><span style="color:#1D7373">EXPR_GOAL</span></li>
<li><span style="color:#1D7373">EXPR_MOBILE</span></li>
<li><span style="color:#1D7373">EXPR_WEATHER</span></li>
<li><span style="color:#1D7373">EXPR_GEO</span></li>
<li><span style="color:#1D7373">EXPR_TRAFFIC_JAM</span></li>
<li><span style="color:#1D7373">DIMENSION</span></li>
<li><span style="color:#1D7373">TIME_COST</span></li>
<li><span style="color:#1D7373">MOBILE_ANDROID_COST</span></li>
<li><span style="color:#1D7373">MOBILE_IOS_COST</span></li>
<li><span style="color:#1D7373">PAGE_DOMAIN</span></li>
<li><span style="color:#1D7373">DONT_SHOW_DOMAIN</span></li>
<li><span style="color:#1D7373">EXPR_VIDEO_CONTENT_DURATION</span></li>
<li><span style="color:#1D7373">DEVICE_TYPE</span></li>
<li><span style="color:#1D7373">AUTO_VIDEO_DIRECT</span></li>
<li><span style="color:#1D7373">PERFORMANCE_TGO</span></li>
<li><span style="color:#1D7373">PRISMA_INCOME_GRADE</span></li>
<li><span style="color:#1D7373">UNKNOWN</span></li>
<li><span style="color:#1D7373">EXPR_SEARCH_GOAL</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L13">Hint</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L38">TargetDomainID</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L91">TsarVectors</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L48">TTsarVectors</a></i>
</li>
<details open><summary><b>Message TTsarVectors</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L50">TsarVectorsByModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L41">TTsarVectorsByModel</a></i>
</li>
<details open><summary><b>Message TTsarVectorsByModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L43">ModelID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L44">BannerVector</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L45">HitVector</a></b>  <i>float</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L92">IsStaffHit</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L94">CtrMxFormulaType</a></b>  <i>sfixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/server/proto/log/stat_mx_features.proto?rev=r9795881#L95">CtrMxFormulaID</a></b>  <i>sfixed32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/join.proto?rev=r9795881#L30">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
