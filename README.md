About
========

基于Android SDK中的ant构建工具，为其添加了multidex支持。可以对主dex中包含的类进行配置，并且能够和proguard良好的合作。


使用
--------

将源码包com.android.ant下编译得到的class文件添加到原有ant-tasks.jar中，将包com.android.sdklib下编译得到的class文件添加到原有sdklib.jar中，替换掉与之对应的原来的类文件。不用担心，这不会影响原有build.xml的执行。还要记得更新ant-tasks.jar中的anttasks.properties。如果不想动手，也可以直接在此处下载 [the releases][1]。

用以上两个修改过的JAR文件替换掉sdk/tools/lib下的原有文件（做好备份），把build.multidex.xml放到sdk/tools/ant下，并且修改位于你工程目录下的build.xml：
```xml
<import file="${sdk.dir}/tools/ant/build.xml" />
```
to:
```xml
<import file="${sdk.dir}/tools/ant/build.multidex.xml" />
```
不要忘了在你的工程中添加android-support-multidex.jar。

在工程目录的根目录下，新建一个maindexfilter.txt来配置主dex中包含的类，支持＊匹配：
```txt
android/support/multidex/*
com/example/multidex/MyApplication.class
```
主dex中起码要包含multidex支持库，如果你扩展了Application，也要包含。

根据你的需要修改xml中minimalMainDex的值，来控制主dex的大小。


License
=======

    Copyright 2016 LimeFamily.com

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.


 [1]: https://github.com/limefamily/apk-build/releases
