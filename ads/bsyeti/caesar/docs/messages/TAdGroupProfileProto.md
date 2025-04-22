
## Message TAdGroupProfileProto
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L140">AdGroupID</a></b>  <i>uint64</i>
<p> == GroupExportID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L141">OrderID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L142">Phrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L39">TBiddableShowConditions</a></i>
</li>
<details open><summary><b>Message TBiddableShowConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L40">PhrasesList</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L19">TPhrase</a></i>
</li>
<details open><summary><b>Message TPhrase</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L20">IterID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L21">ContextType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L22">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L23">DirectPhraseID</a></b>  <i>uint64</i>
<p> PhraseExportID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L24">Cost</a></b>  <i>int32</i>
<p> bid on search in Order currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L25">FlatCost</a></b>  <i>int32</i>
<p> bid on rsya in Order currency </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L26">Suspended</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L27">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L28">DeleteTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L29">HrefParams</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/href_param.proto?rev=r9795881#L9">HrefParam</a></i>
</li>
<details open><summary><b>Message HrefParam</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/href_param.proto?rev=r9795881#L10">name</a></b>  <i>string</i>
<p> не отправляется в Директе, сейчас сюда записывается пустая строка </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/href_param.proto?rev=r9795881#L11">value</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/href_param.proto?rev=r9795881#L12">param_no</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L30">Text</a></b>  <i>string</i>
<p> Only for ContextType=1 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L31">Hits</a></b>  <i>uint32</i>
<p> Hits from direct, forecasted by wordstat.yandex.ru. ContextType=1 </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L32">AutoBudgetAvgCPC</a></b>  <i>int32</i>
<p> Only for smart (ContextType=8) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L33">AutoBudgetAvgCPA</a></b>  <i>int32</i>
<p> Only for smart (ContextType=8) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L34">OnlyOfferRetargeting</a></b>  <i>bool</i>
<p> Only for smart (ContextType=8) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L35">OnlyNewAuditory</a></b>  <i>bool</i>
<p> Only for smart (ContextType=11) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L36">RelevanceMatchData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L9">RelevanceMatchData</a></i>
<p> Only for Autotargeting (ContextType=11) </p>

</li>
<details open><summary><b>Message RelevanceMatchData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L20">relevance_match_categories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L11">RelevanceMatchCategory</a></i>
</li>
<details open><summary><b>Enum RelevanceMatchCategory</b></summary>
<ul>
<li><span style="color:#1D7373">Unknown</span></li>
<li><span style="color:#1D7373">ExactMark</span></li>
<li><span style="color:#1D7373">AlternativeMark</span></li>
<li><span style="color:#1D7373">CompetitorMark</span></li>
<li><span style="color:#1D7373">BroaderMark</span></li>
<li><span style="color:#1D7373">AccessoryMark</span></li>
</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L42">AutobudgetPhraseControlsList</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L5">TAutobudgetPhraseControls</a></i>
<p> List of bids and others autobudget fields  deprecated, empty now </p>

</li>
<details open><summary><b>Message TAutobudgetPhraseControls</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L6">IsSearch</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L7">ContextType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L8">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L9">AutobudgetExperimentID</a></b>  <i>uint64</i>
<p> fields above are "keys" </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L12">AutobudgetBid</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L13">AutobudgetStartTime</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L14">AutoBudgetControlMetaInfo</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L15">AutoBudgetControlModelVersion</a></b>  <i>int64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/yabs/autobudget/libs/bid_importer/proto/autobudget_ad_group_phrases_controls.proto?rev=r9795881#L16">AutoBudgetControlVersion</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L43">AutobudgetPhraseControlsTimestamp</a></b>  <i>uint64</i>
<p> deprecated, empty now </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L143">EmbeddedPhrases</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L68">TEmbeddedPhrases</a></i>
</li>
<details open><summary><b>Message TEmbeddedPhrases</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L70">PhraseEmbeddingsList</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L63">TPhraseEmbeddings</a></i>
</li>
<details open><summary><b>Message TPhraseEmbeddings</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L64">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L65">Embeddings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/embeddings.proto?rev=r9795881#L6">TEmbedding</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L144">Counters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L73">TCounters</a></i>
</li>
<details open><summary><b>Message TCounters</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L74">PackedCounters</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/libs/counter_lib/proto/message.proto?rev=r9795881#L21">TCounterPack</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L145">ShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L77">TShowConditions</a></i>
</li>
<details open><summary><b>Message TShowConditions</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L79">Expression</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/expression/expressions2.proto?rev=r9795881#L10">TargetingExpression</a></i>
<p> Joined showcondition expressions of every type </p>

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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L80">ContextID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L81">IsInternational</a></b>  <i>bool</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L146">CommonFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L84">TCommonFields</a></i>
</li>
<details open><summary><b>Message TCommonFields</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L85">Timestamp</a></b>  <i>uint64</i>
<p> iter_id </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L86">EngineID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L87">Type</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L88">InternalLevel</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L89">MinusPhrases</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L90">PageGroupTags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L91">RemoveMeTargetTags</a></b>  <i>string</i>
<p> TODO: remove after clear </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L92">UpdateTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L93">DeleteTime</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L94">MatchPriority</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L95">ClickUrlTail</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L96">Multipliers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L14">Multiplier</a></i>
<p> Allows adjust BIDs under some condition </p>

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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L98">ProductGalleryOnly</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L99">FrequencyShowsOptions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/rf_options.proto?rev=r9795881#L9">RfOptions</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L101">RelevanceMatchData</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L9">RelevanceMatchData</a></i>
<p> Only for dynamic (Type=2). Dynamics don't have relevanceMatch as show condition, so it's set for AdGroup unlike text groups </p>

</li>
<details open><summary><b>Message RelevanceMatchData</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L20">relevance_match_categories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/show_conditions/relevance_match_data.proto?rev=r9795881#L11">RelevanceMatchCategory</a></i>
</li>
<details open><summary><b>Enum RelevanceMatchCategory</b></summary>
<ul>
<li><span style="color:#1D7373">Unknown</span></li>
<li><span style="color:#1D7373">ExactMark</span></li>
<li><span style="color:#1D7373">AlternativeMark</span></li>
<li><span style="color:#1D7373">CompetitorMark</span></li>
<li><span style="color:#1D7373">BroaderMark</span></li>
<li><span style="color:#1D7373">AccessoryMark</span></li>
</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L102">SerpPlacementType</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L103">FeedFieldForTitle</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L104">FeedFieldForBody</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L105">FeedID</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L147">CatProfiles</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/cat_machine/proto/cat_machine.proto?rev=r9795881#L19">TCatEngineProfiles</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L148">GrutObject</a></b>  <i>TAdGroupV2</i>
</li>
<details open><summary><b>Message TAdGroupV2</b></summary>
<ul>
<li><b>meta</b>  <i>TAdGroupV2Meta</i>
</li>
<details open><summary><b>Message TAdGroupV2Meta</b></summary>
<ul>
<li><b>id</b>  <i>uint64</i>
</li>

<li><b>direct_type</b>  <i>int32</i>
</li>

<li><b>uuid</b>  <i>string</i>
</li>

<li><b>name</b>  <i>string</i>
</li>

<li><b>campaign_id</b>  <i>uint64</i>
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
<li><b>spec</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L21">TAdGroupV2Spec</a></i>
</li>
<details open><summary><b>Message TAdGroupV2Spec</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L80">name</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L83">regions_ids</a></b>  <i>int64</i>
<p> Идентификаторы регионов показа. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L86">minus_phrases_ids</a></b>  <i>uint64</i>
<p> Идентификаторы простых и библиотечных минус фраз группы. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L93">page_group_tags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L94">target_tags</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L96">rf_options</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/rf_options.proto?rev=r9795881#L7">TRfOptions</a></i>
<p> RF атрибуты внутренней рекламы. </p>

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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L97">internal_level</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L99">relevance_match</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L22">TRelevanceMatch</a></i>
</li>
<details open><summary><b>Message TRelevanceMatch</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L24">categories</a></b>  <i>int32</i>
<p> enum ERelevanceMatchCategory </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L104">additional_targetings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L9">TAdGroupAdditionalTargeting</a></i>
</li>
<details open><summary><b>Message TAdGroupAdditionalTargeting</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L239">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L242">targeting_type</a></b>  <i>int32</i>
<p> enum ETargetingType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L245">targeting_mode</a></b>  <i>int32</i>
<p> enum ETargetingMode </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L248">join_type</a></b>  <i>int32</i>
<p> enum EValueJoinType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L251">ints</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L164">TIntList</a></i>
</li>
<details open><summary><b>Message TIntList</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L165">values</a></b>  <i>int64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L252">strings</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L168">TStringList</a></i>
</li>
<details open><summary><b>Message TStringList</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L169">values</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L253">versioned_entries</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L191">TVersionedEntries</a></i>
</li>
<details open><summary><b>Message TVersionedEntries</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L192">values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L185">TVersionedEntry</a></i>
</li>
<details open><summary><b>Message TVersionedEntry</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L186">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L187">min_version</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L188">max_version</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L254">installed_apps</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L200">TMobileApps</a></i>
</li>
<details open><summary><b>Message TMobileApps</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L201">values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L195">TMobileApp</a></i>
</li>
<details open><summary><b>Message TMobileApp</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L196">store_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L197">mobile_content_id</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L255">interface_languages</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L234">TInterfaceLanguagesList</a></i>
</li>
<details open><summary><b>Message TInterfaceLanguagesList</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L236">values</a></b>  <i>int32</i>
<p> enum EInterfaceLanguage </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L256">dates</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L172">TDateList</a></i>
</li>
<details open><summary><b>Message TDateList</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L173">values</a></b>  <i>fixed32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L257">content_categories</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L181">TContentCategoryList</a></i>
</li>
<details open><summary><b>Message TContentCategoryList</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L182">values</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L176">TContentCategory</a></i>
</li>
<details open><summary><b>Message TContentCategory</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L177">goal_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_additional_targeting.proto?rev=r9795881#L178">goal_type</a></b>  <i>int32</i>
<p>ERetargetingGoalType enum </p>

</li>


</ul></details>

</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L107">page_blocks</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L27">TPageBlock</a></i>
</li>
<details open><summary><b>Message TPageBlock</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L28">block_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L29">page_id</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L111">mobile_content_id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L117">mobile_content_details</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L32">TMobileContentDetails</a></i>
</li>
<details open><summary><b>Message TMobileContentDetails</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L55">store_url</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L58">device_types</a></b>  <i>int32</i>
<p> enum EDeviceType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L61">network_types</a></b>  <i>int32</i>
<p> enum ENetworkType </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L63">min_os_version</a></b>  <i>string</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L119">match_priority</a></b>  <i>uint32</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L121">tracking_params</a></b>  <i>string</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L124">biddable_show_conditions_ids</a></b>  <i>uint64</i>
<p> Идентификаторы biddable_show_conditions. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L130">bid_modifiers_ids</a></b>  <i>uint64</i>
<p> Идентификаторы корректировок группы. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L138">status_shows_forecast</a></b>  <i>uint32</i>
<p> EStatusShowsForecast </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L141">start_time</a></b>  <i>fixed32</i>
<p> Время начала показов для внутренней рекламы. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L143">finish_time</a></b>  <i>fixed32</i>
<p> Время конца показов для внутренней рекламы. </p>

</li>


</ul></details>
<li><b>status</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/ad_group_v2.proto?rev=r9795881#L146">TAdGroupV2Status</a></i>
</li>
<details open><summary><b>Message TAdGroupV2Status</b></summary>
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
<li><b>control</b>  <i>TAdGroupV2Control</i>
</li>
<details open><summary><b>Message TAdGroupV2Control</b></summary>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L149">Flags</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L108">TFlags</a></i>
</li>
<details open><summary><b>Message TFlags</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L110">RemovalTimestamp</a></b>  <i>fixed32</i>
<p> The time when object was removed from GrUT. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L112">GrutVersion</a></b>  <i>uint64</i>
<p> Grut Object Version. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L113">SmartParentBanner</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L42">TVersionedBool</a></i>
</li>
<details open><summary><b>Message TVersionedBool</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L43">Value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L44">Version</a></b>  <i>uint64</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L114">DynamicParentBanner</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L42">TVersionedBool</a></i>
</li>
<details open><summary><b>Message TVersionedBool</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L43">Value</a></b>  <i>bool</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/common.proto?rev=r9795881#L44">Version</a></b>  <i>uint64</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L150">LastUpdateInfo</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L117">TLastUpdateInfo</a></i>
</li>
<details open><summary><b>Message TLastUpdateInfo</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L119">GrutSyncTimestamp</a></b>  <i>fixed32</i>
<p> The time of sync GrutObject. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L121">GrutObjectUpdateTimestamp</a></b>  <i>fixed32</i>
<p> The time of object update in GrUT </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L151">ComputedFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L131">TComputedFields</a></i>
</li>
<details open><summary><b>Message TComputedFields</b></summary>
<p> Derivative from GrutObject. </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L132">FullPageGroupTags</a></b>  <i>string</i>
<p> grut has user PageGroupTags. Here technical tags added </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L133">MinusPhrases</a></b>  <i>string</i>
<p> mapping from grut minus_phrases_ID </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L134">ShowConditions</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/public/auxiliary/targeting_expression.proto?rev=r9795881#L16">TTargetingExpression</a></i>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L135">ShowConditionsHash</a></b>  <i>uint64</i>
<p> technical field for yabs-server and debug. func(ShowConditions) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L136">BiddableShowConditionWithPhraseIDs</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L124">TBiddableShowConditionWithPhraseID</a></i>
<p> Phrases </p>

</li>
<details open><summary><b>Message TBiddableShowConditionWithPhraseID</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L125">BiddableShowCondition</a></b>  <i>TBiddableShowCondition</i>
</li>
<details open><summary><b>Message TBiddableShowCondition</b></summary>
<ul>
<li><b>meta</b>  <i>TBiddableShowConditionMeta</i>
</li>
<details open><summary><b>Message TBiddableShowConditionMeta</b></summary>
<ul>
<li><b>id</b>  <i>uint64</i>
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
<li><b>spec</b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L14">TBiddableShowConditionSpec</a></i>
</li>
<details open><summary><b>Message TBiddableShowConditionSpec</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L128">keyword</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L17">TKeyword</a></i>
<p> Ключевые слова и рубрики каталога </p>

</li>
<details open><summary><b>Message TKeyword</b></summary>
<p> Ключевые слова и рубрики каталога, аналог таблицы bids в Директе:  https://direct-dev.yandex-team.ru/db/ppc/tables/bids.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L19">price</a></b>  <i>uint64</i>
<p> Ставка пользователя по данной фразе на поиске для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L21">price_context</a></b>  <i>uint64</i>
<p> ставка в РСЯ (если 0 - вычисляется по ставке на поиске) для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L23">phrase</a></b>  <i>string</i>
<p> Текст фразы (или номер рубрики каталога) </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L25">shows_forecast</a></b>  <i>uint64</i>
<p> Количество показов фразы по таргетингу баннера, полученное из ADVQ может быть неправильным, если phrases.statusShowsForecast != 'Processed' </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L27">is_suspended</a></b>  <i>bool</i>
<p> Флаг приостановленности фразы пользователем(1|0). 0 - фраза активная 1 - фраза приостановлена пользователем. </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L31">href_param_1</a></b>  <i>string</i>
<p> Два последующих поля аналог таблицы bids_href_params в Директе:  https://direct-dev.yandex-team.ru/db/ppc/tables/bids_href_params.html  Первый параметр, заданный пользователем для фразы </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L33">href_param_2</a></b>  <i>string</i>
<p> Второй параметр для фразы </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L130">dynamic</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L66">TDynamic</a></i>
<p> Нацеливания для динамических групп </p>

</li>
<details open><summary><b>Message TDynamic</b></summary>
<p> Нацеливания для динамических групп (условие нацеливания + ставки + флажок приостановки)  Аналог таблицы bids_dynamic в Директе:  https://direct-dev.yandex-team.ru/db/ppc/tables/bids_dynamic.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L74">price</a></b>  <i>uint64</i>
<p> Цена на поиске в валюте кампании для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L77">price_context</a></b>  <i>uint64</i>
<p> Цена в РСЯ в валюте кампании для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L79">is_suspended</a></b>  <i>bool</i>
<p> Приостановлено пользователем </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L86">condition</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L67">TDynamicCondition</a></i>
<p> Условия нацеливания для динамических баннеров. Данные в этой таблице неизменяемы (за исключением condition_name), возможно только добавление новых.  Direct: https://direct-dev.yandex-team.ru/db/ppc/tables/dynamic_conditions.html </p>

</li>
<details open><summary><b>Message TDynamicCondition</b></summary>
<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L68">id</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L70">name</a></b>  <i>string</i>
</li>


</ul></details>

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L132">performance</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L38">TPerformance</a></i>
<p> Фильтры смарт кампаний </p>

</li>
<details open><summary><b>Message TPerformance</b></summary>
<p> Фильтры смарт кампаний, аналог таблицы bids_performance в Директе:  https://direct-dev.yandex-team.ru/db/ppc/tables/bids_performance.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L54">price_cpc</a></b>  <i>uint64</i>
<p> Цена за клик при оптимизации по CPC в валюте кампании для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L56">price_cpa</a></b>  <i>uint64</i>
<p> Цена за действие при оптимизации CPA в валюте кампании для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L58">name</a></b>  <i>string</i>
<p> Название фильтра </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L60">target_funnel</a></b>  <i>int32</i>
<p> enum ETargetFunnel </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L134">retargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L90">TRetargeting</a></i>
<p> Условия ретаргетинга </p>

</li>
<details open><summary><b>Message TRetargeting</b></summary>
<p> Условия ретаргетинга на баннере  Direct: https://direct-dev.yandex-team.ru/db/ppc/tables/bids_retargeting.html </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L92">price_context</a></b>  <i>uint64</i>
<p> Цена в РСЯ в валюте кампании для валютных: без НДС </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L136">offer_retargeting</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L121">TOfferRetargeting</a></i>
<p> Ретаргетинг по просмотренным товарам </p>

</li>
<details open><summary><b>Message TOfferRetargeting</b></summary>
<p> Ретаргетинг по просмотренным товарам  Direct: таблица bids base с типом "offer_retargeting"  В данный момент этот тип таргетинга в разработке в Директе  Может быть 1 запись на группу </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L123">is_suspended</a></b>  <i>bool</i>
<p> Условие показа отключено </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L138">relevance_match</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L99">TRelevanceMatch</a></i>
<p> Бесфразный таргетинг </p>

</li>
<details open><summary><b>Message TRelevanceMatch</b></summary>
<p> Бесфразный таргетинг  Direct: таблица bids base с типом "relevance_match"  https://direct-dev.yandex-team.ru/db/ppc/tables/bids_base.html  всегда 1 запись на группу </p>

<ul>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L101">price</a></b>  <i>uint64</i>
<p> Ставка пользователя на данное условие показа на поиске для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L103">price_context</a></b>  <i>uint64</i>
<p> Cтавка в РСЯ (если 0 - вычисляется по ставке на поиске) для валютных: без НДС </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L105">autobudget_priority</a></b>  <i>uint32</i>
<p> Если включён автобюджет - приоритет выставленный для данного условия показа </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L107">is_suspended</a></b>  <i>bool</i>
<p> Условие показа отключено </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L109">categories</a></b>  <i>int32</i>
<p> enum ERelevanceMatchCategory категории автотаргетинга </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L112">href_param_1</a></b>  <i>string</i>
<p> Direct: https://direct-dev.yandex-team.ru/db/ppc/tables/bids_href_params.html  первый параметр, заданный пользователем для фразы </p>

</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L114">href_param_2</a></b>  <i>string</i>
<p> второй параметр, заданный пользователем для фразы </p>

</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/grut/libs/proto/objects/biddable_show_condition.proto?rev=r9795881#L143">retargeting_condition_id</a></b>  <i>uint64</i>
<p> id на retargeting_condition (пока не используем эту таблицу); заполняется только для BidsRetargeting.  Вынес на верхний уровень, чтобы сделать fk constraint, пока не готов https://st.yandex-team.ru/YTORM-116 </p>

</li>


</ul></details>
<li><b>status</b>  <i>TBiddableShowConditionStatus</i>
</li>
<details open><summary><b>Message TBiddableShowConditionStatus</b></summary>
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
<li><b>control</b>  <i>TBiddableShowConditionControl</i>
</li>
<details open><summary><b>Message TBiddableShowConditionControl</b></summary>
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
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L126">PhraseID</a></b>  <i>uint64</i>
</li>

<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L127">ContextType</a></b>  <i>uint32</i>
</li>


</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L137">BidModifiers</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/adv/direct/proto/multipliers/multiplier.proto?rev=r9795881#L14">Multiplier</a></i>
<p> CNF with keyword_id + operation + value + modifier </p>

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

</ul></details>
<li><b><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/caesar/libs/profiles/proto/ad_group.proto?rev=r9795881#L154">ServiceFields</a></b>  <i><a href="https://a.yandex-team.ru/arc_vcs/ads/bsyeti/big_rt/lib/serializable_profile/proto/options.proto?rev=r9795881#L22">TServiceFields</a></i>
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
