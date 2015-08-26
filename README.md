# Welcome to dirty room.

Here are only some dirty but well-tested runnable code snippets, utils, benchmarking results, studying for solving common or mission critical issues or just curious while proceeding project. I'll write topic by topic in this place to be continued. yay! :)

===========
##### What is the best format(or procedure) to attach simple shaped images to view? PDF, PNG, SVG?

https://github.com/metasmile/jessi-playground/wiki/Compare-performance-in-real-device-:-PNG-vs-PDF-vs-SVG

===========
##### A macro for compatibility of definition typed collection object. (ios 9.x)
```objective-c
#if defined(__IPHONE_OS_VERSION_MAX_ALLOWED) && __IPHONE_OS_VERSION_MAX_ALLOWED >= 90000
#define __typed_collection(iterablesCls, elementsType) iterablesCls<elementsType> *
#define __typed_collection_knd(iterablesCls, elementsType) iterablesCls<__kindof elementsType> *
#else
#define __typed_collection(iterablesCls, elementsType) iterablesCls *
#define __typed_collection_knd(iterablesCls, elementsType) iterablesCls *
#endif

/*
# ex usage of '__typed_collection'

- (__typed_collection(NSArray,UIView *))views; 

- (NSArray *)views; // <= ios8.x
- (NSArray <UIView *> *)views; // >= ios9.x

# ex usage of '__typed_collection_knd'

- (__typed_collection_knd(NSArray,UIView *))views; 

- (NSArray *)views; // <= ios8.x
- (NSArray <__kindof UIView *> *)views; // >= ios9.x
*/
```
===========
##### A macro for writing deallocation method in category class.

```objective-c
#define BEGIN_DEALLOC_CATEGORY + (void)load {\
        SEL originalSelector = NSSelectorFromString(@"dealloc");\
        SEL overrideSelector = @selector(__dealloc__);\
        Method originalMethod = class_getInstanceMethod(self, originalSelector);\
        Method overrideMethod = class_getInstanceMethod(self, overrideSelector);\
        if (class_addMethod(self, originalSelector, method_getImplementation(overrideMethod), method_getTypeEncoding(overrideMethod))) {\
            class_replaceMethod(self, overrideSelector, method_getImplementation(originalMethod), method_getTypeEncoding(originalMethod));\
        } else {\
            method_exchangeImplementations(originalMethod, overrideMethod);\
        }\
    }\
\
- (void)__dealloc__{\

#define END_DEALLOC_CATEGORY }
```
```objective-c
@implementation UIView (STUtil)

BEGIN_DEALLOC_CATEGORY
    // dealloc category
END_DEALLOC_CATEGORY

@end
```
