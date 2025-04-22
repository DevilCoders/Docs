# prices_parser

## Usage

```c++
#pragma once

#include "prices_parser.h"

namespace maps::goods::prices_parser::example {

void processPrice(Price&& price) {
    // ...
}

void processError(ParseError&& error) {
    // ...
}

void usage(std::istream& in, PricelistFileType pricelistFileType) try {
    PricesParserPtr parseResult = parsePricesFromStream(in, pricelistFileType);
    while (parseResult->hasNextPrice()) try {
        auto priceOrError = parseResult->getNextPrice();
        if (std::holds_alternative<Price>(priceOrError)) {
            processPrice(std::move(priceOrError));
        } else {
            processError(std::move(priceOrError));
        }
    }
} catch (const WrongFileFormatException& e) {
    // ...
} catch (...) {
    // ...
}

} // namespace maps::goods::prices_parser::example
```
