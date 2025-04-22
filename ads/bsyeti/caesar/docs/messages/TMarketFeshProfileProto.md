
## Message TMarketFeshProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_fesh.proto?rev=r9795881#L9">FeshID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_fesh.proto?rev=r9795881#L10">DjProfiles</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/dj/proto/dj.proto?rev=r9795881#L10">TDjProfiles</a></i>
</li>
<details open><summary><b>Message TDjProfiles</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/dj/proto/dj.proto?rev=r9795881#L11">ProfileData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/dj/proto/dj.proto?rev=r9795881#L5">TDjProfileData</a></i>
</li>
<details open><summary><b>Message TDjProfileData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/dj/proto/dj.proto?rev=r9795881#L6">Timestamp</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/dj/proto/dj.proto?rev=r9795881#L7">Profile</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L113">TProfileProto</a></i>
</li>
<details open><summary><b>Message TProfileProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L116">ObjectNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L117">ObjectType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L118">ObjectId</a></b>  <i>string</i>
<p> format as in "user_sessions" tables </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L119">IsYandex</a></b>  <i>bool</i>
<p> true if there is at least a single bit of information in this profile from logs from yandex net </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L120">ProfileVersion</a></b>  <i>uint32</i>
<p> profile code version </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L122">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L29">TCountersProto</a></i>
</li>
<details open><summary><b>Message TCountersProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L30">ObjectNames</a></b>  <i>string</i>
<p> maps TCounterProto::ObjectId into string representation </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L31">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L9">TCounterProto</a></i>
</li>
<details open><summary><b>Message TCounterProto</b></summary>
<p> If some field is not present than it should be copied from previous TCounterProto record  when deserializing (see NRecomender::TCounters::TCounters(const TCountersProto&)) </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L13">ObjectNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L14">ObjectType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L15">CounterNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L16">CounterType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L17">Reducer</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L71">EReducer</a></i>
</li>
<details open><summary><b>Enum EReducer</b></summary>
<p> You have to list all reducers you want to use. We need ids for serialization. </p>

<ul>
<li><span style="color:#1D7373">RT_Sum</span></li>
<li><span style="color:#1D7373">RT_Sum_7d</span></li>
<li><span style="color:#1D7373">RT_Sum_21d</span></li>
<li><span style="color:#1D7373">RT_Sum_30d</span></li>
<li><span style="color:#1D7373">RT_Sum_90d</span></li>
<li><span style="color:#1D7373">RT_Sum_180d</span></li>
<li><span style="color:#1D7373">RT_Sum_1d</span></li>
<li><span style="color:#1D7373">RT_Max</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax</span></li>
<li><span style="color:#1D7373">RT_SqrSum</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax_7d</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax_30d</span></li>
<li><span style="color:#1D7373">RT_SqrSum_7d</span></li>
<li><span style="color:#1D7373">RT_SqrSum_30d</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum_7d</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum_30d</span></li>
<li><span style="color:#1D7373">RT_Concat</span></li>
<li><span style="color:#1D7373">RT_Last</span></li>
<li><span style="color:#1D7373">RT_Sum_2h</span></li>
<li><span style="color:#1D7373">RT_Sum_8h</span></li>
<li><span style="color:#1D7373">RT_Sum_3d</span></li>
<li><span style="color:#1D7373">RT_Min</span></li>
<li><span style="color:#1D7373">RT_Min_1d</span></li>
<li><span style="color:#1D7373">RT_Min_7d</span></li>
<li><span style="color:#1D7373">RT_Min_30d</span></li>
<li><span style="color:#1D7373">RT_Max_1d</span></li>
<li><span style="color:#1D7373">RT_Max_7d</span></li>
<li><span style="color:#1D7373">RT_Max_30d</span></li>
<li><span style="color:#1D7373">RT_Sum_5min</span></li>
<li><span style="color:#1D7373">RT_Sum_10min</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L18">ObjectId</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L19">LastUpdateTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L21">Value</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L32">CompressedCounters</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L33">ZstdCompressedObjectNames</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L34">MinLastUpdateTime</a></b>  <i>fixed32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L123">Embeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L43">TAggregatedEmbeddingProto</a></i>
</li>
<details open><summary><b>Message TAggregatedEmbeddingProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L47">EmbeddingNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L48">EmbeddingType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L49">EmbeddingVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L50">Reducer</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L71">EReducer</a></i>
</li>
<details open><summary><b>Enum EReducer</b></summary>
<p> You have to list all reducers you want to use. We need ids for serialization. </p>

<ul>
<li><span style="color:#1D7373">RT_Sum</span></li>
<li><span style="color:#1D7373">RT_Sum_7d</span></li>
<li><span style="color:#1D7373">RT_Sum_21d</span></li>
<li><span style="color:#1D7373">RT_Sum_30d</span></li>
<li><span style="color:#1D7373">RT_Sum_90d</span></li>
<li><span style="color:#1D7373">RT_Sum_180d</span></li>
<li><span style="color:#1D7373">RT_Sum_1d</span></li>
<li><span style="color:#1D7373">RT_Max</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax</span></li>
<li><span style="color:#1D7373">RT_SqrSum</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax_7d</span></li>
<li><span style="color:#1D7373">RT_RectifiedMax_30d</span></li>
<li><span style="color:#1D7373">RT_SqrSum_7d</span></li>
<li><span style="color:#1D7373">RT_SqrSum_30d</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum_7d</span></li>
<li><span style="color:#1D7373">RT_Pow4Sum_30d</span></li>
<li><span style="color:#1D7373">RT_Concat</span></li>
<li><span style="color:#1D7373">RT_Last</span></li>
<li><span style="color:#1D7373">RT_Sum_2h</span></li>
<li><span style="color:#1D7373">RT_Sum_8h</span></li>
<li><span style="color:#1D7373">RT_Sum_3d</span></li>
<li><span style="color:#1D7373">RT_Min</span></li>
<li><span style="color:#1D7373">RT_Min_1d</span></li>
<li><span style="color:#1D7373">RT_Min_7d</span></li>
<li><span style="color:#1D7373">RT_Min_30d</span></li>
<li><span style="color:#1D7373">RT_Max_1d</span></li>
<li><span style="color:#1D7373">RT_Max_7d</span></li>
<li><span style="color:#1D7373">RT_Max_30d</span></li>
<li><span style="color:#1D7373">RT_Sum_5min</span></li>
<li><span style="color:#1D7373">RT_Sum_10min</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L56">Value</a></b>  <i>bytes</i>
<p> just memcpy'd float/float16/i8 arrays (as specified in embedding_type)  NOTE: change "optional" for "repeated" if for some reason we may store more than one embedding  (for ex: centers of biggest clusters in embeddings space)  but there should always be at least one embedding </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L57">Format</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L110">EEmbeddingFormat</a></i>
</li>
<details open><summary><b>Enum EEmbeddingFormat</b></summary>
<ul>
<li><span style="color:#1D7373">EF_float</span></li>
<li><span style="color:#1D7373">EF_i8</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L58">LastUpdateTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L59">WeightMultiplier</a></b>  <i>float</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L124">Filters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L72">TFilterProto</a></i>
</li>
<details open><summary><b>Message TFilterProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L73">FilterNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L74">FilterType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L75">FilterVersion</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L76">Data</a></b>  <i>bytes</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L77">ObjectNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L78">ObjectType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L79">LastUpdateTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L80">MaxChunkSize</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L81">MaxTotalSize</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L125">ArchiveData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L84">TArchiveDataProto</a></i>
</li>
<details open><summary><b>Message TArchiveDataProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L89">Values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L85">TPair</a></i>
</li>
<details open><summary><b>Message TPair</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L86">key</a></b>  <i>string</i>
<p> lowercase for backward compatibility </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L87">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L126">Erfs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L92">TErfProto</a></i>
</li>
<details open><summary><b>Message TErfProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L93">ErfNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L94">ErfType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L95">LastUpdateTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L97">Float</a></b>  <i>float</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L98">Double</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L99">Int32</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L100">Int64</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L101">String</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L102">Bool</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L127">Queues</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L106">TQueueProto</a></i>
</li>
<details open><summary><b>Message TQueueProto</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L107">QueueNamespace</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile_enums.proto?rev=r9795881#L9">EProfileNamespace</a></i>
</li>
<details open><summary><b>Enum EProfileNamespace</b></summary>
<ul>
<li><span style="color:#1D7373">PN_Unknown</span></li>
<li><span style="color:#1D7373">PN_Common</span></li>
<li><span style="color:#1D7373">PN_Test</span></li>
<li><span style="color:#1D7373">PN_News</span></li>
<li><span style="color:#1D7373">PN_TV</span></li>
<li><span style="color:#1D7373">PN_Collections</span></li>
<li><span style="color:#1D7373">PN_Znatoki</span></li>
<li><span style="color:#1D7373">PN_TestWOPolicy</span></li>
<li><span style="color:#1D7373">PN_Crypta</span></li>
<li><span style="color:#1D7373">PN_Video</span></li>
<li><span style="color:#1D7373">PN_Vitrina</span></li>
<li><span style="color:#1D7373">PN_Music</span></li>
<li><span style="color:#1D7373">PN_AlisaSkills</span></li>
<li><span style="color:#1D7373">PN_UserSessions</span></li>
<li><span style="color:#1D7373">PN_Entity</span></li>
<li><span style="color:#1D7373">PN_VHS</span></li>
<li><span style="color:#1D7373">PN_Web</span></li>
<li><span style="color:#1D7373">PN_NewsRegions</span></li>
<li><span style="color:#1D7373">PN_AliceGC</span></li>
<li><span style="color:#1D7373">PN_Images</span></li>
<li><span style="color:#1D7373">PN_MailSR</span></li>
<li><span style="color:#1D7373">PN_Market</span></li>
<li><span style="color:#1D7373">PN_Unity</span></li>
<li><span style="color:#1D7373">PN_Isolenta</span></li>
<li><span style="color:#1D7373">PN_MailSC</span></li>
<li><span style="color:#1D7373">PN_Tutorial</span></li>
<li><span style="color:#1D7373">PN_Kinopoisk</span></li>
<li><span style="color:#1D7373">PN_Talents</span></li>
<li><span style="color:#1D7373">PN_Cmnt</span></li>
<li><span style="color:#1D7373">PN_District</span></li>
<li><span style="color:#1D7373">PN_ShinyDiscovery</span></li>
<li><span style="color:#1D7373">PN_MLPortal</span></li>
<li><span style="color:#1D7373">PN_Morda</span></li>
<li><span style="color:#1D7373">PN_Toloka</span></li>
<li><span style="color:#1D7373">PN_Example</span></li>
<li><span style="color:#1D7373">PN_Trends</span></li>
<li><span style="color:#1D7373">PN_Games</span></li>
<li><span style="color:#1D7373">PN_Geo</span></li>
<li><span style="color:#1D7373">PN_Navpanel</span></li>
<li><span style="color:#1D7373">PN_Ugc</span></li>
<li><span style="color:#1D7373">PN_Mssngr</span></li>
<li><span style="color:#1D7373">PN_Sup</span></li>
<li><span style="color:#1D7373">PN_Ecom</span></li>
<li><span style="color:#1D7373">PN_Zaas</span></li>
<li><span style="color:#1D7373">PN_Chz</span></li>
<li><span style="color:#1D7373">PN_Classified</span></li>
<li><span style="color:#1D7373">PN_Edadeal</span></li>
<li><span style="color:#1D7373">PN_CategMarkup</span></li>
<li><span style="color:#1D7373">PN_Zen</span></li>
<li><span style="color:#1D7373">PN_MusicTutorial</span></li>
<li><span style="color:#1D7373">PN_Ydo</span></li>
<li><span style="color:#1D7373">PN_ChzAfisha</span></li>
<li><span style="color:#1D7373">PN_Eats</span></li>
<li><span style="color:#1D7373">PN_MarketEcom</span></li>
<li><span style="color:#1D7373">PN_Autoru</span></li>
<li><span style="color:#1D7373">PN_Goods</span></li>
<li><span style="color:#1D7373">PN_PersPoi</span></li>
<li><span style="color:#1D7373">PN_StatefulSearchRecs</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L108">QueueType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L109">LastUpdateTime</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L110">Actions</a></b>  <i>bytes</i>
<p> in fact serialized TActionProto </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/dj/lib/proto/profile.proto?rev=r9795881#L129">LastUpdateTime</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/market_fesh.proto?rev=r9795881#L13">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
