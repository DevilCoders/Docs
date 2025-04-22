## Description

It is a small library that can simplify your life with YT.

### Serialization
It's possible to easy serialize ```mrc/lib/db``` objects to table on YT. We use object's introspections, so there is no any need to change code if object's schema is changed. Moreover creted table has the corresponding names of the columns.

```
#include <maps/wikimap/mapspro/services/mrc/libs/db/include/feature_gateway.h>
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/io.h>

const TString table = "//tmp/features";
NYT::IClientPtr client = mrcConfig.externals().yt().makeClient();

db::Features features {...};

yt::saveToTable(*client, table, features);
features = yt::loadFromTable<db::Features>(*client, table);
```

Also you may use serialization/deserialization in your own code. For many common types serialization is already defined (e.g. geolib3::Point2, boost::optional etc).

```
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/common.h>
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/serialize.h>

void Worker::Do(Reader* reader, Writer* writer)
{
    for (; reader->IsValid(); reader->Next()) {
        auto sign = yt::deserialize<db::Sign>(reader->GetRow());

        // Your processing...

        writer->AddRow(yt::serialize(sign));
    }
}
```

if you need to serialize your own class, just add introspection to you type (for base types specialization of serialization is preferred). Full table serialization also works fine.

```
struct Object {
    int64_t number;
    std::string text;

    template<class T>
    static auto introspect(T& t) { return std::tie(t.number, t.text); }

    static constexpr auto columns() { return std::make_tuple("number", "text"); }
};
```

### Schema
For all serializable objects you can automatically infer schema and use it during IO.

```
#include <maps/wikimap/mapspro/services/mrc/libs/db/include/feature_gateway.h>
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/schema.h>
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/io.h>

NYT::IClientPtr client = mrcConfig.externals().yt().makeClient();

db::Features features {...};

const auto table = NYT:TRichYPath(""//tmp/features")
    .Schema(getSchemaOf<db::Feature>());

yt::saveToTable(*client, table, features);
```

### Image uploading
Often it is necessary to proccess a massive set of features. So, you may upload images from MDS to yt table with just two line of code! Sometimes upload of some images are failed. Operation is not aborted and stored in table image is empty.

```
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/operation.h>

const TString table = "//tmp/features";
NYT::IClientPtr client = mrcConfig.externals().yt().makeClient();

const db::Features features {...};

// Create table with full feature desciption
yt::saveToTable(*client, table, features); description

// Upload images from mds (jpeg file is represented as string).
yt::uploadFeatureImage(mrcConfig, *client, table, table);
```

If you want to run the map-reduce operation, just create upload mapper. Pay attention, raw pointer returned (usually ownership is transferred to yt code).
```
const Mapper* upload = makeUploadFeatureImageMapper<db::Feature>();
```

For deserialization you may use FeatureWithImage template type.
```
#include <maps/wikimap/mapspro/services/mrc/libs/yt/include/serialize.h>

using FeatureWithImage = yt::FeatureWithImage<db::Feature>;

using Reader = NYT::TTableReader<NYT::TNode>;
using Writer = NYT::TTableWriter<NYT::TNode>;

void Worker::Do(Reader* reader, Writer* writer) {
    for (; reader->IsValid(); reader->Next()) {
        const auto feature = yt::deserialize<FeatureWithImage>(reader->GetRow());

        if (feature.image.empty()) {
            // If image upload is failed, empty matrix is stored.
        }
    }
}
```
