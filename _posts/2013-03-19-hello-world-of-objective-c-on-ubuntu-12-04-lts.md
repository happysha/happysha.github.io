---
author: bluishoul
comments: true
date: 2013-03-19 14:31:52+00:00
layout: post
slug: hello-world-of-objective-c-on-ubuntu-12-04-lts
title: '"Hello World" of Objective-C on Ubuntu 12.04 LTS'
wordpress_id: 1299
categories:
- 一周一博
---

鉴于 webapp 的性能问题，于是想尝试接触一下 objective-c ，妄图有机会写写 iOS APP。
    所以今天开始尝试学写个“Hello World”,程序参考的是一个台湾翻译版本的文档：
    <a href="http://www.otierney.net/objective-c.html.zh-tw.big5" target="_blank">http://www.otierney.net/objective-c.html.zh-tw.big5
    </a>上面给的"Hello world"例子就是我们比较熟悉的 C 语言的例子,保存为 main.m：
    [code lang="c"]
    #import <stdio.h>
    int main( int argc, const char *argv[] ) {
        printf( "hello world\n" );
        return 0;
    }
    [/code]
    用 GCC 命令编译，然后执行：
    [code lang="shell"]
    gcc main.m -o main
    ./main
    [/code]
    这个比较简单，让我们来个真正的 objc 程序： 在这之前，我们需要安装 GNUStep ，以提供 objc 运行的环境：
    [code lang="shell"]
    sudo apt-get install gnustep gnustep-devel
    [/code]
    安装目录位于:/usr/share/GNUStep/下，执行以下命令：
    [code lang="shell"]
    cd /usr/share/GNUstep/Makefiles/
    sudo chmod a+x GNUstep.sh
    ./GNUstep.sh
    [/code]
    在你的目录下创建以下代码文件： 如下代码，保存为 Fraction.h,详解在文档中有解释：
    [code lang="objc"]
    #import <Foundation/NSObject.h>
    
    @interface Fraction: NSObject {
     int numerator;
     int denominator;
    }
    
    -(void) print;
    -(void) setNumerator: (int) n;
    -(void) setDenominator: (int) d;
    -(int) numerator;
    -(int) denominator;
    @end
    [/code]
    如下代码保存为：Fraction.m
    [code lang="objc"]
    #import "Fraction.h"
    #import <stdio.h>
    
    @implementation Fraction
    -(void) print {
        printf( "%i/%i", numerator, denominator );
    }
    
    -(void) setNumerator: (int) n {
        numerator = n;
    }
    
    -(void) setDenominator: (int) d {
        denominator = d;
    }
    
    -(int) denominator {
        return denominator;
    }
    
    -(int) numerator {
        return numerator;
    }
    @end
    [/code]
    如下代码保存为：main.m
    [code lang="objc"]
    #import <stdio.h>
    #import "Fraction.m"
    
    int main( int argc, const char *argv[] ) {
        // create a new instance
        Fraction *frac = [[Fraction alloc] init];
    
        // set the values
        [frac setNumerator: 1];
        [frac setDenominator: 3];
    
        // print it
        printf( "The fraction is: " );
        [frac print];
        printf( "\n" );
    
        // free memory
        [frac release];
    
        return 0;
    }
    [/code]
    创建一个 GNUmakefile 文件，代码如下：
    [code lang="shell"]
    include $(GNUSTEP_MAKEFILES)/common.make
    TOOL_NAME=Test
    Test_OBJC_FILES=main.m
    include $(GNUSTEP_MAKEFILES)/tool.make
    [/code]
    TOOL_NAME=* 中*与 *_OBJC_FILES 一致，main.m 为目标编译文件名，GNUmakefile 与 main.m 文件同目录。 运行 make 命令编译,编译完将产生 obj 目录，运行 ./Test 即可得到结果：
    [code lang="shell"]
    The fraction is: 1/3
    [/code]
    至此“Hello World” 就搞定了！
