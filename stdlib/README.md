# Stdlib

### Dark v1 stdlib

```text
!=(Any a, Any b) -> Bool
%(Int a, Int b) -> Int
&&(Bool a, Bool b) -> Bool
*(Int a, Int b) -> Int
+(Int a, Int b) -> Int
++(Str s1, Str s2) -> Str
-(Int a, Int b) -> Int
/(Float a, Float b) -> Float
<(Int a, Int b) -> Bool
<=(Int a, Int b) -> Bool
==(Any a, Any b) -> Bool
>(Int a, Int b) -> Bool
>=(Int a, Int b) -> Bool
^(Int base, Int exponent) -> Int
||(Bool a, Bool b) -> Bool

emit_v1(Any event, Str Name) -> Any
equals(Any a, Any b) -> Bool
notEquals(Any a, Any b) -> Bool
toString(Any v) -> Str

AWS::urlencode(Str str) -> Str
Bool::and(Bool a, Bool b) -> Bool
Bool::isNull(Any check) -> Bool
Bool::not(Bool b) -> Bool
Bool::or(Bool a, Bool b) -> Bool
Bool::xor(Bool a, Bool b) -> Bool
Bytes::base64Encode(Bytes bytes) -> Str
Bytes::hexEncode(Bytes bytes) -> Str
Bytes::length(Bytes bytes) -> Int
Crypto::md5(Bytes data) -> Bytes
Crypto::sha1hmac(Bytes key, Bytes data) -> Bytes
Crypto::sha256(Bytes data) -> Bytes
Crypto::sha256hmac(Bytes key, Bytes data) -> Bytes
Crypto::sha384(Bytes data) -> Bytes
DB::count(Datastore table) -> Int
DB::deleteAll_v1(Datastore table) -> Nothing
DB::delete_v1(Str key, Datastore table) -> Nothing
DB::generateKey() -> Str
DB::getAllWithKeys_v2(Datastore table) -> Dict
DB::getAll_v3(Datastore table) -> List
DB::getExisting(List keys, Datastore table) -> List
DB::getManyWithKeys_v1(List keys, Datastore table) -> Dict
DB::getMany_v3(List keys, Datastore table) -> Option
DB::get_v2(Str key, Datastore table) -> Option
DB::keys_v1(Datastore table) -> List
DB::queryCount(Datastore table, Block filter) -> Int
DB::queryExactFields(Dict spec, Datastore table) -> List
DB::queryExactFieldsWithKey(Dict spec, Datastore table) -> Dict
DB::queryOneWithExactFields(Dict spec, Datastore table) -> Option
DB::queryOneWithExactFieldsWithKey(Dict spec, Datastore table) -> Option
DB::queryOneWithKey_v3(Datastore table, Block filter) -> Option
DB::queryOne_v4(Datastore table, Block filter) -> Option
DB::queryWithKey_v3(Datastore table, Block filter) -> Dict
DB::query_v4(Datastore table, Block filter) -> List
DB::schemaFields_v1(Datastore table) -> List
DB::schema_v1(Datastore table) -> Dict
DB::set_v1(Dict val, Str key, Datastore table) -> Dict
Date::<(Date d1, Date d2) -> Bool
Date::<=(Date d1, Date d2) -> Bool
Date::>(Date d1, Date d2) -> Bool
Date::>=(Date d1, Date d2) -> Bool
Date::add(Date d, Int seconds) -> Date
Date::atStartOfDay(Date date) -> Date
Date::day(Date date) -> Int
Date::fromSeconds(Int seconds) -> Date
Date::greaterThan(Date d1, Date d2) -> Bool
Date::greaterThanOrEqualTo(Date d1, Date d2) -> Bool
Date::hour_v1(Date date) -> Int
Date::lessThan(Date d1, Date d2) -> Bool
Date::lessThanOrEqualTo(Date d1, Date d2) -> Bool
Date::minute(Date date) -> Int
Date::month(Date date) -> Int
Date::now() -> Date
Date::parse_v2(Str s) -> Result
Date::second(Date date) -> Int
Date::subtract(Date d, Int seconds) -> Date
Date::toSeconds(Date date) -> Int
Date::toString(Date date) -> Str
Date::toStringISO8601BasicDate(Date date) -> Str
Date::toStringISO8601BasicDateTime(Date date) -> Str
Date::today() -> Date
Date::weekday(Date date) -> Int
Date::year(Date date) -> Int
Dict::empty() -> Dict
Dict::filterMap(Dict dict, Block f) -> Dict
Dict::filter_v1(Dict dict, Block f) -> Dict
Dict::fromList(List entries) -> Option
Dict::fromListOverwritingDuplicates(List entries) -> Dict
Dict::get_v2(Dict dict, Str key) -> Option
Dict::isEmpty(Dict dict) -> Bool
Dict::keys(Dict dict) -> List
Dict::map(Dict dict, Block f) -> Dict
Dict::member(Dict dict, Str key) -> Bool
Dict::merge(Dict left, Dict right) -> Dict
Dict::remove(Dict dict, Str key) -> Dict
Dict::set(Dict dict, Str key, Any val) -> Dict
Dict::singleton(Str key, Any value) -> Dict
Dict::size(Dict dict) -> Int
Dict::toJSON(Dict dict) -> Str
Dict::toList(Dict dict) -> List
Dict::values(Dict dict) -> List
Float::absoluteValue(Float a) -> Float
Float::add(Float a, Float b) -> Float
Float::ceiling(Float a) -> Int
Float::clamp(Float value, Float limitA, Float limitB) -> Float
Float::divide(Float a, Float b) -> Float
Float::floor(Float a) -> Int
Float::greaterThan(Float a, Float b) -> Bool
Float::greaterThanOrEqualTo(Float a, Float b) -> Bool
Float::lessThan(Float a, Float b) -> Bool
Float::lessThanOrEqualTo(Float a, Float b) -> Bool
Float::max(Float a, Float b) -> Float
Float::min(Float a, Float b) -> Float
Float::multiply(Float a, Float b) -> Float
Float::negate(Float a) -> Float
Float::power(Float base, Float exponent) -> Float
Float::round(Float a) -> Int
Float::roundDown(Float a) -> Int
Float::roundTowardsZero(Float a) -> Int
Float::roundUp(Float a) -> Int
Float::sqrt(Float a) -> Float
Float::subtract(Float a, Float b) -> Float
Float::sum(List a) -> Float
Float::truncate(Float a) -> Int
Http::badRequest(Str error) -> Response
Http::forbidden() -> Response
Http::notFound() -> Response
Http::redirectTo(Str url) -> Response
Http::response(Any response, Int code) -> Response
Http::responseWithHeaders(Any response, Dict headers, Int code) -> Response
Http::responseWithHtml(Any response, Int code) -> Response
Http::responseWithJson(Any response, Int code) -> Response
Http::responseWithText(Any response, Int code) -> Response
Http::setCookie_v2(Str name, Str value, Dict params) -> Dict
Http::success(Any response) -> Response
Http::unauthorized() -> Response
HttpClient::basicAuth_v1(Str username, Str password) -> Dict
HttpClient::bearerToken_v1(Str token) -> Dict
HttpClient::delete_v5(Str uri, Dict query, Dict headers) -> Result
HttpClient::formContentType() -> Dict
HttpClient::get_v5(Str uri, Dict query, Dict headers) -> Result
HttpClient::head_v5(Str uri, Dict query, Dict headers) -> Result
HttpClient::htmlContentType() -> Dict
HttpClient::jsonContentType() -> Dict
HttpClient::options_v5(Str uri, Dict query, Dict headers) -> Result
HttpClient::patch_v5(Str uri, Any body, Dict query, Dict headers) -> Result
HttpClient::plainTextContentType() -> Dict
HttpClient::post_v5(Str uri, Any body, Dict query, Dict headers) -> Result
HttpClient::put_v5(Str uri, Any body, Dict query, Dict headers) -> Result
Int::absoluteValue(Int a) -> Int
Int::add(Int a, Int b) -> Int
Int::clamp(Int value, Int limitA, Int limitB) -> Int
Int::divide(Int a, Int b) -> Int
Int::greaterThan(Int a, Int b) -> Bool
Int::greaterThanOrEqualTo(Int a, Int b) -> Bool
Int::lessThan(Int a, Int b) -> Bool
Int::lessThanOrEqualTo(Int a, Int b) -> Bool
Int::max(Int a, Int b) -> Int
Int::min(Int a, Int b) -> Int
Int::mod(Int a, Int b) -> Int
Int::multiply(Int a, Int b) -> Int
Int::negate(Int a) -> Int
Int::power(Int base, Int exponent) -> Int
Int::random_v1(Int start, Int end) -> Int
Int::remainder(Int value, Int divisor) -> Result
Int::sqrt(Int a) -> Float
Int::subtract(Int a, Int b) -> Int
Int::sum(List a) -> Int
Int::toFloat(Int a) -> Float
JSON::parse_v1(Str json) -> Result
JWT::signAndEncodeWithHeaders_v1(Str pemPrivKey, Dict headers, Any payload) -> Result
JWT::signAndEncode_v1(Str pemPrivKey, Any payload) -> Result
JWT::verifyAndExtract_v1(Str pemPubKey, Str token) -> Result
List::append(List as, List bs) -> List
List::drop(List list, Int count) -> List
List::dropWhile(List list, Block f) -> List
List::empty() -> List
List::filterMap(List list, Block f) -> List
List::filter_v2(List list, Block f) -> List
List::findFirst_v2(List list, Block f) -> Option
List::flatten(List list) -> List
List::fold(List list, Any init, Block f) -> Any
List::getAt_v1(List list, Int index) -> Option
List::head_v2(List list) -> Option
List::indexedMap(List list, Block f) -> List
List::interleave(List as, List bs) -> List
List::interpose(List list, Any sep) -> List
List::isEmpty(List list) -> Bool
List::last_v2(List list) -> Option
List::length(List list) -> Int
List::map(List list, Block f) -> List
List::map2(List as, List bs, Block f) -> Option
List::map2shortest(List as, List bs, Block f) -> List
List::member(List list, Any val) -> Bool
List::push(List list, Any val) -> List
List::pushBack(List list, Any val) -> List
List::randomElement(List list) -> Option
List::range(Int lowest, Int highest) -> List
List::repeat(Int times, Any val) -> List
List::reverse(List list) -> List
List::singleton(Any val) -> List
List::sort(List list) -> List
List::sortBy(List list, Block f) -> List
List::sortByComparator(List list, Block f) -> Result
List::tail(List list) -> Option
List::take(List list, Int count) -> List
List::takeWhile(List list, Block f) -> List
List::uniqueBy(List list, Block f) -> List
List::unzip(List pairs) -> List
List::zip(List as, List bs) -> Option
List::zipShortest(List as, List bs) -> List
Math::acos(Float ratio) -> Option
Math::asin(Float ratio) -> Option
Math::atan(Float ratio) -> Float
Math::atan2(Float y, Float x) -> Float
Math::cos(Float angleInRadians) -> Float
Math::cosh(Float angleInRadians) -> Float
Math::degrees(Float angleInDegrees) -> Float
Math::pi() -> Float
Math::radians(Float angleInRadians) -> Float
Math::sin(Float angleInRadians) -> Float
Math::sinh(Float angleInRadians) -> Float
Math::tan(Float angleInRadians) -> Float
Math::tanh(Float angleInRadians) -> Float
Math::tau() -> Float
Math::turns(Float angleInTurns) -> Float
Option::andThen(Option option, Block f) -> Option
Option::map2(Option option1, Option option2, Block f) -> Option
Option::map_v1(Option option, Block f) -> Option
Option::withDefault(Option option, Any default) -> Any
Password::check(Password existingpwr, Str rawpw) -> Bool
Password::hash(Str pw) -> Password
Result::andThen_v1(Result result, Block f) -> Result
Result::fromOption_v1(Option option, Str error) -> Result
Result::map2(Result result1, Result result2, Block f) -> Result
Result::mapError_v1(Result result, Block f) -> Result
Result::map_v1(Result result, Block f) -> Result
Result::toOption_v1(Result result) -> Option
Result::withDefault(Result result, Any default) -> Any
StaticAssets::baseUrlFor(Str deploy_hash) -> Str
StaticAssets::baseUrlForLatest() -> Str
StaticAssets::fetchBytes(Str deploy_hash, Str file) -> Result
StaticAssets::fetchLatestBytes(Str file) -> Result
StaticAssets::fetchLatest_v1(Str file) -> Result
StaticAssets::fetch_v1(Str deploy_hash, Str file) -> Result
StaticAssets::serveLatest_v1(Str file) -> Result
StaticAssets::serve_v1(Str deploy_hash, Str file) -> Result
StaticAssets::urlFor(Str deploy_hash, Str file) -> Str
StaticAssets::urlForLatest(Str file) -> Str
String::append_v1(Str s1, Str s2) -> Str
String::base64Decode(Str s) -> Str
String::base64Encode(Str s) -> Str
String::contains(Str lookingIn, Str searchingFor) -> Bool
String::digest(Str s) -> Str
String::dropFirst(Str string, Int characterCount) -> Str
String::dropLast(Str string, Int characterCount) -> Str
String::endsWith(Str subject, Str suffix) -> Bool
String::first(Str string, Int characterCount) -> Str
String::foreach_v1(Str s, Block f) -> Str
String::fromChar_v1(Character c) -> Str
String::fromList_v1(List l) -> Str
String::htmlEscape(Str html) -> Str
String::isEmpty(Str s) -> Bool
String::join(List l, Str separator) -> Str
String::last(Str string, Int characterCount) -> Str
String::length_v1(Str s) -> Int
String::newline() -> Str
String::padEnd(Str string, Str padWith, Int goalLength) -> Str
String::padStart(Str string, Str padWith, Int goalLength) -> Str
String::prepend(Str s1, Str s2) -> Str
String::random_v2(Int length) -> Result
String::replaceAll(Str s, Str searchFor, Str replaceWith) -> Str
String::reverse(Str string) -> Str
String::slice(Str string, Int from, Int to) -> Str
String::slugify_v2(Str string) -> Str
String::split(Str s, Str separator) -> List
String::startsWith(Str subject, Str prefix) -> Bool
String::toBytes(Str str) -> Bytes
String::toFloat_v1(Str s) -> Result
String::toInt_v1(Str s) -> Result
String::toList_v1(Str s) -> List
String::toLowercase_v1(Str s) -> Str
String::toUUID_v1(Str uuid) -> Result
String::toUppercase_v1(Str s) -> Str
String::trim(Str str) -> Str
String::trimEnd(Str str) -> Str
String::trimStart(Str str) -> Str
Twilio::sendText_v1(Str accountSID, Str authToken, Str fromNumber, Str toNumber, Str body) -> Dict
Uuid::generate() -> UUID
X509::pemCertificatePublicKey(Str pemCert) -> Result

```

