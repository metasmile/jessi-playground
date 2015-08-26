# Welcome to dirty room.

Here are only some dirty but well-tested runnable code snippets, utils, benchmarking results, studying for solving common or mission critical issues or just curious while proceeding project. I'll write topic by topic in this place to be continued. yay! :)

===========
##### What is the best format(or procedure) to attach simple shaped images to view? PDF, PNG, SVG?

https://github.com/metasmile/jessi-playground/wiki/Compare-performance-in-real-device-:-PNG-vs-PDF-vs-SVG

===========
##### A Macro for capability of definition typed collection object. (ios 9.x)
```objective-c
#if defined(__IPHONE_OS_VERSION_MAX_ALLOWED) && __IPHONE_OS_VERSION_MAX_ALLOWED >= 90000
#define __typed_collection(iterablesCls, elementsType) iterablesCls<elementsType> *
#else
#define __typed_collection(iterablesCls, elementsType) iterablesCls *
#endif

#if defined(__IPHONE_OS_VERSION_MAX_ALLOWED) && __IPHONE_OS_VERSION_MAX_ALLOWED >= 90000
#define __typed_collection_knd(iterablesCls, elementsType) iterablesCls<__kindof elementsType> *
#else
#define __typed_collection_knd(iterablesCls, elementsType) iterablesCls *
#endif

// ex usage of '__typed_collection'
- (__typed_collection(NSArray,UIView *))views; 

- (NSArray *)views; // <= ios8.x
- (NSArray <UIView *> *)views; // >= ios9.x

// ex usage of '__typed_collection_knd'
- (__typed_collection_knd(NSArray,UIView *))views; 

- (NSArray *)views; // <= ios8.x
- (NSArray <__kindof UIView *> *)views; // >= ios9.x
```
