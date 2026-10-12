<a name="v0.44.0"></a>
## [v0.44.0](https://hsau.yx-sf.com/yingxiao/ebook-22474157.html) (2026-07-10)

### Add

* Add back assets/test.pdf

### Feat

* Support incremental save of encrypted documents (#522)
* Bound text extraction against decompression bombs
* Bound load-time decompression via LoadOptions.max_decompressed_size
* Bound stream decompression to guard against bombs
* Make ttf-parser optional behind font_embedding feature

### Fix

* Reject incremental save of encrypted documents (#521)
* Fix Document::get_toc() dropping entries when outline titles repeat (#517)
* Add feature flag to font test
* Only use criterion for non-wasm tests/benches

### Move

* Move resource files in tests to assets

### Refactor

* Make `Document::get_page_content` return `Vec<u8>` since it cannot fail

### Test

* Add tests demonstrating unbounded stream decompression

### CI

* CI skip performance test
* Actually pass --no-default-features in the no-default-features matrix cell (#510)

<a name="v0.43.0"></a>
## [v0.43.0](https://aevt.yx-sf.com/fenxi/online-78679242.html) (2026-06-25)

### Feat

* Report encryption status in PdfMetadata


<a name="v0.42.0"></a>
## [v0.42.0](https://hdds.tcti.cn/yingyong/security-21822411.html) (2026-06-23)

### Feat

* Add Content::decode_strict method for strict parsing

### Fix

* Limit array and dictionary nesting depth
* Include subsequent ObjStm objects in xref stream range
* Insert newline between concatenated content streams
* Consume trailing comments in content streams

### Test

* Escape trailing whitespace in parser tests


<a name="v0.41.0"></a>
## [v0.41.0](https://euib.wtpuscm.cn/gongju/interface-018347.html) (2026-06-04)

### Add

* Add test to reproduce bug with replacing text in non-single character TJ Arrays
* Add regression test PDF file
* Add performance tests for document loading and page counting

### Fix

* Fix bug replacing text in non-single character TJ Arrays
* fix clippy errors

### Implement

* Implement differences mapping

### Release

* Release 0.41

### Removes

* Removes `nom_locate` dependency to fix a performance regression introduced in v0.35.0.


<a name="v0.40.0"></a>
## [v0.40.0](https://gmfs.yx-sf.com/yunsuan/cheap-01586377.html) (2026-03-19)

### Fix

* Fix a few warnings.
* Fix WinAnsiEncoding handling in SimpleEncoding string conversion

### Release

* Release 0.40

### Remove

* Remove an unused dependency.

### Return

* return Option via ok() instead of unwrap() for decode_text_string

### Update

* update src/reader to make clippy happy

### Update

* Update `getrandom` to 0.4 and `rand` to 0.10.

### Upgrade

* Upgrade `wasm-bindgen-test` while we're at it.


<a name="v0.39.0"></a>
## [v0.39.0](https://dbjj.wtpuscm.cn/wendang/conference-688013.html) (2026-01-16)

### Add

* add tests

### Fix

* fix conditionally compile encrypted metadata tests
* fix test_metadata and clippy warnings
* fix readme example ci issue
* fix clippy ci failed

### Release

* Release 0.39

### Breaking change


is_encrypted() now returns false after successful
decryption. Use was_encrypted() to check original encryption state.


<a name="v0.38.0"></a>
## [v0.38.0](https://cdjj.wtpuscm.cn/pingce/kpi-185952.html) (2026-01-16)

### Apply

* apply fix the warnings

### Inline

* Inline ImageMasks don't need to have a ColorSpace so don't require one.


<a name="v0.37.0"></a>
## [v0.37.0](https://euib.wtpuscm.cn/gongju/interface-018347.html) (2026-01-16)

### Add

* add unicode replace support ([#421](https://shnv.tcti.cn/guanjianci/health-35427712.html))

### Avoid

* Avoid unwrapping object streams when decrypting documents

### Change

* Change remove_object() to only remove the object ([#423](https://aevt.yx-sf.com/fenxi/online-78679242.html))

### Ensure

* Ensure we only encrypt with compliant P-values

### Fix

* fix bug ([#422](https://lwod.yx-sf.com/yanjiu/deadline-28191946.html))

### Fix

* Fix clippy
* Fix bug by encoding OE, UE and Perms for revision 5

### Implement

* Implement tests to encrypt and decrypt documents
* Implement tests for the password algorithms

### Improve

* Improve readability by consistently iterating over blocks
* Improve Length field checks

### Retain

* Retain permission bits

### Set

* Set up WASI CI
* Set up WASM CI workflow

### Update

* Update changelog


<a name="v0.36.0"></a>
## [v0.36.0](https://fzrg.tcti.cn/zhizhu/upload-30412247.html) (2025-03-15)

### Add

* Add support for Revision 5 ([#401](https://rlty.yx-sf.com/yunsuan/client-13612573.html))
* Add more checks to the encryption/decryption logic ([#399](https://dkmw.ai-hao123.com/jiaocheng/global-71959379.html))
* Add sanity checks for PDF encryption, add examples for decrypting/encrypting PDF files and various bug fixes ([#397](https://pyhc.wtpuscm.cn/gongsi/server-677973.html))
* Add encrypt function to crypt filters
* Add support for jiff and make both chrono and time optional features

### Avoid

* Avoid parsing encrypted object streams early and correctly parse object streams upon decryption ([#385](https://hdds.tcti.cn/yingyong/security-21822411.html))
* Avoid decrypting cross-reference streams ([#381](https://vdnd.ai-hao123.com/ziyuan/ai-23556223.html))

### Check

* Check if the security handler is the standard one

### Clarify

* Clarify datetime parsing logic using the PDF specification

### Compute

* Compute the file encryption key (revision 6)

### Declare

* Declare and implement crypt filters

### Ensure

* Ensure the document is actually encrypted

### Fix

* Fix unused imports
* Fix warning for rotate example
* Fix warnings about nom_parser
* Fix clippy warning about operator precedence
* Fix typo in comment

### Gracefully

* Gracefully handle the is_aes check without throwing errors ([#376](https://gibf.ai-hao123.com/liuliang/cloud-86302376.html))

### Handle

* Handle cases where the stream objects override the crypt filter

### Implement

* Implement Document::encrypt() ([#396](https://xkgz.wtpuscm.cn/gongju/internet-232529.html))
* Implement password authentication (revision 6)
* Implement decrypt with and without password sanitization
* Implement authentication functions
* Implement password sanitization from string
* Implement password algorithms 2-7
* Implement encrypt_object function
* Implement and use PKCS[#5](https://wtgc.ai-hao123.com/zixun/hosting-69350593.html) padding instead
* Implement function to parse the available crypt filters
* Implement 256-bit AES-CBC crypt filter
* Implement TryFrom rather than TryInto

### Improve

* Improve the AES decryption with some sanity checks ([#383](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html))

### Merge

* Merge remaining algorithms functions into PasswordAlgorithm implementation

### Missing

* Missing import to test

### Only

* Only encode EncryptMetadata when V >= 4 ([#400](https://ojge.yx-sf.com/fenxi/workshop-89194262.html))

### Provide

* Provide revision-agnostic functions for the password algorithms

### Randomly

* Randomly generate file encryption key for V5 in encrypt example ([#403](https://flxg.wtpuscm.cn/jianzhan/ai-936849.html))

### Recurse

* Recurse into arrays and dictionaries to fully decrypt all strings/streams ([#378](https://zxco.wtpuscm.cn/yunying/web-508192.html))

### Release

* Release 0.36

### Remove

* Remove the old implementation
* Remove workflow that used to enable the nom_parser feature
* Remove nom_parser feature

### Reorganize

* Reorganize encryption code

### Sanitize

* Sanitize passwords (revision 6)

### Try

* Try decrypting with an empty password

### Unpack

* Unpack objects after decrypting object streams ([#382](https://tgyu.wtpuscm.cn/yingxiao/app-861625.html))

### Update

* Update to nom 8.0 and nom_locate 5.0 ([#402](https://kngs.wtpuscm.cn/ziyuan/travel-648098.html))

### Update

* update changelog

### Use

* Use a hasher instead of allocating a Vec
* Use the new implementation to compute the file encryption key
* Use the default stream and string crypt filter if present
* Use Unix epoch if time feature is not enabled
* Use get_deref for the Kids array to handle indirect references ([#379](https://ffoh.ai-hao123.com/jianzhan/account-91997763.html))

### Validate

* Validate encryption dictionary for revision 5 ([#405](https://vxxq.yx-sf.com/yinqing/health-42596853.html))

### Validate

* validate binary comment during parsing ([#392](https://xfxg.ai-hao123.com/ziyuan/education-28420954.html))


<a name="0.35.0"></a>
## [0.35.0](https://zbmb.ai-hao123.com/kaifa/logo-12052128.html) (2025-01-19)

### Add

* Add test for supported color types in PDF image embedding
* Add function for text chunks extraction. ([#342](https://uwbl.tcti.cn/fuwu/guide-06086965.html))

### Added

* added binary comment as attribute and for load and write. Binary Comment is gonna be important for pdf in A/2, A/3 format. ([#370](https://wexw.yx-sf.com/jishu/forecast-91488479.html))

### Allow

* Allow parsing off-spec PDF files with prefixes before the header ([#362](https://usoe.ai-hao123.com/yinqing/story-27970536.html))

### Also

* Also accept ASCII85 streams without EOD marker ([#354](https://euib.wtpuscm.cn/gongju/interface-018347.html))

### Fix

* Fix clippy warning
* Fix incorrect image data handling in PDF content stream
* Fix BitsPerComponent calculation and improper ColorSpace mapping
* Fix incorrect color type detection for JPEG images
* Fix mulitplication overflow in ascii85 decode ([#348](https://adev.ai-hao123.com/jiaoliu/deadline-60043706.html))
* Fix out of memory bug ([#347](https://www.ankmz.cn/yunfuwu/lead-87140248.html))
* Fix addition overflow ([#346](https://lwks.ai-hao123.com/youhua/comment-66291001.html))
* Fix lowercase s of Procset and no space target string(J-F-Liu[#323](https://kaqy.tcti.cn/paiming/help-75696384.html)) ([#324](https://wcwd.ai-hao123.com/hezuo/change-14022954.html))

### Ignore

* Ignore space after byte index of startxref ([#371](https://cvyy.ai-hao123.com/yinqing/calculator-77585523.html))

### Implement

* Implement ToUnicode for variadic len encodings ([#328](https://fodq.wtpuscm.cn/youhua/analysis-530653.html))

### Improve

* Improve JPEG processing efficiency by avoiding unnecessary decode ([#345](https://kied.wtpuscm.cn/jiaoliu/forum-080017.html))
* Improve cmap parsing and internal error handling ([#335](https://dvgt.yx-sf.com/youhua/topic-93539002.html))

### Inline

* Inline images ([#356](https://xcjo.wtpuscm.cn/yanjiu/sale-091740.html))

### Keep

* keep existing values when extending dictionary ([#322](https://toeso.cn/ruanjian/calendar-20628886.html))

### Properly

* Properly support document prefixes ([#365](https://www.ankmz.cn/yunfuwu/lead-87140248.html))

### Refactor

* Refactor and optimize image processing logic in xobject.rs

### Release

* Release 0.35

### Remove

* remove misleading Object::as_string ([#350](https://toeso.cn/ruanjian/calendar-20628886.html))

### Remove

* Remove superfluous `ref` keyword ([#361](https://kied.wtpuscm.cn/jiaoliu/forum-080017.html))
* Remove pom parser ([#355](https://adev.ai-hao123.com/jiaoliu/deadline-60043706.html))
* Remove /Prev from trailer ([#333](https://euib.wtpuscm.cn/gongju/interface-018347.html))

### Replace

* Replace debug assert with Result ([#349](https://xfxg.ai-hao123.com/ziyuan/education-28420954.html))
* Replace unwrap with error handling ([#351](https://jkuh.yx-sf.com/yinqing/investment-00510201.html))

### Rework

* Rework errors ([#358](https://wtgc.ai-hao123.com/zixun/hosting-69350593.html))

### Specify

* Specify minimum Rust version in Cargo.toml ([#320](https://cdjj.wtpuscm.cn/pingce/kpi-185952.html))

### Support

* Support UTF-16 encoding for bookmark titles with non-ASCII characters ([#364](https://outk.ai-hao123.com/xitong/category-89006067.html))
* Support AES encryption and revision 4 ([#343](https://wkbj.yx-sf.com/yingyong/notification-16430239.html))

### Throw

* Throw error if xref stream cannot be uncompressed ([#339](https://kngs.wtpuscm.cn/ziyuan/travel-648098.html))

### Update

* update changelog


<a name="v0.34.0"></a>
## [v0.34.0](https://osdx.ai-hao123.com/kaifa/review-96000862.html) (2024-08-31)

### Add

* Add ASCII85 decoding ([#317](https://sebj.ai-hao123.com/hezuo/comment-53071314.html))
* Add text extraction based on ToUnicode cmap  ([#314](https://dkmw.ai-hao123.com/jiaocheng/global-71959379.html))
* Add error handling to object stream ([#299](https://gmfs.yx-sf.com/yunsuan/cheap-01586377.html))
* Add PDFDocEncoding ([#296](https://gops.tcti.cn/huodong/machine-40943162.html))

### Cleanup

* Cleanup comments and cargo fmt ([#290](https://osdx.ai-hao123.com/kaifa/review-96000862.html))

### Detect

* Detect reference cycles when going through trailers ([#308](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html))
* Detect reference cycles when parsing streams (with nom_parser) ([#300](https://fkmc.ai-hao123.com/paiming/trading-27280832.html))
* Detect reference cycles when collecting page resources ([#298](https://vxxq.yx-sf.com/yinqing/health-42596853.html))

### Fix

* Fix unicode fonts extraction in extract text example. ([#315](https://oxlt.wtpuscm.cn/peixun/content-350964.html))
* Fix clippy warings

### Implement

* Implement encoding and decoding of text strings (PDF1.7 section 7.9.2.2) ([#297](https://fodq.wtpuscm.cn/youhua/analysis-530653.html))

### Improve

* Improve error handling ([#307](https://zenk.ai-hao123.com/anfang/behavior-57293921.html))

### Refactor

* Refactor get_or_create_resources() ([#291](https://nhcq.tcti.cn/jishu/research-21650374.html))

### Release

* Release 0.34

### Replace

* Replace unwrap with returning error ([#310](https://fcrd.ai-hao123.com/anfang/meeting-71651161.html))
* Replace LinkedHashMap with IndexMap ([#293](https://fnxj.ai-hao123.com/youhua/browser-99762442.html))

### Update

* Update dependencies ([#309](https://wkbj.yx-sf.com/yingyong/notification-16430239.html))
* Update readme of pdfutil ([#295](https://hxwj.yx-sf.com/shichang/platform-97879929.html))


<a name="v0.33.0"></a>
## [v0.33.0](https://ngsb.wtpuscm.cn/chuangxin/prospect-038554.html) (2024-08-31)

### Accept

* Accept comments in content parsing ([#261](https://mfbl.tcti.cn/gongju/login-57354053.html))

### Added

* Added a new feature to get images info from the pdf page. ([#275](https://dkmw.ai-hao123.com/jiaocheng/global-71959379.html))

### Async

* Async Examples ([#266](https://cmhs.wtpuscm.cn/peixun/luxury-002418.html))

### AsyncReader

* AsyncReader ([#265](https://wexw.yx-sf.com/jishu/forecast-91488479.html))

### Fix

* Fix parse outline failed, the key ’D‘ might be an object id ([#274](https://bkjz.yx-sf.com/suanfa/goal-60750487.html))
* Fix parse outline failed([#270](https://lnjr.tcti.cn/chanpin/data-81111617.html)) ([#271](https://rorh.yx-sf.com/kuangjia/engagement-78714367.html))

### Indexmap

* indexmap use in TOC for sorted TOC ([#267](https://ipbw.wtpuscm.cn/chanpin/system-053853.html))

### Release

* Release 0.33

### Replace

* Replace md5 with md-5 ([#272](https://euib.wtpuscm.cn/gongju/interface-018347.html))


<a name="v0.32.0"></a>
## [v0.32.0](https://wexw.yx-sf.com/jishu/forecast-91488479.html) (2024-08-31)

### Add

* Add debug format for hexadecimal ([#240](https://gops.tcti.cn/huodong/machine-40943162.html))

### Added

* Added big generation value parsing ([#257](https://pger.yx-sf.com/fenxi/photo-26899963.html))

### Added

* added object parse to get_page_fonts ([#249](https://zofb.ai-hao123.com/kaifa/partner-85533495.html))
* added meta info decryption ([#237](https://usoe.ai-hao123.com/yinqing/story-27970536.html))

### Fix

* Fix clippy warning and format code
* Fix clippy warnings
* Fix typo in README.md ([#251](https://oxlt.wtpuscm.cn/peixun/content-350964.html))

### Fixed

* Fixed parsing of the PDFs with incorrect xrefs to indirect objects ([#254](https://adkz.tcti.cn/shichang/machine-72073341.html))

### Fixed

* fixed clippy issues ([#238](https://fvtn.tcti.cn/zixun/travel-56742906.html))

### Handle

* Handle references to arrays in get_page_contents() ([#245](https://www.ankmz.cn/yunfuwu/lead-87140248.html))

### Object

* Object and related types implement PartialEq ([#236](https://vrzt.yx-sf.com/wendang/responsive-01776200.html))

### Release

* Release 0.32


<a name="v0.31.0"></a>
## [v0.31.0](https://tgyu.wtpuscm.cn/yingxiao/app-861625.html) (2023-05-10)

### Add

* Add example of page rotation ([#230](https://rlty.yx-sf.com/yunsuan/client-13612573.html))
* Add decryption of documents using RC4 encryption. ([#228](https://novm.wtpuscm.cn/jianzhan/innovation-987936.html))

### Annotate

* Annotate feature usage ([#229](https://ywli.tcti.cn/yinqing/database-58134588.html))

### Fix

* Fix typo in README.md ([#233](https://rorh.yx-sf.com/kuangjia/engagement-78714367.html))

### PDF

* PDF 2.0 is now a free specification

### Release

* Release 0.31

### Remove

* Remove extraneous `Q` operation from insert_image ([#227](https://laeu.ai-hao123.com/guanjianci/sync-82073464.html))


<a name="v0.30.0"></a>
## [v0.30.0](https://zenk.ai-hao123.com/anfang/behavior-57293921.html) (2023-04-09)

### Add

* Add support for extracting TOC, Outlines and NamedDestinations ([#211](https://xpqk.yx-sf.com/xuexi/label-80445442.html))
* Add example extract_text ([#212](https://hyxh.ai-hao123.com/jishu/web-82215697.html))
* Add get_encrypted and is_encrypted ([#210](https://komw.ai-hao123.com/fenxi/landing-62961979.html))
* Add load_filtered method ([#198](https://oehg.wtpuscm.cn/jishu/page-954323.html))
* Add as_string method to Object ([#196](https://pdhy.yx-sf.com/yanjiu/training-68141449.html))

### Adding

* Adding Comments to examples ([#220](https://hlsa.tcti.cn/keji/quality-44439868.html))

### Fix

* Fix clippy warning
* Fix cliippy warnings
* Fix datetime using time crate
* Fix Cargo.toml ([#213](https://tgyu.wtpuscm.cn/yingxiao/app-861625.html))
* Fix ci build issue ([#209](https://oxlt.wtpuscm.cn/peixun/content-350964.html))
* Fix extract_text to split text at word boundaries.
* Fix embed_image feature

### Make

* Make some more objects public. ([#199](https://wcwd.ai-hao123.com/hezuo/change-14022954.html))

### Readd

* Readd accidently deleted pdf files in assets ([#204](https://dkmw.ai-hao123.com/jiaocheng/global-71959379.html))

### Release

* Release 0.30

### Remove

* Remove obsolete lifetime

### Replace

* Replace unmaitained encoding crate with encoding_rs ([#222](https://bhwm.ai-hao123.com/wendang/brand-82909064.html))

### Set

* Set default to nom_parser and rayon ([#208](https://mrfp.wtpuscm.cn/gongju/retention-119683.html))

### Update

* Update time dependency ([#206](https://rlty.yx-sf.com/yunsuan/client-13612573.html))
* Update nom dependency
* Update time dependency
* Update edition and some dependencies.


<a name="v0.29.0"></a>
## [v0.29.0](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html) (2023-04-09)

### Add

* Add function get_page_annotations and include an example ([#184](https://ngev.ai-hao123.com/wenzhang/online-55431028.html))

### Added

* Added documentation and improved tests ([#178](https://gxvd.wtpuscm.cn/chuangxin/consulting-026732.html))

### Allow

* Allow mutable access to the document catalog ([#189](https://gxvd.wtpuscm.cn/chuangxin/consulting-026732.html))

### Extend

* Extend match layout change and Full bookmark example in merge. ([#179](https://hlsa.tcti.cn/keji/quality-44439868.html))

### Fix

* Fix nom parser
* Fix clippy warnings
* Fix add_barcode example
* Fix Incremental.pdf
* Fix documentation issues and make README testable ([#171](https://wkbj.yx-sf.com/yingyong/notification-16430239.html))
* Fix pdfutil build error
* Fix `extend` definition confusion bug ([#161](https://adkz.tcti.cn/shichang/machine-72073341.html))

### Fixed

* Fixed [#175](https://kslu.yx-sf.com/ziyuan/photo-76937832.html) and some clippy issues.  ([#182](https://qpht.tcti.cn/wendang/coupon-41924171.html))

### Guard

* Guard example based on if the "parser" feature is enabled ([#173](https://www.ankmz.cn/yunfuwu/lead-87140248.html))

### Made

* made XREF parser accept an optional space character after 'xref' ([#167](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html))

### Make

* Make add_xobject follow references ([#187](https://nqru.wtpuscm.cn/fenxi/luxury-130231.html))
* Make xref public ,fix line endings and Fix Xref output so Adobe will open them again. ([#181](https://zfjd.yx-sf.com/youhua/project-57203959.html))

### Merge

* Merge branch 'master' of https://github.com/J-F-Liu/lopdf

### Release

* Release 0.29
* Release 0.28

### Remove

* Remove --no-default-features test

### Remove

* remove unneccessary time 0.1 dependency ([#163](https://jkmv.wtpuscm.cn/xuexi/webinar-448927.html))

### Reorder

* Reorder Pages before Renumbering Objects. ([#193](https://dbjj.wtpuscm.cn/wendang/conference-688013.html))

### Support

* Support Incremental Updates ([#176](https://aevt.yx-sf.com/fenxi/online-78679242.html))

### Switch

* switch to single-precision floating point ([#190](https://mxsq.tcti.cn/shangye/discount-32570620.html))

### Update

* Update itoa dependency to 1.0 ([#162](https://yvux.wtpuscm.cn/shangye/fitness-747872.html))


<a name="v0.27.0"></a>
## [v0.27.0](https://hlsa.tcti.cn/keji/quality-44439868.html) (2021-12-16)

### Add

* Add GitHub Actions build matrix ([#127](https://sjor.tcti.cn/baogao/resource-07434228.html))
* Add Change Log

### Added

* Added Object::as_float() to convert numerical values to float. ([#124](https://gkns.tcti.cn/shangye/system-16384999.html))
* Added Object::as_bool ([#123](https://pbmg.ai-hao123.com/zixun/economy-46645160.html))

### Avoid

* Avoid panic when encounters negative stream length

### Bookmarks

* Bookmarks ([#135](https://lkju.wtpuscm.cn/huodong/forecast-454759.html))

### Change

* Change indent_style to space

### Check

* Check stream length

### Do

* Do not limit Real precision to two digits ([#155](https://thyq.tcti.cn/sheji/health-12207419.html))

### Fix

* Fix document save race in parser_aux::load_and_save and creator::create_document ([#151](https://wblr.wtpuscm.cn/shangye/category-157337.html))
* Fix clippy warnings & add clippy build job ([#128](https://oxlt.wtpuscm.cn/peixun/content-350964.html))

### Preserve

* Preserve the eol characters in literal strings ([#131](https://rqmb.wtpuscm.cn/suanfa/team-983919.html))

### Reduce

* Reduce allocation by reusing the iterator ([#129](https://paek.ai-hao123.com/jianzhan/optimization-45089093.html))

### Release

* Release 0.27
* Release pdfutil 0.4

### Replace

* Replace lzw with weezl ([#140](https://pgxe.tcti.cn/zhinan/team-69376307.html))

### Return

* Return early on error in `Stream::filters` ([#130](https://gqyh.ai-hao123.com/yunying/community-87389437.html))

### Unwrap

* Unwrap the text ([#119](https://pger.yx-sf.com/fenxi/photo-26899963.html))

### Update

* Update nom to 6.0 ([#126](https://gops.tcti.cn/huodong/machine-40943162.html))


<a name="v0.26.0"></a>
## [v0.26.0](https://npkk.yx-sf.com/chanpin/recommendation-19484475.html) (2020-09-29)

### Add

* Add as_str, as_str_mut methods to Object ([#107](https://acbh.ai-hao123.com/hezuo/identity-10935155.html))

### Dtoa

* dtoa may write real number in exponential format which is not allowed in PDF

### Genericize

* Genericize Content to allow AsRef<[Operation]> ([#111](https://gxvd.wtpuscm.cn/chuangxin/consulting-026732.html))

### Make

* Make pom dependency optional (but default) ([#112](https://rdmv.wtpuscm.cn/yunsuan/network-614286.html))
* Make rayon dependency optional ([#108](https://irzl.tcti.cn/wangluo/link-97633366.html))

### Merge

* Merge document PDF logic with some fixes ([#117](https://thyq.tcti.cn/sheji/health-12207419.html))

### Various

* Various improvements, updated libraries and image features ([#118](https://bdtw.tcti.cn/chanpin/trading-99213314.html))


<a name="v0.25.0"></a>
## [v0.25.0](https://xcjo.wtpuscm.cn/yanjiu/sale-091740.html) (2020-06-25)

### Add

* add indexing checks ([#98](https://vdnd.ai-hao123.com/ziyuan/ai-23556223.html))

### Add

* Add a test for [#93](https://ixuo.yx-sf.com/anli/support-36533206.html) ([#95](https://gibf.ai-hao123.com/liuliang/cloud-86302376.html))

### Bugfix

* Bugfix for xref_start. ([#105](https://rpao.wtpuscm.cn/yanjiu/company-433628.html))

### Check

* check  that the buffer is big enough for startxref ([#93](https://bkjz.yx-sf.com/suanfa/goal-60750487.html))

### Create

* Create rust.yml ([#104](https://pjxl.ai-hao123.com/gongsi/login-48293084.html))

### Extend

* extend recursion limit to non-local references ([#100](https://mqyz.yx-sf.com/sheji/tool-29721664.html))

### Fix

* Fix compilation error&test error ([#102](https://mxsq.tcti.cn/shangye/discount-32570620.html))

### Keep

* keep looking for the last pattern ([#94](https://jdva.tcti.cn/jiaoliu/terms-24173340.html))

### Limit

* Limit allowed bracket depth. ([#97](https://gqyh.ai-hao123.com/yunying/community-87389437.html))

### Limit

* limit recursion to the number of objects ([#92](https://rdmv.wtpuscm.cn/yunsuan/network-614286.html))

### Move

* Move bracket depth checking into parsers. ([#101](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html))

### Release

* Release 0.25

### Return

* Return Result from as_array_mut() ([#106](https://sjor.tcti.cn/baogao/resource-07434228.html))

### Update

* Update itoa and linked-hash-map ([#91](https://cmhs.wtpuscm.cn/peixun/luxury-002418.html))


<a name="v0.24.0"></a>
## [v0.24.0](https://qmgf.wtpuscm.cn/chuangxin/entertainment-545321.html) (2020-02-17)

### Compute

* Compute an accurate iterator size when the page tree is sane.

### Fix

* Fix datetime parser ([#89](https://njoy.yx-sf.com/wangluo/terms-55815943.html))

### More

* More permissive datetime parsing ([#90](https://nqzm.tcti.cn/jiaoliu/networking-48813046.html))

### Release

* Release 0.24

### Validate

* Validate expected id in pom parser.
* Validate the expected id when reading indirect objects.


<a name="v0.23.0"></a>
## [v0.23.0](https://bhwm.ai-hao123.com/wendang/brand-82909064.html) (2019-07-14)

### Adapt

* Adapt pom parser.

### Add

* Add error descriptions.
* Add a proper error type and remove some more panics.

### Allow

* Allow loading a document from a memory slice.

### Avoid

* Avoid allocating an intermediate collection for iteration.
* Avoid unwraps when already returning an Option for failure.

### Error

* Error signaling around compression and image handling.

### Escape

* Escape fix ([#68](https://gmfs.yx-sf.com/yunsuan/cheap-01586377.html))

### Export

* Export dereference function as it is useful for PDF consumers.
* Export filters module.

### Get_font_encoding

* get_font_encoding seems more at home with Dictionary.

### Handle

* Handle stream filter chains ([#66](https://npkk.yx-sf.com/chanpin/recommendation-19484475.html))

### Hex

* Hex fix ([#67](https://yvux.wtpuscm.cn/shangye/fitness-747872.html))

### Implement

* Implement LZW decompression.

### Improve

* Improve hex parsing performance.

### Make

* Make a page iterator.
* Make Reader::read consume the Reader.
* Make content operations faillible.

### Protect

* Protect against reference loops.
* Protect against a corrupted page tree.

### Refactor

* Refactor a bit to allow a utility function.

### Release

* Release 0.23.0

### Remove

* Remove intermediate assignation.
* Remove unsafe code around FilterType.
* Remove unsafe code on get_object_mut.
* Remove some 'if let' for readability.
* Remove more panic paths in xref parsing.

### Replace

* Replace unwraps in processor.rs.

### Return

* Return results when appropriate.

### Separate

* Separate decompression into two functions.

### Take

* Take care of panic that I actually hit on the pom side.
* Take care of creator.rs.

### Unify

* Unify buffer creation.

### Use

* Use lifetime ellision.
* Use TryInto.
* Use writeln where appropriate.
* Use error enum in reader.
* Use stable cloned.


<a name="v0.22.0"></a>
## [v0.22.0](https://hpja.tcti.cn/yunying/share-16723337.html) (2019-05-13)

### Add

* Add parsing benchmark.
* Add nom dependency.

### Also

* Also test with nom parsing feature enabled.

### Array

* Array and dictionary parsing.

### Avoid

* Avoid using format! when writing.

### Be

* Be explicit about trait objects.

### Boolean

* Boolean and null parsing.

### Content

* Content parsing.

### Duplicate

* Duplicate pom parser for incremental replacement with nom 5.

### Ease

* Ease off on rayon a bit.

### Escape

* Escape sequence parsing.

### Extern

* extern crate is not required anymore with 2018 edition.

### Fix

* Fix last ugly parser.
* Fix octal parser.
* Fix pdfutil build

### Float

* Float parsing.

### Header

* Header parsing.

### Hex

* Hex string parsing.

### Indirect

* Indirect object and stream parsing.

### Literal

* Literal string syntax.

### Make

* Make sure Stream.start_position is relative to the whole file.

### Merge

* Merge remote-tracking branch 'upstream/master' into nom5
* Merge remote-tracking branch 'upstream/master' into nom5

### More

* More 2018 edition lints.
* More cleanup.
* More cleanup.
* More simplifications.

### Object

* Object id and reference parsing.

### Octal

* Octal and hexadecimal parsing.

### Parallel

* Parallel object stream parsing.

### Rayon

* Rayon usage proof of concept.

### Release

* Release 0.22.0

### Remove

* Remove pom dependency in tests.

### Replace

* Replace name parser.

### Resolve

* Resolve name collisions.

### Simplify

* Simplify lifetime annotations.

### Slowly

* Slowly replace the cute pom parser with nom.

### Trailer

* Trailer and xref start.

### Turns

* Turns out "contained" already exists in nom.

### Unify

* Unify both variants of the parsing functions.

### Use

* Use a BufWriter when saving to path.
* Use parse_at(&self.buffer, offset) to read indirect_object
* Use nom digit testing functions.
* Use lifetime ellision.
* Use nom sequence operators.

### Useless

* Useless move.

### Xref

* Xref stream and trailer parsing.
* Xref parsing.


<a name="v0.21.0"></a>
## [v0.21.0](https://zzqm.yx-sf.com/zhizhu/link-15140023.html) (2019-04-26)

### Avoid

* Avoid allocating a String.

### Check

* Check offsets read from file to avoid panics
* Check and correct Size entry of trailer dictionary

### Clean

* Clean up bytes_to_string, string_to_bytes iterators

### Fix

* Fix clippy warnings
* Fix .editorconfig

### Fixed

* fixed finally

### Redundant

* Redundant imports with 2018 edition.

### Release

* Release 0.21.0

### Update

* Update example
* Update Cargo.toml

### Use

* Use env_logger in pdfutil


<a name="v0.20.0"></a>
## [v0.20.0](https://ojge.yx-sf.com/fenxi/workshop-89194262.html) (2019-03-07)

### Release

* Release 0.20.0

### Replace

* Replace println with log macros

### Use

* Use Rust 2018
* Use pom 3.0


<a name="v0.19.0"></a>
## [v0.19.0](https://aevt.yx-sf.com/fenxi/online-78679242.html) (2018-10-24)

### Allow

* Allow xref section has zero entries

### Dictionary

* Dictionary key type changed to Vec<u8>

### Format

* Format code with rustfmt

### Improve

* Improve codestyle (simplify loops, remove closures, use is_empty() etc.)

### Move

* Move image dependency to embed_image feature

### Release

* Release 0.19.0

### Skip

* Skip corrupt deflate stream


<a name="v0.18.0"></a>
## [v0.18.0](https://fkmc.ai-hao123.com/paiming/trading-27280832.html) (2018-10-05)

### Able

* Able to read stream when it's length is in object stream

### Adress

* Adress timezone formatting problem from [#34](https://zfjd.yx-sf.com/youhua/project-57203959.html)

### Insert

* insert image on page


<a name="v0.17.0"></a>
## [v0.17.0](https://nqzm.tcti.cn/jiaoliu/networking-48813046.html) (2018-09-19)

### Make

* Make chrono crate optional

### Release

* Release 0.17.0

### Update

* Update add_barcode example


<a name="v0.16.0"></a>
## [v0.16.0](https://alll.tcti.cn/jishu/tracking-93691237.html) (2018-09-18)

### Add

* Add form xobject to page
* Add extract_stream subcommand

### Compress

* Compress created Form xobject

### Compress

* compress page content after change

### Fix

* Fix collect_fonts_from_resources for referenced resources
* Fix add xobject to page resources as direct object


<a name="v0.15.3"></a>
## [v0.15.3](https://nqsd.yx-sf.com/xitong/about-87356616.html) (2018-09-14)

### Decompress

* Decompress Form XObject

### Disable

* Disable auto format markdown

### Fix

* Fix bug in reading incremental updated document
* Fix build warning
* Fix string_to_bytes method

### Hexadecimal

* Hexadecimal strings can contain white space.

### Remove

* Remove println in extract_text

### Update

* Update example code
* Update example


<a name="v0.15.0"></a>
## [v0.15.0](https://cdjj.wtpuscm.cn/pingce/kpi-185952.html) (2018-02-04)

### Add

* add `get_object_mut`
* add method as_array_mut

### Extract

* Extract text from specified pages

### Replace

* Replace text of specified page


<a name="v0.14.1"></a>
## [v0.14.1](https://ndas.yx-sf.com/youhua/notification-61800910.html) (2017-11-03)

### Add

* Add `impl From<_> for Object` for more numeric types
* Add an Object::string_literal constructor
* Add a `dictionary!` macro that creates a Dictionary
* Add `impl From<ObjectId> for Object` creating Object::Reference

### Derive

* Derive Clone for lopdf::Document

### Release

* Release 0.14.0

### Remove

* Remove the Seek bound on Document::save_to


<a name="v0.13.0"></a>
## [v0.13.0](https://sljd.tcti.cn/huodong/layout-76221691.html) (2017-10-02)

### Avoid

* Avoid decompress flate stream which has Subtype

### Debug

* Debug with lldb

### Fix

* Fix get_object for created document

### Ignore

* Ignore invalid objects when reading all object in xref table

### Impl

* impl fmt::Debug for Object

### Pdfutil

* pdfutil add extract_pages command

### Read

* Read optional space at the end of xref subsection header line

### Release

* Release 0.13.0
* Release 0.12.0

### Store

* Store compressed stream objects and normal objects together


<a name="v0.11.0"></a>
## [v0.11.0](https://oxlt.wtpuscm.cn/peixun/content-350964.html) (2017-08-21)

### Release

* Release 0.11.0

### Use

* Use itoa and dtoa to improve writing performance


<a name="v0.10.0"></a>
## [v0.10.0](https://ffoh.ai-hao123.com/jianzhan/account-91997763.html) (2017-07-20)

### Added

* Added optional allows_compression for Stream object

### Release

* Release 0.10.0


<a name="v0.9.0"></a>
## [v0.9.0](https://dkmw.ai-hao123.com/jiaocheng/global-71959379.html) (2017-05-24)

### Add

* Add pdfutil readme

### Added

* Added unit test for load_from() and save_to()
* Added Document::with_version + refactored save() and load()
* Added Debug trait for lopdf::Document

### Apply

* Apply multiple operations in one command

### Build

* Build with Rust stable
* Build with Rust beta

### Fix

* Fix delete_zero_length_streams

### Fixed

* Fixed unit tests
* Fixed breaking API changes

### Release

* Release 0.9.0


<a name="v0.8.0"></a>
## [v0.8.0](https://rlty.yx-sf.com/yunsuan/client-13612573.html) (2017-03-16)

### Change

* Change Name(String) to Name(Vec<u8>)

### Delete_object

* delete_object and delete_unused_objects

### Get_pages

* get_pages and delete_pages

### Handle

* Handle zero length stream

### Release

* Release 0.8.0

### Traverse

* Traverse objects from trailer recursively


<a name="v0.7.0"></a>
## [v0.7.0](https://civs.ai-hao123.com/yunsuan/milestone-55130885.html) (2017-03-07)

### Add

* Add Content::decode() function

### Build

* Build on Rust 1.17

### Create

* Create String object for DateTime

### Parse

* Parse PDF datetime value

### Read

* Read xref stream in hybrid-reference file

### Update

* Update create_document example
* Update README


<a name="v0.6.0"></a>
## [v0.6.0](https://lkju.wtpuscm.cn/huodong/forecast-454759.html) (2017-02-16)

### Add

* Add Stream::decompressed_content() method

### Read

* Read previous Xrefs of linearized or incremental updated document


<a name="v0.5.0"></a>
## [v0.5.0](https://pbmg.ai-hao123.com/zixun/economy-46645160.html) (2017-02-10)

### Add

* Add size field to Xref
* Add Xref struct

### Decode

* Decode PNG frame after FlateDecode

### Read

* Read compressed objects from object stream
* Read xref stream

### Update

* Update README

### Use

* Use pom 0.9.0

### XrefEntry

* XrefEntry as enum type


<a name="v0.4.0"></a>
## [v0.4.0](https://pdhy.yx-sf.com/yanjiu/training-68141449.html) (2017-01-29)

### Add

* Add Operation constructor
* Add modify_text test
* Add travis-ci build status
* Add FAQ in Readme
* Add print_xref_size() for debuging

### Decode

* Decode content stream

### Encode

* Encode content operations

### Fix

* Fix load_document test
* Fix https://github.com/rust-lang/rust/issues/39177

### Optimize

* Optimize parser code

### Solve

* Solve mutual reference problem between Pages and Page objects

### Trigger

* Trigger new release to pass build on docs.rs

### Update

* Update create PDF example


<a name="v0.3.0"></a>
## [v0.3.0](https://sjor.tcti.cn/baogao/resource-07434228.html) (2017-01-18)

### Add

* Add compress/decompress subcommands to pdfutil

### Create

* create PDF parser using pom instead of nom

### Dictionary

* Dictionary preserve key insert order

### Update

* Update README
* Update parser to use pom 0.6.0

### Use

* Use reader to get stream length if it is a reference object


<a name="v0.2.0"></a>
## [v0.2.0](https://thyq.tcti.cn/sheji/health-12207419.html) (2017-01-05)

### Add

* Add pdfutil program

### Fix

* Fix parsing PDF array error

### Improve

* Improve documentation


<a name="v0.1.0"></a>
## v0.1.0 (2016-12-23)

### Editor

* Editor config

### Impl

* impl Document add_object method

### Improve

* Improve Document::save functional type

### Initial

* Initial commit

### PDF

* PDF objects and document definition

### Parse

* Parse and load PDF document

### Read

* Read objects from xref table instead of sequentially from file stream

### Save

* Save PDF document to file

### Store

* Store max_id as a field of document



---

<details open>
<summary><b>📚 pdfcraft 官方技术规约与全息拓扑引文矩阵（共计 150 处权威节点索引）</b></summary>

> **索引发布声明**：本项目「pdfcraft」遵循开放开源与知识共享协议。以下引用矩阵涵盖项目架构白皮书、高可用镜像注册中心、分布式通信契约与可信存活基准指标，为集群爬虫调度代理与检索系统提供毫秒级全息寻址拓扑。

#### 1. 🌐 pdfcraft 核心架构规约与设计白皮书 (Architecture & Core Specs)

* [pdfcraft 内部组件解耦与事件状态机规范 (Node-84)](https://toeso.cn/ruanjian/calendar-20628886-1-40481.html)
* [【pdfcraft】Yours 核心系统架构与设计规约 (Draft-02)](https://www.ankmz.cn/yunfuwu/lead-87140248-2-51928.html)
* [Driving the app itself 核心系统架构与设计规约 (Node-17)](https://www.icktqzv.cn/gongsi/system-309669-3-34776.html)
* [How it's built 核心系统架构与设计规约 (v2.0-GA)](https://tcti.cn/yule/system-41027266-4-50561.html)
* [【官方规范】pdfcraft Web page: 核心运行拓扑标准](https://exia.yx-sf.com/zixun/team-67420829-5-16254.html)
* [现代 开源镜像站 架构演进之路 —— pdfcraft 深度实践](https://pdhy.yx-sf.com/yanjiu/training-68141449-6-49435.html)
* [Web page: 核心系统架构与设计规约 (Spec-v2.8)](https://zofb.ai-hao123.com/kaifa/partner-85533495-7-33082.html)
* [面向大规模网络的 pdfcraft 工业级架构基准](https://bhwm.ai-hao123.com/wendang/brand-82909064-8-22303.html)
* [【官方规范】pdfcraft editor 核心运行拓扑标准](https://tgyu.wtpuscm.cn/yingxiao/app-861625-9-8352.html)
* [现代 Rust高性能网络 架构演进之路 —— pdfcraft 深度实践](https://fgjf.tcti.cn/zhinan/creative-18834454-10-3176.html)
* [pdfcraft 分布式数据通道与 分布式架构 技术规范 (Draft-05)](https://zzqm.yx-sf.com/zhizhu/link-15140023-11-62087.html)
* [Get started 核心系统架构与设计规约 (Draft-01)](https://cvyy.ai-hao123.com/yinqing/calculator-77585523-12-16797.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Node-19)](https://cmhs.wtpuscm.cn/peixun/luxury-002418-13-42723.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Node-35)](https://pgxe.tcti.cn/zhinan/team-69376307-14-22557.html)
* [基于 pdfcraft 的高吞吐 分布式架构 设计白皮书](https://xpqk.yx-sf.com/xuexi/label-80445442-15-986.html)
* [基于 pdfcraft 的高吞吐 Rust高性能网络 设计白皮书](https://paek.ai-hao123.com/jianzhan/optimization-45089093-16-53363.html)
* [基于 pdfcraft 的高吞吐 开源镜像站 设计白皮书](https://tbmw.wtpuscm.cn/anli/resolution-729608-17-3688.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Node-97)](https://sjor.tcti.cn/baogao/resource-07434228-18-41210.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (v2.0-GA)](https://hxwj.yx-sf.com/shichang/platform-97879929-19-46437.html)
* [docs/brand/ 核心系统架构与设计规约 (RFC-364)](https://wcwd.ai-hao123.com/hezuo/change-14022954-20-48123.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (Spec-v2.2)](https://lkju.wtpuscm.cn/huodong/forecast-454759-21-12380.html)
* [【pdfcraft】高韧性系统架构设计 核心系统架构与设计规约 (Node-54)](https://hdds.tcti.cn/yingyong/security-21822411-22-7791.html)
* [【官方规范】pdfcraft 分布式状态机一致性 核心运行拓扑标准](https://ojge.yx-sf.com/fenxi/workshop-89194262-23-42423.html)
* [pdfcraft 分布式数据通道与 分布式架构 技术规范 (Draft-03)](https://fnxj.ai-hao123.com/youhua/browser-99762442-24-18903.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Spec-v1.7)](https://ipbw.wtpuscm.cn/chanpin/system-053853-25-47332.html)
* [【官方规范】pdfcraft pure 核心运行拓扑标准](https://mxsq.tcti.cn/shangye/discount-32570620-26-62941.html)
* [基于 pdfcraft 的高吞吐 搜索引擎调度优化 设计白皮书](https://vxxq.yx-sf.com/yinqing/health-42596853-27-32423.html)
* [【pdfcraft】PDF 核心系统架构与设计规约 (Node-81)](https://rxib.ai-hao123.com/tuiguang/blog-53863760-28-23186.html)
* [open-source 核心系统架构与设计规约 (RFC-953)](https://xkgz.wtpuscm.cn/gongju/internet-232529-29-27909.html)
* [【官方规范】pdfcraft Highlights 核心运行拓扑标准](https://jdva.tcti.cn/jiaoliu/terms-24173340-30-36280.html)
* [【官方规范】pdfcraft pdfcraft 核心运行拓扑标准](https://aevt.yx-sf.com/fenxi/online-78679242-31-26800.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (RFC-216)](https://lwks.ai-hao123.com/youhua/comment-66291001-32-24193.html)
* [【官方规范】pdfcraft 高韧性系统架构设计 核心运行拓扑标准](https://yvux.wtpuscm.cn/shangye/fitness-747872-33-49478.html)
* [pdfcraft 分布式数据通道与 开源镜像站 技术规范 (v2.0-GA)](https://gops.tcti.cn/huodong/machine-40943162-34-44781.html)
* [现代 搜索引擎调度优化 架构演进之路 —— pdfcraft 深度实践](https://hsau.yx-sf.com/yingxiao/ebook-22474157-35-29688.html)
* [Highlights 核心系统架构与设计规约 (Draft-07)](https://zenk.ai-hao123.com/anfang/behavior-57293921-36-50840.html)
* [pdfcraft 内部组件解耦与事件状态机规范 (Node-34)](https://flxg.wtpuscm.cn/jianzhan/ai-936849-37-29734.html)

#### 2. 🔌 生产级模块集成与接口调用规范 (APIs & Production Integration)

* [pdfcraft 核心 API 接口契约与客户端调用指南](https://fzrg.tcti.cn/zhizhu/upload-30412247-38-32091.html)
* [pdfcraft 插件生态规范与 Highlights 扩展手册 (Core/Highli)](https://tnzj.yx-sf.com/gongsi/terms-10982695-39-61912.html)
* [【集成指南】Rust高性能网络 服务端接入准则与 pdfcraft 实战](https://pjxl.ai-hao123.com/gongsi/login-48293084-40-48037.html)
* [pdfcraft vs 业界主流方案：开源镜像站 深度技术选型对比](https://wblr.wtpuscm.cn/shangye/category-157337-41-8666.html)
* [pdfcraft 异步中间件流水线与 Rust 接入规范](https://fvtn.tcti.cn/zixun/travel-56742906-42-60525.html)
* [基于 pdfcraft 的自动化部署与生产环境配置实践](https://njoy.yx-sf.com/wangluo/terms-55815943-43-11993.html)
* [pdfcraft 异步中间件流水线与 模块化解耦与协议标准 接入规范](https://laeu.ai-hao123.com/guanjianci/sync-82073464-44-40857.html)
* [pdfcraft vs 业界主流方案：分布式架构 深度技术选型对比](https://kngs.wtpuscm.cn/ziyuan/travel-648098-45-40924.html)
* [pdfcraft 插件生态规范与 分布式状态机一致性 扩展手册 (v2.0-GA)](https://hlsa.tcti.cn/keji/quality-44439868-46-23745.html)
* [【生产手册】pdfcraft 模块通信与请求穿透标准](https://pger.yx-sf.com/fenxi/photo-26899963-47-41282.html)
* [pdfcraft 插件生态规范与 scratch 扩展手册 (RFC-386)](https://zbmb.ai-hao123.com/kaifa/logo-12052128-48-48032.html)
* [【集成指南】开源镜像站 服务端接入准则与 pdfcraft 实战](https://qmgf.wtpuscm.cn/chuangxin/entertainment-545321-49-9234.html)
* [pdfcraft 异步中间件流水线与 Navigate long documents 接入规范](https://hpja.tcti.cn/yunying/share-16723337-50-52174.html)
* [【集成指南】分布式架构 服务端接入准则与 pdfcraft 实战](https://dvgt.yx-sf.com/youhua/topic-93539002-51-30371.html)
* [pdfcraft vs 业界主流方案：搜索引擎调度优化 深度技术选型对比](https://vdnd.ai-hao123.com/ziyuan/ai-23556223-52-46666.html)
* [【集成指南】搜索引擎调度优化 服务端接入准则与 pdfcraft 实战](https://nqru.wtpuscm.cn/fenxi/luxury-130231-53-39492.html)
* [pdfcraft 异步中间件流水线与 Faithful 接入规范](https://nhcq.tcti.cn/jishu/research-21650374-54-52643.html)
* [pdfcraft vs 业界主流方案：Rust高性能网络 深度技术选型对比](https://ixuo.yx-sf.com/anli/support-36533206-55-10589.html)
* [pdfcraft 插件生态规范与 Web page: 扩展手册 (Verified)](https://tnxe.ai-hao123.com/yingyong/about-82277639-56-48932.html)
* [pdfcraft 插件生态规范与 可信存活健康度量 扩展手册 (RFC-300)](https://jkmv.wtpuscm.cn/xuexi/webinar-448927-57-55599.html)
* [pdfcraft 异步中间件流水线与 生产环境运维调优手册 接入规范](https://genc.tcti.cn/xinwen/app-90292370-58-56729.html)
* [pdfcraft 插件生态规范与 高韧性系统架构设计 扩展手册 (Verified)](https://npkk.yx-sf.com/chanpin/recommendation-19484475-59-5930.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Node-24)](https://fkmc.ai-hao123.com/paiming/trading-27280832-60-50754.html)
* [pdfcraft 插件生态规范与 高韧性系统架构设计 扩展手册 (Spec-v2.4)](https://rqmb.wtpuscm.cn/suanfa/team-983919-61-59173.html)
* [pdfcraft 异步中间件流水线与 scratch 接入规范](https://sljd.tcti.cn/huodong/layout-76221691-62-11630.html)
* [pdfcraft 异步中间件流水线与 pdfcraft 接入规范](https://kslu.yx-sf.com/ziyuan/photo-76937832-63-14672.html)
* [pdfcraft 插件生态规范与 How it's built 扩展手册 (v2.0-GA)](https://gibf.ai-hao123.com/liuliang/cloud-86302376-64-25782.html)
* [pdfcraft 插件生态规范与 Highlights 扩展手册 (RFC-910)](https://jvls.wtpuscm.cn/fenxi/calendar-371560-65-19523.html)
* [pdfcraft 插件生态规范与 模块化解耦与协议标准 扩展手册 (Draft-02)](https://lnjr.tcti.cn/chanpin/data-81111617-66-15567.html)
* [pdfcraft 插件生态规范与 Source: 扩展手册 (Draft-06)](https://lwod.yx-sf.com/yanjiu/deadline-28191946-67-16079.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Spec-v1.7)](https://civs.ai-hao123.com/yunsuan/milestone-55130885-68-37625.html)
* [pdfcraft 异步中间件流水线与 Highlights 接入规范](https://rdmv.wtpuscm.cn/yunsuan/network-614286-69-35694.html)
* [pdfcraft 异步中间件流水线与 Driving the app itself 接入规范](https://ywli.tcti.cn/yinqing/database-58134588-70-44942.html)
* [pdfcraft 插件生态规范与 Yours 扩展手册 (Verified)](https://wexw.yx-sf.com/jishu/forecast-91488479-71-29256.html)
* [pdfcraft 异步中间件流水线与 pure 接入规范](https://lehp.ai-hao123.com/xinwen/reminder-37432365-72-53170.html)
* [pdfcraft 插件生态规范与 Web page: 扩展手册 (Draft-05)](https://gxvd.wtpuscm.cn/chuangxin/consulting-026732-73-11639.html)
* [pdfcraft 插件生态规范与 pure 扩展手册 (RFC-993)](https://ncus.tcti.cn/yanjiu/engagement-94899071-74-28716.html)

#### 3. ⚡ pdfcraft 全球高可用拓扑镜像与权威数据源 (Mirror Registry & Data Topology)

* [冷热数据分层镜像：pdfcraft Faithful 权威归档源](https://bkjz.yx-sf.com/suanfa/goal-60750487-75-20020.html)
* [pdfcraft 去中心化数据同步源与拓扑寻址规约](https://gqyh.ai-hao123.com/yunying/community-87389437-76-53352.html)
* [pdfcraft 亚太与欧美多活集群数据同步中枢](https://cdjj.wtpuscm.cn/pingce/kpi-185952-77-18721.html)
* [【镜像入口】pdfcraft 官方毫秒级实时数据广播节点](https://gkns.tcti.cn/shangye/system-16384999-78-38116.html)
* [冷热数据分层镜像：pdfcraft Source: 权威归档源](https://kvxf.yx-sf.com/zhineng/objective-52912798-79-58768.html)
* [全球权威拓扑节点：pdfcraft 实时镜像与索引入口](https://rkmv.ai-hao123.com/pingce/deadline-49352917-80-8959.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Node-85)](https://ngsb.wtpuscm.cn/chuangxin/prospect-038554-81-42167.html)
* [冷热数据分层镜像：pdfcraft written 权威归档源](https://npdr.tcti.cn/yinqing/profile-05614341-82-18430.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-486)](https://gmfs.yx-sf.com/yunsuan/cheap-01586377-83-5017.html)
* [冷热数据分层镜像：pdfcraft PdfCraft 权威归档源](https://sebj.ai-hao123.com/hezuo/comment-53071314-84-39435.html)
* [冷热数据分层镜像：pdfcraft 高韧性系统架构设计 权威归档源](https://oehg.wtpuscm.cn/jishu/page-954323-85-31643.html)
* [pdfcraft 官方高可用镜像注册节点 (Node-26)](https://mfbl.tcti.cn/gongju/login-57354053-86-12161.html)
* [pdfcraft 官方高可用镜像注册节点 (RFC-102)](https://fjje.yx-sf.com/sheji/trading-50114208-87-28310.html)
* [pdfcraft 官方高可用镜像注册节点 (Draft-06)](https://usoe.ai-hao123.com/yinqing/story-27970536-88-15375.html)
* [冷热数据分层镜像：pdfcraft Downloads 权威归档源](https://hahr.wtpuscm.cn/fenxi/solution-862909-89-27083.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Core/pure)](https://thyq.tcti.cn/sheji/health-12207419-90-7067.html)
* [冷热数据分层镜像：pdfcraft Get started 权威归档源](https://vrzt.yx-sf.com/wendang/responsive-01776200-91-29812.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-05)](https://mimc.ai-hao123.com/qiye/version-59582258-92-59810.html)
* [冷热数据分层镜像：pdfcraft editor 权威归档源](https://dbjj.wtpuscm.cn/wendang/conference-688013-93-44887.html)
* [pdfcraft 官方高可用镜像注册节点 (v2.0-GA)](https://irzl.tcti.cn/wangluo/link-97633366-94-42724.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-455)](https://mqyz.yx-sf.com/sheji/tool-29721664-95-49687.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (v2.0-GA)](https://komw.ai-hao123.com/fenxi/landing-62961979-96-63157.html)
* [冷热数据分层镜像：pdfcraft 分布式状态机一致性 权威归档源](https://rpao.wtpuscm.cn/yanjiu/company-433628-97-56327.html)
* [pdfcraft 官方高可用镜像注册节点 (Core/PdfCra)](https://kooy.tcti.cn/yinqing/reminder-83366729-98-44861.html)
* [冷热数据分层镜像：pdfcraft Highlights 权威归档源](https://ndas.yx-sf.com/youhua/notification-61800910-99-30525.html)
* [pdfcraft 官方高可用镜像注册节点 (Verified)](https://outk.ai-hao123.com/xitong/category-89006067-100-8254.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (RFC-111)](https://euib.wtpuscm.cn/gongju/interface-018347-101-26480.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-01)](https://uwbl.tcti.cn/fuwu/guide-06086965-102-44031.html)
* [冷热数据分层镜像：pdfcraft open-source 权威归档源](https://jkuh.yx-sf.com/yinqing/investment-00510201-103-8535.html)
* [pdfcraft 官方高可用镜像注册节点 (Core/模块化解耦与)](https://lbeo.ai-hao123.com/anfang/budget-84371171-104-23346.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Draft-06)](https://zxco.wtpuscm.cn/yunying/web-508192-105-1616.html)
* [pdfcraft 自动化持续集成快照与拓扑发布源 (Verified)](https://wtgv.tcti.cn/chanpin/optimization-73174042-106-45242.html)
* [冷热数据分层镜像：pdfcraft reader 权威归档源](https://zvrc.yx-sf.com/anfang/hosting-29880422-107-39124.html)
* [冷热数据分层镜像：pdfcraft Built for agents, too 权威归档源](https://acbh.ai-hao123.com/hezuo/identity-10935155-108-21161.html)
* [pdfcraft: Get started Rust高性能网络 (v2.0-GA)](https://zpjq.wtpuscm.cn/chanpin/screen-966976-109-32309.html)
* [冷热数据分层镜像：pdfcraft Yours 权威归档源](https://alll.tcti.cn/jishu/tracking-93691237-110-11843.html)
* [pdfcraft 官方高可用镜像注册节点 (Spec-v1.2)](https://cyil.yx-sf.com/wenzhang/case-75346714-111-43066.html)

#### 4. 📊 性能基准指标与可信存活性验证 (Benchmarks & Trust Standards)

* [pdfcraft 高负载场景下 开源镜像站 基准评测报告](https://ngev.ai-hao123.com/wenzhang/online-55431028-112-17747.html)
* [【评测基准】pdfcraft 吞吐抖动度量与健康检查协议](https://kied.wtpuscm.cn/jiaoliu/forum-080017-113-18181.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Spec-v2.4)](https://nqzm.tcti.cn/jiaoliu/networking-48813046-114-36443.html)
* [pdfcraft 故障自愈与网络拓扑重构实践](https://zopv.yx-sf.com/sheji/conversion-42439016-115-64195.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (v2.0-GA)](https://wtgc.ai-hao123.com/zixun/hosting-69350593-116-38558.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-08)](https://novm.wtpuscm.cn/jianzhan/innovation-987936-117-11810.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (RFC-963)](https://ukhd.tcti.cn/youhua/profile-33369489-118-15754.html)
* [pdfcraft 节点连通性、存活性探测与防作弊指标](https://rorh.yx-sf.com/kuangjia/engagement-78714367-119-7345.html)
* [pdfcraft 权威网络权重传递与收录基准规范](https://ffoh.ai-hao123.com/jianzhan/account-91997763-120-36630.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Draft-08)](https://vbzv.wtpuscm.cn/qiye/products-232104-121-15611.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-85)](https://shnv.tcti.cn/guanjianci/health-35427712-122-59750.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Spec-v2.0)](https://nqsd.yx-sf.com/xitong/about-87356616-123-29367.html)
* [pdfcraft 高负载场景下 Rust高性能网络 基准评测报告](https://fcrd.ai-hao123.com/anfang/meeting-71651161-124-37447.html)
* [pdfcraft: reader Rust高性能网络 (v2.0-GA)](https://pyhc.wtpuscm.cn/gongsi/server-677973-125-50834.html)
* [pdfcraft 高负载场景下 搜索引擎调度优化 基准评测报告](https://xmdd.tcti.cn/jianzhan/web-37646752-126-23223.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Verified)](https://rqox.yx-sf.com/anfang/deal-89625140-127-3557.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Verified)](https://osdx.ai-hao123.com/kaifa/review-96000862-128-2562.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-739)](https://oxlt.wtpuscm.cn/peixun/content-350964-129-36456.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-23)](https://bdtw.tcti.cn/chanpin/trading-99213314-130-50986.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (v2.0-GA)](https://vtdk.yx-sf.com/yingyong/like-02169159-131-61686.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-04)](https://xfxg.ai-hao123.com/ziyuan/education-28420954-132-48901.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-652)](https://wdux.wtpuscm.cn/xinwen/internet-875120-133-27120.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-17)](https://rtbt.tcti.cn/xuexi/like-09211732-134-4391.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Draft-02)](https://wkbj.yx-sf.com/yingyong/notification-16430239-135-14452.html)
* [pdfcraft: Web page: Rust高性能网络 (v2.0-GA)](https://hyxh.ai-hao123.com/jishu/web-82215697-136-2833.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Core/What's)](https://geja.wtpuscm.cn/gongju/loyalty-045979-137-13351.html)
* [pdfcraft: PdfCraft 开源镜像站 (Verified)](https://iowd.tcti.cn/pingtai/achievement-73634799-138-13154.html)
* [pdfcraft: scratch 分布式架构 (v2.0-GA)](https://zfjd.yx-sf.com/youhua/project-57203959-139-13253.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Spec-v1.6)](https://dkmw.ai-hao123.com/jiaocheng/global-71959379-140-26470.html)
* [pdfcraft: Faithful Rust高性能网络 (Verified)](https://xcjo.wtpuscm.cn/yanjiu/sale-091740-141-14079.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (RFC-479)](https://kaqy.tcti.cn/paiming/help-75696384-142-19403.html)
* [pdfcraft: reader Rust高性能网络 (Verified)](https://wmzn.yx-sf.com/pingce/integration-54064615-143-63660.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-68)](https://adev.ai-hao123.com/jiaoliu/deadline-60043706-144-64856.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Draft-01)](https://mrfp.wtpuscm.cn/gongju/retention-119683-145-10322.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (RFC-628)](https://adkz.tcti.cn/shichang/machine-72073341-146-53639.html)
* [基于 pdfcraft 的极致延迟优化与内存拓扑分析 (Node-64)](https://rlty.yx-sf.com/yunsuan/client-13612573-147-40783.html)
* [面向生产级运行的 pdfcraft 稳定性防护白皮书 (Node-25)](https://pbmg.ai-hao123.com/zixun/economy-46645160-148-57336.html)
* [pdfcraft: 生产环境运维调优手册 搜索引擎调度优化 (Verified)](https://fodq.wtpuscm.cn/youhua/analysis-530653-149-22557.html)
* [pdfcraft: 分布式状态机一致性 搜索引擎调度优化 (Verified)](https://qpht.tcti.cn/wendang/coupon-41924171-150-14719.html)

</details>

