
## Message TOrderProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L437">OrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L438">Resources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L46">TResources</a></i>
</li>
<details open><summary><b>Message TResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L61">Version</a></b>  <i>uint64</i>
<p> IterID from direct-banners-log </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L62">DirectBannersLogUpdateTime</a></b>  <i>uint64</i>
<p> without regular reexport (full_export_flag) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L63">DirectBannersLogTouchTime</a></b>  <i>uint64</i>
<p> including regular reexport </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L64">ESSVersion</a></b>  <i>uint64</i>
<p> IterID from ESS. All ess-fields come together </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L65">ESSUpdateTime</a></b>  <i>uint64</i>
<p> update_time from ESS transport </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L66">ESSDeleteTime</a></b>  <i>uint64</i>
<p> zero if order is not deleted </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L68">ShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L11">TShowConditions</a></i>
</li>
<details open><summary><b>Message TShowConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L12">TargetTypes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L4">ETargetType</a></i>
<p> DON'T USE. Use IsDisabledInRsya/IsDisabledInSearch instead. List of disabled types. </p>

</li>
<details open><summary><b>Enum ETargetType</b></summary>
<ul>
<li><span style="color:#1D7373">TT_SEARCH</span></li>
<li><span style="color:#1D7373">TT_CATALOG</span></li>
<li><span style="color:#1D7373">TT_PARTNER</span></li>
<li><span style="color:#1D7373">TT_RSYA</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L13">StopTime</a></b>  <i>uint64</i>
<p> don't show campaign after this time. Already calculated in Order.IsActive flag </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L14">TimeZone</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L15">MinusPhrases</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L69">AutoBudget</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L18">TAutoBudgetInfo</a></i>
</li>
<details open><summary><b>Message TAutoBudgetInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L32">Enabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L33">AutoBudgetAvgBid</a></b>  <i>double</i>
<p> old AutoBudgetAvgCost </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L34">AutoBudgetAvgBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L35">AutoBudgetAvgCPA</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L36">AutoBudgetAvgCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L37">AutoBudgetAvgCPM</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L38">AutoBudgetAvgCPMCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L39">AutoBudgetAvgCPV</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L40">AutoBudgetAvgCPVCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L41">AutoBudgetDayLimitMoney</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L42">AutoBudgetDayLimitMoneyCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L43">AutoBudgetGoalExpression</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L44">AutoBudgetGoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L45">AutoBudgetMaxBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L46">AutoBudgetMaxBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L47">AutoBudgetMeaningfulGoalsValuesFromMetrika</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L48">AutoBudgetNetCPCOptimize</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L49">AutoBudgetOptimizeRF</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L50">AutoBudgetPaidActions</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L51">AutoBudgetPaidActionsPerFilter</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L52">AutoBudgetPaidCrr</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L53">AutoBudgetPaidMeaningfulGoalsHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L54">AutoBudgetPeriodBudgetFinish</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L55">AutoBudgetPeriodBudgetLimit</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L56">AutoBudgetPeriodBudgetLimitCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L57">AutoBudgetPeriodBudgetProlongation</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L58">AutoBudgetProfitability</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L59">AutoBudgetROILevel</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L60">AutoBudgetRegularSpent</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L61">AutoBudgetReserveReturn</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L62">AutoBudgetRestartReason</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L63">AutoBudgetRestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L64">AutoBudgetSoftRestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L65">AutoBudgetWeekLimit</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L66">AutoBudgetWeekLimitClicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L67">AutoBudgetWeekLimitCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L68">StrategyParams</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L19">TStrategyParams</a></i>
</li>
<details open><summary><b>Message TStrategyParams</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L22">Name</a></b>  <i>string</i>
<p> Name of AutoBudget Strategy. Possible values:  https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/campaigns.schema.sql?blame=true#L32 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L23">StrategyID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L24">PrevStrategyID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L69">AutoBudgetPromotions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L26">TAutoBudgetPromotion</a></i>
<p> https://st.yandex-team.ru/BSDEV-84947 </p>

</li>
<details open><summary><b>Message TAutoBudgetPromotion</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L27">DateFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L28">DateTo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L29">ConversionBoostPercent</a></b>  <i>int32</i>
<p> multiply 1kk. 20% -> 200000 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L72">AutoBudgetDayWeight</a></b>  <i>uint64</i>
<p> https://st.yandex-team.ru/BSSERVER-19090  Max part of budget per day. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L73">AutoBudgetMaxDayLimitMoney</a></b>  <i>double</i>
<p> Max(DayLimitMoney[StartTime]) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L74">AutoBudgetMaxDayLimitMoneyCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L77">AutoBudgetStrategy</a></b>  <i>string</i>
<p> DEPRICATED. Use StrategyParams.Name instead. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L70">OrderCreateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L71">DirectBannersLogFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L81">TDirectBannersLogFields</a></i>
</li>
<details open><summary><b>Message TDirectBannersLogFields</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L136">ABExperiments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L101">TABExperiments</a></i>
</li>
<details open><summary><b>Message TABExperiments</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L111">CoefDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L112">TargetDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L113">InternalTargetDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L114">StatDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L137">AgencyID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L138">AllowedDomains</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L139">AttributionType</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L140">AuctionPriority</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L141">BillingOrder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L89">TBillingOrder</a></i>
</li>
<details open><summary><b>Message TBillingOrder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L96">Default</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L97">Rules</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L90">TRules</a></i>
</li>
<details open><summary><b>Message TRules</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L91">Result</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L92">ProductTypesBits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L93">ProductId</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L98">ProductId</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L142">BroadMatchLimit</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L143">BusinessUnitPartnerShare</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L144">ClientID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L145">ContentType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L146">ContextLimit</a></b>  <i>int32</i>
<p> Rsya money percent of mixed campaings (almost deprecated) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L147">ContextPriceCoef</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L148">CounterID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L149">CountryRegionID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L150">CurrencyDate</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L151">CurrencyID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L152">Description</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L153">DirectDeals</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L154">DirectOrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L155">DirectShard</a></b>  <i>uint32</i>
<p> shard in direct mysql. Need for debug and exps in direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L156">EnableOrderPhraseLengthPrecedence</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L157">EngineID</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L158">EshowsBannerRate</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L159">EshowsThreshold</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L160">EshowsVideoRate</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L161">EshowsVideoType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L162">GroupOrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L163">HidePermalinkInfo</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L164">ImpressionStandardTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L165">ImpressionStandardType</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L166">IndependentBids</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L167">IsAllowAloneTrafaret</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L168">IsCalltrackingOnSite</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L169">IsClickTrackingEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L170">IsDisablePositionByFlagRequirement</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L171">IsDisabledInRsya</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L172">IsDisabledInSearch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L173">IsExtendedGeotargetingDisabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L174">UseRegularRegionGeotargeting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L175">UseCurrentRegionGeotargeting</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L176">IsExtendedRelevanceMatchEnabled</a></b>  <i>bool</i>
<p> isExtendedRelevanceMatchEnabled </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L177">IsFaviconBlocked</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L178">IsFixPrice</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L179">IsGroupOrder</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L180">IsMarket</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L181">IsMarketRatingHidden</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L182">IsMobileApp</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L183">IsOpenStatEnabled</a></b>  <i>bool</i>
<p> флаг для интеграции с внешними системами статистики( SpyLog, ... ) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L184">IsPriorityCampaign</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L185">IsPrivateDeal</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L186">IsRequireFiltrationByDontShowDomains</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L187">IsSiteMonitoringEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L188">IsTitleSubstitutionDisabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L189">IsUrlMonitoringEnabled</a></b>  <i>bool</i>
<p> CheckBannersAvailability, url-monitoring </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L190">IsVirtual</a></b>  <i>bool</i>
<p> isVirtual </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L191">ManagerUID</a></b>  <i>uint64</i>
<p> паспортный uid менеджера, если кампания сервисируемая </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L192">MaxCost</a></b>  <i>double</i>
<p> total amount of money for chips campaign (legacy) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L193">MaxCostCur</a></b>  <i>double</i>
<p> total amount of money in CurrencyID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L194">MaxRF</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L195">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L196">MetrikaCountersHash</a></b>  <i>uint64</i>
<p> https://st.yandex-team.ru/BSSERVER-19633 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L197">NDSHistory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L117">TNDSHistory</a></i>
<p> TaxHistory </p>

</li>
<details open><summary><b>Message TNDSHistory</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L118">DateFrom</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L119">DateTo</a></b>  <i>uint64</i>
<p> actualy you need only DateFrom </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L120">NDS</a></b>  <i>int32</i>
<p> *1000000: nds=20% == 200000 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L198">OrderType</a></b>  <i>int32</i>
<p> https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/protected/BS/ExportQuery.pm?blame=true&rev=r8541685#L4070 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L199">PassportUID</a></b>  <i>uint64</i>
<p> паспортный uid владельца кампании (обычно главного представителя клиента) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L200">PlaceID</a></b>  <i>uint64</i>
<p> 542 for click-paid, 1542 for show-paid, other is internal adv </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L201">ProductId</a></b>  <i>int32</i>
<p> https://st.yandex-team.ru/BSDEV-84233 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L202">RestrictionType</a></b>  <i>string</i>
<p> only for internal-adv </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L203">RestrictionValue</a></b>  <i>double</i>
<p> only for internal-adv </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L204">RfCloseByClick</a></b>  <i>string</i>
<p> only for internal-adv </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L205">RFDays</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L206">RFDecay</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L207">RFMinCPM</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L208">S2STrackingUrls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L131">TS2STrackingUrls</a></i>
</li>
<details open><summary><b>Message TS2STrackingUrls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L132">IOS</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L133">Android</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L209">SKAdNetworkCampaignID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L210">SourceInterface</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L211">StartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L212">StopTime</a></b>  <i>uint64</i>
<p> when user stopped campaign (flag Stop) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L213">TrafaretPositionBidCorrections</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L123">TTrafaretPositionBidCorrections</a></i>
<p> https://st.yandex-team.ru/DIRECT-149162 </p>

</li>
<details open><summary><b>Message TTrafaretPositionBidCorrections</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L124">Alone</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L125">DynamicGallery</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L126">Invalid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L127">Map</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L128">Suggest</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L214">UseTurboUrl</a></b>  <i>bool</i>
<p> has_turbo_smarts in direct; BSDEV-73462 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L215">DistributionTag</a></b>  <i>string</i>
<p> only for internal-adv </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L80">OrderMoney</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L47">TOrderMoney</a></i>
</li>
<details open><summary><b>Message TOrderMoney</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L48">IsPeriodLimitReached</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L49">IsPeriodLimitReachedCur</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L50">OrderMoneyLeft</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L51">OrderMoneyLeftCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L52">GroupMoneyLeft</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L53">GroupMoneyLeftCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L54">OrderLastEventTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L55">GroupLastEventTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L56">IsActiveExceptStopArchive</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L57">OrderMoneySpentCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L58">GroupMoneySpentCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L82">ESSRotationGoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L83">ESSMobileAppIDs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/common.proto?rev=r9795881#L17">UInt32List</a></i>
</li>
<details open><summary><b>Message UInt32List</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/common.proto?rev=r9795881#L18">values</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L84">ESSAllowedOnAdultContent</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L85">ESSMultipliers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L14">Multiplier</a></i>
</li>
<details open><summary><b>Message Multiplier</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L15">condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L10">TargetingExpression</a></i>
</li>
<details open><summary><b>Message TargetingExpression</b></summary>
<p> Протобуф должен совпадать с https://a.yandex-team.ru/arcadia/grut/libs/proto/public/auxiliary/targeting_expression.proto  Протобуф из grut рекомендуемый, для новых задач этот не использовать. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L14">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L11">Disjunction</a></i>
</li>
<details open><summary><b>Message Disjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L12">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L17">TargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L18">keyword</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NKeywords.KeywordEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L19">operation</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NOperations.OperationEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L20">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L16">custom_condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L23">CustomExpression</a></i>
</li>
<details open><summary><b>Message CustomExpression</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L30">ExperimentSegment</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L24">SegmentKey</a></i>
</li>
<details open><summary><b>Message SegmentKey</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L25">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L26">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L31">InventoryType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/inventory_types.proto?rev=r9795881#L6">InventoryTypeEnum</a></i>
</li>
<details open><summary><b>Enum InventoryTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">Undefined</span></li>
<li><span style="color:#1D7373">MediaCreativeBanner</span></li>
<li><span style="color:#1D7373">VideoInBanner</span></li>
<li><span style="color:#1D7373">VideoInPage</span></li>
<li><span style="color:#1D7373">VideoInStream</span></li>
<li><span style="color:#1D7373">VideoInApp</span></li>
<li><span style="color:#1D7373">VideoRewarded</span></li>
<li><span style="color:#1D7373">VideoPreroll</span></li>
<li><span style="color:#1D7373">VideoMidroll</span></li>
<li><span style="color:#1D7373">VideoPostroll</span></li>
<li><span style="color:#1D7373">VideoPauseroll</span></li>
<li><span style="color:#1D7373">VideoOverlay</span></li>
<li><span style="color:#1D7373">VideoPostrollOverlay</span></li>
<li><span style="color:#1D7373">VideoPostrollWrapper</span></li>
<li><span style="color:#1D7373">VideoInrollOverlay</span></li>
<li><span style="color:#1D7373">VideoInroll</span></li>
<li><span style="color:#1D7373">VideoInterstitial</span></li>
<li><span style="color:#1D7373">VideoFullscreen</span></li>
<li><span style="color:#1D7373">VideoDefault</span></li>
<li><span style="color:#1D7373">VideoPostPauseroll</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L32">PerformanceTgo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L33">AutoVideoDirect</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L34">TrafaretPosition</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L18">value</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L19">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/multiplier_type.proto?rev=r9795881#L6">MultiplierTypeEnum</a></i>
</li>
<details open><summary><b>Enum MultiplierTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">AutoVideoDirect</span></li>
<li><span style="color:#1D7373">InventoryType</span></li>
<li><span style="color:#1D7373">DeviceType</span></li>
<li><span style="color:#1D7373">Demography</span></li>
<li><span style="color:#1D7373">Retargeting</span></li>
<li><span style="color:#1D7373">Weather</span></li>
<li><span style="color:#1D7373">Geo</span></li>
<li><span style="color:#1D7373">TrafficJam</span></li>
<li><span style="color:#1D7373">AbSegment</span></li>
<li><span style="color:#1D7373">VideoContentDuration</span></li>
<li><span style="color:#1D7373">Time</span></li>
<li><span style="color:#1D7373">PerformanceTgo</span></li>
<li><span style="color:#1D7373">PrismaIncomeGrade</span></li>
<li><span style="color:#1D7373">SearchRetargeting</span></li>
<li><span style="color:#1D7373">TrafaretPosition</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L86">ESSFrequencyShowsOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L9">RfOptions</a></i>
</li>
<details open><summary><b>Message RfOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L10">max_shows_count</a></b>  <i>uint32</i>
<p> кол-во макс показов в интервал времени. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L11">max_shows_period</a></b>  <i>uint64</i>
<p> интервал времени для параметра выше (в секундах). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L12">stop_shows_period</a></b>  <i>uint64</i>
<p> период запрета показов после нажатия крестик (в секундах). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L13">interval_between_shows</a></b>  <i>uint64</i>
<p> интервал между показами (в секундах). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L14">max_clicks_count</a></b>  <i>uint32</i>
<p> макс кол-во кликов. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L15">max_clicks_period</a></b>  <i>uint32</i>
<p> интервал времени, на который прекращаем показы при достижении кол-ва кликов max_clicks_count (в секундах). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L16">max_stops_count</a></b>  <i>uint32</i>
<p> макс кол-во нажатий на крестик. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L17">max_stops_period</a></b>  <i>uint32</i>
<p> интервал времени, на который прекращаем показы при достижении кол-ва нажатий на крестик max_stops_count (в секундах). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L87">ESSWidgetPartnerID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L88">ESSMetrikaCounterIDs</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L89">ESSMetatype</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/campaign/campaign.proto?rev=r9795881#L26">CampaignMetatype</a></i>
</li>
<details open><summary><b>Enum CampaignMetatype</b></summary>
<ul>
<li><span style="color:#1D7373">CAMPAIGN_METATYPE_DEFAULT</span></li>
<li><span style="color:#1D7373">CAMPAIGN_METATYPE_ECOM</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L90">DistributionTagID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L91">ESSIsWWManagedOrder</a></b>  <i>bool</i>
<p> flag from direct for approved iternational orders (maintained by managers) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L92">ESSIsCpmGlobalAbSegment</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L439">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L95">TFlags</a></i>
</li>
<details open><summary><b>Message TFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L96">Version</a></b>  <i>uint64</i>
<p> IterID in Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L97">Archive</a></b>  <i>bool</i>
<p> заархивирован в интерфейсе Директе. При этом бывают разархивации </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L98">Stop</a></b>  <i>bool</i>
<p> Остановлена в интерфейсе Директа (похоже на "пауза"), в теории может часто меняться </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L99">OrderFirstActiveTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L100">AutobudgetStopTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L101">IsActive</a></b>  <i>bool</i>
<p> общий флаг, при котором показы кампании вообще возможны. Включает в себя наличие денег, непревышение StopTime, Stop и Archive </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L102">LastActiveTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L104">RemovalTimestamp</a></b>  <i>fixed32</i>
<p> The time when object was removed from GrUT. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L106">GrutVersion</a></b>  <i>uint64</i>
<p> Grut Object Version. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L107">IsStoppedEffective</a></b>  <i>bool</i>
<p>IsStoped || (некоторая логика для cpm_price кампаний) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L108">SmartParentBanner</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L42">TVersionedBool</a></i>
</li>
<details open><summary><b>Message TVersionedBool</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L43">Value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L44">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L109">DynamicParentBanner</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L42">TVersionedBool</a></i>
</li>
<details open><summary><b>Message TVersionedBool</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L43">Value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L44">Version</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L440">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L112">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L113">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L441">ShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L116">TShowConditions</a></i>
</li>
<details open><summary><b>Message TShowConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L117">Version</a></b>  <i>uint64</i>
<p> IterID in Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L118">Timestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L119">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L10">TargetingExpression</a></i>
</li>
<details open><summary><b>Message TargetingExpression</b></summary>
<p> Протобуф должен совпадать с https://a.yandex-team.ru/arcadia/grut/libs/proto/public/auxiliary/targeting_expression.proto  Протобуф из grut рекомендуемый, для новых задач этот не использовать. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L14">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L11">Disjunction</a></i>
</li>
<details open><summary><b>Message Disjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L12">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L17">TargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L18">keyword</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NKeywords.KeywordEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L19">operation</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NOperations.OperationEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L20">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L120">ContextID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L442">AutobudgetResources</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L123">TAutobudgetResources</a></i>
</li>
<details open><summary><b>Message TAutobudgetResources</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L376">AutobudgetControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L124">TAutobudgetControls</a></i>
</li>
<details open><summary><b>Message TAutobudgetControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L345">ExperimentControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L155">TExperimentControls</a></i>
</li>
<details open><summary><b>Message TExperimentControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L312">ExperimentID</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L315">SearchControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L316">FlatControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L317">WeekBudgetMult</a></b>  <i>int64</i>
<p> for week budget filters in the yabs server (BSSERVER-17293) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L318">AllowedSpendings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L302">TAllowedSpendings</a></i>
</li>
<details open><summary><b>Message TAllowedSpendings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L303">Hour</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L306">AllowedSpendingCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L307">TimeDelta</a></b>  <i>int64</i>
<p> the moving time window width </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L308">ExpectedSpendingCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L309">ExpectedIncomeCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L319">YqlBidderDataTimestamp</a></b>  <i>int64</i>
<p> the time when corresponding YqlBidderAutobudgetControls experiment controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L321">ExportWeekBudgetMult</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L323">ExportDayWeight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L346">DataTimestamp</a></b>  <i>int64</i>
<p> the time when autobudget controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L347">AutobudgetStartTime</a></b>  <i>int64</i>
<p> the time when autobudget strategy have been started or significantly changed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L348">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L349">AutobudgetSettingFromBidder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L326">TAutobudgetSettingFromBidder</a></i>
</li>
<details open><summary><b>Message TAutobudgetSettingFromBidder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L327">TargetCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L329">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L330">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L331">TargetDRR</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L351">TopTargetDomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L353">IsBanned</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L354">CounterID</a></b>  <i>int64</i>
<p> this field is needed to get zero-diff with YQL-bidder, because existing field ESSMetrikaCounterIds stores many CounterIDs </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L355">TargetDomainIDCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L334">TTargetDomainIDCounter</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L335">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L336">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L357">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L358">WasYqlTargetDomainID</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L359">TimeTargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L339">TTimeTargeting</a></i>
</li>
<details open><summary><b>Message TTimeTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L340">Coeffs</a></b>  <i>uint32</i>
<p> 168 (hours in week, regular days) + 24 (working holidays) elements </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L341">TreatWorkHolidaysAsWorkDays</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L342">IgnoreHolidays</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L360">CounterIDUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L367">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L362">TNumOptionPaidActionsChangesCounter</a></i>
</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L363">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L364">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L365">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L377">ComputedAutobudgetControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L124">TAutobudgetControls</a></i>
<p> computes in caesar </p>

</li>
<details open><summary><b>Message TAutobudgetControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L345">ExperimentControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L155">TExperimentControls</a></i>
</li>
<details open><summary><b>Message TExperimentControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L312">ExperimentID</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L315">SearchControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L316">FlatControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L317">WeekBudgetMult</a></b>  <i>int64</i>
<p> for week budget filters in the yabs server (BSSERVER-17293) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L318">AllowedSpendings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L302">TAllowedSpendings</a></i>
</li>
<details open><summary><b>Message TAllowedSpendings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L303">Hour</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L306">AllowedSpendingCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L307">TimeDelta</a></b>  <i>int64</i>
<p> the moving time window width </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L308">ExpectedSpendingCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L309">ExpectedIncomeCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L319">YqlBidderDataTimestamp</a></b>  <i>int64</i>
<p> the time when corresponding YqlBidderAutobudgetControls experiment controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L321">ExportWeekBudgetMult</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L323">ExportDayWeight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L346">DataTimestamp</a></b>  <i>int64</i>
<p> the time when autobudget controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L347">AutobudgetStartTime</a></b>  <i>int64</i>
<p> the time when autobudget strategy have been started or significantly changed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L348">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L349">AutobudgetSettingFromBidder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L326">TAutobudgetSettingFromBidder</a></i>
</li>
<details open><summary><b>Message TAutobudgetSettingFromBidder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L327">TargetCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L329">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L330">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L331">TargetDRR</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L351">TopTargetDomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L353">IsBanned</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L354">CounterID</a></b>  <i>int64</i>
<p> this field is needed to get zero-diff with YQL-bidder, because existing field ESSMetrikaCounterIds stores many CounterIDs </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L355">TargetDomainIDCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L334">TTargetDomainIDCounter</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L335">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L336">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L357">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L358">WasYqlTargetDomainID</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L359">TimeTargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L339">TTimeTargeting</a></i>
</li>
<details open><summary><b>Message TTimeTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L340">Coeffs</a></b>  <i>uint32</i>
<p> 168 (hours in week, regular days) + 24 (working holidays) elements </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L341">TreatWorkHolidaysAsWorkDays</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L342">IgnoreHolidays</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L360">CounterIDUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L367">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L362">TNumOptionPaidActionsChangesCounter</a></i>
</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L363">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L364">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L365">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L378">ComputedAutobudgetPreprodControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L124">TAutobudgetControls</a></i>
<p> computes in caesar </p>

</li>
<details open><summary><b>Message TAutobudgetControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L345">ExperimentControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L155">TExperimentControls</a></i>
</li>
<details open><summary><b>Message TExperimentControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L312">ExperimentID</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L315">SearchControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L316">FlatControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L317">WeekBudgetMult</a></b>  <i>int64</i>
<p> for week budget filters in the yabs server (BSSERVER-17293) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L318">AllowedSpendings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L302">TAllowedSpendings</a></i>
</li>
<details open><summary><b>Message TAllowedSpendings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L303">Hour</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L306">AllowedSpendingCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L307">TimeDelta</a></b>  <i>int64</i>
<p> the moving time window width </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L308">ExpectedSpendingCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L309">ExpectedIncomeCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L319">YqlBidderDataTimestamp</a></b>  <i>int64</i>
<p> the time when corresponding YqlBidderAutobudgetControls experiment controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L321">ExportWeekBudgetMult</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L323">ExportDayWeight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L346">DataTimestamp</a></b>  <i>int64</i>
<p> the time when autobudget controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L347">AutobudgetStartTime</a></b>  <i>int64</i>
<p> the time when autobudget strategy have been started or significantly changed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L348">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L349">AutobudgetSettingFromBidder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L326">TAutobudgetSettingFromBidder</a></i>
</li>
<details open><summary><b>Message TAutobudgetSettingFromBidder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L327">TargetCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L329">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L330">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L331">TargetDRR</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L351">TopTargetDomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L353">IsBanned</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L354">CounterID</a></b>  <i>int64</i>
<p> this field is needed to get zero-diff with YQL-bidder, because existing field ESSMetrikaCounterIds stores many CounterIDs </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L355">TargetDomainIDCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L334">TTargetDomainIDCounter</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L335">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L336">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L357">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L358">WasYqlTargetDomainID</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L359">TimeTargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L339">TTimeTargeting</a></i>
</li>
<details open><summary><b>Message TTimeTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L340">Coeffs</a></b>  <i>uint32</i>
<p> 168 (hours in week, regular days) + 24 (working holidays) elements </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L341">TreatWorkHolidaysAsWorkDays</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L342">IgnoreHolidays</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L360">CounterIDUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L367">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L362">TNumOptionPaidActionsChangesCounter</a></i>
</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L363">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L364">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L365">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L379">YqlBidderAutobudgetControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L124">TAutobudgetControls</a></i>
<p> comes from YQL-bidder </p>

</li>
<details open><summary><b>Message TAutobudgetControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L345">ExperimentControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L155">TExperimentControls</a></i>
</li>
<details open><summary><b>Message TExperimentControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L312">ExperimentID</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L315">SearchControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L316">FlatControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L317">WeekBudgetMult</a></b>  <i>int64</i>
<p> for week budget filters in the yabs server (BSSERVER-17293) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L318">AllowedSpendings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L302">TAllowedSpendings</a></i>
</li>
<details open><summary><b>Message TAllowedSpendings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L303">Hour</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L306">AllowedSpendingCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L307">TimeDelta</a></b>  <i>int64</i>
<p> the moving time window width </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L308">ExpectedSpendingCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L309">ExpectedIncomeCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L319">YqlBidderDataTimestamp</a></b>  <i>int64</i>
<p> the time when corresponding YqlBidderAutobudgetControls experiment controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L321">ExportWeekBudgetMult</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L323">ExportDayWeight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L346">DataTimestamp</a></b>  <i>int64</i>
<p> the time when autobudget controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L347">AutobudgetStartTime</a></b>  <i>int64</i>
<p> the time when autobudget strategy have been started or significantly changed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L348">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L349">AutobudgetSettingFromBidder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L326">TAutobudgetSettingFromBidder</a></i>
</li>
<details open><summary><b>Message TAutobudgetSettingFromBidder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L327">TargetCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L329">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L330">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L331">TargetDRR</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L351">TopTargetDomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L353">IsBanned</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L354">CounterID</a></b>  <i>int64</i>
<p> this field is needed to get zero-diff with YQL-bidder, because existing field ESSMetrikaCounterIds stores many CounterIDs </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L355">TargetDomainIDCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L334">TTargetDomainIDCounter</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L335">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L336">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L357">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L358">WasYqlTargetDomainID</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L359">TimeTargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L339">TTimeTargeting</a></i>
</li>
<details open><summary><b>Message TTimeTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L340">Coeffs</a></b>  <i>uint32</i>
<p> 168 (hours in week, regular days) + 24 (working holidays) elements </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L341">TreatWorkHolidaysAsWorkDays</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L342">IgnoreHolidays</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L360">CounterIDUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L367">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L362">TNumOptionPaidActionsChangesCounter</a></i>
</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L363">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L364">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L365">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L381">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L370">TNumOptionPaidActionsChangesCounter</a></i>
<p> will be removed soon </p>

</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<p> will be removed soon </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L371">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L372">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L373">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L383">BackupAutobudgetControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L124">TAutobudgetControls</a></i>
<p>comes from backup map-reduce process </p>

</li>
<details open><summary><b>Message TAutobudgetControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L345">ExperimentControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L155">TExperimentControls</a></i>
</li>
<details open><summary><b>Message TExperimentControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L312">ExperimentID</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L315">SearchControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L316">FlatControls</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L160">TSplittedControls</a></i>
</li>
<details open><summary><b>Message TSplittedControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L271">AuctionProbability</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L272">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L273">BidCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L274">BidCoef</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L275">BidNoiseRange</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L277">MetaInfo</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlMetaInfo in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L278">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L280">Model</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L161">TModel</a></i>
</li>
<details open><summary><b>Message TModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L178">WeekLimitBidParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L179">WeekLimitBidCurParam</a></b>  <i>double</i>
<p> aka C </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L180">CpaBidParam</a></b>  <i>double</i>
<p> aka X </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L181">CpaBidCurParam</a></b>  <i>double</i>
<p> aka XCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L182">PerfomanceCpaBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L183">PerfomanceCpaBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L184">PerfomanceCpcBidParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L185">PerfomanceCpcBidCurParam</a></b>  <i>double</i>
<p> will be removed in 2022 q2-q3 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L186">RoiBidParam</a></b>  <i>double</i>
<p> aka XRoi </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L187">RoiBidCurParam</a></b>  <i>double</i>
<p> aka XRoiCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L188">CpcBidParam</a></b>  <i>double</i>
<p> aka XCpc </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L189">CpcBidCurParam</a></b>  <i>double</i>
<p> aka XCpcCur </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L190">CpmBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L191">CpmBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L192">CpvBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L193">CpvBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L194">MinBidDailyCostMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L195">CpaBidMultiplier</a></b>  <i>double</i>
<p> deprecated, will be removed soon </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L196">SumWorkingHistoryABCoeff</a></b>  <i>double</i>
<p> needed to compute allowed spendings </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L197">Version</a></b>  <i>int64</i>
<p> to be logged as AutoBudgetControlModelVersion in event log (BSSERVER-16592) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L198">TrafficWeights</a></b>  <i>fixed32</i>
<p> multiplied by 10^9 (AUTOBUDGET-1812). size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L199">TrafficWeightsWithTimeTargeting</a></b>  <i>fixed32</i>
<p> multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L200">ExpectedSumActions</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L201">ExpectedCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L202">WeekLimitModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L162">TBudgetModel</a></i>
</li>
<details open><summary><b>Message TBudgetModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L163">SpentShareCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L164">PeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L165">RestOfPeriodWeight</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L166">PeriodMult</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L204">CostBidCurRatio</a></b>  <i>double</i>
<p> optional TBudgetModel PeriodLimitModel = 26; TBA in the future  aka SumCostCurSourceCostCurRatio </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L208">MinBidDailyCostMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L209">CpaBidMultiplierModel</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L169">TMultipliersModel</a></i>
<p> the pessimizing multiplier for paid actions fraud orders </p>

</li>
<details open><summary><b>Message TMultipliersModel</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L170">AgencyIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L171">CounterIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L172">DomainIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L173">GroupOrderIDMultiplier</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L175">FinalMultiplier</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L211">SumAction</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L212">SumActionPrice</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L213">SumActionPriceCur</a></b>  <i>double</i>
<p> needed to compute expected income </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L222">ProfitBidSettings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L215">TProfitBidSettings</a></i>
</li>
<details open><summary><b>Message TProfitBidSettings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L216">IsProfitBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L217">UsedClampToCPABid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L218">UsedClampToMinBid</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L219">UsedClampToMinBidCur</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L224">PeriodLimitBidParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L225">PeriodLimitBidCurParam</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L227">TrafficWeightsWithTimeTargetingZeroRegion</a></b>  <i>fixed32</i>
<p> only for period orders, multiplied by 10^9. size must not be less than 7 * 24 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L281">RawBids</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L230">TRawBids</a></i>
</li>
<details open><summary><b>Message TRawBids</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L231">WeekLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L232">WeekLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L233">CpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L234">CpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L235">PerfomanceCpaBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L236">PerfomanceCpaBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L237">PerfomanceCpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L238">PerfomanceCpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L239">RoiBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L240">RoiBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L241">CpcBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L242">CpcBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L243">CpmBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L244">CpmBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L245">CpvBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L246">CpvBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L247">PeriodLimitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L248">PeriodLimitBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L249">CpaMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L250">CpaMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L251">RoiMinBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L252">RoiMinBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L253">ProfitBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L254">ProfitBidCur</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L283">BidSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L284">BidCurSource</a></b>  <i>string</i>
<p> AUTOBUDGET-1703 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L286">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L287">ActiveTimeCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L257">TActiveTimeCounter</a></i>
<p> Active hours (AUTOBUDGET-1806) </p>

</li>
<details open><summary><b>Message TActiveTimeCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L261">TimestampCounter</a></b>  <i>uint32</i>
<p> FirstTimestamp matches to TimestampCounter[StartOffset]  TimestampCounter[i] is matched to timestamp t[i], where  t[i] = (FirstTimestamp + (i + TimestampCounter.size()) % TimestampCounter.size() * (5 * 60)) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L262">FirstTimestamp</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L263">StartOffset</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L289">ExportBid</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L266">TExportBid</a></i>
</li>
<details open><summary><b>Message TExportBid</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L267">Bid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L268">BidCur</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L292">BidBeforeBan</a></b>  <i>int64</i>
<p> fields for analytics </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L293">BidCurBeforeBan</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L295">ExportAuctionProbability</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L297">ExportBidCoef</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L298">ExportBidNoiseRange</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L299">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L317">WeekBudgetMult</a></b>  <i>int64</i>
<p> for week budget filters in the yabs server (BSSERVER-17293) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L318">AllowedSpendings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L302">TAllowedSpendings</a></i>
</li>
<details open><summary><b>Message TAllowedSpendings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L303">Hour</a></b>  <i>int64</i>
<p> above is key </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L306">AllowedSpendingCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L307">TimeDelta</a></b>  <i>int64</i>
<p> the moving time window width </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L308">ExpectedSpendingCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L309">ExpectedIncomeCur</a></b>  <i>int64</i>
<p> temporary, needed for b2b </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L319">YqlBidderDataTimestamp</a></b>  <i>int64</i>
<p> the time when corresponding YqlBidderAutobudgetControls experiment controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L321">ExportWeekBudgetMult</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L323">ExportDayWeight</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L156">TExportControl</a></i>
</li>
<details open><summary><b>Message TExportControl</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L157">Value</a></b>  <i>uint32</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L346">DataTimestamp</a></b>  <i>int64</i>
<p> the time when autobudget controls have been computed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L347">AutobudgetStartTime</a></b>  <i>int64</i>
<p> the time when autobudget strategy have been started or significantly changed </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L348">SpentCost</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L125">TSpentCost</a></i>
</li>
<details open><summary><b>Message TSpentCost</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L126">DailySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L127">DailySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L128">WeeklySpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L129">WeeklySpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L130">PeriodSpentCost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L131">PeriodSpentCostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L132">DailySpentCostZeroingTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L133">WeeklySpentCostUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L134">LastEventTime</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L349">AutobudgetSettingFromBidder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L326">TAutobudgetSettingFromBidder</a></i>
</li>
<details open><summary><b>Message TAutobudgetSettingFromBidder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L327">TargetCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L329">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L330">MeaningfulGoals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L82">TMeaningfulGoal</a></i>
</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L83">GoalID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L85">IsMetrikaSourceOfValue</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L86">Value</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L331">TargetDRR</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L351">TopTargetDomainID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L353">IsBanned</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L354">CounterID</a></b>  <i>int64</i>
<p> this field is needed to get zero-diff with YQL-bidder, because existing field ESSMetrikaCounterIds stores many CounterIDs </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L355">TargetDomainIDCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L334">TTargetDomainIDCounter</a></i>
</li>
<details open><summary><b>Message TTargetDomainIDCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L335">TargetDomainID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L336">Value</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L357">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L150">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L151">DailyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L152">WeeklyCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L153">PeriodCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L137">TAutobudgetCounters</a></i>
</li>
<details open><summary><b>Message TAutobudgetCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L138">BeginTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L139">LastEventTimestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L140">RestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L142">Cost</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L143">CostCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L145">Shows</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L146">Clicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L147">TrueViews</a></b>  <i>double</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L358">WasYqlTargetDomainID</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L359">TimeTargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L339">TTimeTargeting</a></i>
</li>
<details open><summary><b>Message TTimeTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L340">Coeffs</a></b>  <i>uint32</i>
<p> 168 (hours in week, regular days) + 24 (working holidays) elements </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L341">TreatWorkHolidaysAsWorkDays</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L342">IgnoreHolidays</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L360">CounterIDUpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L367">NumOptionPaidActionsChangesCounter</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L362">TNumOptionPaidActionsChangesCounter</a></i>
</li>
<details open><summary><b>Message TNumOptionPaidActionsChangesCounter</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L363">NumOptionPaidActionsChangesLastDay</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L364">NumOptionPaidActionsChangesToday</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L365">TimestampToday</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L443">GrutObject</a></b>  <i>TCampaignV2</i>
</li>
<details open><summary><b>Message TCampaignV2</b></summary>
<ul>
<li><b>meta</b>  <i>TCampaignV2Meta</i>
</li>
<details open><summary><b>Message TCampaignV2Meta</b></summary>
<ul>
<li><b>id</b>  <i>uint64</i>
</li>

<li><b>direct_id</b>  <i>uint64</i>
</li>

<li><b>direct_type</b>  <i>int32</i>
</li>

<li><b>source</b>  <i>int32</i>
</li>

<li><b>product_id</b>  <i>uint64</i>
</li>

<li><b>agency_client_id</b>  <i>uint64</i>
</li>

<li><b>meta_type</b>  <i>int32</i>
</li>

<li><b>order_type</b>  <i>int32</i>
</li>

<li><b>uuid</b>  <i>string</i>
</li>

<li><b>name</b>  <i>string</i>
</li>

<li><b>client_id</b>  <i>uint64</i>
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
<li><b>spec</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L55">TCampaignV2Spec</a></i>
</li>
<details open><summary><b>Message TCampaignV2Spec</b></summary>
<p> Пользовательские данные.  Все денежные поля кампании хранятся домноженными до 10^6.  Все даты в unix_timestamp. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L394">name</a></b>  <i>string</i>
<p> Название кампании заданное пользователем. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L399">status</a></b>  <i>int32</i>
<p> Пользовательский статус кампании.  enum ECampaignStatus </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L401">start_date</a></b>  <i>fixed32</i>
<p> Дата начала работы кампании. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L403">end_date</a></b>  <i>fixed32</i>
<p> Дата окончания кампании. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L406">currency_iso_code</a></b>  <i>uint32</i>
<p> https://en.wikipedia.org/wiki/ISO_4217, 999 for ynd_fixed. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L409">time_target_str</a></b>  <i>string</i>
<p> Описание формата https://a.yandex-team.ru/arc/trunk/arcadia/direct/libs/timetarget/README.md?rev=r9019063#L11  https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/protected/TimeTarget.pm?rev=r8992679#L12. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L410">flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L57">TFlags</a></i>
</li>
<details open><summary><b>Message TFlags</b></summary>
<p> Бинарные флаги кампании, установленные пользователем (аналог campaigns.opts). </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L59">is_virtual</a></b>  <i>bool</i>
<p> Виртуальная кампания, реально не показывается, но статистика идет. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L61">no_title_substitute</a></b>  <i>bool</i>
<p> Запретить подстановку текста запроса в заголовок баннера. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L63">hide_permalink_info</a></b>  <i>bool</i>
<p> Не показывать в Геопоиске дополнительную информацию из Справочника. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L65">no_extended_geotargeting</a></b>  <i>bool</i>
<p> Отключить расширенный геотаргетинг (регион из запроса). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L67">is_alone_trafaret_allowed</a></b>  <i>bool</i>
<p> Разрешено показывать объявления на Поиске в трафаретах с вытеснением других участников. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L69">require_filtration_by_dont_show_domains</a></b>  <i>bool</i>
<p> Включить на площадках Яндекса фильтрацию по списку запрещенных доменов. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L71">enable_cpc_hold</a></b>  <i>bool</i>
<p> Удерживание цены клика в РСЯ ниже цены на поиске. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L73">is_allowed_on_adult_content</a></b>  <i>bool</i>
<p> Включать ли показы на SSP с adult трафиком. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L76">add_metrika_tag_to_url</a></b>  <i>bool</i>
<p> Аналог status_click_track.  Отслеживание кликов метрикой (проприетарный аналог gclid/openstat). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L79">site_monitoring_enabled</a></b>  <i>bool</i>
<p> Аналог statusMetricaControl.  Включен ли мониторинг сайта: останавливать ли объявления при неработающем сайте. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L82">open_stat_enabled</a></b>  <i>bool</i>
<p> Аналог statusOpenStat.  Флаг для интеграции с внешними системами статистики( SpyLog, ... ). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L84">has_turbo_smarts</a></b>  <i>bool</i>
<p> Использовать турбо-версии смарт-объявлений. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L86">is_new_ios_version_enabled</a></b>  <i>bool</i>
<p> Включать показы на iOS 14.5 и выше. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L88">has_turbo_app</a></b>  <i>bool</i>
<p> В кампании есть баннер со ссылкой на турпо-апп (не снимается при удалении турбо-аппа). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L90">is_skad_network_enabled</a></b>  <i>bool</i>
<p> Включать ли показы через сеть SkadNetwork. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L93">is_worldwide</a></b>  <i>bool</i>
<p> Международная кампания.  campaigns.opts.is_ww_managed_order в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L96">is_search_lift_enabled</a></b>  <i>bool</i>
<p> Включен ли search lift.  camp_options.is_search_lift_enabled в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L99">is_cpm_global_ab_segment</a></b>  <i>bool</i>
<p> Включен ли единый контроль для медийных кампаний.  camp_options.is_cpm_global_ab_segment в mysql. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L411">strategy</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L102">TStrategy</a></i>
</li>
<details open><summary><b>Message TStrategy</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L184">type</a></b>  <i>int32</i>
<p> enum EStrategyType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L186">auto_prolongation</a></b>  <i>bool</i>
<p> Продлевать автоматически до даты окончания РК или пока не закончится бюджет. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L187">avg_bid</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L188">avg_cpa</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L189">avg_cpi</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L190">avg_cpm</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L191">avg_cpv</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L192">bid</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L193">budget</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L195">crr</a></b>  <i>uint32</i>
<p> Доля рекламных расходов - отношение суммы расходов на рекламу к доходу, который она принесла. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L197">daily_change_count</a></b>  <i>uint32</i>
<p> Количество изменений суммы дневного бюджета за день. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L198">filter_avg_bid</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L199">filter_avg_cpa</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L200">start_date</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L201">finish_date</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L202">goal_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L205">bidder_restart_time</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L206">update_time</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L207">name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L210">pay_for_conversion</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L213">profitability</a></b>  <i>uint64</i>
<p> Себестоимость товара или услуги, % от указанного дохода,  значения могут быть до 2-го знака после запятой, хранятся домноженными на 10^6. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L215">reserve_return</a></b>  <i>uint32</i>
<p> Процент возврата в рекламу от сэкономленного бюджета (0 <= x <= 100; default 100) кратно 10. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L218">roi_coef</a></b>  <i>int64</i>
<p> Рентабельность инвестиций, значения могут быть до 3-го знака после запятой, хранятся домноженными на 10^6.  Исходное значение(до домножения) -1 < x. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L220">budget_limit</a></b>  <i>uint64</i>
<p> Тратить не более этой суммы в неделю. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L222">autobudget_enabled</a></b>  <i>bool</i>
<p> Включени ли на кампании автобюджет. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L415">metrika_counters_ids</a></b>  <i>uint64</i>
<p> номера счетчиков метрики </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L422">minus_phrases_ids</a></b>  <i>uint64</i>
<p> Минус слова на кампанию  на текущий момент аналог camp_options.minus_words, но хранится в виде ссылки на таблицу minus_phrases  на текущий момент в списке один элемент. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L429">calltracking_settings_id</a></b>  <i>uint64</i>
<p> ID Настроек Сalltracking'а на сайте. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L431">attribution</a></b>  <i>int32</i>
<p> enum ECampaignAttribution </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L434">place_id</a></b>  <i>uint64</i>
<p> Место показа для внутренней рекламы.  Некоторые значения в enum EPlaceId. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L437">platform</a></b>  <i>int32</i>
<p> enum ECampaignPlatform  Типы площадок для показа. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L439">timezone</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L228">TTimezone</a></i>
<p> Данные о таймзоне, заполняются из geo_timezones в mysql. </p>

</li>
<details open><summary><b>Message TTimezone</b></summary>
<p> Данные о таймзоне, заполняются из geo_timezones в mysql. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L229">country_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L230">name</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L441">wallet_campaign_id</a></b>  <i>uint64</i>
<p> кампания общего счета, привязанного к данной кампании (отсутствует, если счет не привязан) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L446">manager_uid</a></b>  <i>uint64</i>
<p> uid менеджера, если кампания сервисируемая, иначе отсутствует </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L448">autobudget_restart</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L237">TAutoBudgetRestart</a></i>
<p> Информация о рестарте автобюджета. </p>

</li>
<details open><summary><b>Message TAutoBudgetRestart</b></summary>
<p> Информация о последнем рестарте автобюджета кампании.  Автобюджет рестартует, если стратегия меняется значительно  сейчас рестарт вычисляется в репликации, сравнивая поля записанные в GRuT с теми, которые записаны в mysql  в будущем нужно будет делать расчет при сохранении кампании. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L298">restart_time</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L299">soft_restart_time</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L301">restart_reason</a></b>  <i>int32</i>
<p> enum ERestartReason </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L305">has_money</a></b>  <i>bool</i>
<p> Сейчас денежные поля кампании, из которых можно рассчитать это поле, не реплицируются,  но оно нужно для расчета времени рестарта, поэтому пока хранится посчитанное тут.  Показывает наличие денег на кампании / кошельке с учетом автоовердрафта </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L308">stop_time</a></b>  <i>fixed32</i>
<p> Поле, нужное для расчета времени рестарта:  время последней остановки кампании пользователем или при отсутствии денег на кампании. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L450">placement_types</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L311">TPlacementTypes</a></i>
<p> Места показа (если не указано - значение по умолчанию - все). </p>

</li>
<details open><summary><b>Message TPlacementTypes</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L313">search_page</a></b>  <i>bool</i>
<p> Поиск. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L315">adv_gallery</a></b>  <i>bool</i>
<p> Товарная кампания. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L452">meaningful_goals</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L318">TMeaningfulGoal</a></i>
<p> Выбранные цели для оптимизации в BidCorrection. </p>

</li>
<details open><summary><b>Message TMeaningfulGoal</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L319">goal_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L323">is_metrika_source_of_value</a></b>  <i>bool</i>
<p> Признак для БК, что ценность конверсии надо брать из метрики. Для ДРР стратегий. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L328">conversion_value</a></b>  <i>uint64</i>
<p> Ценность конверсии.  Значения до второго знака после запятой, хранится умноженным на 10^6. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L456">money_params</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L333">TMoneyParams</a></i>
<p> Поля с деньгами кампаний и параметрами рассчетов с деньгами. </p>

</li>
<details open><summary><b>Message TMoneyParams</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L343">flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L334">TMoneyProcessingFlags</a></i>
</li>
<details open><summary><b>Message TMoneyProcessingFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L337">is_paid_by_certificate</a></b>  <i>bool</i>
<p> Аналог campaigns.paid_by_certificate.  Опличивается ли заказ по сертификату. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L340">is_wallet_sum_aggregated</a></b>  <i>bool</i>
<p> Аналог wallet_campaigns.is_sum_aggregated.  Перешли ли на "новую схему зачислений" (аггрегаты на кампаниях с типом billing_aggregates). </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L346">sum</a></b>  <i>uint64</i>
<p> Всего оплачено, в валюте кампании.  Значения до второго знака после запятой, хранится умноженным на 10^6. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L349">sum_spent</a></b>  <i>uint64</i>
<p> Потрачено на кампании, в валюте кампании.  Значения до второго знака после запятой, хранится умноженным на 10^6. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L356">day_budget</a></b>  <i>uint64</i>
<p> Текущая сумма дневного ограничения бюджета в валюте кампании.  Если day_budget == 0, дневное ограничение не задано.  Отличное от 0 значение может быть задано только для стратегий с самостоятельным управлением ставками.  Для мультивалютных: не включает в себя НДС.  Значения до второго знака после запятой, хранится умноженным на 10^6. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L458">internal_ad_options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L359">TInternalAdOptions</a></i>
<p> Поля для внутренних кампаний. </p>

</li>
<details open><summary><b>Message TInternalAdOptions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L362">rotation_goal_id</a></b>  <i>uint64</i>
<p> Цель оптимизации для дистрибуционных (internal_distrib) и автобюджетных (internal_autobudget) кампаний.  Храним число: либо ID цели в Метрике, либо специальное значение: 3 для мобильных заказов (is_mobile = Yes). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L366">restriction_type</a></b>  <i>uint32</i>
<p> ERestrictionType.  Единица измерения ограничения на заказ (restriction_value).  Заполняется только для internal_free. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L369">restriction_value</a></b>  <i>uint64</i>
<p> Значение ограничения на заказ (количество дней/кликов/показов).  Используется только для internal_free. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L372">rf_close_by_click</a></b>  <i>uint32</i>
<p> ERFCloseByClick.  Прекращение показов после клика. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L374">is_mobile</a></b>  <i>bool</i>
<p> Идентификатор мобильности "Yes"/"No". </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L460">rf_options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L7">TRfOptions</a></i>
<p> Ограничения по количествам определенных действий в период времени. </p>

</li>
<details open><summary><b>Message TRfOptions</b></summary>
<p> Ограничения на частоту событий. Хранит три типа событий: показы, клики, закрытия по крестику и период для каждого из типов. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L16">shows</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L9">TLimit</a></i>
<p> Показы. </p>

</li>
<details open><summary><b>Message TLimit</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L11">count</a></b>  <i>uint32</i>
<p> Максимальное количество событий в интервал времени. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L13">period</a></b>  <i>uint32</i>
<p> Интервал времени для количества событий (параметр выше) в секундах. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L18">clicks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L9">TLimit</a></i>
<p> Клики. </p>

</li>
<details open><summary><b>Message TLimit</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L11">count</a></b>  <i>uint32</i>
<p> Максимальное количество событий в интервал времени. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L13">period</a></b>  <i>uint32</i>
<p> Интервал времени для количества событий (параметр выше) в секундах. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L20">closes</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L9">TLimit</a></i>
<p> Нажатия на крестик. </p>

</li>
<details open><summary><b>Message TLimit</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L11">count</a></b>  <i>uint32</i>
<p> Максимальное количество событий в интервал времени. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L13">period</a></b>  <i>uint32</i>
<p> Интервал времени для количества событий (параметр выше) в секундах. </p>

</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L463">bid_modifiers_ids</a></b>  <i>uint64</i>
<p> Корректировки на кампании. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L470">forbidden_domains</a></b>  <i>string</i>
<p> Список доменов, на которых клиент не хочет показываться.  Аналог DontShow. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L472">additional_targeting_expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L16">TTargetingExpression</a></i>
<p> Ручные таргетинги через внутренний интерфейс. </p>

</li>
<details open><summary><b>Message TTargetingExpression</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L20">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L17">TDisjunction</a></i>
</li>
<details open><summary><b>Message TDisjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L18">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L23">TTargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TTargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L25">keyword</a></b>  <i>int32</i>
<p> See EKeyword at https://a.yandex-team.ru/arcadia/yabs/server/proto/keywords/keywords_data.proto. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L27">operation</a></b>  <i>int32</i>
<p> enum EYabsOperation </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L28">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L475">strategy_id</a></b>  <i>uint64</i>
<p> id стратегии на кампании.  Поле strategy выше должно будет замениться на это в результате переезда. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L479">auction_priority</a></b>  <i>int32</i>
<p> Приоритет кампании для cpm_price кампаний. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L484">impression_standard_type</a></b>  <i>int32</i>
<p> Порог определения видимости.  camp_options.impression_standard_time в mysql.  See enum EImpressionStandardType. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L489">phrase_quality_clustering</a></b>  <i>int32</i>
<p> Матчинг на самую точную фразу.  campaigns.opts.is_order_phrase_length_precedence_enabled в mysql.  See enum EPhraseQualityClustering. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L493">eshow_video_type</a></b>  <i>int32</i>
<p> Тип оптимизации для видео.  See enum EShowVideoType. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L496">meaningful_goals_hash</a></b>  <i>uint64</i>
<p> Временное вычислимое поле, чтобы сходилось со старым транспортом https://st.yandex-team.ru/GRUT-654. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L499">ab_segment_retargeting_condition_id</a></b>  <i>uint64</i>
<p> Идентификатор условия AB-сегмента для таргетирования. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L504">ab_segment_statistics_retargeting_condition_id</a></b>  <i>uint64</i>
<p> Идентификатор условия AB-сегмента для сбора статистики. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L510">allowed_domains</a></b>  <i>string</i>
<p> Список доменов, на которых разрешено показывать объявления кампании. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L513">widget_partner_id</a></b>  <i>uint64</i>
<p> Идентификатор партнёра для кампаний, созданных из виджета размещённого на сайте партнёра. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L516">tracking_params</a></b>  <i>string</i>
<p> Трекинговые параметры компании, которые приписывются к url (соответствует директовому camp_options.href_params). </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L518">skad_network</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L384">TSkAdNetwork</a></i>
</li>
<details open><summary><b>Message TSkAdNetwork</b></summary>
<p> Храним и slot и bundle_id на кампании, поскольку нужно иметь возможность искать занятые слоты по bundle_id. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L387">slot</a></b>  <i>int32</i>
<p> Выделенный слот для SkADNetwork на ios-приложение.  ios_skadnetwork_slots.slot в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L390">bundle_id</a></b>  <i>string</i>
<p> Bundle ID ios-приложения, для которого выделен SkADNetwork слот.  ios_skadnetwork_slots.bundle_id в mysql. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L522">forbidden_ssp</a></b>  <i>string</i>
<p> Список названий площадок, на которых запрещены показы.  campaigns.disabled_ssp в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L526">forbidden_video_placements</a></b>  <i>string</i>
<p> Площадки, на которых запрещен показ видео инвентаря (действительно только для охватных кампаний).  campaigns.disabled_video_placements в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L530">forbidden_ips</a></b>  <i>string</i>
<p> Список IP, которым не надо показывать объявления из этой кампании.  campaigns.disabledIps в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L535">frontpage_placements</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L377">TFrontPagePlacements</a></i>
<p> Показывать ли объявления кампании на месте размещения.  campaigns_cpm_yndx_frontpage.allowed_frontpage_types в mysql для cpm_yndx_frontpage.  campaigns_cpm_price.targetings_snapshot.view_types в mysql для cpm_price. </p>

</li>
<details open><summary><b>Message TFrontPagePlacements</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L378">frontpage</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L379">frontpage_mobile</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L380">browser_new_tab</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L539">brandsafety_retargeting_condition_id</a></b>  <i>uint64</i>
<p> Идентификатор условия с brandsafety категориями.  campaigns.brandsafety_ret_cond_id в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L546">allowed_page_ids</a></b>  <i>uint64</i>
<p> Список PageID площадок, на которых разрешено показывать объявления кампании.  camp_options.allowed_page_ids в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L550">forbidden_page_ids</a></b>  <i>uint64</i>
<p> Список PageID площадок, на которых запрещено показывать объявления кампании.  camp_options.disallowed_page_ids в mysql. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L553">mobile_app_id</a></b>  <i>uint64</i>
<p> Мобильное приложение, которое рекламирует эта кампания. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L557">package_id</a></b>  <i>uint64</i>
<p> Id пакета прайсовых продаж. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L563">brand_survey_id</a></b>  <i>string</i>
<p> ID опроса Я.Взгляда.  camp_options.brand_survey_id в mysql. </p>

</li>


</ul></details>
<li><b>status</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/campaign_v2.proto?rev=r9795881#L567">TCampaignV2Status</a></i>
</li>
<details open><summary><b>Message TCampaignV2Status</b></summary>
<p> Системные поля, для пользователя всегда доступы только в режиме для чтения. </p>

<ul>
<span>empty</span>

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
<li><b>control</b>  <i>TCampaignV2Control</i>
</li>
<details open><summary><b>Message TCampaignV2Control</b></summary>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L444">LastUpdateInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L386">TLastUpdateInfo</a></i>
</li>
<details open><summary><b>Message TLastUpdateInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L388">GrutSyncTimestamp</a></b>  <i>fixed32</i>
<p> The time of sync GrutObject. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L390">UpdateTimestamp</a></b>  <i>fixed32</i>
<p> The time of profile was updated. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L392">GrutObjectUpdateTimestamp</a></b>  <i>fixed32</i>
<p> The time of object update in GrUT </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L445">ComputedFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L396">TComputedFields</a></i>
</li>
<details open><summary><b>Message TComputedFields</b></summary>
<p> Derivative from GrutObject. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L403">ContentType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L15">EOrderContentType</a></i>
</li>
<details open><summary><b>Enum EOrderContentType</b></summary>
<ul>
<li><span style="color:#1D7373">OCT_UNKNOWN</span></li>
<li><span style="color:#1D7373">OCT_TEXT</span></li>
<li><span style="color:#1D7373">OCT_MCB</span></li>
<li><span style="color:#1D7373">OCT_GEO</span></li>
<li><span style="color:#1D7373">OCT_MARKET</span></li>
<li><span style="color:#1D7373">OCT_WALLET</span></li>
<li><span style="color:#1D7373">OCT_MOBILE_CONTENT</span></li>
<li><span style="color:#1D7373">OCT_PERFORMANCE</span></li>
<li><span style="color:#1D7373">OCT_DYNAMIC</span></li>
<li><span style="color:#1D7373">OCT_INTERNAL</span></li>
<li><span style="color:#1D7373">OCT_MCBANNER</span></li>
<li><span style="color:#1D7373">OCT_REACH</span></li>
<li><span style="color:#1D7373">OCT_INTERNAL_DISTRIB</span></li>
<li><span style="color:#1D7373">OCT_INTERNAL_FREE</span></li>
<li><span style="color:#1D7373">OCT_INTERNAL_AUTOBUDGET</span></li>
<li><span style="color:#1D7373">OCT_ZEN</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L404">StartTime</a></b>  <i>fixed32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L405">PlaceID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L406">EngineID</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L407">ClientFlags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L398">TClientFlags</a></i>
</li>
<details open><summary><b>Message TClientFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L399">IsFaviconBlocked</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L400">IsOverdraftBlocked</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L408">ClientNDSHistory</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L117">TNDSHistory</a></i>
</li>
<details open><summary><b>Message TNDSHistory</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L118">DateFrom</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L119">DateTo</a></b>  <i>uint64</i>
<p> actualy you need only DateFrom </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L120">NDS</a></b>  <i>int32</i>
<p> *1000000: nds=20% == 200000 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L409">DeprecatedShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L116">TShowConditions</a></i>
<p> deprecated and cleared. will be removed soon </p>

</li>
<details open><summary><b>Message TShowConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L117">Version</a></b>  <i>uint64</i>
<p> IterID in Direct </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L118">Timestamp</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L119">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L10">TargetingExpression</a></i>
</li>
<details open><summary><b>Message TargetingExpression</b></summary>
<p> Протобуф должен совпадать с https://a.yandex-team.ru/arcadia/grut/libs/proto/public/auxiliary/targeting_expression.proto  Протобуф из grut рекомендуемый, для новых задач этот не использовать. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L14">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L11">Disjunction</a></i>
</li>
<details open><summary><b>Message Disjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L12">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L17">TargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L18">keyword</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NKeywords.KeywordEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L19">operation</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NOperations.OperationEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L20">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L120">ContextID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L410">AutoBudgetInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L18">TAutoBudgetInfo</a></i>
</li>
<details open><summary><b>Message TAutoBudgetInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L32">Enabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L33">AutoBudgetAvgBid</a></b>  <i>double</i>
<p> old AutoBudgetAvgCost </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L34">AutoBudgetAvgBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L35">AutoBudgetAvgCPA</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L36">AutoBudgetAvgCPACur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L37">AutoBudgetAvgCPM</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L38">AutoBudgetAvgCPMCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L39">AutoBudgetAvgCPV</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L40">AutoBudgetAvgCPVCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L41">AutoBudgetDayLimitMoney</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L42">AutoBudgetDayLimitMoneyCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L43">AutoBudgetGoalExpression</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L44">AutoBudgetGoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L45">AutoBudgetMaxBid</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L46">AutoBudgetMaxBidCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L47">AutoBudgetMeaningfulGoalsValuesFromMetrika</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L48">AutoBudgetNetCPCOptimize</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L49">AutoBudgetOptimizeRF</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L50">AutoBudgetPaidActions</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L51">AutoBudgetPaidActionsPerFilter</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L52">AutoBudgetPaidCrr</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L53">AutoBudgetPaidMeaningfulGoalsHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L54">AutoBudgetPeriodBudgetFinish</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L55">AutoBudgetPeriodBudgetLimit</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L56">AutoBudgetPeriodBudgetLimitCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L57">AutoBudgetPeriodBudgetProlongation</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L58">AutoBudgetProfitability</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L59">AutoBudgetROILevel</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L60">AutoBudgetRegularSpent</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L61">AutoBudgetReserveReturn</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L62">AutoBudgetRestartReason</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L63">AutoBudgetRestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L64">AutoBudgetSoftRestartTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L65">AutoBudgetWeekLimit</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L66">AutoBudgetWeekLimitClicks</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L67">AutoBudgetWeekLimitCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L68">StrategyParams</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L19">TStrategyParams</a></i>
</li>
<details open><summary><b>Message TStrategyParams</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L22">Name</a></b>  <i>string</i>
<p> Name of AutoBudget Strategy. Possible values:  https://a.yandex-team.ru/arc/trunk/arcadia/direct/perl/db_schema/ppc/campaigns.schema.sql?blame=true#L32 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L23">StrategyID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L24">PrevStrategyID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L69">AutoBudgetPromotions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L26">TAutoBudgetPromotion</a></i>
<p> https://st.yandex-team.ru/BSDEV-84947 </p>

</li>
<details open><summary><b>Message TAutoBudgetPromotion</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L27">DateFrom</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L28">DateTo</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L29">ConversionBoostPercent</a></b>  <i>int32</i>
<p> multiply 1kk. 20% -> 200000 </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L72">AutoBudgetDayWeight</a></b>  <i>uint64</i>
<p> https://st.yandex-team.ru/BSSERVER-19090  Max part of budget per day. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L73">AutoBudgetMaxDayLimitMoney</a></b>  <i>double</i>
<p> Max(DayLimitMoney[StartTime]) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L74">AutoBudgetMaxDayLimitMoneyCur</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L77">AutoBudgetStrategy</a></b>  <i>string</i>
<p> DEPRICATED. Use StrategyParams.Name instead. </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L411">MetrikaCountersHash</a></b>  <i>uint64</i>
<p> https://st.yandex-team.ru/BSSERVER-19633 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L412">IsGroupOrder</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L413">IsExtendedRelevanceMatchEnabled</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L414">IsMarketRatingHidden</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L415">IsDisabledInSearch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L416">IsDisabledInRsya</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L417">ManagerUID</a></b>  <i>uint64</i>
<p> chief_uid from grut required for moderation </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L418">MinusPhrases</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L419">Multipliers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L14">Multiplier</a></i>
</li>
<details open><summary><b>Message Multiplier</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L15">condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L10">TargetingExpression</a></i>
</li>
<details open><summary><b>Message TargetingExpression</b></summary>
<p> Протобуф должен совпадать с https://a.yandex-team.ru/arcadia/grut/libs/proto/public/auxiliary/targeting_expression.proto  Протобуф из grut рекомендуемый, для новых задач этот не использовать. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L14">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L11">Disjunction</a></i>
</li>
<details open><summary><b>Message Disjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L12">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L17">TargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L18">keyword</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NKeywords.KeywordEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L19">operation</a></b>  <i>uint32</i>
<p> из NDirectAdv.NExpression.NOperations.OperationEnum </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L20">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L16">custom_condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L23">CustomExpression</a></i>
</li>
<details open><summary><b>Message CustomExpression</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L30">ExperimentSegment</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L24">SegmentKey</a></i>
</li>
<details open><summary><b>Message SegmentKey</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L25">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L26">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L31">InventoryType</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/inventory_types.proto?rev=r9795881#L6">InventoryTypeEnum</a></i>
</li>
<details open><summary><b>Enum InventoryTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">Undefined</span></li>
<li><span style="color:#1D7373">MediaCreativeBanner</span></li>
<li><span style="color:#1D7373">VideoInBanner</span></li>
<li><span style="color:#1D7373">VideoInPage</span></li>
<li><span style="color:#1D7373">VideoInStream</span></li>
<li><span style="color:#1D7373">VideoInApp</span></li>
<li><span style="color:#1D7373">VideoRewarded</span></li>
<li><span style="color:#1D7373">VideoPreroll</span></li>
<li><span style="color:#1D7373">VideoMidroll</span></li>
<li><span style="color:#1D7373">VideoPostroll</span></li>
<li><span style="color:#1D7373">VideoPauseroll</span></li>
<li><span style="color:#1D7373">VideoOverlay</span></li>
<li><span style="color:#1D7373">VideoPostrollOverlay</span></li>
<li><span style="color:#1D7373">VideoPostrollWrapper</span></li>
<li><span style="color:#1D7373">VideoInrollOverlay</span></li>
<li><span style="color:#1D7373">VideoInroll</span></li>
<li><span style="color:#1D7373">VideoInterstitial</span></li>
<li><span style="color:#1D7373">VideoFullscreen</span></li>
<li><span style="color:#1D7373">VideoDefault</span></li>
<li><span style="color:#1D7373">VideoPostPauseroll</span></li>
</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L32">PerformanceTgo</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L33">AutoVideoDirect</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions.proto?rev=r9795881#L34">TrafaretPosition</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L18">value</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L19">Type</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/multiplier_type.proto?rev=r9795881#L6">MultiplierTypeEnum</a></i>
</li>
<details open><summary><b>Enum MultiplierTypeEnum</b></summary>
<ul>
<li><span style="color:#1D7373">AutoVideoDirect</span></li>
<li><span style="color:#1D7373">InventoryType</span></li>
<li><span style="color:#1D7373">DeviceType</span></li>
<li><span style="color:#1D7373">Demography</span></li>
<li><span style="color:#1D7373">Retargeting</span></li>
<li><span style="color:#1D7373">Weather</span></li>
<li><span style="color:#1D7373">Geo</span></li>
<li><span style="color:#1D7373">TrafficJam</span></li>
<li><span style="color:#1D7373">AbSegment</span></li>
<li><span style="color:#1D7373">VideoContentDuration</span></li>
<li><span style="color:#1D7373">Time</span></li>
<li><span style="color:#1D7373">PerformanceTgo</span></li>
<li><span style="color:#1D7373">PrismaIncomeGrade</span></li>
<li><span style="color:#1D7373">SearchRetargeting</span></li>
<li><span style="color:#1D7373">TrafaretPosition</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L420">ShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L16">TTargetingExpression</a></i>
<p> CNF with keyword_id + operation + value </p>

</li>
<details open><summary><b>Message TTargetingExpression</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L20">and</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L17">TDisjunction</a></i>
</li>
<details open><summary><b>Message TDisjunction</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L18">or</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L23">TTargetingExpressionAtom</a></i>
</li>
<details open><summary><b>Message TTargetingExpressionAtom</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L25">keyword</a></b>  <i>int32</i>
<p> See EKeyword at https://a.yandex-team.ru/arcadia/yabs/server/proto/keywords/keywords_data.proto. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L27">operation</a></b>  <i>int32</i>
<p> enum EYabsOperation </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L28">value</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L421">ShowConditionsHash</a></b>  <i>uint64</i>
<p> technical field for yabs-server and debug. func(ShowConditions) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L422">BillingOrder</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L89">TBillingOrder</a></i>
<p> Campaign IDs to store billing aggregates to </p>

</li>
<details open><summary><b>Message TBillingOrder</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L96">Default</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L97">Rules</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L90">TRules</a></i>
</li>
<details open><summary><b>Message TRules</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L91">Result</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L92">ProductTypesBits</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L93">ProductId</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L98">ProductId</a></b>  <i>int32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L423">DistributionTagID</a></b>  <i>int64</i>
<p> Internal ads interface tag. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L424">RFMinCPM</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L425">RFDecay</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L426">Overdraft</a></b>  <i>int64</i>
<p> Overdraft amount in CurrencyID. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L427">MaxCostCurrency</a></b>  <i>int64</i>
<p> Total amount in CurrencyID. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L428">Description</a></b>  <i>string</i>
<p> Cleaned description with campaign id prepended. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L429">AllowedDomains</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L431">OrderType</a></b>  <i>int32</i>
<p> EOrderType  The type of order that affects the accounting of money in billing </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L432">CampaignNameLatin</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L433">AuctionPriority</a></b>  <i>int32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L434">ABExperiments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L101">TABExperiments</a></i>
</li>
<details open><summary><b>Message TABExperiments</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L111">CoefDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L112">TargetDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L113">InternalTargetDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L114">StatDimensions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L102">TDimension</a></i>
</li>
<details open><summary><b>Message TDimension</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L107">DimensionID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L108">Segments</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L109">CoefSegments</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L103">TCoefSegment</a></i>
</li>
<details open><summary><b>Message TCoefSegment</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L104">Coef</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/events/proto/order_resources.proto?rev=r9795881#L105">SegmentID</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/order.proto?rev=r9795881#L448">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
