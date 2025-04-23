Обертка для MapReduce операций.  
Имеет схожий с `NYT::IMapper` / `NYT::IReducer` интерфейс.
Позволяет выполнять MapReduce операции как в YT, так и локально без участия YT.  
Может быть использована для локальной отладки MapReduce операций или для ускорения выполнения операций с небольшим объемом входных данных.


Пример маппера/редьюсера:
```
class LineMergeReducer : public JobBase {
public:
    void DoImpl(TReader* reader, TWriter* writer) final
    {
        std::vector<GeometryHolder> geoms;

        for (; reader->IsValid(); reader->Next()) {
            geoms.push_back(
                readEwkbGeometry(reader->GetRow().ChildAsString("geom")));
        }

        geoms = mergeLines(geoms);

        for (auto& geom : geoms) {
            writer->AddRow(
                NYT::TNode()("geom", writeEwkbGeometry(*geom)));
        }
    }
};
REGISTER_TILEMILL_MAPREDUCE_JOB(LineMergeReducer);
```

Пример локального запуска:
```
    runLocal(
        MakeIntrusive<LineMergeReducer>(),
        createReader(MakeHolder<TFileInput>(inputFileName)).Get(),
        createWriter(MakeHolder<TFileOutput>(outputFileName)).Get(),
        groupByAttributes,
        {.numThreads = 0});

    auto client = NYT::CreateClientFromEnv();
    runLocal(
        MakeIntrusive<LineMergeReducer>(),
        client->CreateTableReader<NYT::TNode>("//tmp/input_table").Get(),
        client->CreateTableWriter<NYT::TNode>("//tmp/output_table").Get(),
        groupByAttributes,
        {.numThreads = 8, .maxReaderQueueBatches = 512, .maxWriterQueueBatches = 512});
```

Пример запуска в YT:
```
    runInYt(
        MakeIntrusive<LineMergeReducer>(),
        NYT::CreateClientFromEnv(),
        NYT::TRichYPath{"//tmp/input_table"},
        NYT::TRichYPath{"//tmp/output_table"},
        groupByAttributes,
        YtParams{.memoryLimitPerJob = 2 * GB});
```
Где `groupByAttributes` могут быть как списком атрибутов `{"ft_type_id", "network"}` так и пустыми `{}`.
