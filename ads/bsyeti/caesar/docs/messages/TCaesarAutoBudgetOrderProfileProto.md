
## Message TCaesarAutoBudgetOrderProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L10">OrderID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L12">AvgCPA</a></b>  <i>int64</i>
<p>optional int64 AuctionProbability = 2 [(NBigRT.FieldName) = "AuctionProbability", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L13">AvgCPACur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L14">AvgCPM</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L15">AvgCPMCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L16">AvgCPV</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L17">AvgCPVCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L18">AvgCost</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L19">AvgCostCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L23">ContextLimit</a></b>  <i>int64</i>
<p>optional int64 BidCoef = 11 [(NBigRT.FieldName) = "BidCoef", (NBigRT.FieldType) = PFT_SIMPLE]; optional string ChosenStrategy = 12 [(NBigRT.FieldName) = "ChosenStrategy", (NBigRT.FieldType) = PFT_SIMPLE]; optional uint64 ChosenStrategyAsInt = 13 [(NBigRT.FieldName) = "ChosenStrategyAsInt", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L24">DayWeight</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L28">GoalExpression</a></b>  <i>string</i>
<p>optional int64 Easy = 16 [(NBigRT.FieldName) = "Easy", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 FirstStartTime = 17 [(NBigRT.FieldName) = "FirstStartTime", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 GenerateBids = 18 [(NBigRT.FieldName) = "GenerateBids", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L29">GoalID</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L30">LastUpdateTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L31">LimitDayMoney</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L32">LimitDayMoneyCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L33">LimitWeek</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L34">LimitWeekClicks</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L35">LimitWeekCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L38">MaxCost</a></b>  <i>int64</i>
<p>optional int64 MaxCPM = 27 [(NBigRT.FieldName) = "MaxCPM", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 MaxCPMCur = 28 [(NBigRT.FieldName) = "MaxCPMCur", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L39">MaxCostCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L40">MaxLimitDayMoney</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L41">MaxLimitDayMoneyCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L42">ModifyTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L43">OptimizeType</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L44">Options</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L45">OptionsAdjustBidCoef</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L46">OptionsCrm</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L47">OptionsDiscretePaidActions</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L48">OptionsDynamicDailyBudget</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L49">OptionsMeaningfulGoalsValuesFromMetrika</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L50">OptionsNetcpcoptimize</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L51">OptionsPaidActions</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L52">OptionsPaidActionsPerFilter</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L53">OptionsPaidCrr</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L54">OptionsPeriodBudgetProlongation</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L55">OptionsPostbackCrm</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L56">OptionsYaMoneyOfferConv</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L57">PaidMeaningfulGoalsHash</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L58">PeriodBudgetFinish</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L59">PeriodBudgetLimit</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L60">PeriodBudgetLimitCur</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L62">Profitability</a></b>  <i>int64</i>
<p>optional int64 Problems = 51 [(NBigRT.FieldName) = "Problems", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L63">ROILevel</a></b>  <i>double</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L64">RegularSpent</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L65">ReserveReturn</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L66">StartTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L68">StrategyName</a></b>  <i>string</i>
<p>optional int64 StopDays = 57 [(NBigRT.FieldName) = "StopDays", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L73">RestartReason</a></b>  <i>string</i>
<p>optional int64 Testing = 59 [(NBigRT.FieldName) = "Testing", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 TransportDelayed = 60 [(NBigRT.FieldName) = "TransportDelayed", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 Type = 61 [(NBigRT.FieldName) = "Type", (NBigRT.FieldType) = PFT_SIMPLE]; optional int64 WeekStartTime = 62 [(NBigRT.FieldName) = "WeekStartTime", (NBigRT.FieldType) = PFT_SIMPLE]; </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L74">StrategyID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/caesar_autobudget_order.proto?rev=r9795881#L76">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
