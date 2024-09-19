# Text-组件
在使用<Text/>的时候如果字体在Opensans,SourceSerif4,NotoSerifJP,可以使用以下组件

1.NotoSerifJP
`/src/components/text/SourceSerif4Text`

(1).导入

`import { SourceSerif4Text } from '../text';`

(2).使用
![SourceSerif4Text.png](SourceSerif4Text.png)
可传参数:
    text:文本内容,string
    weight:字体粗细,number，默认400
    fontStyle:字体是否倾斜,默认正常,传入italic时字体设置为倾斜
    numberOfLines:文本行数,number,
    style
    ![use-SourceSerif4Text.png](use-SourceSerif4Text.png)
    支持传入children

2.Opensans

`/src/components/text/OpenSansText`
同SourceSerif4Text使用


3.NotoSerifJP
`/src/components/text/NotoSerifJPText`

同NotoSerifJP

不过存在差别,由于NotoSerifJP字体存在中英文使用差别 ，所有使用NotoSerifJP的英文字体转换为中文之后使用默认字体
但是在使用的时候不需要特殊处理 如果需要将中文字体使用NotoSerifJP,需要掺入family='useJP'
![NotoSerifJP.png](NotoSerifJP.png)
这样中文字体也会使用NotoSerifJP字体,否则为默认








Start typing here...